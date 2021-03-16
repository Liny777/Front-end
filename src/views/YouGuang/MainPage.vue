<template>
  <el-container class="body">
    <el-header>
      <el-row>
        <el-col :span="4" :offset="1">
          <div>
            <h1 class="text"><span>功能选择</span></h1>
          </div>
        </el-col>
        <el-col :span="8">
          <el-select v-model="value1" filterable placeholder="请选择" @change="changefunction">
            <el-option
              v-for="item in options1"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            />
          </el-select>
        </el-col>
      </el-row>
    </el-header>
    <el-container>
      <el-aside width="320px">
        <div class="headerup">
          <div v-if="big_show1">
            <el-menu
              :default-active="activeIndex"
              class="el-menu-demo"
              mode="horizontal"
              background-color="#D3DCE6"
              text-color="#333"
              active-text-color="#009966"
              @select="handleSelect1"
            >
              <el-menu-item class="elmenu1" index="1">定向分析</el-menu-item>
              <el-menu-item class="elmenu1" index="2">图分析</el-menu-item>
              <el-menu-item class="elmenu1" index="3">图解读</el-menu-item>
            </el-menu>
          </div>
          <div v-if="big_show2">
            <el-menu
              :default-active="activeIndex"
              class="el-menu-demo"
              mode="horizontal"
              background-color="#D3DCE6"
              text-color="#333"
              active-text-color="#009966"
              @select="handleSelect2"
            >
              <el-menu-item class="elmenu1" index="1">定向分析</el-menu-item>
              <el-menu-item class="elmenu1" index="2">图分析</el-menu-item>
              <el-menu-item class="elmenu1" index="3">图解读</el-menu-item>
            </el-menu>
          </div>
        </div>
        <div class="footerdown">
          <div v-if="big_show1">
            <div v-show="small_show11" class="item1">
              <path-search-component :catedata="category" />
            </div>
            <div v-show="small_show12" class="item2">
              <path-image-read />
            </div>
            <div v-show="small_show13" class="item3">
              <path-image-analyze />
              <!-- <path-image-analyze :link-data="LinkData" /> -->
            </div>
          </div>
          <div v-if="big_show2">
            <div v-show="small_show21" class="item1">
              <relation-search-component :catedata="category" />
            </div>
            <div v-show="small_show22" class="item2">
              <relation-image-read />
            </div>
            <div v-show="small_show23" class="item3">
              <relation-image-analyze />
            </div>
          </div>
        </div></el-aside>
      <el-main>
        <div v-if="big_show1">
          <el-row>
            <el-col :span="21">
              <path-force-chart />
            </el-col>
            <el-col :span="3">
              <el-row>
                <i class="el-icon-s-tools" @click="drawer11 = true"> 筛选</i>
                <el-drawer
                  title="我是标题"
                  :visible.sync="drawer11"
                  :with-header="false"
                  :modal-append-to-body="false"
                  :modal="false"
                  size="20%"
                >
                  <path-filter-component />
                </el-drawer>
              </el-row>
              <el-divider />
              <el-row>
                <el-badge is-dot class="item" :hidden="redpoint1">
                  <i class="el-icon-pie-chart" @click="drawer12 = true"> 历史</i>
                  <el-drawer
                    title="我是标题"
                    :visible.sync="drawer12"
                    :with-header="false"
                    :modal-append-to-body="false"
                    :modal="false"
                    size="30%"
                  >
                    <path-history-component />
                  </el-drawer>
                </el-badge>
              </el-row>
              <el-divider />
              <el-row>
                <i class="el-icon-refresh" @click="recover"> 恢复</i>
              </el-row>
              <el-divider />
              <el-row>
                <el-switch
                  v-model="value3"
                  active-text="图标"
                  inactive-text="圆形"
                  @change="change_radio"
                />
              </el-row>
            </el-col>
          </el-row>
        </div>
        <div v-if="big_show2">
          <el-row>
            <el-col :span="21">
              <relation-force-chart />
            </el-col>
            <el-col :span="3">
              <el-row>
                <i class="el-icon-s-tools" @click="drawer21 = true"> 筛选</i>
                <el-drawer
                  title="我是标题"
                  :visible.sync="drawer21"
                  :with-header="false"
                  :modal-append-to-body="false"
                  :modal="false"
                  size="20%"
                >
                  <relation-filter-component />
                </el-drawer>
              </el-row>
              <el-divider />
              <el-row>
                <el-badge is-dot class="item" :hidden="redpoint2">
                  <i class="el-icon-pie-chart" @click="drawer22 = true"> 历史</i>
                  <el-drawer
                    title="我是标题"
                    :visible.sync="drawer22"
                    :with-header="false"
                    :modal-append-to-body="false"
                    :modal="false"
                    size="30%"
                  >
                    <relation-history-component />
                  </el-drawer>
                </el-badge>
              </el-row>
              <el-divider />
              <el-row>
                <i class="el-icon-refresh" @click="recover"> 恢复</i>
              </el-row>
              <el-divider />
            </el-col>
          </el-row>
        </div>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import axios from 'axios'
// path
import PathForceChart from './components/Path/ForceChartComponent'
import PathImageAnalyze from './components/Path/ImageAnalyze'
import PathImageRead from './components/Path/ImageRead'
import PathHistoryComponent from './components/Path/HistoryComponent'
import PathFilterComponent from './components/Path/FilterComponent'
import PathSearchComponent from './components/Path/SearchComponent'
// relation
import RelationForceChart from './components/Relation/ForceChartComponent'
import RelationImageAnalyze from './components/Relation/ImageAnalyze'
import RelationImageRead from './components/Relation/ImageRead'
import RelationHistoryComponent from './components/Relation/HistoryComponent'
import RelationFilterComponent from './components/Relation/FilterComponent'
import RelationSearchComponent from './components/Relation/SearchComponent'
import { mapActions, mapGetters } from 'vuex'
// import data from '../pdf/content'
// 非甾体类抗炎药
export default {
  components: {
    // path
    PathForceChart,
    PathImageAnalyze,
    PathImageRead,
    PathHistoryComponent,
    PathFilterComponent,
    PathSearchComponent,
    // relation
    RelationForceChart,
    RelationImageAnalyze,
    RelationImageRead,
    RelationHistoryComponent,
    RelationFilterComponent,
    RelationSearchComponent
  },
  data() {
    return {
      value3: '',
      ForceChartData: {
        id1: '',
        id2: ''
      },
      options1: [{
        value: '1',
        label: '路径分析功能'
      }, {
        value: '2',
        label: '关联分析功能'
      }],
      value1: '',
      startpoints: [],
      endpoints: [],
      state1: '',
      state2: '',
      size1: 0,
      drawer11: false,
      drawer12: false,
      drawer21: false,
      drawer22: false,
      isshow1: true,
      category: [],
      categories: [],
      graph_length: 0,
      graph_length_start_content: 0,
      graph_length_end_content: 0,
      activeIndex: '1',
      options: [],
      big_show1: false,
      big_show2: false,
      small_show11: true,
      small_show12: false,
      small_show13: false,
      small_show21: true,
      small_show22: false,
      small_show23: false,
      NodeData: [{
        id: '',
        name: ''
      }],
      // LinkData: [{
      //   path: ''
      // }],
      startName: '',
      endName: '',
      countnumber: 0,
      EntityOption: [],
      RelationOption: [],
      redpoint1: true,
      redpoint2: true
      // filterinformation: {}
    }
  },
  computed: {
    ...mapGetters([
      'radio',
      'hisotries',
      'relation_histories'
    ])
  },
  watch: {
    hisotries: function(val, oldVal) {
      console.log('his: ' + val.length)
      if (val.length === 0) {
        this.redpoint1 = true
      } else {
        this.redpoint1 = false
      }
    },
    relation_hisotries: function(val, oldVal) {
      if (val.length === 0) {
        this.redpoint2 = true
      } else {
        this.redpoint2 = false
      }
    }
  },
  mounted() {
    // if (this.$route.params.userId === 1) {
    //   this.big_show1 = true
    //   this.big_show2 = false
    // }
    // console.log('this.$route.query.useId: ' + this.$route.params.userId)
    this.$nextTick(() => {
      this.loadData_entitytype()
    })
  },
  created() {
    console.log('this.$route.query.useId: ' + this.$route.params.userId)
    if (this.$route.params.userId === 1) {
      this.big_show1 = true
      this.big_show2 = false
    }
    if (this.$route.params.userId === 2) {
      this.big_show1 = false
      this.big_show2 = true
    }
    // console.log()
    this.$nextTick(() => {
      this.loadData_entitytype()
    })
  },
  // watch: {
  //   this.$route.query.useId:
  // },
  methods: {
    change_radio(data) {
      if (data === true) {
        this.$store.dispatch('path/setRadio', true)
      } else {
        this.$store.dispatch('path/setRadio', false)
      }
    },
    recover() {
      this.$store.dispatch('path/setChosenId', 0)
      this.$store.dispatch('path/setChosenEdge', 0)
      this.$store.dispatch('relation/setChosenId', 0)
      this.$store.dispatch('relation/setChosenEdge', 0)
    },
    ...mapActions(
      {
        // path
        setnodelabel: 'path/setNodeLabel',
        setedgelabel: 'path/setEdgeLabel',
        setChosenNodeLabel: 'path/setChosenNodeLabel',
        setChosenEdgeLabel: 'path/setChosenEdgeLabel',
        // relation
        relation_setnodelabel: 'relation/setNodeLabel',
        relation_setedgelabel: 'relation/setEdgeLabel',
        relation_setChosenNodeLabel: 'relation/setChosenNodeLabel',
        relation_setChosenEdgeLabel: 'relation/setChosenEdgeLabel'
      }
    ),
    loadData_entitytype() {
      axios.get('http://localhost:10088/MongoDB/getEntityType').then((response) => {
        for (var i = 0; i < response.data.length; i++) {
          this.EntityOption[i] = response.data[i].name
          var cate = {}
          cate['label'] = response.data[i].name
          cate['value'] = response.data[i].name
          this.categories[i] = cate
        }
        this.category = []
        this.category = this.categories
      })
    },
    // getfilterinfo(data) {
    //   this.filterinformation = data
    //   console.log('finaldegree: ' + this.filterinformation['maxdegree'])
    // },
    changefunction(value) {
      if (value === '1') {
        this.big_show1 = true
        this.big_show2 = false
      } else if (value === '2') {
        this.big_show1 = false
        this.big_show2 = true
      }
    },
    handleSelect1(key, keyPath) {
      if (key === '3') {
        this.small_show13 = true
        this.small_show12 = false
        this.small_show11 = false
      }
      if (key === '2') {
        this.small_show13 = false
        this.small_show12 = true
        this.small_show11 = false
      }
      if (key === '1') {
        this.small_show13 = false
        this.small_show12 = false
        this.small_show11 = true
      }
    },
    handleSelect2(key, keyPath) {
      if (key === '3') {
        this.small_show23 = true
        this.small_show22 = false
        this.small_show21 = false
      }
      if (key === '2') {
        this.small_show23 = false
        this.small_show22 = true
        this.small_show21 = false
      }
      if (key === '1') {
        this.small_show23 = false
        this.small_show22 = false
        this.small_show21 = true
      }
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
    margin-bottom: 0px;
    height: 575px;
  }

  .el-main {
    background-color:#fff;
     /* #E9EEF3; */
    color: #333;
    text-align: center;
  }
  .el-menu-demo{
      margin-top: 20px;
  }
  .elmenu1{
    width: 80px;
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
  /* .item1{
    margin-top: 20px;
  } */
h1 {
        font-family: "Arial", sans-serif;
        font-size: 30px;
        text-align: center;
        font-weight: bold;
    color: #99CCCC;
    /* margin-top: 0px; */
    }
    .text {
        position:relative;
         margin-top: 0px;
    }
    span {
    text-shadow:
    0 -1px 0 #858585,
    0 1px 10px rgba(0,0,0,.6),
    0 6px 1px rgba(0,0,0,.1),
    0 0 5px rgba(0,0,0,.2),
    0 1px 3px rgba(0,0,0,.3),
    0 3px 5px rgba(0,0,0,.2),
    0 7px 10px rgba(0,0,0,.25),
    0 15px 10px rgba(0,0,0,.2),
    0 25px 15px rgba(0,0,0,.15);
    }
</style>
