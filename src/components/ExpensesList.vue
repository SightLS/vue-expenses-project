<template>
  <div>
    <div v-if="paymentsList" class="payments-list">
      <div class="payment">
        <div class="payment__row">#</div>
        <div class="payment__row">Date</div>
        <div class="payment__row">Category</div>
        <div class="payment__row">Value</div>
      </div>
      <div class="payment"
           v-for="(payment, i_payment) in paymentsList[pages]" :key="i_payment"
      >
        <div class="payment__row">{{ i_payment + 1 }}</div>
        <div class="payment__row">{{ payment.date }}</div>
        <div class="payment__row">{{ payment.category }}</div>
        <div class="payment__row">{{ payment.value }}</div>
      </div>
    </div>
    <div class="pages">
      <a v-for="(payment, i_pagePayment) in paymentsList"
         :key="i_pagePayment"
         @click="switchPage(i_pagePayment)"
      >
        {{ i_pagePayment + 1 }}
      </a>
    </div>
  </div>
</template>

<script>

export default {
  name: 'ExpensesList',
  components: {},
  props: {
    paymentsList: {
      type: Array,
      required: true
    }
  },
  data: () => ({
    pages: 0
  }),
  methods: {
    switchPage (index) {
      this.pages = index
    }
  }
  // чет я не догнал как сделать так, чтобы он открывал последнюю страницу при запуске и при добавлении
  // последнего элемента
  // mounted () {
  //     this.pages = this.paymentsList.length - 1
  // }
}
</script>

<style scoped lang="scss">
.payments-list {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  height: 250px;
}

.pages {
  display: flex;
  gap: 10px;
  padding-left: 40px;
}

a:hover {
  cursor: pointer;
}

.payment {
  width: 550px;
  border-bottom: 1px solid #F5F5F5;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  padding: 10px 0 10px 0;

  &__row {
    width: 100px;
  }

  &__row:first-child {
    width: 0px;
  }
}

.payment:last-child {
  border-bottom: 0px;
}
</style>
