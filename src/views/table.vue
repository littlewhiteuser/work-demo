<template>
  <div>
    <template>
      <el-table :data="tableData">
        <el-table-column>
          <template slot-scope="scope">
            <el-checkbox
              v-model="scope.row.isCheck"
              @change="changeCheck(scope.row, scope.$index)"
            ></el-checkbox>
            <span></span>
          </template>
        </el-table-column>
        <el-table-column
          v-for="(item, index) in colConfigs"
          :prop="item.prop"
          :key="item.prop + index"
          :label="item.label"
        >
          <!-- <template slot-scope="scope">
            {{ scope.row.date }}
          </template> -->
        </el-table-column>
      </el-table>
      <el-checkbox
        @change="allSelect"
        v-model="isAllSelect"
      ></el-checkbox>
    </template>
  </div>
</template>

<script>
export default {
  name: 'baseTable',
  props: ['tableData'],
  data () {
    return {
      isAllSelect: false, // 是否全选
      colConfigs: [
        { prop: 'id', label: 'id' },
        { prop: 'name', label: '姓名' },
        { prop: 'age', label: '年龄' }
      ],
      arr: []
    }
  },
  methods: {
    allSelect (value) {
      this.tableData.map((item, index) => {
        this.$set(this.tableData[index], 'isCheck', value)
        this.$set(this.arr, index, value)
      })
    },
    changeCheck (row, index) {
      this.$set(this.arr, index, row.isCheck)
      console.log(this.arr, '测试')
      this.$emit('calcNum', this.arr)
    }
  },
  watch: {
    'tableData.length': {
      handler (newValue, oldValue) {
        console.log(newValue, oldValue)
        if (newValue !== oldValue) {
          this.arr = Array.from({ length: newValue }, () => false)
        }
      },
      immediate: true
    },
    arr: {
      handler (newValue, oldValue) {
        if (newValue.includes(false)) {
          this.isAllSelect = false
        } else if (!newValue.includes(false)) {
          this.isAllSelect = true
        }
      },
      deep: true
    }
  }
}
</script>

<style scoped lang="scss">
</style>
