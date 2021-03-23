# canvas

## 安装

```
npm install canvas-vue-nyc
```

### 使用

```
<canvas-nyc />

import CanvasNyc from 'canvas-vue-nyc'

export default {
    components: {
        CanvasNyc,
    },
}
```

### 属性说明

| 属性   | 说明           | 类型   | 默认值 |
| ------ | -------------- | ------ | ------ |
| widht  | canvas 的宽度  | number | 1820   |
| height | canvas 的高度  | number | 260    |
| opt    | 用来划线的属性 | object | --     |

### Opt 说明

| 属性            | 说明                         | 类型   | 默认值 |
| --------------- | ---------------------------- | ------ | ------ |
| start           | 起点坐标                     | array  | [0,0]  |
| radius          | 弧度半径                     | number | --     |
| bgcolor         | 用来划线的属性               | object | --     |
| width           | 线的宽度                     | number | --     |
| color           | 线的颜色                     | color  | --     |
| notStartedColor | 未开始线段                   | color  | --     |
| path            | 线的路径（见 tip 1）         | array  | --     |
| tags            | 标示                         | array  | --     |
| notStarted      | 未开始路线的路径（见 tip 1） | array  | --     |

### tip1 路径说明

| 项    | 说明                |
| ----- | ------------------- |
| point | 画图坐标（见 tip2） |
| b     | 向下移动一个宽度    |
| t     | 向上移动一个宽度    |
| l     | 向左移动一个宽度    |
| r     | 向左移动一个宽度    |
| tr    | 上右弧度            |
| tl    | 上左弧度            |
| lb    | 左下弧度            |
| lt    | 左上弧度            |
| br    | 下右弧度            |
| bl    | 下左弧度            |
| rb    | 右下弧度            |
| rt    | 右上弧度            |

### tip2 point

point 数据类型 object
属性 X，Y
左右画传 X，上下画传 Y
X > 0 向右画 反之向左画
Y > 0 向下画 反之向上画
