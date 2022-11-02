<template>
  <div class="menu-bar">
    <ul
      class="widget-list"
      @mousedown="updateSrollTop">
      <li
        v-for="item in widgets"
        v-if="item.name==='braid-h2' || item.name==='braid-txt' || item.name==='braid-container' || item.name==='braid-button' "
        :key="item.name"
        class="menu-item column col-6"
        @click="(e) => {addWidget(e, item)}">
        <vpd-icon
          :svg="item.icon"
          :title="item.title"/>
        <span class="menu-caption">{{ item.title }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import widget from '../plugins/widget'
import {move} from '../mixins'
import {checkInView, cumulativeOffset} from '../utils/offset'
import vpd from '../mixins/vpd'

export default {
  mixins: [move, vpd],
  props: ['zoom'],
  computed: {
    widgets () {
      return widget.getWidgets()
    },
    layers () {
      return this.$vpd.state.widgets
    },
    activeElement () {
      return this.$vpd.state.activeElement
    }
  },
  methods: {
    addWidget (e, item) {
      this.$vpd.dispatch('addWidget', item)
    },

    updateSrollTop () {
      var top = document.getElementById('viewport').scrollTop / this.zoom * 100
      this.$vpd.commit('updateSrollTop', top)
    },

    activeLayer (e, item) {
      this.$vpd.commit('select', {
        uuid: item.uuid
      })
      let viewport = document.querySelector('#viewport')
      let target = viewport.querySelector(`[data-uuid='${item.uuid}']`)
      if (target && !checkInView(target)) {
        viewport.scrollTop = (cumulativeOffset(target).top - 50) * this.zoom / 100
      }
    },

    getWidgetTitle (type) {
      return this.widgets[type].title || ''
    }
  }
}
</script>

<style lang="scss">
@import '../_variables.scss';

.menu-bar {
  ul {
    list-style: none;
    margin: 0;
  }

  details {
    padding: 10px;
  }

  summary {
    padding: 5px 0;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
    border-bottom: 1px solid #f5f5f5;

    .svg-icon {
      margin-right: 5px;
    }
  }
}

.widget-list {
  padding: 0;
}

.menu-item {
  text-align: center;
  cursor: pointer;
  padding: 15px 0 8px;
  transition: all 0.2s;
  position: relative;

  &:hover {
    transform: scale(1.2);
  }

  .svg-icon {
    font-size: 24px;
  }

  .menu-caption {
    display: block;
    font-size: 12px;
    width: 100%;
  }
}

.layer-list {
  padding: 10px;

  li {
    text-align: left;
    cursor: pointer;
    white-space: nowrap;
    line-height: 24px;
    padding-left: 5px;

    &:hover {
      background: #f5f5f5;
    }

    &::before {
      content: '› ';
    }

    &.layer-active {
      color: $light-color;
      background: $primary-color;
    }
  }
}
</style>
