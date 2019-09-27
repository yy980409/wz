<template>
  <div>
    <el-row>
      <el-col :span="2" :offset="0">
        <div style="margin-top: 10px">{{ name }}</div>
      </el-col>
      <el-col :span="7" :offset="0">
        <el-input v-model="content" style="width:100%"></el-input>
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
        content: '',
        keyword: {
          name: this.name,
          value: '',
        },
      }
    },
    methods:{

    },
    watch:{
      content:{
        handler(val,oldval){
          this.keyword.value = val
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
