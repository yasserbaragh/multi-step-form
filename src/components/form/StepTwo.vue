<template>
    <div>
        <div class="container">
            <h2>Select your plan</h2>
            <p class="par">You have the option of monthly or yearly billing</p>
            <div class="plans">
                <div class="plan" v-for="plan in plans" :key="plan" 
                @click="selectePlan(plan)" :class="{ active: plan.act}">
                    <span><img :src="require('../../assets/' + plan.icon)" alt="" /></span>
                    <h5>{{plan.name}}</h5>
                    <p v-if="month" class="desc">$ {{ plan.monthlyPrice }} /mo</p>
                    <p v-if="year" class="desc">$ {{ plan.yearlyPrice }} / yr</p>
                    <p v-if="year" class="year">2 month free</p>
                </div>
            </div>

            <div class="chosed">
                <label for="">Monthly</label>
                <input type="checkbox" @change="check">
                <label for="">Yearly</label>
            </div>
        </div>
    </div>
</template>

<script>


export default {
    name: "StepTwo",
    props:["month", "year","selecteddPlan", "planss"],
    data() {
        return {

            plans: this.planss, 
            selectedPlan: null
            
        }
    },
    
    methods: {
        check() {
            this.$emit("checkk")
        },
        selectePlan(plan) {
            this.plans.forEach((plane) => {
                plane.act = false
            })
            plan.act = true
            this.selectedPlan = {
                name: plan.name,
                monthlyPrice: plan.monthlyPrice,
                yearlyPrice: plan.yearlyPrice
            };
            this.$emit("plan-selected", this.selectedPlan)
            this.$emit("plansy", this.plans)
            
            
        }
    },
    
   
}



</script>

<style lang="scss">
.container {
    .plans {
        margin-bottom: 40px;
        .plan {
            outline: 1px solid hsl(229, 24%, 87%);
            border-radius: 7px;
            margin: 13px 0;
            padding: 15px 5px;
            cursor: pointer;
            transition: 0.1s ease-in-out;
            display: grid;
            grid-template-areas: "icon title title title title"
                                "icon desc desc desc desc"
                                ". year year year year";

            &:hover {
                outline-color: hsl(213, 96%, 18%);
                transition: 0.5s ease-in-out;
            }

            &.active {
                outline-color: hsl(213, 96%, 18%);
                background-color: hsl(231, 100%, 99%);
            }

            span {
                grid-area: icon;
                text-align: center;
                

                img {
                    width: 35px;
                }
            }
            h5 {
                grid-area: title;
            }
            .desc {
                grid-area: desc;
                font-size: 0.7rem;
                color: hsl(231, 11%, 63%);
            }
            .year {
                grid-area: year;
                font-size: 0.7rem;
                color: hsl(231, 11%, 63%);
            }

            
        }

    }
    .chosed {
        margin-bottom: 20px;
        width: 100%;
        text-align: center;

        input[type="checkbox"] {
            appearance: none;
            outline: none;
            position: relative;
            width: 32px;
            height: 16px;
            border-radius: 25px;
            background-color: hsl(213, 96%, 18%);
            margin: 0 10px;
            cursor: pointer;
            transition: 0.5s;
            
            
            &::before {
                content: "";
                height: 11px;
                width: 11px;
                background-color: white;
                position: absolute;
                margin: auto;
                top: 0;
                left: 3px;
                bottom: 0;
                border-radius: 50%;
                transition: 0.15s;

                
            }
            /* Checked Styles */
            &:checked {

                &::before {
                left: 19px;
                }
            }
        }
    }
}

//responsive 
@media (min-width: 768px){
    .container {
        .plans {
            display: flex;
            justify-content:space-between;

            .plan {
                width: 30%;
                display: flex;
                flex-direction: column;

                span {
                    height: 40px;
                    text-align: start;
                    margin-bottom: 20px;
                

                    img {
                        width: 40px;
                    }
                }
            }
        }
    }
}
    
</style>
