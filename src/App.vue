<template>
  <div id="app">
    <AntvG></AntvG>
    <!-- <DragView></DragView> -->
  </div>
</template>

<script>
// import MyCollapse from './views/collapse'
// import MultiSel from './views/multiSel/indexSelect.vue'
import AntvG from './views/avteG6/index.vue'
// import DragView from "./views/dragView/index.vue"

export default {
  name: 'App',
  components: {
    // MyCollapse,
    AntvG,
    // DragView
  },
  data() {
    return {
      myfields: [
        {
          order: 1,
          key: 'task_types',
          name: '任务类型',
          sub_key: 'tree_params',
          sub_name: null,
          type: 'str',
          children: [
            {
              order: 11,
              key: 'max_depth',
              name: '任务类型',
              sub_name: null,
              type: 'str',
              children: []
            },
            {
              order: 22,
              key: 'min_sample_split',
              name: '任务类型',
              sub_name: null,
              type: 'str',
              children: []
            },
            {
              order: 33,
              key: 'min_child_weight',
              name: '最小的孩子权重',
              sub_name: null,
              type: 'str',
              children: [
                {
                  order: 44,
                  key: 'subsample_feature_rate',
                  name: '子简单将来速率',
                  sub_name: null,
                  type: 'str',
                  children: []
                },
                {
                  order: 55,
                  key: 'calculator_param',
                  name: '随机速率',
                  sub_name: null,
                  type: 'str',
                  children: []
                }
              ]
            }
          ]
        },
        {
          order: 2,
          key: 'objective_param',
          name: '目标参数',
          sub_key: 'tree_params',
          sub_name: null,
          type: 'str',
          children: [
            {
              order: 11,
              key: 'use_missing',
              name: '任务类型',
              sub_name: null,
              type: 'str',
              children: []
            },
            {
              order: 22,
              key: 'zero_as_missing',
              name: '任务类型',
              sub_name: null,
              type: 'str',
              children: []
            },
            {
              order: 33,
              key: 'objective',
              name: '任务类型',
              sub_name: null,
              type: 'str',
              children: []
            }
          ]
        },
        {
          order: 77,
          key: 'objective',
          name: '任务类型',
          sub_name: null,
          type: 'str',
          children: []
        }
      ],
      iphone: 100000
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
