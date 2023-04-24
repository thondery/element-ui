<template>
  <el-submenu v-if="children?.length > 0" :index="index">
    <template slot="title">
      <i v-if="icon" v-bind:class="icon"></i>
      {{ name }}
    </template>
    <template v-for="(item, key) in children">
      <kl-sidebar-item v-if="item" 
        :key="key"
        :name="item.name"
        :icon="item.icon"
        :index="item.route ?? item.key"
        :children="item.children"
        :tag="item.tag"
        >
        
      </kl-sidebar-item>
    </template>
    
  </el-submenu>
  <el-menu-item v-else :index="index">
    <i v-if="icon" v-bind:class="icon"></i>
    {{ name }}
    <el-tag v-if="tag" class="kl-sidebar-item_tag" :type="getag(tag, 'type')" effect="dark">{{ getag(tag, 'label') }}</el-tag>
  </el-menu-item>
</template>

<script lang="ts">
import { Component, Emit, Model, Prop, Provide, Vue, Watch } from 'vue-property-decorator'
import { ChannelDataNode, CommonDataNode, FilterQuery, initMaps } from '@kenote/common'
// import { SidebarItem } from './'
import { get } from 'lodash'

@Component<KlSidebarItem>({
  name: 'KlSidebarItem',
  components: {
    // SidebarItem: KlSidebarItem
  }
})
export default class KlSidebarItem extends Vue {

  @Prop({ default: '' })
  name!: string

  @Prop({ default: '' })
  icon!: string

  @Prop({ default: undefined })
  children!: ChannelDataNode<{ tag?: string }>[]

  @Prop({ default: '' })
  index!: string

  @Prop({ default: '' }) // 3_(success/info/warning/danger)
  tag!: string

  getag (value: string, name: string) {
    let [ label, type ] = value.split('_')
    return get({ label, type }, name)
  }

}
</script>

<style lang="less">
.kl-sidebar-item_tag {
  float: right;
  margin-top: 9px;
  border-radius: 15px;
  min-width: 30px;
  text-align: center;
  height: 30px;
  line-height: 30px;
  scale: .95;
}
</style>