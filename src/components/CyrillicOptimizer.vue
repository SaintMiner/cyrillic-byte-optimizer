<template>
  <div>
    <div class="text-input">
      <h2> Input </h2>
      <textarea name="input" id="" rows="10" v-model="inputText">
      </textarea>
      <div class="indicator">
        <div> Symbol count: {{ inputInfo.symbolCount }} </div>
        <div> Bytes: {{ inputInfo.bytes }} </div>
      </div>
    </div>
    <div class="text-output">
      <h2> Output </h2>
      <div class="processed-text">
        {{ processedText }}
      </div>
      <div class="indicator">
        <div> Symbol count: {{ processedInfo.symbolCount }} </div>
        <div> Bytes: {{ processedInfo.bytes }} </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputText: null,
    }
  },

  computed: {
    processedText() {
      const patterns = [
        { from: /а/g, to: "a" },
        { from: /е/, to: "e" },
        { from: /у/, to: "y" },
        { from: /о/, to: "o" },
        { from: /х/, to: "x" },
        { from: /с/, to: "c" },
        { from: /р/, to: "p" },
        { from: /А/, to: "A" },
        { from: /О/, to: "O" },
        { from: /Е/, to: "E" },
        { from: /С/, to: "C" },
        { from: /Т/, to: "T" },
        { from: /Х/, to: "X" },
        { from: /К/, to: "K" },
        { from: /Н/, to: "H" },
        { from: /Р/, to: "P" },
        { from: /р/, to: "p" },
        { from: /В/, to: "B" },
        { from: /М/, to: "M" },
      ];

      let output = this.inputText;

      if (output) {
        patterns.forEach(pattern => {
          output = output.replace(pattern.from, pattern.to);
        });
      }

      return output;
    },

    inputInfo() {
      return this.getTextInfo(this.inputText);
    },

    processedInfo() {
      return this.getTextInfo(this.processedText);
    },
  },

  methods: {
    getTextInfo(text) {
      let info = {
        symbolCount: 0,
        bytes: 0
      };

      if (text) {
        info.symbolCount = text.length;
        info.bytes = (new TextEncoder().encode(text)).length;
      }

      return info;
    }
  },

  mounted() {
    this.inputText = "";
  },
}
</script>

<style>

.text-input {
  margin: 20px;

}
.text-input textarea {
  width: 100%;
}

.text-output {
  margin: 20px;  
}

.processed-text {
  border: solid 1px gray;
  height: 100px;
}

.indicator {
  display: flex;
}

.indicator > div {
  margin: 10px;
}

</style>