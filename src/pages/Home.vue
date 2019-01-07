<style scoped>
.layout {
    background: #f5f7f9;
    position: relative;
    overflow: hidden;
    height: 100%;
}

.layout-breadcrumb {
    padding: 10px 15px 0;
}

.layout-content {
    min-height: 200px;
    margin: 15px;
    overflow: auto;
    background: #fff;
    border-radius: 4px;
    height: 90%;
}

.layout-content-main {
    padding: 10px;
}

.layout-copy {
    text-align: center;
    padding: 10px 0 20px;
    color: #9ea7b4;
}

.layout-menu-left {
    background: #464c5b;
    display: none;
}

.layout-header {
    height: 50px;
    background: #fff;
}

.layout-logo-left {
    width: 90%;
    height: 55px;
    line-height: 55px;
    font-size: 28px;
    text-align: center;
    /*  background: #5b6270;
        border-radius: 3px;
        margin: 15px auto;*/
}

.layout-ceiling-main a {
    color: #9ba7b5;
}

.layout-hide-text .layout-text {
    display: none;
}

.ivu-col {
    transition: width .2s ease-in-out;
}

.ivu-row-flex {
    height: 100%;
}

.userinfo {
    display: inline-block;
    float: right;
}

.userinfo .ivu-dropdown {
    margin-top: 50px;
}

.ivu-dropdown {
    margin-right: 25px;
    margin-top: 22px;
}

.ivu-menu-submenu-title {
    padding: 14px;
}

.head-img {
    width: 100%;
    height: 55px;
    line-height: 55px;
    float: right;
    margin-top: -50px;
}

.head-img img {
    border-radius: 20px;
    margin: 10px 0px 10px 10px;
    width: 40px;
    height: 40px;
    float: right;
}

.layout-icon {
    padding: 5px 10px;
    float: left;
}

.layout-icon2 {
    position: absolute;
    right: 10px;
    top: 5px;
}

.layout-text {
    text-align: center;
    height: 55px;
    line-height: 55px;
}

.hc-modal {
    position: fixed;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
    background-color: rgba(0, 0, 0, 0.6);
    z-index: 1000;
    overflow: scroll;
}

.ivu-layout-sider {
    height: 100%;
}
</style>
<template>
    <div class="layout" :class="{'layout-hide-text': spanLeft < 5}">
        <Row type="flex">
            <i-col span='24'>
                <div class="layout-header">
                    <!-- fdsd -->
                    <Icon class="layout-icon" type="ios-arrow-back" size='40' color='ccc' />
                    <div class="layout-text">标题</div>
                    <Icon v-show="!modal1" @click="modal1=true" class="layout-icon2" size='40' color='ccc' type="navicon-round"></Icon>
                </div>
                <div class="layout-content">
                    <div class="layout-content-main">
                        <router-view></router-view>
                    </div>
                </div>
            </i-col>
        </Row>

        <!-- <Modal v-model="modal1" @on-ok.prevent="comfirmModifyPS" @on-cancel="cancel">
                                                                                                            fsdsdf
                                                                                                        </Modal> -->
        <div v-show='modal1' class="hc-modal" @click="modal1=false">
            <Sider hide-trigger :style="{background: '#fff'}">
                <Menu active-name="1-2" theme="light" width="auto" :open-names="['1']">
                    <Submenu name="1">
                        <template slot="title">
                            <Icon type="ios-navigate"></Icon>
                            Item 1
                        </template>
                        <MenuItem name="1-1">Option 1</MenuItem>
                        <MenuItem name="1-2">Option 2</MenuItem>
                        <MenuItem name="1-3">Option 3</MenuItem>
                    </Submenu>
                    <Submenu name="2">
                        <template slot="title">
                            <Icon type="ios-keypad"></Icon>
                            Item 2
                        </template>
                        <MenuItem @click.native="popMenu" name="2-1">Option 1</MenuItem>
                        <MenuItem name="2-2">Option 2</MenuItem>
                    </Submenu>
                    <Submenu name="3">
                        <template slot="title">
                            <Icon type="ios-analytics"></Icon>
                            Item 3
                        </template>
                        <MenuItem name="3-1">Option 1</MenuItem>
                        <MenuItem name="3-2">Option 2</MenuItem>
                    </Submenu>
                </Menu>
            </Sider>
            <Icon @click="modal1=true" :style="{'transform':modal1?'rotate(90deg)':'rotate(0deg)'}" style="color: #fff;transform: rotate(90deg);transition: all .5s;" class="layout-icon2" size='40' color='ccc' type="navicon-round"></Icon>
        </div>

    </div>
    <!-- 修改密码 模态框 -->

    <!-- 修改密码 模态框 -->
</template>

<script>
export default {
    data() {
        return {
            openNames: [this.$route.matched[0].name],
            curUserName: sessionStorage.getItem('user').replace(/\"/g, ""),
            modeType: "vertical",
            spanLeft: 5,
            spanRight: 19,
            logoIsDisplay: false,
            loading: true,
            modal1: false,
            formValidate: {
                oldPassword: '',
                newPassword: '',
                resetPassword: ''
            },
            ruleValidate: {
                oldPassword: [
                    { required: true, message: '密码不能为空', trigger: 'blur' }
                ],
                newPassword: [
                    { required: true, message: '密码不能为空', trigger: 'blur' }
                ],
                resetPassword: [
                    { required: true, message: '密码不能为空', trigger: 'blur' }
                ],
            }
        }
    },
    computed: {
        iconSize() {
            return this.spanLeft === 5 ? 14 : 24;
        },
        logoSize() {
            if (this.spanLeft !== 5) {
                this.logoIsDisplay = true;
                return 50;
            } else {
                this.logoIsDisplay = false;
                return 0;
            }
        }
    },
    methods: {
        popMenu() {
            // alert(90)
            this.$router.push('/')
        },
        toggleClick() {
            if (this.spanLeft === 5) {
                this.spanLeft = 1;
                this.spanRight = 23;
            } else {
                this.spanLeft = 5;
                this.spanRight = 19;
            }
        },
        modifyPassWord() {
            this.modal1 = true;
        },
        logout() {
            this.$router.push('/login');
        },
        comfirmModifyPS() {
            return false;
            this.$refs.formValidate.validate((valid) => {
                if (valid) {
                    this.modal1 = false;
                    //         this.loading = false;
                    this.$Message.success('提交成功!');
                } else {
                    this.$Message.error('表单验证失败!');
                    return false;
                }
            })
            // this.$Message.info('点击了确定');
        },
        cancel() {
            this.modal1 = false;
            this.$Message.info('点击了取消');
        },
        menuSelect(name) {
            this.$router.push({ path: name });
        },
        dropDown(name) {
            this.$router.push({ path: name });
            console.log(name);
        }

    },
    mounted() {
    }
}
</script>
<style scoped>
.ivu-select-dropdown .ivu-dropdown {
    margin: 0px 12px 0px 0px;
}

._dropdownList {
    /*  width: 100%;
    text-align: center; */
}

._iconCls {
    width: 56px;
    text-align: center;
}
</style>
