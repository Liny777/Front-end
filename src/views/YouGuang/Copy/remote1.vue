<template>
  <div class="form-group">
     <el-form-item label="所属机构" prop="org">
         <el-select
             v-model="queryForm.org"
             clearable="true"
             filterable
             remote
             reserve-keyword
             placeholder="请输入关键词"
             :remote-method="remoteMethod"
             :loading="loading">
             <el-option
                 v-for="item in orgList"
                 :key="item.value"
                 :label="item.label"
                 :value="item.value">
             </el-option>
         </el-select>
      </el-form-item>
    </div>
</template>
 
<script>
  export default {
    data() {
      return {
        //远程搜索组件
        orgList: [],
        list: [],
        loading: false,
        allOrds: []
      }
    },
    mounted() {
            this.initData();
    },
    methods: {
      initData() {
          //远程搜索机构
          this.http.get('/admin/doctorInfo/queryOrg').then(resp => {
          //设置机构的选择项
          this.allOrds = resp.data;
 
          this.list = this.allOrds.map(item => { //组装，只需要id和name
              return {value: item.id, label: item.name};
             });
          });
        }
      }
      remoteMethod(query) {
          if (query !== '') {
              this.loading = true;
              setTimeout(() => {
                  this.loading = false;
                  this.orgList = this.list.filter(item => {
                      return item.label.toLowerCase()
                                .indexOf(query.toLowerCase()) > -1;
                        });
                    }, 200);
                } else {
                    this.orgList = [];
                }
            }
    }
  }
</script>