<template>
  <div class="security-wrapper">
    <span>{{title}}</span>
    <div>
      <span>Fair Market Value:</span>
      <a-input prefix="$" v-model="fairValue_d" placeholder="fair market value" />
    </div>

    <div>
      <span>Quantity:</span>
      <a-input v-model="quantity_d" placeholder="quantity" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Security',
  props: ['title', 'quantity', 'fairValue'],
  data() {
    return {
      fairValue_d: '',
      quantity_d: '',
    };
  },
  watch: {
    fairValue_d(val) {
      this.$emit('change-fair', val);
    },

    quantity_d(val) {
      this.$emit('change-quantity', val);
    },
  },
  methods: {

    emitEmpty() {
      this.$refs.userNameInput.focus();
      this.userName = '';
    },
  },
};
</script>

<style>
.security-wrapper {
  width: 500px;
  height: fit-content;
  border-style: solid;
  border-width: 1px;
  border-color: black;

  padding: 10px 10px;

  text-align: left;
}
</style>
