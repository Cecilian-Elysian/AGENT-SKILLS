# Obsidian Canvas JSON 格式参考

## 文件结构

Obsidian `.canvas` 文件是一个 JSON 格式，包含了节点(nodes)和边(edges)的定义。

## 完整结构

```json
{
  "nodes": [],
  "edges": []
}
```

## 节点 (Nodes)

### 通用属性

| 属性 | 类型 | 描述 |
|------|------|------|
| id | string | 节点唯一标识符 |
| type | string | 节点类型: "text", "image", "link" |
| x | number | 左上角 X 坐标 |
| y | number | 左上角 Y 坐标 |
| width | number | 节点宽度(px) |
| height | number | 节点高度(px) |

### text 类型

```json
{
  "id": "node-1",
  "type": "text",
  "text": "这是卡片内容，支持 **Markdown** 格式",
  "width": 300,
  "height": 200,
  "x": 100,
  "y": 100
}
```

### image 类型

```json
{
  "id": "node-2",
  "type": "image",
  "file": "attachments/image.png",
  "width": 400,
  "height": 300,
  "x": 500,
  "y": 100
}
```

### link 类型

```json
{
  "id": "node-3",
  "type": "link",
  "link": "path/to/note.md",
  "title": "相关笔记标题",
  "width": 250,
  "height": 100,
  "x": 300,
  "y": 400
}
```

## 边 (Edges)

### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| id | string | 边唯一标识符 |
| fromNode | string | 源节点 ID |
| fromSide | string | 源连接边: "top", "right", "bottom", "left" |
| toNode | string | 目标节点 ID |
| toSide | string | 目标连接边: "top", "right", "bottom", "left" |

### 示例

```json
{
  "id": "edge-1",
  "fromNode": "node-1",
  "fromSide": "right",
  "toNode": "node-2",
  "toSide": "left"
}
```

## 布局建议

### 坐标系统
- 原点 (0,0) 在画布左上角
- X 向右增加
- Y 向下增加

### 常用间距
- 水平节点间距：250-350px
- 垂直节点间距：200-300px
- 边距：至少 50px

### 推荐节点尺寸
| 类型 | 建议宽度 | 建议高度 |
|------|----------|----------|
| text | 250-400px | 150-300px |
| image | 300-500px | 自动(按比例) |
| link | 200-300px | 80-120px |

## 完整示例

```json
{
  "nodes": [
    {
      "id": "central",
      "type": "text",
      "text": "# 设计模式\n\n软件开发中的最佳实践",
      "width": 300,
      "height": 150,
      "x": 400,
      "y": 300
    },
    {
      "id": "creational",
      "type": "text",
      "text": "## 创建型\n- 工厂方法\n- 单例模式\n- 建造者模式",
      "width": 200,
      "height": 180,
      "x": 100,
      "y": 150
    },
    {
      "id": "structural",
      "type": "text",
      "text": "## 结构型\n- 适配器\n- 装饰器\n- 代理模式",
      "width": 200,
      "height": 180,
      "x": 100,
      "y": 400
    },
    {
      "id": "behavioral",
      "type": "text",
      "text": "## 行为型\n- 观察者\n- 策略\n- 命令模式",
      "width": 200,
      "height": 180,
      "x": 700,
      "y": 150
    }
  ],
  "edges": [
    {
      "id": "edge-1",
      "fromNode": "creational",
      "fromSide": "right",
      "toNode": "central",
      "toSide": "left"
    },
    {
      "id": "edge-2",
      "fromNode": "structural",
      "fromSide": "right",
      "toNode": "central",
      "toSide": "left"
    },
    {
      "id": "edge-3",
      "fromNode": "central",
      "fromSide": "right",
      "toNode": "behavioral",
      "toSide": "left"
    }
  ]
}
```

## 注意事项

1. **ID 唯一性**：所有节点和边的 ID 必须在同一文件中唯一
2. **有效引用**：边的 fromNode 和 toNode 必须引用存在的节点 ID
3. **数值类型**：坐标和尺寸必须为数字，不能是字符串
4. **Markdown 支持**：text 类型的 text 字段支持标准 Markdown 语法
5. **相对路径**：image 的 file 和 link 的 link 应使用相对路径
