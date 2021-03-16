<template>
  <el-table ref="singleTable" :data="path2" highlight-current-row style="width: 100%;padding-top: 15px;" @current-change="handleCurrentChange">
    <el-table-column
      type="index"
      label="2"
      width="50"
    />
    <!-- <el-table-column label="Path Node Id" min-width="200"> -->
    <el-table-column
      property="start"
      label="Head"
      width="70"
    />
    <el-table-column
      property="relation"
      label="Edge"
      width="80"
    />
    <!-- </el-table-column> -->
    <el-table-column
      property="end"
      label="Tail"
      width="70"
    />
  </el-table>
</template>

<script>
// import { transactionList } from '@/api/remote-search'

export default {
  // filters: {
  //   statusFilter(status) {
  //     const statusMap = {
  //       success: 'success',
  //       pending: 'danger'
  //     }
  //     return statusMap[status]
  //   },
  //   orderNoFilter(str) {
  //     return str.substring(0, 30)
  //   }
  // },
  data() {
    return {
      currentRow: null,
      path1: [{
        'start': '氯吡格雷',
        'relation': '相互作用(化学名)',
        'end': '雷尼替丁'
      }, {
        'start': '雷尼替丁',
        'relation': '相互作用(化学名)',
        'end': '非甾体类抗炎药'
      }],
      path2: [{
        'start': '氯吡格雷',
        'relation': '相互作用(化学名)',
        'end': '乙醇'
      }, {
        'start': '乙醇',
        'relation': '相互作用(化学名)',
        'end': '非甾体类抗炎药'
      }]
    }
  },
  created() {
    // this.fetchData()
  },
  methods: {
    handleCurrentChange(val) {
      this.currentRow = val
    }
    // fetchData() {
    //   transactionList().then(response => {
    //     this.list = response.data.items.slice(0, 8)
    //   })
    // }
  }
}
</script>
<style scoped>
        .to_right {
            width: 0;
            height: 0;
            border-left: 10px solid greenyellow;
            border-top: 10px solid transparent;
            border-bottom: 10px solid transparent;
        }
</style>
