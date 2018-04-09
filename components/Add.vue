<template>
  <div>
      <el-button type="text" @click="dialogVisible = true">点击打开 Dialog</el-button>

        <el-dialog
        title="提示"
        :visible.sync="dialogVisible"
        width="30%"
        :before-close="handleClose">
        <span>name: <input type="text" v-model="h.name"></span><br>
        <span>sex: <input type="text" v-model="h.sex"></span><br>
        <span>state: <input type="text" v-model="h.state"></span>
        <span slot="footer" class="dialog-footer">
            <el-button @click="dialogVisible = false">取 消</el-button>
            <el-button type="primary" @click="add">确 定</el-button>
        </span>
        </el-dialog>
  </div>
</template>


<script>
  export default {
    data() {
      return {
        dialogVisible: false,
        h:{},
        j:[]
      };
    },
    methods: {
      handleClose(done) {
        this.$confirm('确认关闭？')
          .then(_ => {
            done();
          })
          .catch(_ => {});
      },
      add(){
          this.dialogVisible=false
          this.$http.post('http://localhost:3000/add',this.h,{emulateJSON:true}).then(()=>this.j.push(this.h))

      }
    }
  };
</script>