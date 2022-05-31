<template>
  <div>
    <el-card style="margin: 20px 0">
      <!-- 三级联动是全局组件 -->
      <CategorySelect
        @getCategoryId="getCategoryId"
        :show="scene != 0"
      ></CategorySelect>
    </el-card>
    <el-card>
      <!-- 三部分切换 -->
      <div v-show="scene==0">
        <!-- 展示SPU列表的结构 -->
        <el-button type="primary" icon="el-icon-plus" :disabled="!category3Id" @click="addSpu">添加SPU</el-button>
        <el-table style="width: 100%" border :data="records">
          <el-table-column type="index" label="序号" width="80px" ailgn="center">
          </el-table-column>
          <el-table-column prop="spuName" label="spu名称" width="width">
          </el-table-column>
          <el-table-column prop="description" label="spu描述" width="width">
          </el-table-column>
          <el-table-column prop="prop" label="操作" width="width">
            <template slot-scope="{row,$index}">
              <!-- 这里按钮将来用hintButton替换 -->
              <hint-button type="success" icon="el-icon-plus" size="mini" title="添加sku" @click="addSku(row)"></hint-button>
              <hint-button type="warning" icon="el-icon-edit" size="mini" title="修改spu" @click="updateSpu(row)"></hint-button>
              <hint-button type="info" icon="el-icon-info" size="mini" title="查看当前spu全部sku列表" @click="handler(row)"></hint-button>
              <el-popconfirm title="这是一段内容确定删除吗？" @onConfirm="deleteSpu(row)">
                <hint-button type="danger" icon="el-icon-delete" size="mini" title="删除spu" slot="reference"></hint-button>
              </el-popconfirm>             
            </template>
          </el-table-column>
        </el-table>
        <!-- 分页器 -->
        <el-pagination
          style="text-align:center"         
          :current-page="page"
          :page-sizes="[3, 5, 10]"
          :page-size="limit"
          layout="prev, pager, next, jumper, ->, total, sizes"
          :total="total"
          @current-change="getSpuList"
          @size-change="handleSizeChange">
        </el-pagination>
      </div>
      <SpuForm v-show="scene==1" ref="spu" @changeScene="changeScene"></SpuForm>
      <SkuForm v-show="scene==2" ref="sku" @changeScenes="changeScenes"></SkuForm>
    </el-card>
    <el-dialog :title="`${spu.spuName}的sku列表`" :visible.sync="dialogTableVisible" :before-close="close">
      <el-table :data="skuList" style="100%" border v-loading="loading">
        <el-table-column property="skuName" label="名称" width="150"></el-table-column>
        <el-table-column property="price" label="价格" width="200"></el-table-column>
        <el-table-column property="weight" label="重量"></el-table-column>
        <el-table-column label="默认图片">
          <template slot-scope="{row,$index}">
            <img :src="row.skuDefaultImg" alt="" style="width:100px;height:100px">
          </template>
        </el-table-column>
      </el-table>
    </el-dialog>
  </div>
</template>

<script>
//引入子组件
import SpuForm from './SpuForm'
import SkuForm from './SkuForm'
export default {
  name: "Spu",
  data() {
    return {
      //分类id
      category1Id: "",
      category2Id: "",
      category3Id: "",
      page:1, //分页器当前第几页
      limit:3,   //3级分类id
      records: [], //spu列表的数据
      total:0,  //分页器一共需要展示数据的条数
      scene:0,  //0代表展示SPU列表数据    1代表添加|修改SPU  2代表添加SKU
      //控制对话框的显示与隐藏
      dialogTableVisible:false,
      //存储spu
      spu: {},
      //存储sku列表的数据
      skuList: [],
      //loading加载
      loading: true
    };
  },
  components:{
    SpuForm,
    SkuForm
  },
  methods: {
    //三级联动的自定义事件，可以把子组件的相应的id传递给父组件
    getCategoryId({ categoryId, level }) {
      //categoryId:获取到一、二、三级分类的id  level：为了区分是几级id
      if (level == 1) {
        this.category1Id = categoryId;
        //清除2、3级分类的id
        this.category2Id = "";
        this.category3Id = "";
      } else if (level == 2) {
        this.category2Id = categoryId;
        this.category3Id = "";
      } else {
        this.category3Id = categoryId;
        //获取SPU列表数据展示
        this.getSpuList();
      }
    },
    //获取SPU列表数据
    async getSpuList(pager = 1) {
      this.page = pager;
      const {page,limit,category3Id} = this;
      //携带三个参数:page 第几页  limit 每一页需要展示多少条数据  三级分类id
      let result = await this.$API.spu.reqSpuList(page,limit,category3Id);
      if(result.code == 200){
        this.total = result.data.total;
        this.records = result.data.records;
      }
    },
    //点击分页器的第几页按钮的回调
    // handleCurrentChange(page){
    //   this.page = page;
    //   this.getSpuList();
    // }
    //当分页器某一页展示数据的条数发生变化时
    handleSizeChange(limit){
      //修改参数，发请求
      this.limit = limit;
      this.getSpuList();
    },
    //添加Spu按钮的回调
    addSpu(){
      //切换为场景为1
      this.scene = 1;
      //通知子组件SpuForm发请求---两个
      this.$refs.spu.addSpuData(this.category3Id);
    },
    //修改某一个spu
    updateSpu(row){
      this.scene = 1;
      //获取子组件SpuForm的方法
      //在父组件当中可以通过$refs获取子组件
      this.$refs.spu.initSpuData(row);
    },
    //自定义事件回调（SpuForm）
    changeScene({scene,flag}){
      //切换场景
      this.scene = scene;
      //子组件通知父组件切换场景，需要再次获取SPU列表的数据进行展示
      if(flag=="修改"){
        this.getSpuList(this.page);
      }else{
        this.getSpuList();
      }
    },
    //删除某个spu
    async deleteSpu(row){
      let result = await this.$API.spu.reqDeleteSpu(row.id);
      if(result.code == 200){
        this.$message({type:'success',message:"删除成功"});
        //如果SPU个数大于1，则停留在当前页。如果SPU个数小于等于1，则回到上一页。
        this.getSpuList(this.records.length > 1 ? this.page : this.page - 1);
      }
    },
    //添加SKU按钮的回调
    addSku(row){
      //切换场景为2
      this.scene = 2;
      //父组件调用子组件的方法,让子组件发请求-----三个请求
      this.$refs.sku.getData(this.category1Id,this.category2Id,row);
    },
    //自定义事件回调（SkuForm）
    changeScenes(scene){
      this.scene =scene;
    },
    //查看SKU按钮的回调
    async handler(spu){
      //显示对话框
      this.dialogTableVisible = true;
      //保存spu的信息
      this.spu = spu;
      //获取sku列表的数据
      let result = await this.$API.spu.reqSkuList(spu.id);
      if(result.code == 200){
        this.skuList = result.data;
        this.loading = false;
      }
    },
    //关闭dialog的回调
    close(done){
      //loading变为true
      this.loading = true;
      //清除sku列表数据
      this.skuList = [];
      //关闭dialog
      done();
    }
  },
};
</script>

<style>
</style>