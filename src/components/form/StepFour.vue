<template>
    <div>
        <div class="container">
            <h2>Finishing up</h2>
            <p class="par">Double-check everything looks OK before confirming</p>
        </div>
        <div class="prices">
            <div class="slectedPlan">
                <h5 v-if="month">{{ selecteddPlan.name }} (monthly)</h5>
                <h5 v-if="year">{{ selecteddPlan.name }} (yearly)</h5>
                <p v-if="month">${{ selecteddPlan.monthlyPrice }}/mo</p>
                <p v-if="year">${{ selecteddPlan.yearlyPrice }}/yr</p>
                <button @click="$emit('go-to-step-two')">change</button>
            </div>
            <div class="selectedAddOn">
                <div class="add" v-for="add in selectedAddon" :key="add">
                    <p>{{ add.name }}</p>
                    <span v-if="month">+${{ add.monthlyPrice }}/mo</span>
                    <span v-if="year">+${{ add.yearlyPrice }}/yr</span>
                </div>
            </div>
        </div>
        <div class="total">
            <div class="pr">
                <p v-if="month">Total (per month)</p>
                <p v-if="year">Total (per year)</p>
            </div>
           <div class="prix">
                <span v-if="month">+${{ getTotal }}/mo</span>
                <span v-if="year">+${{ getTotal }}/yr</span>
           </div>
        </div>
    </div>
</template>

<script>

export default {
    name: "StepTwo",
   props: ["month","year","selecteddPlan","selectedAddon", "Page"],
   data() {
    return {
        mois: this.month,
        annee: this.year,
        selectedPlane: this.selecteddPlan,
        selectedAddone: this.selectedAddon,
        total: 0,
        Pagee: this.Page
    }
   },
   computed: {
    getTotal() {
        let totalPrice = 0
       
        if (this.mois) {
        totalPrice += parseFloat(this.selectedPlane.monthlyPrice);
        } else if (this.annee) {
        totalPrice += parseFloat(this.selectedPlane.yearlyPrice);
        }
        

        if(this.selectedAddon != null) {
            this.selectedAddone.forEach((addon) => {
                if (this.mois) {
                totalPrice += parseFloat(addon.monthlyPrice);
                } else if (this.annee) {
                totalPrice += parseFloat(addon.yearlyPrice);
                }
            })
        }

        return totalPrice;
    }
   },
   
}

</script>

<style lang="scss">
.prices {
    background-color: hsl(231, 100%, 99%);
    padding: 5px 15px;
    letter-spacing: -0.9px;

    .slectedPlan {
        position: relative;
        &::after {
            content: "";
            position: absolute;
            bottom: 8px;
            left: 50%;
            transform: translateX(-50%);
            width: 100%;
            height: 1px;
            background-color: hsl(231, 11%, 63%);
        }
        h5 {
            margin-top: 10px;
            letter-spacing: -0.9px;
        }
        p {
            float: right;
            font-size: 0.8rem;
            font-weight: 500;
            color: hsl(213, 96%, 18%)
        }
        button {
            background-color: transparent;
            border: none;
            text-decoration: underline 1.5px;
            margin-bottom: 20px;
            color: hsl(231, 11%, 63%);
            cursor: pointer;
            transition: 0.3s;

            &:hover {
                color: hsl(243, 100%, 62%);
            }
        }
    }
    .selectedAddOn {
        .add {
            display: flex;
            justify-content: space-between;
            margin: 15px 0;
            p {
                color: hsl(231, 11%, 63%);
                font-size: 0.8rem;
                font-weight: 300;
            }
            span {
                font-size: 0.8rem;
            }
        }
    }
}

.total {
    display: flex;
    justify-content: space-between;
    margin: 15px 0;
    padding: 5px 15px;
    letter-spacing: -0.9px;

    .pr {
        p {
            color: hsl(231, 11%, 63%);
            font-size: 0.8rem;
            font-weight: 300;
        }
    }

    .prix {
        span {
            font-size: 0.9rem;
            font-weight: 500;
            color: hsl(243, 100%, 62%);
        }
    }
}
    
</style>