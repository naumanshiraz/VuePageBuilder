<template>
  <header class="header">
    <div class="navbar container grid-lg">
      <section class="logo navbar-section text-white">
        Page Builder
      </section>
      <section class="navbar-section">
        <a
          class="btn btn-link tooltip tooltip-bottom"
          @click="dele">
          <vpd-icon name="trash-2" /> {{ $t('data.actions.delete') }}
        </a>
        <a
          class="btn btn-link tooltip tooltip-bottom"
          @click="save"><vpd-icon name="save" /> {{ $t('data.actions.save') }}</a>
      </section>
    </div>
  </header>
</template>

<script>
import vpd from '../mixins/vpd'
export default {
  mixins: [vpd],
  data () {
    return {
      langs: this.$inter.availableLocales
    }
  },
  computed: {
    show () {
      return this.$vpd.state.type !== 'page'
    }
  },
  mounted () {
    document.addEventListener(
      'keyup',
      e => {
        e.stopPropagation()
        if (e.keyCode === 46) {
          this.dele()
        }
      },
      true
    )

    document.addEventListener(
      'keyup',
      e => {
        e.stopPropagation()
        if ((e.ctrlKey || e.metaKey) && e.keyCode === 83) {
          this.save()
        }
      },
      true
    )
  },

  methods: {
    save () {
      this.$vpd.dispatch('save')
    },

    dele () {
      this.$vpd.commit('delete')
    }
  }
}
</script>

<style lang="scss">
@import '../_variables.scss';
.header {
  background-color: navy;
  padding: 12px 0;
}
.navbar {
  .svg-icon {
    svg {
      vertical-align: middle;
    }
  }
  .btn.btn-link {
    color: $gray-color;
    margin-right: 15px;
  }
  .btn.btn-link:hover {
    color: $light-color;
  }
  .logo {
    font-size: 20px;
    color: #FFF;
    .svg-icon {
      width: 30px;
      text-align: center;
      background-color: $light-color;
      border-radius: 50%;
    }
  }
  .lang-change {
    width: 80px;
  }
}
</style>
