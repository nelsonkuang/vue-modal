<template>
  <div class="modal-mask" v-show="show" transition="modal">
    <div class="modal-wrapper">
      <div class="modal-container">

        <div class="modal-header">
          {{ header }}
        </div>
        
        <div class="modal-body">
          {{ body }}
        </div>

        <div class="modal-footer"
          :class="{'border-none': !showcancel && !showok}">
          <slot name="footer">

            <button class="modal-default-button modal-button-ok"
              :class="{'border-none': !showcancel==true}"
              v-show="showok"
              @click="okcallback()">
              {{ oktext }}
            </button>

            <button class="modal-default-button modal-button-cancel"
              v-show="showcancel"
              @click="cancelcallback()">
              {{ canceltext }}
            </button>

          </slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {

  name: 'Modal',

  props: {
    show: {
      type: Boolean,
      required: true,
      twoWay: true,
      default: false
    },
    showok: {
      type: Boolean,
      required: true,
      twoWay: true,
      default: true
    },
    showcancel: {
      type: Boolean,
      required: true,
      twoWay: true,
      default: true
    },
    header: {
      type: String,
      default: 'Tips'
    },
    body: {
      type: String,
      default: ''
    },
    oktext: {
      type: String,
      default: 'OK'
    },
    canceltext: {
      type: String,
      default: 'Cancel'
    },
    okcallback: {
      type: Function,
      default: function () {
        this.show = false
      }
    },
    cancelcallback: {
      type: Function,
      default: function () {
        this.show = false
      }
    },
    duration: {
      type: Number,
      default: 0
    }
  }

}

</script>


<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 250px;
  margin: 0px auto;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
  max-width: 100%;
  box-sizing: border-box;
}
.modal-container:after{
  content: '';
  display: block;
  height: 0;
  width: 0;
  clear: both;
}
.modal-header {
  padding: 10px 20px 0;
  text-align: center;
  font-size: 16px;
}

.modal-body {
  padding: 20px;
  text-align: center;
  font-size: 14px;
}

.modal-footer {
  border-top: 1px solid #cdc7c7;
  display: -webkit-box;
  display: -moz-box;
  display: box;
  width: 100%;
}

.modal-footer button {
  -moz-box-flex: 1;
  box-flex: 1;
  -webkit-box-flex: 1;
  display: block;
  color: #999;
  text-align: center;
  padding: 15px 0px;
  text-decoration: none;
  border: none;
}

.modal-footer button:first-child {
  color: #ff8903;
  border-right: 1px solid #cdc7c7;
}

.border-none{
  border: none !important;
}
/*
 * the following styles are auto-applied to elements with
 * v-transition="modal" when their visiblity is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter, .modal-leave {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>