<template lang="pug">
section
  back-to-top(visibleoffset="300" bottom="1rem" right="1rem")
    b-button(icon-right="chevron-up" size="is-normal")

  b-modal(
    :active.sync="modal.active"
    :can-cancel="modal.escape"
    :on-cancel="closeModal"
    :custom-class="modal.class"
    :full-screen="modal.fullscreen"
    :animation="modal.animation"
    :aria-role="modal.role"
    :has-modal-card="modal.modalCard"
    :width="modal.width"
  )
    component(:is="modal.component" v-bind="modal.props")
</template>

<script>
import modalModule from '@/store/modules/modal'

export default {
  components: {
    Media: () => import(/* webpackChunkName: "media-manager" */ '@/components/media/Manager'),
    Tags: () => import(/* webpackChunkName: "media-manager" */ '@/components/filters/Tags')
  },

  computed: {
    modal () {
      return this.$store.state.modal
    }
  },

  created () {
    if (!this.$store.state.modal) {
      this.$store.registerModule('modal', modalModule)
    }
  },

  methods: {
    closeModal () {
      this.$store.dispatch('modal/close')
    }
  }
}
</script>
