<template>
  <div class="calculator">
    <h1>Arithmetic Sequence Calculator</h1>
    
    <div class="tips" style="display: none;">
      <strong>Tips:</strong> Use Tab to move to the next field. Use Shift+Tab to move to the previous field. Press Enter to calculate.
    </div>

    <div class="calc-group">
      <label>Calculate Arithmetic Sequence:</label><br>
      <input 
        type="number" 
        v-model="firstTerm" 
        placeholder="First term a₁"
        @keypress="handleEnterKey($event, 'sequence')"
      >
      <input 
        type="number" 
        v-model="commonDiff" 
        placeholder="Common diff d"
        @keypress="handleEnterKey($event, 'sequence')"
      >
      <input 
        type="number" 
        v-model="terms" 
        placeholder="Terms n" 
        min="1"
        @keypress="handleEnterKey($event, 'sequence')"
      >
      <button @click="calculateSequence">Calculate</button>
      
      <div class="result-container">
        <div>
          <div class="result-box">
            <strong>Sequence Sum:</strong>
            <div class="result">{{ sumResult }}</div>
          </div>
        </div>
        <div>
          <strong>First n Terms:</strong>
          <div class="sequence-box">
            <div 
              v-for="(item, index) in sequenceItems" 
              :key="index" 
              class="sequence-item"
            >
              {{ item }}
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="calc-group">
      <label>Calculate nth Term:</label><br>
      <input 
        type="number" 
        v-model="firstTerm2" 
        placeholder="First term a₁"
        @keypress="handleEnterKey($event, 'nthTerm')"
      >
      <input 
        type="number" 
        v-model="commonDiff2" 
        placeholder="Common diff d"
        @keypress="handleEnterKey($event, 'nthTerm')"
      >
      <input 
        type="number" 
        v-model="nthTerm" 
        placeholder="n" 
        min="1"
        @keypress="handleEnterKey($event, 'nthTerm')"
      >
      <button @click="calculateNthTerm">Calculate</button>
      
      <div class="result-box">
        <strong>Value of nth Term:</strong>
        <div class="result">{{ nthTermResult }}</div>
      </div>
    </div>

    <div class="faq">
      <h2>FAQ</h2>
      
      <h3>What is an Arithmetic Sequence?</h3>
      <p>An arithmetic sequence is a sequence where the difference between each consecutive term is constant. This constant difference is called the common difference, usually denoted by the letter d.</p>

      <h3>How to Calculate the nth Term?</h3>
      <p>The formula for the nth term of an arithmetic sequence is: aₙ = a₁ + (n-1)d, where:<br>
         - aₙ is the nth term<br>
         - a₁ is the first term<br>
         - d is the common difference<br>
         - n is the position number</p>

      <h3>How to Calculate the Sum?</h3>
      <p>The sum of the first n terms of an arithmetic sequence can be calculated using the formula: Sₙ = n(a₁ + aₙ)/2, where:<br>
         - Sₙ is the sum of n terms<br>
         - n is the number of terms<br>
         - a₁ is the first term<br>
         - aₙ is the nth term</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ArithmeticSequence',
  data() {
    return {
      firstTerm: null,
      commonDiff: null,
      terms: null,
      firstTerm2: null,
      commonDiff2: null,
      nthTerm: null,
      sumResult: '-',
      sequenceItems: [],
      nthTermResult: '-'
    }
  },
  methods: {
    calculateSequence() {
      const a1 = parseFloat(this.firstTerm);
      const d = parseFloat(this.commonDiff);
      const n = parseInt(this.terms);
      
      if (isNaN(a1) || isNaN(d) || isNaN(n) || n < 1) {
        alert('Please enter valid numbers!');
        return;
      }

      // Calculate all terms
      this.sequenceItems = [];
      
      for (let i = 0; i < n; i++) {
        const term = a1 + i * d;
        const formattedTerm = Number.isInteger(term) ? term : parseFloat(term.toFixed(4));
        this.sequenceItems.push(`a${i + 1} = ${formattedTerm}`);
      }
      
      // Calculate sequence sum
      const lastTerm = a1 + (n - 1) * d;
      const sum = n * (a1 + lastTerm) / 2;
      this.sumResult = Number.isInteger(sum) ? sum : parseFloat(sum.toFixed(4));
    },

    calculateNthTerm() {
      const a1 = parseFloat(this.firstTerm2);
      const d = parseFloat(this.commonDiff2);
      const n = parseInt(this.nthTerm);
      
      if (isNaN(a1) || isNaN(d) || isNaN(n) || n < 1) {
        alert('Please enter valid numbers!');
        return;
      }

      const nthTermValue = a1 + (n - 1) * d;
      const formattedTerm = Number.isInteger(nthTermValue) ? nthTermValue : parseFloat(nthTermValue.toFixed(4));
      this.nthTermResult = formattedTerm;
    },

    handleEnterKey(event, calculationType) {
      if (event.key === 'Enter') {
        if (calculationType === 'sequence') {
          this.calculateSequence();
        } else if (calculationType === 'nthTerm') {
          this.calculateNthTerm();
        }
      }
    }
  }
}
</script>

<style scoped>
.calculator {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.calc-group {
  margin: 20px 0;
}

input {
  padding: 8px;
  margin: 5px;
  border: 1px solid #ddd;
  border-radius: 4px;
  width: 100px;
}

.result-box {
  margin-top: 15px;
  padding: 10px;
  background-color: #f8f9fa;
  border-radius: 4px;
  border: 1px solid #ddd;
}

.sequence-box {
  height: 200px;
  overflow-y: auto;
  margin-top: 10px;
  padding: 10px;
  background-color: #f8f9fa;
  border-radius: 4px;
  border: 1px solid #ddd;
}

.sequence-item {
  margin: 5px 0;
  padding: 5px;
  border-bottom: 1px solid #eee;
}

.result {
  font-weight: bold;
  margin-top: 10px;
  word-wrap: break-word;
}

.faq {
  margin-top: 40px;
}

button {
  padding: 8px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
}

button:hover {
  background-color: #45a049;
}

.result-container > div {
  margin-bottom: 20px;
}

.tips {
  margin: 10px 0;
  padding: 10px;
  background-color: #e8f5e9;
  border-radius: 4px;
  color: #2e7d32;
  font-size: 0.9em;
}
</style> 
