<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <i class="icon-basic-world" style="color: black"></i>
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

    <section class="section-features">
      <div class="row">
        <div class="col-1-of-4">
          <div class="feature-box">
            <i class="feature-box__icon icon-basic-world"></i>
            <h3 class="heading-terriary"></h3>
            <p class="feature-box__text">Lorem ipsum dolor</p>
          </div>
        </div>
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
@import '../css/icon-font.css';
@import '../sass/main';
.hello {
  max-width: $grid-width;
}
h1 {
  font-size: 14px;
}
.section-features {
  i {
    color: #000;
  }
}
</style>
