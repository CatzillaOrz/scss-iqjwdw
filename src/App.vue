<template>
  <div id="app">
    <img v-if="img" :src="img" />
    <p>Counter: {{ state.count }}</p>
    <button @click="increment">increment</button>
    <input v-model="countRef" @keyup.enter="setCount(countRef)" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script lang="ts">
import { useRxState, syncRef } from 'vuse-rx';
import { defineComponent, toRef } from 'vue';
import { tap } from 'rxjs/operators';
import HelloWorld from './components/HelloWorld.vue';
import { getCharacter } from 'rickmortyapi';
import { from, Observable, Subject, interval } from 'rxjs';
import { repeat, map, share, exhaustMap, delay, tap } from 'rxjs/operators';
import { takeUntil } from 'rxjs/operators';
export const source$ = from(getCharacter(1)).pipe(share(), delay(3000));

export default defineComponent({
  setup() {
    const {
      actions: { increment, setCount },
      state,
      state$, // state observable
    } = useRxState({ count: 0 })(
      {
        // stateful reducer with mutation context
        increment: () => (state, mutation) => ({
          // automatic type inference for the state
          count: state.count + 1,
        }),

        // stateless reducer
        setCount: (count: string) => ({
          // custom business logic
          count: isNaN(Number(count)) ? 0 : Number(count),
        }),
      },
      (state$) =>
        state$.pipe(tap((state) => console.log('state is updated', state)))
    );

    // "Activating" the actions
    state$.subscribe((state) => console.log('counter: ', state.count));

    return {
      increment,
      setCount,
      state,

      // One-way data binding from reactive state (with type convertation)
      countRef: syncRef(toRef(state, 'count'), { to: String }),
    };
  },
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
    this.img = source$.pipe(
      map((res) => res.data.image),
      tap((e) => console.log(e))
    );
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
