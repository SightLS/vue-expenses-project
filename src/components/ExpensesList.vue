<template>
  <div>
    <div v-if="paymentsList" class="payments-list">
      <div class="payment">
        <div class="payment__row">#</div>
        <div class="payment__row">Date</div>
        <div class="payment__row">Category</div>
        <div class="payment__row">Value</div>
      </div>
      <ul class="payment"
          v-for="(payment, i_payment) in paymentsList[pages]" :key="i_payment"
      >
        <li class="payment__row">{{ numberList(i_payment) }}</li>
        <li class="payment__row">{{ payment.date }}</li>
        <li class="payment__row">{{ payment.category }}</li>
        <li class="payment__row">{{ payment.value }}</li>
        <li>
          <img class="setting-menu"
               src="../assets/menu.png"
               alt="settings"
               @click="showSettings = !showSettings"
          >
          <ModalSettings v-if="showSettings"/>
        </li>
      </ul>
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
// import ModalWindowAddPayment from '@/components/ModalWindowAddPayment'
import ModalSettings from '@/components/ModalSettings'

export default {
  name: 'ExpensesList',
  components: {
    // ModalWindowAddPayment,
    ModalSettings
  },
  props: {
    paymentsList: {
      type: Array,
      required: true
    }
  },
  data: () => ({
    pages: 0,
    showSettings: false
  }),
  methods: {
    switchPage (index) {
      this.pages = index
    },
    numberList (index) {
      return (index + 1) + (5 * this.paymentsList.indexOf(this.paymentsList[this.pages]))
    }
  },
  mounted () {
    this.$settings.EventBus.$on('show', this.modalOpen)
    this.$settings.EventBus.$on('hide', this.modalClose)
  }
}
</script>

<style scoped lang="scss">
.payments-list {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  margin-bottom: 30px;
  height: 250px;
}

.test {
  //display: flex;
  position: absolute;
  border: 1px solid black;
  flex-direction: column;
  background-color: white;
  //display: none;
}

.test li:hover {
  display: inherit;
}

.setting-menu {
  width: 24px;
}

.setting-menu:hover {
  cursor: pointer;
}

li {
  list-style-type: none;
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
