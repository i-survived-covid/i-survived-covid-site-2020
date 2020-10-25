<template>
  <main>
    <div class="flex flex-wrap items-center justify-center m-8 lg:m-auto">
      <div>
        <article class="text-4xl mb-4">
          <h1>You might have survived Covid.</h1>
          <h2>They didnt.</h2>
        </article>
        <nav class="nav-vote text-6xl mb-8">
          <ul>
            <li>
              <a href="https://vote.gov/" rel="noopener" ref="noreferral"
                >GO VOTE</a
              >
            </li>
          </ul>
        </nav>
        <footer class="w-full">
          <p><Copyright/></p>
        </footer>
      </div>
    </div>
    <Counter :start="0" :stop="200000" :duration="120"></Counter>
  </main>
</template>

<script lang="ts">
import Vue from 'vue'
import Component from 'vue-class-component'

export default Vue.extend({})
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
main {
  display: grid;
  min-height: 100vh;
}

@media (min-width: 1024px) {
  main {
    grid-template-columns: repeat(2, 1fr);
  }
}

a {
  text-decoration: underline;
}

.sr {
  position: absolute;
  left: -10000px;
  top: auto;
  width: 1px;
  height: 1px;
  overflow: hidden;
}
</style>
