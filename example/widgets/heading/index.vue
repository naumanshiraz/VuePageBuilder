<template>
  <h2
    :class="[playState ? 'anm-' + val.animationName : '']"
    :style="{
      position: 'absolute',
      width: val.width / 7.5 + '%',
      height: val.height / h * 100 + '%',
      left: val.left / 7.5 + '%',
      top: val.top / h * 100 + '%',
      zIndex: val.z,
      backgroundColor: val.bgColor,
      color: val.color,
      fontSize: '15px'
    }"
    contenteditable="true"
    @input="(e) => updateText(e, val.uuid)"
    v-html="val.text"/>
</template>

<script>
const WIDGET_NAME = 'braid-h2'

export default {
  name: WIDGET_NAME,
  title: 'H2',
  setting: {
    type: WIDGET_NAME,
    animationName: '',
    belong: 'page',
    color: '#000000',
    dragable: true,
    fontSize: 1.2,
    fontWeight: false,
    hasGuide: true,
    height: 100,
    href: '',
    isChild: true,
    isContainer: false,
    isUpload: false,
    left: 50,
    lineHeight: 1.6,
    resizable: true,
    text: 'Add Heading H2',
    textAlign: 'left',
    top: 0,
    width: 650,
    z: 0
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
