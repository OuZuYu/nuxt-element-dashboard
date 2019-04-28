<template>
  <div>
    <el-data-table v-bind="tableConfig"></el-data-table>
  </div>
</template>

<script>
import {formatDate} from '../const/filter'

export default {
  data() {
    let validateVersion = (rule, value, callback) => {
      if (!value) {
        return callback(new Error('请输入版本'))
      }
      if (!/^\d\d*\.\d{1}$/.test(value)) {
        return callback(new Error('保留一位的小数'))
      } else {
        callback()
      }
    }

    return {
      tableConfig: {
        url: '/api/components',

        columns: [
          {
            type: 'selection',
            width: 30
          },
          {
            prop: 'name',
            label: '组件名称',
            width: 150
          },
          {
            prop: 'category',
            label: '分类'
          },
          {
            prop: 'version',
            label: '版本'
          },
          {
            prop: 'language',
            label: '开发语言'
          },
          {
            prop: 'date',
            label: '最后更新时间',
            formatter: row => {
              return formatDate(row.date, 'YYYY-MM-DD')
            }
          },
          {
            prop: 'status',
            label: '状态',
            formatter: row => {
              if (row.status === 1) {
                return <div class="on">上架</div>
              } else {
                return <div class="off">下架</div>
              }
            }
          }
        ],

        searchForm: [
          {
            $type: 'input',
            $id: 'name',
            label: '组件名称',
            $el: {
              placeholder: '请输入'
            }
          },
          {
            $type: 'select',
            $id: 'category',
            label: '分类',
            $el: {
              placeholder: '请输入'
            },
            $options: ['A', 'B', 'C'].map(f => ({label: f + '类', value: f}))
          },
          {
            $type: 'select',
            $id: 'status',
            label: '状态',
            $el: {
              placeholder: '请输入'
            },
            $options: [
              {
                label: '上架',
                value: 1
              },
              {
                label: '下架',
                value: 0
              }
            ]
          }
        ],

        extraButtons: [
          {
            type: 'default',
            text: '下架',
            show: row => row.status === 1,
            atClick: row => {
              return this.$axios.put('/api/components', {status: 0})
            }
          },
          {
            type: 'default',
            text: '上架',
            show: row => row.status === 0,
            atClick: row => {
              return this.$axios.put('/api/components', {status: 1})
            }
          }
        ],

        form: [
          {
            $type: 'input',
            $id: 'name',
            label: '组件名称',
            rules: [
              {required: true, message: '请输入组件名称', trigger: 'blur'}
            ],
            $el: {
              placeholder: '请输入组件名称'
            }
          },
          {
            $type: 'input',
            $id: 'version',
            label: '版本',
            rules: [{validator: validateVersion, trigger: 'blur'}],
            $el: {
              placeholder: '请输入组件版本'
            }
          },
          {
            $type: 'select',
            $id: 'category',
            label: '分类',
            $options: ['A', 'B', 'C'].map(f => ({label: f + '类', value: f})),
            rules: [
              {
                required: true,
                message: '请选择分类',
                trigger: 'blur'
              }
            ],
            $el: {
              style: 'width: 100%',
              placeholder: '请选择'
            }
          },
          {
            $type: 'select',
            $id: 'status',
            label: '状态',
            $options: [
              {
                label: '上架',
                value: 1
              },
              {
                label: '下架',
                value: 0
              }
            ],
            rules: [
              {
                required: true,
                message: '请选择状态',
                trigger: 'blur'
              }
            ],
            $el: {
              style: 'width: 100%',
              placeholder: '请选择'
            }
          },
          {
            $type: 'select',
            $id: 'language',
            label: '语言',
            $options: ['javascript', 'java', 'node'].map(f => ({
              label: f,
              value: f
            })),
            rules: [
              {
                required: true,
                message: '请选择状态',
                trigger: 'blur'
              }
            ],
            $el: {
              style: 'width: 100%',
              placeholder: '请选择'
            }
          }
        ],

        hasView: true,

        onEdit(data, row) {
          data.id = row.id
          return this.$axios.put('/api/components/', data).then(res => {
            console.log(res)
          })
        }
      }
    }
  }
}
</script>

<style lang="less">
.on {
  color: #00cd00;
}

.off {
  color: #333;
}
</style>
