<template>
  <el-data-table
    v-bind="tableConfig"
    :columns="columns"
    :form="form"
    :beforeConfirm="beforeConfirm"
    :onNew="onNew"
    :onEdit="onEdit"
     :onDelete="onDelete"
  >
  </el-data-table>
</template>

<script>
import Axios from 'axios'
export default {
  data() {
    return {
      tableConfig: {
        url: 'http://yapi.demo.qunar.com/mock/56001/nav?page=1&size=10',
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
            $options: ['web', 'java', 'text', 'yun'].map(f => ({
              label: f,
              value: f
            }))
          },
          {
            $el: {placeholder: '请选择'},
            label: '状态',
            $id: 'status',
            $type: 'select',
            $options: ['上架', '下架'].map(f => ({label: f, value: f}))
          }
        ]
      },
      form: [
         
        {
          $type: 'select',
          $id: 'classify',
          label: '分类',
          rules: [{required: true, message: '请选择分类', trigger: 'blur'}],
          $options: ['web', 'java', 'text', 'yun'].map(f => ({
            label: f,
            value: f
          })),
          $el: {
            placeholder: '请选择'
          }
        },
       
        {
          $type: 'select',
          $id: 'type',
          label: '版本',
          rules: [{required: true, message: '请选择版本', trigger: 'blur'}],
          $options: ['1.0.1', '2.1.1', '3.1.1', '4.1.2', '5.1.2'].map(f => ({
            label: f,
            value: f
          })),
          $el: {
            placeholder: '请选择'
          }
        },
        {
          $type: 'select',
          $id: 'language',
          label: '开发语言',
          rules: [{required: true, message: '请选择开发语言', trigger: 'blur'}],
          $options: ['JavaScript', 'java', 'php', 'c++', 'c语言'].map(f => ({
            label: f,
            value: f
          })),
          $el: {
            placeholder: '请选择'
          }
        },
        {
          $type: 'select',
          $id: 'type',
          label: '状态',
          rules: [{required: true, message: '请选择状态', trigger: 'blur'}],
          $options: ['上架', '下架'].map(f => ({
            label: f,
            value: f
          })),
          $el: {
            placeholder: '请选择'
          }
        },
        {
          $type: 'input',
          $id: 'modulename',
          label: '组件名称',
          rules: [
            {
              required: true,
              message: '请输入组件名称',
              trigger: 'blur',
              transform: v => v && v.trim()
            }
          ],
          $el: {placeholder: '请输入组件名称'}
        }
      ],
      columns: [
        {type: 'selection', selectable: (row, index) => index > 0},
        {prop: 'modulename', label: '组件名称'},
        {prop: 'classify', label: '分类'},
        {
          prop: 'type',
          label: '版本',
          width: '150px'
        },
        {
          prop: 'language',
          label: '开发语言',
          width: '150px'
        },
        {
          prop: 'last_date',
          label: '最后更新时间',
          width: '150px'
        },
        {
          prop: 'status',
          label: '状态',
          formatter: row => (row.status === '0' ? '上架' : '下架')
        }
      ],
      headerButtons: [
        {
          text: '删除',
          //   disabled: selected => selected.length == 0,
          // selected 是选中行所组成的数组
          atClick: selected => {
            let ids = selected.map(s => s.id)
            // alert(ids)
          }
        }
      ]
    }
  },
  mounted() {
      
  },
  methods: {
      beforeConfirm(data, isNew) {
  console.log(data, isNew)

  if (isNew) {
	// alert('新增可以发送请求')
	return Promise.resolve()
  } else {
	// alert('修改不可以发送请求')
	return Promise.reject()
  }
},
onNew(data, row) {
  console.log(data, row)
  return Axios.post(
	'http://yapi.demo.qunar.com/mock/56001/nav',
	data
  )
},
onEdit(data, row) {
  console.log(data, row)
  return Axios.put(
	'http://yapi.demo.qunar.com/mock/56001/nav/:id',
	data
  )
},
// 多选时, 参数为selected, 代表选中的行组成的数组
onDelete: selected => {
  return Axios.delete(
    'http://yapi.demo.qunar.com/mock/56001/nav',
    {
      id: selected.map(v => v.id)
    }
  )
}


  }
}
</script>
<style lang="less">
</style>