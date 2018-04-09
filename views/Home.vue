<template>
    <div>
      <el-table
      :data="arr"
      style="width: 100%">
      <el-table-column
        prop="id"
        label="id"
        width="180">
      </el-table-column>
      <el-table-column
        prop="name"
        label="姓名"
        width="180">
      </el-table-column>
      <el-table-column
        prop="sex"
        label="性别">
      </el-table-column>
      <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.row)">删除</el-button>
      </template>
    </el-table-column>
    </el-table>  
    <div style="margin-top: 20px">
    
    <!-- <el-button @click="add">+</el-button> -->
    <Add></Add>
  </div>  
    </div>
  </template>
 <script>
// // @ is an alias to /src
import Add from '@/components/Add.vue'


export default {
  name: 'home',
  components: {
    Add
  },
   data() {
        return {
         arr:[]       
        }
      },
      watch:{
          '$route'(){
            this.he()
          }
      },
      created(){
        this.he()
       
      },
      methods:{
        he(){
            this.$http.post('http://localhost:3000/',{state:this.$route.params.id},{emulateJSON:true}).then(e=>this.arr=e.body)
        },

        add(){

        },
      handleDelete(row) {
        console.log(row);
        this.$http.post('http://localhost:3000/del',{id:row.id},{emulateJSON:true}).then(e=>this.row=e.body)
        var _index = this.arr.indexOf(row)
         this.arr.splice(_index,1)
        console.log(this.arr) 
      }
      }
}
</script>
