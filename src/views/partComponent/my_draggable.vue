<template>
  <div
    ref="editMainBox"
    id="editMainBox"
    class="editMainBox_container"
    :style="{
            width: editorAreaSize.width + 'px',
            height: editorAreaSize.height + 'px',
            backgroundImage: `url(${pageBgImgUrl})`,
            backgroundColor: pageBgColor
        }"
  >
    <template v-for="item in widgetList">
      <vue-draggable-resizable
        :key="item.uuid"
        :parent="true"
        :x="item.dragPosition.x"
        :y="item.dragPosition.y"
        :w="item.dragSize.width"
        :h="item.dragSize.height"
        :minWidth="20"
        :minHeight="20"
        @dragstop="onDragStop"
        @resizestop="onResizeStop"
        @activated="onActivated(item)"
      >
        <component :is="item.componentKey" :uuid="item.uuid"></component>
      </vue-draggable-resizable>
    </template>
  </div>
</template>

<script>
import { mapActions, mapState, mapGetters } from 'vuex'
import VueDraggableResizable from './draggable/vue-draggable-resizable'
import _ from 'lodash'
import TestComponentOne from './testComponents/testComponentOne'
import TestComponentTwo from './testComponents/testComponentTwo'
import TestComponentThree from './testComponents/testComponentThree'
import TitleChildOne from './components/title/TitleChildOne/index'
import TitleChildTwo from './components/title/TitleChildTwo/index'
export default {
  name: 'myDraggable',
  components: {
    VueDraggableResizable,
    TestComponentOne,
    TestComponentTwo,
    TestComponentThree,
    TitleChildOne,
    TitleChildTwo
  },
  props: {},
  data() {
    return {
      activeUUid: ''
    }
  },
  computed: {
    ...mapState('partComponent', ['widgetList', 'pageBgColor', 'pageBgImgUrl']),
    ...mapGetters('partComponent', ['editorAreaSize', 'requestDataList'])
  },

  created() {},
  methods: {
    ...mapActions('partComponent', [
      'setActivedWidget',
      'updateWidgetDragPos',
      'updateWidgetDragSize'
    ]),

    onDragStop(x, y) {
      this.updateWidgetDragPos({
        x: x,
        y: y,
        uuid: this.activeUUid
      })
    },

    onResizeStop(x, y, width, height) {
      this.updateWidgetDragPos({
        x: x,
        y: y,
        uuid: this.activeUUid
      })
      this.updateWidgetDragSize({
        width: width,
        height: height,
        uuid: this.activeUUid
      })
    },

    onActivated(params) {
      this.activeUUid = params.uuid
      const actWidget = this.widgetList.find(v => v.uuid === params.uuid)
      console.log('actWidget: ', actWidget)
      this.setActivedWidget(_.cloneDeep(actWidget))
    }
  }
}
</script>

<style lang="scss" scoped>
.editMainBox_container {
  cursor: pointer;
  position: relative;
  background-size: 100% 100%;
  background-repeat:no-repeat;
  box-shadow: 0 2px 12px 0 #777777;
}
</style>
