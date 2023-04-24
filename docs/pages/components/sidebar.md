# Sidebar

导航菜单

## Example

<dc-sidebar type="01" />

### Code

```vue
<template>
  <kl-sidebar :data="channels" />
</template>

<script lang="ts">
import { Component, Provide, Vue } from 'vue-property-decorator'
import { ChannelDataNode } from '@kenote/common'
import { PlusKeywordsNode } from '@kenote/element-ui'

const channels: ChannelDataNode<PlusKeywordsNode>[] = [
  {
    key: 'utilities',
    name: '工具集',
    label: 'utilities',
    route: '/utilities',
    children: [
      {
        key: 'command',
        name: '指令',
        children: [
          {
            key: 'parse-command',
            name: 'parseCommand',
            keywords: [ 'utilities', '工具', 'command', '指令', 'parse-command' ],
            route: '/utilities/parse-command',
            description: '解析字符串指令'
          },
          {
            key: 'run-command',
            name: 'runCommand',
            keywords: [ 'utilities', '工具', 'command', '指令', 'run-command' ],
            route: '/utilities/run-command',
            description: '运行指令集'
          }
        ]
      },
      {
        key: 'filter',
        name: '检索',
        children: [
          {
            key: 'filter-channel-datanode',
            name: 'filterChannelDataNode',
            keywords: [ 'utilities', '工具', 'filter', '检索', 'channel', 'datanode' ],
            route: '/utilities/filter-channel-datanode',
            description: '检索频道数据节点，结果返回到列表'
          }
        ]
      }
    ]
  },
  {
    key: 'components',
    name: '组件',
    label: 'components',
    route: '/components',
    children: [
      {
        key: 'basic',
        name: '基础',
        children: [
          {
            key: 'searchbar',
            name: 'Searchbar 频道搜索框',
            keywords: [ 'components', '组件', 'searchbar', '频道搜索框' ],
            route: '/components/searchbar',
            description: '频道搜索框，用于搜索频道下子页面'
          }
        ]
      }
    ]
  }
]

@Component
export default class Demo extends Vue {

  @Provide()
  channels: ChannelDataNode<PlusKeywordsNode>[] = channels

}
</script>
```

## Example

<dc-sidebar type="02" />

### Code

```vue
<template>
  <kl-sidebar :data="channels" >
    <template slot="header">
      <i class="iconfont icon-system" />
      导航菜单
    </template>
  </k-sidebar>
</template>

<script lang="ts">
import { Component, Provide, Vue } from 'vue-property-decorator'
import { ChannelDataNode } from '@kenote/common'
import { PlusKeywordsNode } from '@kenote/element-ui'

const channels: ChannelDataNode<PlusKeywordsNode>[] = [
  {
    key: 'utilities',
    name: '工具集',
    label: 'utilities',
    route: '/utilities',
    children: [
      {
        key: 'command',
        name: '指令',
        children: [
          {
            key: 'parse-command',
            name: 'parseCommand',
            keywords: [ 'utilities', '工具', 'command', '指令', 'parse-command' ],
            route: '/utilities/parse-command',
            description: '解析字符串指令'
          },
          {
            key: 'run-command',
            name: 'runCommand',
            keywords: [ 'utilities', '工具', 'command', '指令', 'run-command' ],
            route: '/utilities/run-command',
            description: '运行指令集'
          }
        ]
      },
      {
        key: 'filter',
        name: '检索',
        children: [
          {
            key: 'filter-channel-datanode',
            name: 'filterChannelDataNode',
            keywords: [ 'utilities', '工具', 'filter', '检索', 'channel', 'datanode' ],
            route: '/utilities/filter-channel-datanode',
            description: '检索频道数据节点，结果返回到列表'
          }
        ]
      }
    ]
  },
  {
    key: 'components',
    name: '组件',
    label: 'components',
    route: '/components',
    children: [
      {
        key: 'basic',
        name: '基础',
        children: [
          {
            key: 'searchbar',
            name: 'Searchbar 频道搜索框',
            keywords: [ 'components', '组件', 'searchbar', '频道搜索框' ],
            route: '/components/searchbar',
            description: '频道搜索框，用于搜索频道下子页面'
          }
        ]
      }
    ]
  }
]

@Component
export default class Demo extends Vue {

  @Provide()
  channels: ChannelDataNode<PlusKeywordsNode>[] = channels

}
</script>
```






## API

### Porps

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| ------ | ------ | ------ | ------ | :------: |
| mode | 模式 | string | horizontal / vertical | vertical |
| data | 菜单数据 | ChannelDataNode[] | -- | -- |
| collapse | 是否水平折叠收起菜单（仅在 mode 为 vertical 时可用） | boolean | -- | false |