<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="page">
    <!-- 节点面板 -->
    <div class="node_panel">
      <div
        v-for="item in nodeList"
        :key="item"
        class="node_li"
      >
        <div
          :class="['item_shape', item]"
          :draggable="true"
          @dragend="addNode(item, $event)"
        ></div>
        <div>{{ item }}</div>
      </div>
    </div>
    <!-- 画布挂载点 -->
    <div id="mountNode"></div>
  </div>
</template>

<script>
import G6 from '@antv/g6'

export default {
  name: 'AntvG',
  data(){
    return {
      nodeList:  [
        'rect',
        'circle',
        'rect-node',
      ],
      // 点集
      nodes: [
        {
          id: 'node1',
          x: 300,
          y: 200,
        },
        {
          id: 'node2',
          x: 600,
          y: 200,
        },
      ],
      // 边集
      edges: [
        // 表示一条从 node1 节点连接到 node2 节点的边
        {
          source: 'node1',
          target: 'node2',
        },
      ],
      graph: null
    }
  },
  async mounted() {
    const data = {
      nodes: [
        {
          id: 'node_circle',
          x: 100,
          y: 100,
          type: 'circle',
          label: 'circle'
        },
        {
          id: 'node_rect',
          x: 200,
          y: 100,
          type: 'rect',
          label: 'rect'
        },
        {
          id: 'node-diamond',
          x: 460,
          y: 100,
          type: 'diamond',
          label: 'diamond'
        },
        {
          id: 'node-star',
          x: 660,
          y: 100,
          //size: [60, 30],
          type: 'star',
          label: 'star'
        },
        {
          id: 'node-modelRect',
          x: 900,
          y: 100,
          description: '描述文本xxxxxxxxxxx',
          type: 'modelRect',
          label: 'modelRect',
          stateStyles: {
            hover: {
              // keyShape 的状态样式
              fill: '#d3adf7',
              // name 为 node-label 的子图形在该状态值下的样式
              'node-label': {
                fontSize: 15
              }
            }
          }
        }
      ]
    }

    this.graph = new G6.Graph({
      container: 'mountNode',
      width: 1500,
      height: 300,
      nodeStateStyles: {
        hover: {
          // keyShape 的状态样式
          fill: '#d3adf7',
          // name 为 node-label 的子图形在该状态值下的样式
          'node-label': {
            fontSize: 15
          }
        }
      },
      animate: true, // Boolean，切换布局时是否使用动画过度，默认为 false
      animateCfg: {
        duration: 500, // Number，一次动画的时长
        easing: 'linearEasing' // String，动画函数
      },
      modes: {
          // 支持的 behavior
          default: [
            'zoom-canvas',
            'drag-canvas',
            'drag-node',
            'drag-shadow-node',
            'canvas-event',
            'delete-item',
            'select-node',
            'hover-node',
            'active-edge'
          ]
        },
    })
    this.graph.data(data)
    this.graph.render()
  },
  methods:{
    // 向画布添加节点
    addNode(type, e) {
      console.log('添加节点---', type, e);
      // 将屏幕/页面坐标转换为渲染坐标
      const point = this.graph.getPointByClient(e.x, e.y)
      // 新创建的节点信息
      const model = {
        id: 'node' + Math.random(), // id使用了随机数，尽可能避免重复
        label: type, // 文本标签
        type: type, // 图片类型的节点
        x: point.x,
        y: point.y
      }
      this.graph.addItem('node', model, false)
    }

  }
}
</script>

<style>

.page {
  flex: 1;
  height: 100%;
  overflow: hidden;
  position: relative;
}

#graph {
  width: 100%;
  height: 100%;
}

.node_panel {
  position: absolute;
  left: 10px;
  top: 10px;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.3);
  box-sizing: border-box;
  padding: 10px 4px;
  border-radius: 4px;
}

.node_li {
  margin-bottom: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
  user-select: none;
}

.item_shape {
  width: 20px;
  height: 20px;
  border: 1px solid #ccc;
}

.circle {
  border-radius: 50%;
}
</style>