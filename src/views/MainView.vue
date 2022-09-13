<template>
  <div class="expenses">
    <expensesList :paymentsList="paymentsList"/>
    <div class="expenses-form">
      <button @click="addFormBtn">{{ addForm }} форму</button>
      <expensesForm
        v-if="show"
        @add-expenses="addExpenses"
        :categoryList="categoryList"
        :addExpensesLink="addExpensesLink"
      />
    </div>
  </div>
</template>

<script>
import expensesList from '@/components/ExpensesList'
import expensesForm from '@/components/expensesForm'
import { mapActions, mapGetters, mapMutations } from 'vuex'

export default {
  name: 'App',
  components: {
    expensesList,
    expensesForm
  },
  data: () => ({
    show: false,
    addForm: 'показать',
    addExpensesLink: []
  }),
  computed: {
    ...mapGetters(['paymentsList', 'categoryList'])
  },
  methods: {
    ...mapActions(['fetchData', 'fetchCategoryData']),
    ...mapMutations(['ADD_PAYMENT']),
    addExpenses (data) {
      this.ADD_PAYMENT(data)
    },
    addFormBtn () {
      this.show = !this.show
      !this.show ? this.addForm = 'показать' : this.addForm = 'скрыть'
    }
  },
  created () {
    this.fetchData()
    this.fetchCategoryData()
  },
  mounted () {
    if (this.$route.name === 'addPayment') {
      this.addForm = 'скрыть'
      this.show = true
      this.addExpensesLink.push(this.$route.params.category)
      this.addExpensesLink.push(this.$route.query.value)
    }

    // this.addExpenses({})
  }
}
</script>

<style scoped lang="scss">
.expenses-form {
  width: 250px;
}
.expenses {
  display: flex;
  justify-content: center;
}

button {
  background-color: #32AB9B;
  border: 0;
  width: 100px;
  height: 40px;
  border-radius: 5px;
}
button:hover{
  cursor: pointer;
}

</style>
