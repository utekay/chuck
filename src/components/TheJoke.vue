<template lang="html" functional>
  <div class="joke">
    <p class="joke__number">
      Joke #{{ props.joke.id }}
    </p>
    <h1 v-html="props.joke.joke"
      class="joke__message"
    />
  </div>
</template>

<style lang="css">
.joke__number {
  margin: 0;
}
.joke__message {
  font-family: serif;
}
</style>
