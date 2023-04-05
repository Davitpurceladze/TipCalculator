<template>
    <div class="bill">
        <div class="input"> 
                <label for="bill"  >Bill</label>
                <input type="number" id="bill-input" class="bill-input " :class="{ validInput: billInputValidity === true}" v-model="bill">
                <label for="">Select Tip %</label>
            <div class="tip">
                <div class="tips tip-5" :class="{activeTip: tipPercent == 5 }" @click="tip('5')">5%</div>
                <div class="tips tip-10" :class="{activeTip: tipPercent == 10 }" @click="tip('10')" >10%</div>
                <div class="tips tip-15" :class="{activeTip: tipPercent == 15 }" @click="tip('15')" >15%</div>
                <div class="tips tip-25" :class="{activeTip: tipPercent == 25 }" @click="tip('25')">25%</div>
                <div class="tips tip-50" :class="{activeTip: tipPercent == 50 }" @click="tip('50')">50%</div>
                <div  id="tip-custom"><input type="number" class="tip-custom" :class="{validInput: customTipValidity === true }" placeholder="CUSTOM" v-model="customTip"></div>
            </div>
            <div class="people-label">
                <label for="" >Number of People</label>
                <label for="" class="error" v-show="numberOfPeopleValidity === 'invalid'"> Can't be Zero</label>
            </div>
            <input 
            type="number" 
            class="people-input" 
            :class="{   
                validInput: numberOfPeopleValidity === 'valid', 
                invalidInput: numberOfPeopleValidity === 'invalid'
                }" 
            v-model="numberOfPeople">
        </div>
        <div class="result">
            <div class="tip-amount">
                <div class="text">
                    <p>Tip Amount</p>
                    <p class="person">/ person</p>
                </div>
                <div class="amount" id="tip-amount"> <span v-if="tipVisibility && totalVisibility" > {{tipPerPerson}} </span></div>
            </div>
            <div class="total-amount">
                <div class="text">
                    <p>Total</p>
                    <p class="person">/ person</p>
                </div>
                <div class="amount" id="total-amount"> <span v-if="tipVisibility && totalVisibility"> {{billPerPerson}}</span></div>
            </div>
            <div class="reset" @click="reset">RESET</div>
        </div>
    </div>
</template>

<script>
import {ref, computed, watch} from 'vue'
export default {
    setup() {
        const bill = ref(null)
        const tipTotal = ref(null)
        const numberOfPeople = ref(null)
        const customTip = ref(null)
        const tipVisibility = ref(false)
        const totalVisibility = ref(false)
        const tipPercent = ref(null)

        function tip(perc) {
            tipTotal.value = bill.value * perc / 100
            tipPercent.value = perc
        }

        watch(customTip, function(newValues) {
            if(newValues > 0 ) {
                tipTotal.value = bill.value * newValues / 100
                tipPercent.value = newValues
            }
        })
        
        const tipPerPerson = computed(function() {
            return (tipTotal.value / numberOfPeople.value).toFixed(2)
        })

        const billPerPerson = computed(function() {
            return ((bill.value + tipTotal.value) / numberOfPeople.value).toFixed(2)
        })

        watch([bill, numberOfPeople], function(newValues,) {
            if(newValues[0] > 0 && newValues[1] > 0) {
                tipVisibility.value = true
                totalVisibility.value = true
            }
        })

        function reset() {

            bill.value = null
            tipTotal.value= null
            numberOfPeople.value = null
            customTip.value = null
            tipVisibility.value = false
            totalVisibility.value = false
            tipPercent.value = null  
        }

        const billInputValidity = ref(false)
        const numberOfPeopleValidity = ref("pending")
        const customTipValidity = ref(false)

        watch([bill, numberOfPeople, customTip], function(newValues) {
            if(newValues[0] > 0 ) {
                billInputValidity.value = true
            } else {
                billInputValidity.value = false
            }

            if(newValues[1] > 0) {
                numberOfPeopleValidity.value = 'valid'
            } else if( newValues[1] === 0) {
                numberOfPeopleValidity.value = 'invalid'
                
            }else {
                numberOfPeopleValidity.value = 'pending'
            }

            if(newValues[2] > 0) {
                customTipValidity.value = true
            } else {
                customTipValidity.value = false
            }
        })

        return {
            bill,
            tip,
            numberOfPeople,
            tipPerPerson,
            billPerPerson,
            customTip,
            tipVisibility, 
            totalVisibility,
            tipPercent,
            reset,
            billInputValidity,
            numberOfPeopleValidity,
            customTipValidity
            
            }
    }

}
</script>

<style scoped>
.validInput {
    border: 2px solid #26C2AE
}

.invalidInput {
    border: 2px solid red
}


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

.activeTip {
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