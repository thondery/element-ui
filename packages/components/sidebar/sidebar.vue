<template>
  <div class="kl-sidebar">
    <div class="header" v-if="$slots.header">
      <slot name="header"></slot>
    </div>
    <perfect-scrollbar :options="{ suppressScrollX: true }" style="flex: 1">
      <el-menu mode="vertical"
        :default-active="defaultActive"
        :collapse="collapse"
        :unique-opened="uniqueOpened"
        :router="router"
        @select="handleSelect"
        >
        <sidebar-item v-for="(item, key) in data ?? []" 
          :key="key"
          :name="item.name"
          :icon="item.icon"
          :children="item.children"
          :index="item.route ?? item.key"
          :tag="item.tag"
          >
          
        </sidebar-item>
      </el-menu>
    </perfect-scrollbar>
    <div class="footer" v-if="$slots.footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>



<script lang="ts">
import { Component, Emit, Model, Prop, Provide, Vue, Watch } from 'vue-property-decorator'
import { ChannelDataNode } from '@kenote/common'
import SidebarItem from './item.vue'

@Component<KlSidebar>({
  name: 'KlSidebar',
  components: {
    SidebarItem
  }
})
export default class KlSidebar extends Vue {

  @Prop({ default: '' })
  defaultActive!: string

  @Prop({ default: false })
  collapse!: boolean

  @Prop({ default: false })
  uniqueOpened!: boolean

  @Prop({ default: false })
  router!: boolean

  @Prop({ default: undefined })
  data!: ChannelDataNode<{ tag?: string }>[]

  @Emit('select')
  handleSelect (index: string) {}

}
</script>

<style lang="less">
.el-menu {
  border-right: 0;
  padding-left: 0 !important;
  margin-bottom: 0 !important;

  &.el-menu--horizontal {
    border-bottom: 0;
  }

  li+li {
    margin-top: 0;
  }

  .el-submenu .el-menu-item {
    padding: 0 16px;
  }
}

.kl-sidebar {
  display: flex;
  flex-direction: column;
  border-right: 1px solid #e6e6e6;
  background-color: #fff;
  color: #303133;
  font-size: 14px;
  height: inherit;
  justify-content: space-between;

  .header {
    height: 56px;
    line-height: 56px;
    display: flex;
    justify-content: center;
    font-weight: 400;
    border-bottom: 1px solid #e6e6e6;

    i {
      margin-right: 6px;
    }
  }

  .footer {
    height: 56px;
    line-height: 56px;
    display: flex;
    justify-content: center;
    font-weight: 400;
    border-top: 1px solid #e6e6e6;
    opacity: .7;

    i {
      margin-right: 6px;
    }
  }
}
</style>