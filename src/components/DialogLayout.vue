<template>
  <v-dialog
    content-class="relative"
    v-model="isActive"
    :fullscreen="fullscreen"
    ref="vdialog"
    :max-width="getWidth"
    :persistent="persistent || loading"
    :scrollable="scrollable"
    :transition="transition"
    @keydown.esc="dismiss"
  >
    <!-- <div
      v-if="showClose && !persistent && !loading"
      class="vdialog-layout__closeBtn"
      @click.stop="close"
    >×</div> -->
    <dialog-child
      v-bind="childProps"
      ref="dialog"
    />
  </v-dialog>
</template>

<script>
  export default {
    props: {
      fullscreen: Boolean,
      scrollable: Boolean,
      transition: {
        type: [String, Boolean],
        default: 'dialog-transition'
      },
      showClose: {
        type: Boolean,
        default: () => true
      }
    },
    methods: {
      _destroy() {
        // Allow to draw transition, cause vuetify doesn't have onClose method
        setTimeout(() => {
          this.$destroy()
        }, 1000)
        // this.$refs.vdialog.$refs.dialog.addEventListener('transitionend', this.onTransitionEnd)
      }
      // onTransitionEnd (event) {
      //   if (['opacity', 'z-index'].indexOf(event.propertyName) >= 0) {
      //     this.$refs.vdialog.$refs.dialog.removeEventListener('transitionend', this.onTransitionEnd)
      //     this.$destroy()
      //   }
      // }
    },
    computed: {
      childProps() {
        return {
          ...this.$options.props,
          dialogLoading: this.loading,
          dialogPersistent: this.persistent
        }
      },
    },
  }
</script>
<!-- <style>
  .vdialog-layout {
    position: relative;
  }

  .vdialog-layout__closeBtn {
    position: absolute;
    top: 0px;
    font-family: -webkit-pictograph;
    right: 14px;
    font-size: 29px;
    opacity: 0.5;
    z-index: 1000;
    cursor: pointer;
  }

  .vdialog-layout__closeBtn:hover {
    opacity: 1;
  }
</style> -->
