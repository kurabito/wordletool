<template>
  <h2>Wordle Tool</h2>
  <div>
    <p>
      <input type="text" id="l1" v-model="l1" maxlength="1" class="letter">
      <input type="text" id="l2" v-model="l2" maxlength="1" class="letter">
      <input type="text" id="l3" v-model="l3" maxlength="1" class="letter">
      <input type="text" id="l4" v-model="l4" maxlength="1" class="letter">
      <input type="text" id="l5" v-model="l5" maxlength="1" class="letter">
    </p>
    <p>
      <label for="include">
        Include
      </label>
      <input type="text" id="include" v-model="include">
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
    name: 'ABVfromOGandFG',
    data() {
      return {
        wordarray: wordlist.split("\n"),
        l1: "",
        l2: "",
        l3: "",
        l4: "",
        l5: "",
        include: "",
        exclude: "",
      }
    },
    computed: {
      words() {
        // return (wordlist);
    // this.wordarray = this.wordlist.split(" ")
    // this.wordarray[0] = "arraytest"
        
        const positions = [this.l1, this.l2, this.l3, this.l4, this.l5]
        var possiblewords = ""
        // possiblewords = "pwtest"


                for (const word of this.wordarray){
                    var match = true
                    for (var i = 0; i < 5; i++) {
                        if (positions[i] == "") { continue }
                        if (word[i] != positions[i]) { 
                            match = false
                            break
                        }
                    }

                    if (match) {
                        for (var i = 0; i < this.include.length; i++) {
                            if (!word.includes(this.include[i])) {
                                match = false
                                break
                            }
                        }
                    }
                        
                    if (match) {
                        for (var i = 0; i < this.exclude.length; i++) {
                            if (word.includes(this.exclude[i])) {
                                match = false
                                break
                            }
                        }
                    }

                    if (match) {
                        possiblewords += word 
                    }
                }

    //         if (word.includes("x")) {
    //             possiblewords += word + word[0] + positions[0] +this.l1
    // }                
                // }

                return (possiblewords);

                // return (this.wordarray[1]);
      }
    },


  }
  </script>

<style scoped>
.letter {
  width: 20px;
}
label {
  display: inline-block;
  width: 60px;
}
</style>