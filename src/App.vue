<template>
  <div id="app">

    <button id="show-modal" @click="showModal({
      showcancel: false,
      showok: false,
      header: 'Tips 1',
      body: 'body 1',
      okcallback: okcallback1,
      cancelcallback: cancelcallback1,
      duration: 1000
    })">Show Modal 1</button>

    <button id="show-modal2" @click="showModal({
      header: 'Tips 2',
      body: 'body 2',
      okcallback: okcallback2,
      cancelcallback: cancelcallback2
    })">Show Modal 2</button>

    <!-- use the modal component, pass in the prop -->
    <modal v-ref:dialog :show.sync='false'></modal>
  </div>
</template>

<script>
import Modal from './components/Modal.vue'

// util
/**
 * like jQuery's extend, just for props copying from 
 * source to target
 *
 * @param {Object} target
 * @param {Object} source
 */
function extend (target, source) {
  var length = arguments.length
  if (length === 1) {
    source = arguments[0]
    target = this
  }
  for (var p in source) {
    if (source.hasOwnProperty(p)) {
      target[p] = source[p]
    }
  }
  return target
}

export default {
  components: {
    Address,
    Modal
  },

  methods: {
    showModal: function (options) {
      // reset modal component
      extend(this.$refs.dialog, {
        showok: true,
        showcancel: true,
        oktext: 'OK',
        canceltext: 'Cancel',
        header: 'Tips',
        body: '',
        okcallback: function () {
          this.show = false
        },
        cancelcallback: function () {
          this.show = false
        },
        duration: 0
      })
      // init modal
      extend(this.$refs.dialog, options)
      this.$refs.dialog.show = true
      if (options.duration && options.duration > 0) {
        setTimeout(() => {
          this.$refs.dialog.show = false
        }, options.duration)
      }
    },
    okcallback1: function () {
      alert('You\'ve clicked OK，from dialog 1!')
      this.$refs.dialog.show = false
    },
    cancelcallback1: function () {
      alert('You\'ve clicked Cancel，from dialog 1!')
      this.$refs.dialog.show = false
    },
    okcallback2: function () {
      alert('You\'ve clicked OK，from dialog 2!')
      this.$refs.dialog.show = false
    },
    cancelcallback2: function () {
      alert('You\'ve clicked Cancel，from dialog 2!')
      this.$refs.dialog.show = false
    }
  }
}
</script>
