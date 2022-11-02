<template>
  <button
    :class="[playState ? 'anm-' + val.animationName : '']"
    :style="{
      position: 'absolute',
      width: val.width / 7.5 + '%',
      height: val.height / h * 100 + '%',
      left: val.left / 7.5 + '%',
      top: val.top / h * 100 + '%',
      zIndex: val.z,
      backgroundColor: 'navy',
      color: val.color
    }"
    contenteditable="true"
    @blur="(e) => updateText(e, val.uuid)"
    v-html="val.text"/>
</template>

<script>

const WIDGET_NAME = 'braid-button'

export default {
  name: WIDGET_NAME,
  title: 'Button',
  setting: {
    type: WIDGET_NAME,
    isContainer: false,
    isUpload: false,
    hasGuide: true,
    isChild: true,
    dragable: true,
    resizable: true,
    name: '',
    width: 250,
    height: 60,
    left: 50,
    top: 0,
    z: 0,
    bgColor: '#000000',
    backPic: '',
    backPicUrl: '',
    color: '#ffffff',
    text: 'Button',
    belong: 'page',
    animationName: ''
  },
  props: ['h', 'val', 'playState'],

  methods: {
    updateText (e, uuid) {
      this.$emit('update', e.target.innerText);
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
