<template>
  <v-card>
    <v-card-title v-if="title">
      <slot name="title">
        <span
          :class="titleClass"
          v-html="title"
        />
      </slot>
    </v-card-title>
    <v-divider v-if="showCardTextDividers"></v-divider>
    <v-card-text>
      <slot />
    </v-card-text>
    <v-divider v-if="showCardTextDividers"></v-divider>
    <v-card-actions>
      <v-spacer />
      <DialogActions
        :actions="actions"
        flat
        ref="actions"
        :handle="handle"
      />
    </v-card-actions>
  </v-card>
</template>

<script>

  import DialogActions from './DialogActions.vue'

  export default {
    components: {
      DialogActions
    },
    props: {
      title: String,
      titleClass: {
        type: String,
        default: 'headline'
      },
      actions: [Array, Object, Function],
      handle: Function,
      scrollable: {
        type: Boolean,
        default: false
      }
    },
    methods: {
      trigger(name) {
        this.$refs.actions && this.$refs.actions.trigger(name)
      }
    },
    computed: {
      showCardTextDividers() {
        return this.scrollable
      },
    },
  }
</script>
