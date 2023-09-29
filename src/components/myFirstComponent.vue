<template>
  <div class="myComponent">
    <div class="btns">
      <button @click="likes++">
        like
      </button>
      <button @click="dislikes++">
        dislike
      </button>
    </div>
    <span   class="likes">Кол-во лайков: {{ likes  }}</span>
    <span   class="dislikes">Кол-во дизлайков: {{ dislikes  }}</span>
  </div>
</template>

<script>

export default {
  data() {
    return {
      likes: 0,
      dislikes: 0
    }
  }
}

</script>

<style>

</style>