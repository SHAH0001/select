<template>
  <div id="app">
    <div class="wrapper">
      <Select 
        :items="cars"
        :itemText="'mark'"
        :label="'Выберите марку'"
        @select="select"
      />
    </div>
  </div>
</template>

<script>
import Select from './components/Select.vue'

export default {
  name: 'App',
  data() {
    return {
      cars: [
        { id: 1, mark: 'Audi', country: 'Germany' },
        { id: 2, mark: 'Ford', country: 'USA' },
        { id: 3, mark: 'Honda', country: 'Japan' }
        // 'Germany', 'USA', 'Japan'
      ]
    }
  },
  components: {
    Select
  },
  methods: {
    select(item) {
      console.log('From App: ', item)
    }
  }
}
</script>

<style>
  .wrapper {
    display: flex;
    justify-content: center;
    margin-top: 60px;
  }
</style>
