<template>
  <div class="demo">
    <template v-if="type == '01'">
      <div class="flex" style="flex-wrap: wrap;">
        <div style="min-width: 280px; margin: 0 20px 20px;">
          <kl-sidebar :data="channels" @select="handleSelect">
          </kl-sidebar>
        </div>
        <div style="min-width: 280px; margin: 0 20px 20px;">
          <kl-sidebar :data="channels" @select="handleSelect" class="kl-sidebar-dark">
          </kl-sidebar>
        </div>
      </div>
    </template>
    <template v-else-if="type == '02'">
      <div class="flex" style="flex-wrap: wrap;">
        <div style="min-width: 280px; margin: 0 20px 20px;">
          <kl-sidebar :data="channels" @select="handleSelect">
            <template slot="header">
              <i class="iconfont icon-system" />
              导航菜单
            </template>
          </kl-sidebar>
        </div>
        <div style="min-width: 280px; margin: 0 20px 20px; height: 300px;">
          <kl-sidebar :data="channels" @select="handleSelect" class="kl-sidebar-dark">
            <template slot="header">
              <i class="iconfont icon-system" />
              导航菜单
            </template>
            <template slot="footer">
              <i class="iconfont icon-github" />
              Version: v0.14.56
            </template>
          </kl-sidebar>
        </div>
      </div>
    </template>
  </div>
</template>

<script lang="ts">
import { Component, Emit, Model, Prop, Provide, Vue, Watch } from 'vue-property-decorator'

import type { ChannelDataNode, FilterQuery } from '@kenote/common'
import type { PlusKeywordsNode } from '@/types'

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
            route: '/components/searchbar',
            description: '频道搜索框，用于搜索频道下子页面',
            tag: '3_success'
          }
        ]
      }
    ]
  }
]

@Component
export default class Demo extends Vue {

  @Prop({ default: 'default' })
  type!: string

  @Provide()
  channels: ChannelDataNode<PlusKeywordsNode>[] = channels

  handleSelect (index: string) {
    console.log(index)
  }

}
</script>

<style lang="less">
// .markdown-body {
//   .demo ol, .demo ul {
//     padding-left: 0;
//   }
//   // .demo li+li {
//   //   margin-top: 0;
//   // }
// }

.kl-sidebar-dark {
  &.kl-sidebar, .el-menu--vertical, .el-menu--horizontal {
    background-color: rgb(68, 76, 84) ;
    border-right: 1px solid #373737;
    .header {
      background-color: #3c444a;
      color: rgb(255, 255, 255) !important;
      border-bottom: 1px solid #373737;
    }
    .footer {
      background-color: #3c444a;
      color: rgb(255, 255, 255) !important;
      border-top: 1px solid #373737;
    }
    .el-menu {
      background-color: rgb(68, 76, 84);
      
    }

    .el-submenu__title, .el-menu-item {
      color: rgb(255, 255, 255) !important;
      background-color: rgb(68, 76, 84) !important;

      &:hover {
        background-color: rgb(54, 61, 67) !important;
      }
    }

    .el-menu-item.is-active {
      background-color: #373d41 !important;
      color: rgb(255, 208, 75) !important;
    }
  }
}
</style>