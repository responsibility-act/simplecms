<template>
  <div class="pr-4">
    <div>
      <p class="lead mb-1"><i class="el-icon-arrow-down"></i>&nbsp;三栏内容</p>
      <p class="small text-muted pl-4">操作说明</p>
    </div>
    <div class="pl-4">
      <el-table :data="tableData" stripe style="width: 100%">
        <el-table-column type="index" width="50">
        </el-table-column>
        <el-table-column label="图标与名称">
          <template slot-scope="scope">
            <i class="el-icon-share"></i>&nbsp;&nbsp;{{ scope.row.name }}
          </template>
        </el-table-column>
        <el-table-column label="内容类型" width="200">
          <template slot-scope="scope">
            {{ scope.row.name }}
          </template>
        </el-table-column>
        <el-table-column label="分类、行数" width="200">
          <template slot-scope="scope">
            {{ scope.row.name }}&nbsp;&nbsp;7条
          </template>
        </el-table-column>
        <el-table-column label="操作" width="200">
          <template slot-scope="scope">
            <el-button size="mini" type="success" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
            <el-button size="mini" type="danger" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
      <div class="pt-3">
        <el-button type="success">添加新项</el-button>
      </div>
    </div>
    <div class="pt-4">
      <p class="lead mb-1"><i class="el-icon-arrow-down"></i>&nbsp;编辑单项</p>
      <p class="small text-muted pl-4">无操作说明</p>
    </div>
    <div class="pl-4">
      <el-form style="max-width:1080px;" ref="form" :model="form" label-width="80px">
        <el-form-item label="内容类型">
          <el-input  style="max-width:300px" v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="图标">
          <el-input  style="max-width:300px" v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="栏目名称">
          <el-input style="max-width:300px" v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="分类">
          <el-input  style="max-width:300px" v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="行数">
          <el-input  style="max-width:300px" v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item class="pt-2">
          <el-button type="primary">保存</el-button>
          <el-button type="text">取消</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'admin',
  head: {
    title: '标题',
    meta: [
      { hid: 'description', name: 'description', content: 'Home page description' }
    ],
    link: [
      { rel: 'stylesheet', href: 'https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css', integrity: 'sha384-PsH8R72JQ3SOdhVi3uxftmaW6Vc51MKb0q5P2rRUpPvrszuE4W1povHYgTpBfshb', crossorigin: 'anonymous' }
    ]
  },
  methods: {
  },
  data () {
    return {
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1517 弄'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄'
      }],
      form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      formInline: {
        user: '',
        region: ''
      }
    }
  },
  components: {
  }
}
</script>

<style>

</style>
