<template>
  <div
    :class="[playState ? 'anm-' + val.animationName : '']"
    :style="{
      position: 'absolute',
      width: val.width / 7.5 + '%',
      height: val.height / h * 100 + '%',
      left: val.left / 7.5 + '%',
      top: val.top / h * 100 + '%',
      zIndex: val.z,
      color: val.color
    }"
    contenteditable="true"
    @blur="(e) => updateText(e, val.uuid)"
    v-html="val.text"/>
</template>

<script>
const WIDGET_NAME = 'braid-container'

export default {
  name: WIDGET_NAME,
  title: 'Container',
  setting: {
    type: WIDGET_NAME,
    align: 'flex-start',
    animationName: '',
    backPic: '',
    backPicUrl: '',
    belong: 'page',
    bgColor: '',
    borderColor: '',
    borderWidth: 0,
    dir: 'row',
    display: 'flex',
    dragable: true,
    hasGuide: true,
    height: 300,
    isChild: false,
    isContainer: true,
    isUpload: false,
    justify: 'flex-start',
    left: 50,
    name: '',
    radius: 0,
    resizable: true,
    top: 0,
    width: 650,
    z: 0
  },
  props: ['h', 'val', 'playState'],

  methods: {
    updateText (e, uuid) {
      let text = e.target.innerHTML
      this.$vpd.commit('updateData', {
        uuid: uuid,
        key: 'text',
        value: text
      })
    }
  }
}
</script>

<style scoped>
.lz-container {
  background-repeat: no-repeat;
  background-position: center;
  background-size: 100%;
}
</style>
