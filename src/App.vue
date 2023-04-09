<template>
  <div id="app">
    <img v-if="img" :src="img" />
    

    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script lang="ts">
import { useRxState, syncRef, refFrom } from 'vuse-rx';
import { defineComponent, toRef } from 'vue';
import { tap } from 'rxjs/operators';
import HelloWorld from './components/HelloWorld.vue';
import { getCharacter } from 'rickmortyapi';
import { from, Observable, Subject, interval } from 'rxjs';
import {
  repeat,
  map,
  share,
  exhaustMap,
  delay,
  tap,
  pipe,
} from 'rxjs/operators';
import { takeUntil } from 'rxjs/operators';
// export const source$ = from(getCharacter(1)).pipe(share(), delay(3000));
import { onMounted } from 'vue';
export default defineComponent({
  name: 'App',
  components: {
    HelloWorld,
  },
  data() {
    return {
      img: '',
    };
  },
  mounted() {
    // this.img = this.image$.pipe(
    //   map((res) => res.data.image),
    //   tap((e) => console.log(e))
    // );
  },
  domStreams: ['plus$'],
  subscriptions: function () {
    const image$ = source$.pipe(
      map((res) => res.data.image),
      tap((e) => console.log(e))
    );
    const tick$ = this.plus$.pipe(
      exhaustMap(() => interval(500)),
      map((i) => i++),
      tap((i) => {
        console.log(i);
      }),
      takeUntil(this.reset$),
      repeat()
    );
    return { image$, tick$ };
  },
});
</script>

<style lang="scss">
@import './sass/main';
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  img {
    max-width: 2rem;
  }
}
</style>
