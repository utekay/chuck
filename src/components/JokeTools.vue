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
      <a v-on:click.prevent="onCopyLinkClick"
        class="tools__link"
        href="#"
      >
        Copy link
      </a>
    </li>
  </ul>
</template>

<script>
const onCopyLinkClick = () => {
  let input = document.createElement('input')
  document.body.appendChild(input)
  input.value = window.location.href
  input.select()
  document.execCommand('copy')
  document.body.removeChild(input)
  alert('Copied!')
}
</script>

<style lang="css">
.tools {
  margin-top: 55px;
  padding-left: 0;
  list-style: none;
}
.tools__item {
  margin: 1rem 0;
}
</style>
