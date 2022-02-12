<template>
  <div>
    <div class="text-input">
      <h2> Input </h2>
      <textarea name="input" id="" rows="10" v-model="inputText">
      </textarea>
    </div>
    <div class="text-output">
      <h2> Output </h2>
      <div class="processed-text">
        {{ processedText }}
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  
  data() {
    return {
      inputText: null,
    }
  },

  computed: {
    processedText() {
      return this.inputText;
    }
  },
}
</script>

<style lang="scss">

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

.text-input {
  margin: 20px;

  textarea {
    width: 100%;
  }
}

.text-output {
  margin: 20px;  
}

.processed-text {
  border: solid 1px gray;
  height: 100px;
}
</style>
