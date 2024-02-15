# project_todolist

## 第一阶段练习成果,来源,尚硅谷v2->v3视频课程.
  ### 逻辑
  - 组件内通信依靠App总件下传props,数据在App内处理,再发送给末端item组件渲染到页面;
  - 新增数据由input组件收集用户输入,处理数据后依赖App事先传入的方法,通过传入参数的行为引起App内同等变化,从而实现数据的新增.
  - 修改,删除皆在App内完成,App将方法传入item组件,每当item发生变化时,item调用相应方法,命令App做出对应更新.
  ### 收获
  - nanoid:简易的id生成npm库,通过nanoid()生成独立id.
  - v-model方法适合用于组件内状态/状况/数据的改变.不建议通过v-model改变props传入的外部数据,可能引起bug.
  - 写了个很隐秘的复合bug,艰难改好,今后遇到bug时,首先一定要确认范围,将复杂任务拆分,不要心急...
## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
