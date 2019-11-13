<template>
  <!-- 编写页面静态部分，即view部分 -->
  <div>
    <el-button type="primary" size="mini" v-on:click="query">查询</el-button>
    <el-table
      :data="list"
      stripe
      style="width: 100%">
      <el-table-column type="index" width="35">
      </el-table-column>
        <el-table-column prop="pageName" label="页面名称" width="120">
        </el-table-column>
        <el-table-column prop="pageAliase" label="别名" width="120">
        </el-table-column>
        <el-table-column prop="pageType" label="页面类型" width="150">
        </el-table-column>
        <el-table-column prop="pageWebPath" label="访问路径" width="250">
        </el-table-column>
        <el-table-column prop="pagePhysicalPath" label="物理路径" width="250">
        </el-table-column>
        <el-table-column prop="pageCreateTime" label="创建时间" width="180">
        </el-table-column>
    </el-table>
    <el-pagination
      background
      layout="prev, pager, next"
      :total="100"
      :page-size="params.size"
      :current-page="params.page"
      v-on:current-change="changePage"
      style="float: right">
    </el-pagination>
  </div>
</template>

<script>

  import * as cmsApi from '../api/cms.js'

  /*编写页面静态部分，即model及vm部分 */
  export default {
      data() {
          return {
              list: [],
              total: 0,
              params: {
                  page: 1,
                  size: 10
              }

          }
      },
      methods:{
          query:function () {
              // alert("查询方法执行")
              //调用服务端方法接口
              cmsApi.page_list(this.params.page, this.params.size).then((res) => {
                  //将res结果数据赋值给数据模型对象
                  this.list = res.queryResult.list;
                  this.total = res.queryResult.total;
              })

          },
          changePage:function (page) {//形参就是当前页码
              //调用query方法
              this.params.page = page;
              this.query();
          }
      },
      mounted(){
          //当DOM元素渲染完成后调用query
          this.query();
      }

  }
</script>

<style>
  /*编写页面样式，不是必须*/
</style>
