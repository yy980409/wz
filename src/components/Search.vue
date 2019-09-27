<template>
  <div>
    <div>
      <Select v-for="(choice,index) in name"
              :key="index" :line="choice" :index="index"
              @uploaddata="getdata"
      ></Select>
    </div>
    <br>
    <div>
      <el-row>
        <el-col :span="4">
          <el-button type="primary" @click="choose" >选择搜索字段</el-button>
        </el-col>
        <el-col :span="4">
          <el-button type="primary" @click="reset">重置搜索字段</el-button>
        </el-col>
        <el-col :span="3">
          <el-button type="primary" @click="upload">搜索</el-button>
        </el-col>
      </el-row>
    </div>
    <div>
      <el-dialog title="选择搜索字段" :visible.sync="selectView">
        <el-checkbox-group v-model="choices">
          <el-checkbox border v-for="(line,index) in lines"
                       :label="line.name" :key="index">
          </el-checkbox>
        </el-checkbox-group>
        <el-button @click="formatChoices">确定</el-button>
      </el-dialog>
    </div>

  </div>
</template>

<script>
  import Select from './Select.vue'
  export default {
    props:{
      lines:{
        type: Array,
        required: true
      },
      currentPage:{
        type: Number,
        required: true
      },
      pageSize:{
        type: Number,
        required: true
      },
      device:{
        type: String,
        required: true
      }
    },
    data(){
      return {
        temp: '',
        //lines: [{name:'温度',type:'float'},{name:'风速',type:'int'}],
        name: [],
        choices: [],
        keywords: [],
        selectView: false,
        Host: "http://172.26.47.71:8082",
      }
    },
    components:{
      Select,
    },
    mounted: function(){
      this.$nextTick(function (){
        this.name = []
      })
    },
    methods:{
      getdata(val){
        let index = val.index;
        this.keywords[index]=val.keyword
      },
      choose(){
        this.selectView = true
      },
      formatChoices(){
        this.name = []
        this.choices.forEach((choice)=>{
          var temp = this.lines.find((ele=>(ele.name == choice)));
          this.name.push(temp)
        })
        this.keywords[this.name.length-1] = {}
        this.selectView = false
      },
      reset(){
        this.name=[]
      },
      upload(){
        this.keywords.push({'设备名':this.device})
        let temp = {currentPage: this.currentPage, pageSize: this.pageSize, queryString: this.keywords}
        this.$emit('uploaddata', temp)
      },
    },
  }
</script>

<style>

</style>
