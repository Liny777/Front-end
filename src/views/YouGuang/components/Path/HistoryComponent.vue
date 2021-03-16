<template>
  <div>
    <el-table ref="singleTable" :data="hisotries" highlight-current-row style="width: 100%;">
      <el-table-column
        type="index"
        width="50"
      />
      <el-table-column
        property="start"
        label="Start"
        width="200"
      />
      <el-table-column
        property="end"
        label="End"
        width="200"
      />
      <el-table-column
        property="time"
        label="Time"
        width="200"
      />
    </el-table>
    <el-divider />
    <el-button @click="clearhistory">清空</el-button>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
export default {
  data() {
    return {
    }
  },
  computed: {
    ...mapGetters([
      'hisotries'
    ])
  },
  watch: {
  },
  created() {
  },
  mounted() {
  },
  methods: {
    ...mapActions(
      { clearhistory: 'path/clearHistoryRecord' })
  }
}
</script>

<style scoped>
tr.current-row > td,
    .el-table__body tr:hover > td {
      background:#f19944;
    }
</style>
