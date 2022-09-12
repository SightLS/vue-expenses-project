<template>
  <div id="app">
    <header></header>
    <main>
      <expensesList :paymentsList="paymentsList"/>
      <div class="expenses-form">
        <button @click="addFormBtn">{{ addForm }} форму</button>
        <expensesForm
          v-if="show"
          @add-expenses="addExpenses"
          :categoryList="categoryList"
        />
      </div>
    </main>
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
    addForm: 'показать'
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
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

main {
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

.expenses-form {
  width: 250px;
}
</style>
