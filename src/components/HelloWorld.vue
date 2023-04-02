<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <section>
      <div class="grid-test">
        <div class="row">
          <div class="col-1-of-2">col 1 of 2</div>
          <div class="col-1-of-2">col 1 of 2</div>
        </div>

        <div class="row">
          <div class="col-1-of-3">col 1 of 3</div>
          <div class="col-1-of-3">col 1 of 3</div>
          <div class="col-1-of-3">col 1 of 3</div>
        </div>

        <div class="row">
          <div class="col-1-of-3">col 1 of 3</div>
          <div class="col-2-of-3">col 2 of 3</div>
        </div>
      </div>

      <div class="row">
        <div class="col-1-of-4">col 1 of 4</div>
        <div class="col-1-of-4">col 1 of 4</div>
        <div class="col-1-of-4">col 1 of 4</div>
        <div class="col-1-of-4">col 1 of 4</div>
      </div>

      <div class="row">
        <div class="col-1-of-4">col 1 of 4</div>
        <div class="col-1-of-4">col 1 of 4</div>
        <div class="col-2-of-4">col 2 of 4</div>
      </div>

      <div class="row">
        <div class="col-1-of-4">col 1 of 4</div>
        <div class="col-3-of-4">col 3 of 4</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@import '../sass/main';
.hello {
  max-width: 14rem;
}
h1 {
  font-size: 14px;
}
</style>
