<template>
  <div>
    <el-row>
      <el-col :span="2" :offset="0">
        <div style="margin-top: 10px">{{ name }}</div>
      </el-col>
      <el-col :span="3" :offset="0">
        <el-input v-model="content1" style="width: 100%"></el-input>
      </el-col>
      <el-col :span="1" :offset="0">
        <div style="margin-top: 10px">——</div>
      </el-col>
      <el-col :span="3" :offset="0">
        <el-input v-model="content2" style="width: 100%;"></el-input>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  export default {
    props:{
      name:{
        type: String,
        required: true
      },
      index:{
        type: Number,
        required: true
      }
    },
    data(){
      return{
        content1: '',
        content2: '',
        keyword: {
          name: this.name,
          value1: '',
          value2: '',
        },
      }
    },
    methods:{

    },
    watch:{
      content1:{
        handler(val,oldval){
          this.keyword.value1 = val
          let temp = {keyword: this.keyword, index: this.index}
          this.$emit('uploaddata',temp)
        }
      },
      content2:{
        handler(val,oldval){
          this.keyword.value2 = val
          let temp = {keyword: this.keyword, index: this.index}
          this.$emit('uploaddata',temp)
        },
        immediate: true
      }
    }
  }
</script>

<style>

</style>
