<template lang="html" functional>
  <ul class="tools">
    <li class="tools__item">
      <a v-on:click.prevent="listeners['getJoke']"
        class="tools__link"
        href="#"
      >
        Random joke
      </a>
    </li>
    <li v-if="props.joke"
      class="tools__item"
    >
      <a v-on:click.prevent="listeners['copyLink']"
        class="tools__link"
        href="#"
      >
        Copy link
      </a>
    </li>
  </ul>
</template>

<style lang="css">
.tools {
  margin-top: 55px;
  padding-left: 0;
  list-style: none;
}
.tools__item {
  margin: 3% 0;
}
</style>
