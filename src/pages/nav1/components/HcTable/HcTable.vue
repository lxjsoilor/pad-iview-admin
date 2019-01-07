<template>
    <div>
        <Table :loading='loading' :data="tableData" :columns="tableColumns" stripe border></Table>
        <div style="margin: 10px;overflow: hidden">
            <div style="float: right;">
                <Page :total="total" :current="page" @on-change="changePage" show-total></Page>
            </div>
        </div>
    </div>
</template>

<script>
import {
    getUserListPage,
    removeUser,
    editUser,
    addUser
} from '../../../api/api';
export default {
    props: {
        tableData: {
            type: Array,
            default() {
                return [];
            }
        },
        tableColumns: {
            type: Object,
            default() {
                return {}
            }
        },
        queryString: {
            type: Object,
            default() {
                return {
                    page: 1
                }
            }
        },
        queryUrl: {
            type: String,
            default: ''
        }
    },
    data() {
        return {
            loading: false,
            total: 0,
            page: 1
        }
    },
    methods: {
        changePage(page) {

        },
        getTableData() {
            let para = {
                page: this.page
            };
            this.$Loading.start();
            getUserListPage(para).then((res) => {
                this.$Loading.finish();
                this.total = res.data.total;
                console.log(res.data.users, 9909090)
                this.tableData = res.data.users;

            });
        }
    },
}
</script>

<style>

</style>
