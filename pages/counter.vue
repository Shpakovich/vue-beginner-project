<template>
  <section class="container">
    <div class="counter-block">
        <p class="number">{{ counter }}</p>
        <div class="button-block">
          <button 
            v-on:click="plusClick()"
            class="button"
          >
            +
          </button>
          <button 
            v-on:click="minusClick()"
            class="button"
          >
            -
          </button>
        </div>
    </div>
  </section>
</template>

<script>

export default {

  layout: 'project',

  data: () => ({
    counter: 0
  }),

  methods: {
    plusClick() {
      this.counter += 1;
    },
    minusClick() {
      this.counter > 0 ?
      this.counter -= 1:
      this.counter;
    }
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.counter-block {
  display: grid;
  padding: 20px;
  width: 200px;
  height: 300px;
  border: 1px solid lightskyblue;
}

.number {
  font-size: 100px;
}

.button-block{
  display: grid;
  grid-auto-flow: column;
  margin: auto;
  grid-column-gap: 25px;
}

.button {
  grid-column-gap: 10px;
  font-size: 40px;
  width: 50px;
  background: lightskyblue;
  color: white;
  outline: none;
  border:0;
  border-radius: 50px;
  cursor: pointer;
}

</style>

