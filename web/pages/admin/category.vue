<template>
  <div class="pr-4">
    <!-- 分类树 -->
    <div>
      <p class="lead mb-1"><i class="el-icon-arrow-down"></i>&nbsp;分类树</p>
      <p class="small text-muted pl-4">单击分类名称编辑</p>
    </div>
    <div class="pl-4">
      <el-tree :data="data4" :props="defaultProps" :show-checkbox="false" node-key="id" 
        default-expand-all :expand-on-click-node="false" :highlight-current="true" :render-content="renderContent" 
        class="p-2" style="width:auto;max-width:460px;">
      </el-tree>
    </div>
    <!-- 单项编辑 -->
    <transition name="slide-fade">
      <div v-if="currentEditingMode !== 'none'">
        <div class="pt-4">
          <p class="lead mb-0"><i class="el-icon-arrow-down"></i>&nbsp;单项编辑</p>
          <p class="small text-muted pl-4">在保存后生效</p>
        </div>
        <div class="pl-4">
          <el-form :model="currentEditingNode" label-width="40px" style="width:460px">
            <el-form-item class="mb-0" label="分类" width="">
              <el-input v-model="currentEditingCatetory" placeholder="text" style="max-width:200px"></el-input>
            </el-form-item>
            <el-form-item class="pt-2">
              <el-button @click="editNodeSave" type="primary">保存</el-button>
              <el-button @click="onCancel" type="text">取消</el-button>
            </el-form-item>
          </el-form>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
let id = 1000
export default {
  layout: 'admin',
  head: {
    title: '导航菜单',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      { hid: 'description', name: 'description', content: 'Home page description' }
    ],
    link: [
      { rel: 'favicon', href: '/static/favicon.ico' },
      { rel: 'stylesheet', href: 'https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css', integrity: 'sha384-PsH8R72JQ3SOdhVi3uxftmaW6Vc51MKb0q5P2rRUpPvrszuE4W1povHYgTpBfshb', crossorigin: 'anonymous' }
    ],
    script: [
      // { src: '/static/js/holder-v2.9.0.min.js', type: 'text/javascript' }
    ]
  },
  mounted: function () {
  },
  methods: {
    getRawdataOfNode (node, data) {
      const parent = node.parent
      const children = parent.data.children || parent.data
      const index = children.findIndex(d => d.id === data.id)
      const rawdata = children[index]
      return rawdata
    },
    editNodeSave () {
      this.currentEditingNode.label = this.currentEditingCatetory
      this.currentEditingNode = {}
    },
    append (data) {
      const newChild = { id: id++, label: '子项', link: '#' }
      if (!data.children) {
        this.$set(data, 'children', [])
      }
      data.children.push(newChild)
    },
    edit (node, data) {
      const rawdata = this.getRawdataOfNode(node, data)
      if (rawdata.id === 1) {
        this.currentEditingNode = {}
        return
      }
      this.currentEditingNode = rawdata
      this.currentEditingCatetory = rawdata.label
      this.currentEditingMode = 'edit'
    },
    onCancel () {
      this.currentEditingMode = 'none'
    },
    remove (node, data) {
      const parent = node.parent
      const children = parent.data.children || parent.data
      const index = children.findIndex(d => d.id === data.id)
      children.splice(index, 1)
    },
    renderContent (h, { node, data, store }) {
      const rawdata = this.getRawdataOfNode(node, data)
      if (rawdata.id === 1) {
        return (
          <span class="sc-tree-item">
            <span>
              <span>{node.label}</span>
            </span>
            <span>
              <el-button size="mini" type="success" on-click={ () => this.append(data) }>添加子项</el-button>
              <el-button size="mini" type="danger" on-click={ () => this.remove(node, data) }>移除</el-button>
            </span>
          </span>)
      } else {
        return (
          <span class="sc-tree-item">
            <span>
              <span><a href="javascript:;" on-click={ () => this.edit(node, data) }>{node.label}</a></span>
            </span>
            <span>
              <el-button size="mini" type="success" on-click={ () => this.append(data) }>添加子项</el-button>
              <el-button size="mini" type="danger" on-click={ () => this.remove(node, data) }>移除</el-button>
            </span>
          </span>)
      }
    }
  },
  data () {
    return {
      formInline: {
        user: '',
        region: ''
      },
      // 当前编辑状态：edit、none
      currentEditingMode: 'none',
      currentEditingNode: {},
      currentEditingCatetory: '',
      data4: [{
        id: 1,
        label: '顶级菜单',
        link: '/',
        children: [{
          id: 4,
          label: '二级 1-1',
          link: '#'
        }, {
          id: 5,
          label: '二级 1-2',
          link: '#'
        }]
      }],
      defaultProps: {
        id: 'id',
        children: 'children',
        label: 'label',
        link: '#'
      }
    }
  },
  components: {}
}
</script>

<style>
.el-tree-node__content{
  height:auto !important;
  padding:5px 0 5px;
}
.el-tree-node__content a{
  text-decoration: none !important;
}
.sc-tree-item{
  flex: 1; display: flex; align-items: center; justify-content: space-between; font-size: 14px; padding-right: 8px;
}
</style>
