<template>
  <el-container class="body">
    <el-header>
      <el-row>
        <el-col :span="4" offset="1">
          <div>功能选择</div>
        </el-col>
        <el-col :span="8">
          <el-select v-model="value" filterable placeholder="请选择">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            />
          </el-select>
        </el-col>
        <!-- <el-col :span="12"><div class="grid-content bg-purple-light" /></el-col> -->
      </el-row>
    </el-header>
    <el-container>
      <el-aside width="320px">
        <div class="headerup">
          <el-menu
            :default-active="activeIndex"
            class="el-menu-demo"
            mode="horizontal"
            background-color="#D3DCE6"
            text-color="#333"
            active-text-color="#009966"
            @select="handleSelect"
          >
            <el-menu-item index="1">定向分析</el-menu-item>
            <el-menu-item index="2">图分析</el-menu-item>
            <el-menu-item index="3">图解读</el-menu-item>
          </el-menu>
        </div>
        <div class="footerdown">
          <div class="item1">
            <el-row class="item1-1">
              <el-col :span="4">起点</el-col>
              <el-col :span="16" :offset="2">
                <el-autocomplete
                  v-model="state1"
                  popper-class="my-autocomplete"
                  :fetch-suggestions="querySearch1"
                  placeholder="请输入内容"
                  @select="handleSelect1"
                >
                  <i
                    slot="suffix"
                    class="el-icon-circle-close"
                    @click="handleIconClick1"
                  />
                  <template slot-scope="{ item }">
                    <div class="name">{{ item.value }}</div>
                    <span class="addr">{{ item.address }}</span>
                  </template>
                </el-autocomplete>
              </el-col>
            </el-row>
            <el-row class="item1-2">
              <el-col :span="4">终点</el-col>
              <el-col :span="16" :offset="2">
                <el-autocomplete
                  v-model="state2"
                  popper-class="my-autocomplete"
                  :fetch-suggestions="querySearch2"
                  placeholder="请输入内容"
                  @select="handleSelect2"
                >
                  <i
                    slot="suffix"
                    class="el-icon-circle-close"
                    @click="handleIconClick2"
                  />
                  <template slot-scope="{ item }">
                    <div class="name">{{ item.value }}</div>
                    <span class="addr">{{ item.address }}</span>
                  </template>
                </el-autocomplete>
              </el-col>
            </el-row>
          </div>
          <!-- <div class="item2" />
          <div class="item3" /> -->
        </div>
        <el-footer>
          <el-row>
            <el-col :span="8" :offset="16">
              <el-button type="primary">预览</el-button>
            </el-col>
          </el-row>
        </el-footer>
      </el-aside>
      <el-main>
        <el-row>
          <el-col :span="21">
            <div
              v-if="isshow1"
              class="right"
              style="width: 600px;height:500px;"
            > <relation-chart /></div>
          </el-col>
          <el-col span="3">
            <i class="el-icon-s-data" @click="drawer = true" />
            <el-drawer
              title="我是标题"
              :visible.sync="drawer"
              :with-header="false"
              :modal-append-to-body="false"
              :modal="false"
              size="20%"
            >
              <el-row class="drawer1_title">设定分析路长</el-row>
              <el-row class="drawer1_content">
                <el-radio-group v-model="radio">
                  <el-radio :label="2">3</el-radio>
                  <el-radio :label="4">4</el-radio>
                  <el-radio :label="6">5</el-radio>
                  <el-radio :label="8">6</el-radio>
                </el-radio-group>
              </el-row>
              <el-divider />
              <el-row class="drawer2_title">设定分析主体</el-row>
              <el-row class="drawer2_content" />
              <el-divider />
              <el-row class="drawer3_title">设定分析关系</el-row>
              <el-row class="drawer3_content" />
              <el-divider />
              <el-footer>
                <el-row>
                  <el-col :span="8" :offset="16">
                    <el-button type="primary">预览</el-button>
                  </el-col>
                </el-row>
              </el-footer>
            </el-drawer>
          </el-col>
        </el-row>
        <el-row>
          <el-col span="24">
            <div class="block">
              <el-slider v-model="size1" />
            </div>
          </el-col>
        </el-row>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
// :sm="{span: 14}" :md="{span: 24}" :lg="{span: 12}" :xl="{span: 12}"
import echarts from 'echarts'
import axios from 'axios'
// var that = this
export default {
  data() {
    return {
      options: [{
        value: '1',
        label: '路径分析功能'
      }, {
        value: '2',
        label: '关联分析功能'
      }, {
        value: '3',
        label: '时态分析功能'
      }],
      value: '',
      startpoints: [],
      endpoints: [],
      state1: '',
      state2: '',
      size1: 0,
      drawer: false,
      radio: '1',
      isshow1: true
    }
  },
  watch: {},
  mounted() {
    this.startpoints = this.loadAll1()
    this.endpoints = this.loadAll2()
  },
  created() {
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath)
    },
    handleSelect1(item) {
      console.log(item)
    },
    handleSelect2(item) {
      console.log(item)
    },
    handleIconClick1(ev) {
      console.log(ev)
    },
    handleIconClick2(ev) {
      console.log(ev)
    },
    querySearch1(queryString, cb) {
      var startpoints = this.startpoints
      var results = queryString ? startpoints.filter(this.createFilter1(queryString)) : startpoints
      // 调用 callback 返回建议列表的数据
      cb(results)
    },
    querySearch2(queryString, cb) {
      var endpoints = this.endpoints
      var results = queryString ? endpoints.filter(this.createFilter2(queryString)) : endpoints
      // 调用 callback 返回建议列表的数据
      cb(results)
    },
    createFilter1(queryString) {
      return (startpoint) => {
        return (startpoint.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0)
      }
    },
    createFilter2(queryString) {
      return (endpoint) => {
        return (endpoint.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0)
      }
    },
    loadAll1() {
      return [
        { 'value': '三全鲜食（北新泾店）', 'address': '长宁区新渔路144号' }
      ]
    },
    loadAll2() {
      return [
        { 'value': '三全鲜食（北新泾店）', 'address': '长宁区新渔路144号' }
      ]
    }
  }

}
</script>

<style scoped>
 .el-header {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
  }

  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
  }

  .el-main {
    background-color: #E9EEF3;
    color: #333;
    text-align: center;
  }
  .el-menu-demo{
      margin-top: 20px;
  }
  .headerup{
      height: 50px;
  }
  .footerdown{
       height: 450px;
        text-align: center;
  }
  .block{
    bottom: 0px;
    left: 0px;
  }
  .drawer{
    background-color: #B3C0D1;
  }
  .drawer1_title{
    /* padding-left: -20px; */
    height: 20px;
    margin-top: 20px;
    margin-left: -100px;
    margin-right: 10px;
    margin-bottom: 20px;
  }
  .drawer2_title{
 height: 20px;
 margin-top: 20px;
    margin-left: -100px;
    margin-right: 10px;
    margin-bottom: 20px;
  }
  .drawer3_title{
 height: 20px;
 margin-top: 20px;
    margin-left: -100px;
    margin-right: 10px;
    margin-bottom: 20px;
  }
  .drawer1_content{
    height: 30px;
    margin-top: 20px;
    margin-left: 10px;
    margin-right: 10px;
    margin-bottom: 20px;
  }
   .drawer2_content{
     height: 80px;
margin-top: 20px;
    margin-left: 10px;
    margin-right: 10px;
    margin-bottom: 20px;
  }
   .drawer3_content{
     height: 80px;
margin-top: 20px;
    margin-left: 10px;
    margin-right: 10px;
    margin-bottom: 20px;
  }
  .item1{
    margin-top: 20px;
  }
  .item1-1{
    margin-bottom: 10px;
  }
  .item1-2{
    margin-bottom: 10px;
  }
</style>
