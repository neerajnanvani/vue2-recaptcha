<template>
  <div
    class="simplert"
    role="modal"
    :class="classSimplert"
    @click="closeOverlay"
  >
    <div class="simplert__content" :class="classContent">
      <div class="simplert__header">
        <div class="simplert__x" v-if="showXclose" @click="justCloseSimplert">
          &#9587;
        </div>
        <div v-if="useIcon">
          <div
            class="simplert__icon simplert__icon--info"
            v-if="type === 'info'"
          >
            <div class="simplert__line simplert__line--info" />
            <div class="simplert__line simplert__line--info-2" />
          </div>
          <div
            class="simplert__icon simplert__icon--success"
            v-if="type === 'success'"
          >
            <div class="simplert__line simplert__line--success" />
            <div class="simplert__line simplert__line--success-2" />
          </div>
          <div
            class="simplert__icon simplert__icon--warning"
            v-if="type === 'warning'"
          >
            <div class="simplert__line simplert__line--warning" />
            <div class="simplert__line simplert__line--warning-2" />
          </div>
          <div
            class="simplert__icon simplert__icon--error"
            v-if="type === 'error'"
          >
            <div class="simplert__line simplert__line--error" />
            <div class="simplert__line simplert__line--error-2" />
          </div>
          <div class="simplert__icon" v-if="customIconUrl !== ''">
            <img :src="customIconUrl" />
          </div>
        </div>
        <b class="simplert__title" v-if="title" v->{{ title }}</b>
        <slot name="header"></slot>
      </div>
      <div class="simplert__body">
        <div v-html="message" />
        <slot></slot>
      </div>
      <div class="simplert__footer">
        <button
          :class="classBtnConfirm"
          v-if="useConfirmBtn && !hideAllButton"
          @click="whenConfirm"
          v-html="customConfirmBtnText"
        ></button>
        <button
          :class="classBtnClose"
          v-if="!hideAllButton"
          @click="closeSimplert"
          v-html="customCloseBtnText"
        ></button>
        <slot name="footer"></slot>
      </div>
    </div>
  </div>
</template>

<script>
import simplertMixin from "vue2-simplert-core";
export default {
  name: "Simplert",
  mixins: [simplertMixin],
};
</script>

<style
  src="vue2-simplert-core/simplert.css">
</style>