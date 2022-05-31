<template>
  <div>
    <div class="card-header">
      <span>{{title}}</span>
      <svg t="1650111775080" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="2854" width="32" height="32"><path d="M509.92 795.84c157.904 0 285.92-128.016 285.92-285.92C795.84 352 667.808 224 509.92 224 352 224 224 352 224 509.92c0 157.904 128 285.92 285.92 285.92z m0 48C325.504 843.84 176 694.32 176 509.92 176 325.504 325.504 176 509.92 176c184.416 0 333.92 149.504 333.92 333.92 0 184.416-149.504 333.92-333.92 333.92z m-2.448-400.704h16a16 16 0 0 1 16 16v201.728a16 16 0 0 1-16 16h-16a16 16 0 0 1-16-16V459.136a16 16 0 0 1 16-16z m0-100.176h16a16 16 0 0 1 16 16v23.648a16 16 0 0 1-16 16h-16a16 16 0 0 1-16-16v-23.648a16 16 0 0 1 16-16z" p-id="2855" fill="#d9d9d9"></path></svg>
    </div>
    <div class="card-content">{{count}}</div>
    <div class="card-chart">
        <slot name="charts"></slot>
    </div>
    <div class="card-footer">
        <slot name="footer"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "",
  props:['title','count']
};
</script>

<style scoped>
.card-header{
    display:flex;
    justify-content: space-between;
    align-items: center;
    color:#ccc
}
.card-content{
    font-size: 30px;
    margin:10px auto;
}
.card-chart{
    height: 50px;
}
.card-footer{
    border-top:1px solid #ccc;
    padding-top:5px;
}
</style>