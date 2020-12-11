<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <security
      :quantity="quantity"
      :fairValue="fairValue"
      @change-fair="onChangeFair"
      @change-quantity="onChangeQuantity"
    />
    <a-button type="primary" @click="onSubmit">
      Primary
    </a-button>
    <h2>${{ result }}</h2>
  </div>
</template>

<script>
// @ is an alias to /src
import Security from '../components/Security.vue';

export default {
  name: 'Home',
  data() {
    return {
      quantity: 10,
      fairValue: 10,
      result: '',
    };
  },
  components: {
    Security,
  },
  methods: {
    onChangeFair(fairValue) {
      this.fairValue = fairValue;
    },
    onChangeQuantity(quantity) {
      this.quantity = quantity;
    },
    onSubmit() {
      fetch('http://127.0.0.1:5000/api/price', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          market_val: parseInt(this.fairValue, 10),
          quantity: parseInt(this.quantity, 10),
        }),
      })
        .then((response) => response.json())
        .then(({ data, status_code }) => {
          if (status_code === 200) {
            this.result = `${data}`;
          }
        })
        .catch(() => {
          this.result = 'Something went wrong!';
        });
    },
  },
};
</script>
