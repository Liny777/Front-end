<template>
    <div class="short-visit">
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="130px" class="demo-ruleForm" v-if="textFlag">
        <el-form-item label="出访国家(地区)" prop="foreignName" class="nation-select">
          <el-select
            style="min-height: 30px;line-height: 30px;height: auto;"
            class="selects"
            v-model="ruleForm.foreignName"
            multiple
            filterable
            remote
            reserve-keyword
            :multiple-limit="3"
            @focus="tt"
            :remote-method="remoteMethod"
            placeholder="请选择国家">
            <el-option
              v-for="item in options4"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
          <div class="titles">提示：如出访台湾地区，请按照国际处网页赴台流程及所需材料进行线下审批。</div>
        </el-form-item>
 
        
        <el-form-item class="submitBtn">
          <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
        </el-form-item>
    </div>
</template>
 
<script>
import api from '../../utils/api'
export default {
  name: 'short-visit',
  data () {
      uploadUrl: '',
      ruleForm: {
        foreignName: [], // 出访国家
      },
      options4: [],
      list: [],
      rules: {
        foreignName: [
          { required: true, message: '请选择国家', trigger: 'change' }
        ]
      }
    }
  },
  created () {
    /**
     * 国家的请求
     * */
    this.getContryData()
    
  },
  methods: {
    
    /**
     * 数据的提交
     * */
    submitForm (formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          
          this.$confirm('是否确认提交', {
            confirmButtonText: '确定',
            cancelButtonText: '取消',
            type: 'warning',
            center: true
          }).then(() => {
            
          }).catch(() => {
          })
        } else {
          return false
        }
      })
    },
    /**
     * 国家
     * */
    getContryData () {
      api.getContrys().then((res) => {
        // console.log(res)
        // console.log(res.data.code)
        if (res.data.code === 0) {
          for (var i = 0; i < res.data.data.length; i++) {
            let obj = {}
            obj.value = res.data.data[i].codeLabel
            obj.codeValue = res.data.data[i].codeValue
            this.list.push(obj)
          }
          // console.log(this.ruleForm.foreignName)
        }
      })
    },
    /**
     * 选择国家获取焦点
     * */
    tt () {
      this.options4 = this.list
      console.log(this.options4)
    },
    /**
     * 选择国家
     * */
    remoteMethod (query) {
      console.log(query)
      if (query !== '') {
        this.loading = true
        setTimeout(() => {
          this.loading = false
          this.options4 = this.list.filter(item => {
            return item.value.toLowerCase()
              .indexOf(query.toLowerCase()) > -1
          })
        }, 200)
      } else {
        this.options4 = []
      }
    }
  }
}
</script>
 
<style rel="stylesheet/scss" lang="scss">
   
</style>