<style lang="less">
  .vertical-center-modal {
    display: flex;
    align-items: center;
    justify-content: center;

    .ivu-modal {
      top: 0;
    }
  }
  .main .single-page-con .single-page {
      height: 100%;
      margin: 0 10px 0 10px;
  }
</style>
<template>
  <div class="area_manage">
    <div class="area_manageWrap" :style="{width: shrink?'20px':'200px', overflow: shrink ? 'visible' : 'auto'}">

    </div>
    <div class="area_container" :style="{left: shrink?'20px':'200px'}">
      <div style="width:100%;">
        <Row type="flex" justify="start" class="code-row-bg">
          <i-col span="6"></i-col>
          <i-col span="6"></i-col>
          <i-col span="6"></i-col>
          <i-col span="6"><i-button type="ghost" size="small" :loading="modal_loading">新增</i-button></i-col>
        </Row>
      </div>
      <div style="width:100%;">
        <Table border :columns="columns7" :data="data6"></Table>
      </div>

    </div>
    <div>
      <Modal :width="600" v-model="modal10" :mask-closable="false" title="编辑" :closable="true" :scrollable="true"
             class="modalForms" class-name="vertical-center-modal">
        <Form ref="formRedacct" :model="formRedacct" :rules="ruleRedacct" :label-width="60" :show-message="false">
          <Row :gutter="20" class="code-row-bg">
            <i-col span="12" class-name="empty_icol">
              <div>
                <FormItem label="编号" prop="serialNumber">
                  <i-input v-model.trim="formRedacct.serialNumber" placeholder="请输入编号"
                           size="small"></i-input>
                </FormItem>
              </div>
            </i-col>
            <i-col span="12" class-name="empty_icol">
              <div>
                <FormItem label="营业厅" prop="serviceHall">
                  <i-input v-model.trim="formRedacct.serviceHall" placeholder="请输入营业厅"
                           size="small"></i-input>
                </FormItem>
              </div>
            </i-col>
          </Row>
        </Form>
        <div slot="footer">
          <Button type="primary" size="small" @click="handleEnsure('formRedacct')">提交</Button>
          <Button type="ghost" size="small" @click="handleEmpty('formRedacct')" style="margin-left: 8px">清空
          </Button>
          <Button type="ghost" size="small" :loading="modal_loading" @click="callOff">关闭</Button>
        </div>
      </Modal>
    </div>
  </div>


</template>

<script>
  export default {
    name: 'area_manage',
    data() {
      return {
        shrink: false,
        columns7: [
          {
            title: '编号',
            key: 'serialNumber'
          },
          {
            title: '营业厅',
            key: 'serviceHall'
          },
          {
            title: '操作',
            key: 'action',
            width: 190,
            align: 'center',
            render: (h, params) => {
              return h('div', [
                h('Button', {
                  props: {
                    type: 'primary',
                    size: 'small'
                  },
                  style: {
                    marginRight: '5px'
                  },
                  on: {
                    click: () => {
                      this.showone(params.index)
                    }
                  }
                }, '编辑'),
                h('Button', {
                  props: {
                    type: 'error',
                    size: 'small'
                  },
                  on: {
                    click: () => {
                      this.removes(params.index)
                    }
                  }
                }, '删除')
              ])
            }
          }
        ],
        data6: [
          {
            serviceHall: '郑州营业厅',
            serialNumber: 18
          },
          {
            serviceHall: '洛阳营业厅',
            serialNumber: 24
          },
          {
            serviceHall: '泰州营业厅',
            serialNumber: 30
          },
          {
            serviceHall: '陕州营业厅',
            serialNumber: 26
          }
        ],
        modal10: false,
        modal11: false,
        modal_loading: false,
        value1: '1',
        formRedacct: {
          serialNumber: '',
          serviceHall: ''
        },
        ruleRedacct: {
          serialNumber: [
            {
              required: false,
              message: '',
              trigger: 'blur'
            }
          ],
          serviceHall: [
            {
              required: false,
              message: '',
              trigger: 'blur'
            }
          ]
        },
        formRedact: {
          serviceHallName: ''
        },
        ruleRedact: {
          serviceHallName: [
            {
              required: false,
              message: '',
              trigger: 'blur'
            }
          ]
        }
      }
    },
    methods: {
      showone(index) {
        this.modal10 = true
        this.formRedacct.serialNumber = this.data6[index].serialNumber
        this.formRedacct.serviceHall = this.data6[index].serviceHall
      },
      removes(index) {
        this.data6.splice(index, 1)
      },
      handleEnsure(name) {
        this.$refs[name].validate(valid => {
          if (valid) {
            this.$Message.success('提交成功!')
          } else {
            this.$Message.error('提交失败!')
          }
        })
      },
      handleEmpty(name) {
        this.$refs[name].resetFields()
      },
      callOff() {
        this.modal_loading = true
        setTimeout(() => {
          this.modal_loading = false
          this.modal10 = false
        }, 200)
      }
    }
  }
</script>

<style lang="less">
  .area_manage {
    height: 100%;
    position: relative;
    border: 1px solid red;
    .area_manageWrap {
      height: 100%;
      top: 0;
      left: 0;
      z-index: 21;
      transition: width 0.3s;
      border: 1px solid blue;
    }
    .area_container {
      position: absolute;
      top: 0px;
      right: 0;
      bottom: 0;
      overflow: auto;
      border-left: 1px solid #e7e8ea;
      z-index: 1;
      transition: left 0.3s;
      border: 1px solid #333;
    }
    .ivu-tree li ul {
      padding: 0 0 0 5px;
    }
  }
</style>
