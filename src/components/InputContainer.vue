<template>
    <div class="bill">
        <div class="input"> 
                <label for="bill"  >Bill</label>
                <input type="number" id="bill-input" class="bill-input">
                <label for="">Select Tip %</label>
            <div class="tip">
                <div class="tips tip-5">5%</div>
                <div class="tips tip-10">10%</div>
                <div class="tips tip-15 active-tip" >15%</div>
                <div class="tips tip-25">25%</div>
                <div class="tips tip-50">50%</div>
                <div  id="tip-custom"><input type="number" class="tip-custom" placeholder="CUSTOM"></div>
            </div>
            <div class="people-label">
                <label for="">Number of People</label>
                <label for="" class="error"> Can't be Zero</label>
            </div>
            <input type="number" class="people-input">
        </div>
        <div class="result">
            <div class="tip-amount">
                <div class="text">
                    <p>Tip Amount</p>
                    <p class="person">/ person</p>
                </div>
                <div class="amount" id="tip-amount">$4.27</div>
            </div>
            <div class="total-amount">
                <div class="text">
                    <p>Total</p>
                    <p class="person">/ person</p>
                </div>
                <div class="amount" id="total-amount">$32.79</div>
            </div>
            <div class="reset">RESET</div>
        </div>
    </div>
</template>

<script>
export default {
    
}
</script>

<style scoped>
.bill-input {
  background-image: url('../assets/icon-dollar.svg');
  margin-bottom: 36px;
}

.tip{
    margin-top: 0.7rem;
    display: grid;
    grid-template-columns: 144px 144px;
    row-gap: 2rem;
    column-gap: 18px;
    margin-bottom: 2rem;
}

.tips {
    background-color: #00474B;
    color: white;
    height: 48px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    border-radius: 4px;
    cursor: pointer;
}

.tip-custom {
    box-sizing: border-box;
    width: 100%;
}

.active-tip {
    color: #00474B;
    background-color: #26C2AE;
    font-weight: bolder;
}

.people-input {
    background-image: url('../assets/icon-person.svg');
    margin-bottom: 2.4rem;
}

.result {
    background-color:#00474B;
    color: white;
    border-radius: 12px;
}

.tip-amount, .total-amount {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 1.7rem;
}

.person {
    font-size: 12px;
    color: #7F9D9F;
    font-weight: 700;
}

.amount{
    font-size: 28px;
    color: #26C2AE;
    font-weight: 700;
}

.reset {
    text-align: center;
    font-size: 20px;
    font-weight: 700;
    color: #00474B;
    background-color: #26C2AE;
    padding: 9px 0 9px 0;
    border-radius: 5px;
    cursor: pointer;
}

.people-label {
    display: flex;
    justify-content: space-between;
}

.error {
    color: red;
}

@media only screen and (min-width: 1000px) {
    input {
      width: 415px;
      padding: 9px;
      background-position: 17px 18px;
    }

    .bill {
      width: 990px;
      flex-direction: row;
      border-radius: 1.4rem;
      padding: 2.3rem;
      height: 479px;
    }

    .input {
      margin-top: 1rem;
      margin-left: 1.2rem;
      display: flex;
      flex-direction: column;
    }

    .bill-input {
      margin-bottom: 3.4rem;
    }

    .tip {
      grid-template-columns: 135px 135px 135px;
      row-gap: 1.2rem;
      column-gap: 17px;
      margin-bottom: 3.2rem;
    }

    .tips {
      height: 55px;
    }

    .result {
        margin-left: auto;
        width: 400px;
        display: flex;
        flex-direction: column;
        align-content: space-between;
        padding: 48px 38px;
    }

    .amount {
        font-size: 55px;
    }

    .reset {
        padding: 13px 0 13px 0;
        margin-top: auto;
    }
}
 

</style>