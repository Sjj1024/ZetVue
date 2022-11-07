<template>
  <div class="fields">
    <div
      v-for="item in fields"
      :key="item.id"
    >
      <!-- 是折叠面板 -->
      <template v-if="item.children ? item.children.length > 0 : false">
        <div>
          <el-collapse
            v-model="activeNames"
            @change="handleChange"
          >
            <el-collapse-item :name="item.id">
              <!-- 标题提示 -->
              <template slot="title">
                <span class="title">{{item.key}}</span>
                <el-tooltip
                  :content="item.name"
                  effect="dark"
                  placement="top"
                >
                  <span class="el-icon-warning-outline"></span>
                </el-tooltip>
              </template>
              <!-- 折叠面板内容 -->
              <div>
                <MyCollapse :fields="item.children"></MyCollapse>
              </div>
            </el-collapse-item>
          </el-collapse>
        </div>
      </template>
      <!-- 是输入框 -->
      <template v-else>
        <div class="field-input">
          <div>
            <span class="title">{{item.key}}</span>
            <el-tooltip
              :content="item.name"
              effect="dark"
              placement="top"
            >
              <span class="el-icon-warning-outline"></span>
            </el-tooltip>
          </div>
          <input
            type="text"
            class="input"
          >
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyCollapse',
  props: {
    fields: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      activeNames: ['1']
    }
  },
  methods: {
    handleChange(val) {
      console.log(val)
    }
  }
}
</script>

<style scoped>
.fields {
  width: 350px;
}

.title {
  margin-right: 6px;
}

.field-input {
  display: flex;
  justify-content: space-between;
  margin-top: 6px;
  font-size: 13px;
}
</style>