<template>
    <h2>Wordle Letter Bomb</h2>
    <div>
      <p><label for="include">
          Letters to include
        </label>
        <input type="text" id="include" v-model="include">
      </p>
      <p>
        Possible words: {{ words }}
      </p>
    </div>
  </template>
    
  <script>
    import wordlist from '/src/assets/wordlist.txt?raw';
    export default {
      name: 'LetterBomb',
      data() {
        return {
          wordarray: wordlist.split("\n"),
          include: "",
        }
      },
      computed: {
        words() {
          var possiblewords = ""
          for (const word of this.wordarray){
            var match = true
            // Throw out words that don't contain letters to be included
            for (var i = 0; i < this.include.length; i++) {
                if (!word.includes(this.include[i])) {
                    match = false
                    break
                }
            }
            if (match) {
                possiblewords += word + " "
            }
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
      width: 150px;
    }
  </style>