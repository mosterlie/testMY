<template>
  <div class="app-container">
    <div>
      <el-form ref="form" :model="form" label-width="120px">
        <el-form-item label="Activity name">
          <el-input v-model="form.title"></el-input>
          <el-input inputSize="10px" style="width:100px"></el-input>
        </el-form-item>
      </el-form>
    </div>
    <el-table :data="list" v-loading.body="listLoading" element-loading-text="Loading" border fit highlight-current-row>
      <el-table-column align="center" label='Num' width="60">
        <template slot-scope="scope">
          {{scope.$index + 1}}
        </template>
      </el-table-column>
      <el-table-column align="center" label='Name' width="210">
        <template slot-scope="scope">
          {{scope.$index}}
        </template>
      </el-table-column>
      <el-table-column label="City" width="330" align="center">
        <template slot-scope="scope">
          {{scope.row.author}}
        </template>
      </el-table-column>
      <el-table-column label="Region" width="150" align="center">
        <template slot-scope="scope">
          <span>{{scope.row.author}}</span>
        </template>
      </el-table-column>
      <el-table-column label="Mobile" width="150" align="center">
        <template slot-scope="scope">
          {{scope.row.pageviews}}
        </template>
      </el-table-column>
      <el-table-column class-name="status-col" label="Vehicle Info" width="200" align="center">
        <template slot-scope="scope">
        </template>
      </el-table-column>
      <el-table-column align="center" prop="created_at" label="Operation">
        <template slot-scope="scope">
          <button @click="getData()">tt</button>
          <el-tag :type="'published' | statusFilter" @click="getData()">view</el-tag>
          <el-tag :type="'draft' | statusFilter">draft</el-tag>
          <el-tag :type="'deleted' | statusFilter">delete</el-tag>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
  import { getList } from '@/api/table'

  export default {
    data() {
      return {
        list: null,
        listLoading: true,
        form: {
          content: '33',
          title: 'sss',
          deleted: 'deleted',
          published: 'published',
          draft: 'draft'
        }
      }
    },
    filters: {
      statusFilter(status) {
        const statusMap = {
          published: 'success',
          draft: 'gray',
          deleted: 'danger'
        }
        return statusMap[status]
      }
    },
    created() {
      this.fetchData()
    },
    methods: {
      fetchData() {
        this.listLoading = true
        getList(this.listQuery).then(response => {
          this.list = response.data.items
          this.listLoading = false
        })
      },
      getData() {
        this
          .$http
          .get({ url: 'http://localhost:8080/customer/23' })
          .then((data) => {
            alert(data);
          })
      }
    }
  }
</script>
