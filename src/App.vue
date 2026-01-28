<template>
  <div class="container">
    <h1>Gold & Silver Calculator</h1>
    
    <div class="calculator-card">
      <div class="form-group">
        <label>Metal Type</label>
        <select v-model="metalType" class="input-field">
          <option value="gold">Gold</option>
          <option value="silver">Silver</option>
        </select>
      </div>

      <div class="form-group">
        <label>Rate per Gram (₱)</label>
        <input 
          type="number" 
          v-model.number="ratePerGram" 
          class="input-field"
          placeholder="Enter rate per gram"
          step="0.01"
        >
      </div>

      <div class="form-group">
        <label>Weight (grams)</label>
        <input 
          type="number" 
          v-model.number="weight" 
          class="input-field"
          placeholder="Enter weight in grams"
          step="0.01"
        >
      </div>

      <div class="form-group">
        <label>Design Charge (₱)</label>
        <input 
          type="number" 
          v-model.number="designCharge" 
          class="input-field"
          placeholder="Enter design charge"
          step="0.01"
        >
      </div>

      <div class="calculation-breakdown">
        <h3>Calculation Breakdown</h3>
        <div class="breakdown-item">
          <span>Base Cost ({{ weight }}g × ₱{{ ratePerGram }})</span>
          <span class="amount">₱{{ baseCost.toFixed(2) }}</span>
        </div>
        <div class="breakdown-item">
          <span>Design Charge</span>
          <span class="amount">₱{{ designCharge.toFixed(2) }}</span>
        </div>
        <div class="breakdown-item">
          <span>Subtotal</span>
          <span class="amount">₱{{ subtotal.toFixed(2) }}</span>
        </div>
        <div class="breakdown-item">
          <span>12% PH Tax</span>
          <span class="amount">₱{{ taxAmount.toFixed(2) }}</span>
        </div>
        <div class="breakdown-item total">
          <span>Total Amount</span>
          <span class="amount">₱{{ totalAmount.toFixed(2) }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      metalType: 'gold',
      ratePerGram: 0,
      weight: 0,
      designCharge: 0
    }
  },
  computed: {
    baseCost() {
      return this.ratePerGram * this.weight
    },
    subtotal() {
      return this.baseCost + this.designCharge
    },
    taxAmount() {
      return this.subtotal * 0.12
    },
    totalAmount() {
      return this.subtotal + this.taxAmount
    }
  }
}
</script>
