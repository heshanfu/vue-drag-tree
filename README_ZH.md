# vue-drag-tree

[![Version](http://img.shields.io/npm/v/vue-drag-tree.svg)](https://www.npmjs.com/package/vue-drag-tree)[![Downloads](http://img.shields.io/npm/dm/vue-drag-tree.svg)](https://www.npmjs.com/package/vue-drag-tree)[![License](https://img.shields.io/npm/l/vue-drag-tree.svg?style=flat)](https://opensource.org/licenses/MIT)

> 这是一个Vue2.x的树组件。它允许你去拖拽任意节点，当然，“交换”会反映在data数据中。

**功能**

- **双击**节点**添加**一个字节点 
- 对节点进行**任意拖拽**
- **控制**特定节点**是否可拖**、**是否可放置**其他节点
- **增加/删除** 任意层级的节点（#待添加）

**[EN](README.md)** || **如果它对你有帮助的话，请Star支持！！！**

### 预览

------

![demo](static/preview.gif)

### 快速开始

------

**Install**

`npm install vue-drag-tree --save`

**Usage**

[一个简单的项目，用了vue-drag-tree](https://github.com/shuiRong/vue-drag-tree-demo)



main.js

```vue
import Vue from 'vue'
import VueDragTree from 'vue-drag-tree'

Vue.component('vue-drag-tree', VueDragTree)
```

test.vue

```vue
<template>
	<vue-drag-tree :data='data' :allowDrag='allowDrag' :allowDrop='allowDrop' :defaultText='"新节点"' @current-clicked='curNodeClicked' @drag="dragHandler" @drag-enter="dragEnterHandler" @drag-leave="dragLeaveHandler" @drag-over="dragOverHandler" @drag-end="dragEndHandler" @drop="dropHandler">
    </vue-drag-tree>
</template>
<script>
export default{
  data(){
    return{
      data: [
        {
          name: 'Node 0-0',
          id: 0,
          children: [
            {
              name: 'Node 1-1',
              id: 3,
              children: [
                {
                  name: 'Node 2-1',
                  id: 4,
                  children: []
                },
                {
                  name: 'Node 2-2',
                  id: 10,
                  children: []
                }
              ]
            },
            {
              name: 'Node 1-2',
              id: 13,
              children: []
            }
          ]
        },
        {
          name: 'Node 0-1',
          id: 14,
          children: []
        }
      ]
    }
  },
  methods: {
   	allowDrag(model, component) {
      if (model.name === 'Node 0-1') {
        // 不允许拖拽
        return false;
      }
      // 允许拖拽
      return true;
    },
    allowDrop(model, component) {
      if (model.name === 'Node 2-2') {
        // 不允许被放置
        return false;
      }
      // 允许被放置  
      return true;
    },
    curNodeClicked(model, component) {
      // console.log('curNodeClicked', model, component);
    },
    dragHandler(model, component, e) {
      // console.log('dragHandler: ', model, component, e);
    },
    dragEnterHandler(model, component, e) {
      // console.log('dragEnterHandler: ', model, component, e);
    },
    dragLeaveHandler(model, component, e) {
      // console.log('dragLeaveHandler: ', model, component, e);
    },
    dragOverHandler(model, component, e) {
      // console.log('dragOverHandler: ', model, component, e);
    },
    dragEndHandler(model, component, e) {
      // console.log('dragEndHandler: ', model, component, e);
    },
    dropHandler(model, component, e) {
      // console.log('dropHandler: ', model, component, e);
    }
  }
}
<script>
```

### 接口

---

**属性**

| 属性名      | 描述                                                  | 类型     | 默认值   |
| :---------- | :---------------------------------------------------- | :------- | :------- |
| data        | 节点树的数据                                          | Array    | －－     |
| defaultText | 新生成的节点的文本(name属性)                          | String   | 新增节点 |
| allowDrag   | 判断哪些节点可以被拖拽（return true表示允许）         | Function | ()=>true |
| allowDrop   | 判断哪些节点可以被塞入其他节点（return true表示允许） | Function | ()=>true |



**方法**

| 方法名          | 描述                                                       | 参数                                                         |
| --------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| current-clicked | 告诉你哪个节点被点击了，这个节点所在的组件是哪个           | (model,component) model: 当前被点击节点的数据． component: 当前节点所在的树组件 |
| drag            | 节点被拖动时触发的 `drag` 事件                             | (model,component,e) model: 当前被拖动节点的数据; component: 当前被拖动节点所在的树组件（VNode）; e: 拖拽事件 |
| drag-enter      | 当被拖动节点进入有效的放置目标时， `dragenter` 事件被触发  | (model,component,e) model: 有效放置目标节点的数据; component: 有效放置目标节点所在的树组件（VNode）; e: 拖拽事件 |
| drag-leave      | 当被拖动节点离开有效的放置目标时， `dragleave` 事件被触发  | (model,component,e) model: 有效放置目标节点的数据; component: 有效放置目标节点所在的树组件（VNode）; e: 拖拽事件 |
| drag-over       | 当节点被拖拽到一个有效的放置目标上时，触发 `dragover `事件 | (model,component,e) model: 有效放置目标节点的数据; component: 有效放置目标节点所在的树组件（VNode）; e: 拖拽事件 |
| drag-end        | 拖放事件在拖放操作结束时触发                               | (model,component,e) model: 当前被拖动节点的数据; component: 当前被拖动节点所在的树组件（VNode）; e: 拖拽事件 |
| drop            | 当节点被放置到一个有效的防止目标上时，`drop`被触发         | (model,component,e) model: 当前被拖动节点的数据; component: 当前被拖动节点所在的树组件（VNode）; e: 拖拽事件 |



**License**

------

[MIT](LICENSE)
