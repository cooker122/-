<template>
  <el-data-table
    v-bind="tableConfig"
    :url="url"
    :columns="columns"
  
    :form="form"
  >
  </el-data-table>
</template>

<script>
import Axios from 'axios'
export default {
  data() {
    return {
    
      tableConfig: {
     url: 'https://easy-mock.com/mock/5b586c9dfce1393a862d034d/example/img',
        columns: [
          {
            prop: 'modulename',
            label: '组件名称'
          },
          {
            prop: 'classify',
            label: '分类'
          },
          {
            prop: 'status',
            label: '状态'
          }
        ],
        searchForm: [
          {
            $el: {placeholder: '请输入'},
            label: '组件名称',
            $id: 'modulename',
            $type: 'input'
          },
          {
            $el: {placeholder: '请选择'},
            label: '分类',
            $id: 'classify',
            $type: 'select',
            $options: ['DUBBO', 'HSF'].map(f => ({label: f, value: f})),
          },
          {
            $el: {placeholder: '请选择'},
            label: '状态',
            $id: 'status',
            $type: 'select',
            $options: ['DUBBO', 'HSF'].map(f => ({label: f, value: f})),
          }
        ]
      },
      form: [
  {
    $type: 'select',
    $id: 'backendFramework',
    label: '后端框架',
    rules: [{required: true, message: '请选择后端框架', trigger: 'blur'}],
    $options: ['DUBBO', 'HSF'].map(f => ({label: f, value: f})),
    $el: {
      placeholder: '请选择'
    }
  },
  {
    $type: 'input',
    $id: 'name',
    label: '名称',
    rules: [
      {
        required: true,
        message: '请输入名称',
        trigger: 'blur',
        transform: v => v && v.trim()
      }
    ],
    $el: {placeholder: '请输入'}
  }
],
      columns: [
        {type: 'selection', selectable: (row, index) => index > 0},
        {prop: 'code', label: '品牌编号'},
        {prop: 'name', label: '品牌名称'},
        {prop: 'alias', label: '品牌别名'},
        {
          prop: 'logoUrl',
          label: '品牌Logo',
          width: '150px'
        },
        {
          prop: 'status',
          label: '状态',
          formatter: row => (row.status === 'normal' ? '上架' : '下架')
        }
      ],
    //   extraButtons: [
    //     {
    //       type: 'primary',
    //       text: '查看',
    //       // row 是单行的数据
    //       atClick: row => {
    //         alert('查看' + row.code)
    //         return Promise.resolve()
    //       }
    //     },
    //     {
    //       type: '',
    //       text: '下架',
    //       // row 是单行的数据
    //       atClick: row => {
    //         alert('下架' + row.code)
    //         return Promise.resolve()
    //       }
    //     }
    //   ],
      headerButtons: [
        {
          text: '批量导出',
          disabled: selected => selected.length == 0,
          // selected 是选中行所组成的数组
          atClick: selected => {
            let ids = selected.map(s => s.id)
            alert(ids)
          }
        }
      ]
    }
  },
    mounted(){
        
    },
  methods: {}
}
</script>
<style lang="less">
</style>