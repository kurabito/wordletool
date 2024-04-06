<template>
  <h2>Wordle Help</h2>
  <div>
    <p>
      <label for="l1">
        Correct
      </label>
      <input type="text" id="l1" v-model="l1" maxlength="1" class="letter">
      <input type="text" id="l2" v-model="l2" maxlength="1" class="letter">
      <input type="text" id="l3" v-model="l3" maxlength="1" class="letter">
      <input type="text" id="l4" v-model="l4" maxlength="1" class="letter">
      <input type="text" id="l5" v-model="l5" maxlength="1" class="letter">
    </p>
    <p>
      <label for="m11">
        Wrong place
      </label>
      <input type="text" id="m11" v-model="m11" maxlength="1" class="letter">
      <input type="text" id="m12" v-model="m12" maxlength="1" class="letter">
      <input type="text" id="m13" v-model="m13" maxlength="1" class="letter">
      <input type="text" id="m14" v-model="m14" maxlength="1" class="letter">
      <input type="text" id="m15" v-model="m15" maxlength="1" class="letter">
    </p>
    <p>
      <label for="m21">
        Wrong place
      </label>
      <input type="text" id="m21" v-model="m21" maxlength="1" class="letter">
      <input type="text" id="m22" v-model="m22" maxlength="1" class="letter">
      <input type="text" id="m23" v-model="m23" maxlength="1" class="letter">
      <input type="text" id="m24" v-model="m24" maxlength="1" class="letter">
      <input type="text" id="m25" v-model="m25" maxlength="1" class="letter">
    </p>
    <p><label for="exclude">
        Exclude
      </label>
      <input type="text" id="exclude" v-model="exclude">
    </p>
    <p>
      Possible words: {{ words }}
    </p>
  </div>
</template>
  
<script>
  import wordlist from '/src/assets/wordlist.txt?raw';
  export default {
    name: 'WordleTool',
    data() {
      return {
        wordarray: wordlist.split("\n"),
        l1: "",
        l2: "",
        l3: "",
        l4: "",
        l5: "",
        m11: "",
        m12: "",
        m13: "",
        m14: "",
        m15: "",
        m21: "",
        m22: "",
        m23: "",
        m24: "",
        m25: "",
        exclude: "",
      }
    },
    computed: {
      words() {
        const correct = [this.l1, this.l2, this.l3, this.l4, this.l5]
        const misplaced1 = [this.m11, this.m12, this.m13, this.m14, this.m15]
        const misplaced2 = [this.m21, this.m22, this.m23, this.m24, this.m25]
        var possiblewords = ""
        for (const word of this.wordarray){
          var match = true
          for (var i = 0; i < 5; i++) {
              if (correct[i] == "") { continue }
              // Throw out words that don't have known letters in the known correct position
              if (word[i] != correct[i]) { 
                  match = false
                  break
              }
          }
          if (match) {
            for (var i = 0; i < 5; i++) {
                // if (misplaced1[i] == "") { continue }
                // Throw out words that have known letters in a known incorrect position
                if (word[i] == misplaced1[i]) { 
                    match = false
                    break
                }
                if (word[i] == misplaced2[i]) { 
                    match = false
                    break
                }
                // Throw out words that don't contain a known letter in an unknown position
                if (!word.includes(misplaced1[i])) { 
                    match = false
                    break
                }
                if (!word.includes(misplaced2[i])) { 
                    match = false
                    break
                }
            }
          }
          // if (match) {
          //     for (var i = 0; i < this.include.length; i++) {
          //         if (!word.includes(this.include[i])) {
          //             match = false
          //             break
          //         }
          //     }
          // }
          if (match) {
            // Throw out words that contain letters known to be not included
            for (var i = 0; i < this.exclude.length; i++) {
                if (word.includes(this.exclude[i])) {
                    match = false
                    break
                }
            }
          }
          if (match) {
              possiblewords += word + " "
          }
          // if (possiblewords.length > 5400) {
          if (possiblewords.length > 1800) {
            possiblewords += "..." 
            break
          }
        }
        return (possiblewords);
      }
    }
  }
</script>

<style scoped>
  label {
    display: inline-block;
    width: 100px;
  }
  .letter {
    width: 20px;
  }
</style>