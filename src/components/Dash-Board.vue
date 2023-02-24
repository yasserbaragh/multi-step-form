<template>
    <div class="template">
        <div class="login">
            <div class="dash">
                <div class="container">
                    <ul class="flex">
                        <li v-for="step in steps" :key="step"
                        ref="num">
                            <div :id="step.number" class="a">
                                <span :id="step.number" :class="{active: step.act}">{{ step.number }}</span>
                                <div class="description">
                                    <p :id="step.number" class="grey">{{ step.stepa }}</p>
                                    <p :id="step.number">{{ step.desc }}</p>
                                </div>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
            <div class="content">
                <div v-if="Page === 1"><StepOne :infos="infos" @ifos="onStepOneComplete"/></div>
                <div v-else-if="Page === 2"><StepTwo :month="month"
                :year="year" @checkk="checked" :selectedPlan="selectedPlan"
                @plan-selected="onPlanSelected" :planss="planss" @plansy="planso"/></div>
                <div v-else-if="Page === 3"><StepThree :month="month" 
                :year="year" @selecte="onAddonSelected" /></div>
                <div v-else-if="Page === 4"><StepFour :month="month" 
                :year="year" :selecteddPlan="selecteddPlan" 
                :selectedAddon="selectedAddon" @go-to-step-two="Page = 2; toggleClass()"/></div>
                <div v-else-if="Page === 5"><StepFive :month="month" :year="year" /></div>
                <div class="lastc" v-if="Page < 5">
                    <button v-if="Page > 1" @click="Page--; toggleClass()" class="back">Go Back</button>
                    <button :disabled="!isValid" v-if="Page < 4" @click="Page++; toggleClass()" class="forward">Next step</button>
                    <button v-if="Page === 4" @click="Page++" class="forward confirm">Confirm</button>
                </div>
            </div>
        </div>
        <div class="last" v-if="Page < 5">
            <button v-if="Page > 1" @click="Page--; toggleClass()" class="back">Go Back</button>
            <button :disabled="!isValid" v-if="Page < 4" @click="Page++; toggleClass()" class="forward">Next step</button>
            <button v-if="Page === 4" @click="Page++" class="forward confirm">Confirm</button>
        </div>
    </div>
</template>

<script>
import StepFive from './form/StepFive.vue';
import StepFour from './form/StepFour.vue';
import StepOne from './form/StepOne.vue';
import StepThree from './form/StepThree.vue';
import StepTwo from './form/StepTwo.vue';





export default {
    name: "DashBoard",
    components: { StepOne, StepTwo, StepThree,
        StepFour, StepFive },
    props: {
        selectedPlan: Object,
        selectedAddons: Object,
        info: Object

    },
    data() {
        return {
            steps: [
                {
                    number: 1,
                    stepa: "step 1",
                    desc: "your info",
                    act: true
                },
                {
                    number: 2,
                    stepa: "step 2",
                    desc: "select plan",
                    act: false
                },
                {
                    number: 3,
                    stepa: "step 3",
                    desc: "add-ons",
                    act: false
                },
                {
                    number: 4,
                    stepa: "step 4",
                    desc: "summary",
                    act: false
                }
            ],
            planss: [
                {
                    icon: "icon-arcade.svg",
                    name: "Arcade",
                    monthlyPrice: 9,
                    yearlyPrice: 90,
                    act: true
                },
                {
                    icon: "icon-advanced.svg",
                    name: "Advanced",
                    monthlyPrice: 12,
                    yearlyPrice: 120,
                    act: false
                },
                {
                    icon: "icon-pro.svg",
                    name: "Pro",
                    monthlyPrice: 15,
                    yearlyPrice: 150,
                    act: false
                }
            ], 
            Page: 1,

            infos: {
                name: "",
                email: "",
                number: "",
            },
            
            month: true,
            year: false,

            selecteddPlan: {
                name: "Arcade",
                monthlyPrice: 9,
                yearlyPrice: 90
            },
            selectedAddon: this.selectedAddons
            
        }
    },
    methods: {
        toggleClass() {
            this.steps.forEach((step) => {
                step.act = false
            })
            if(this.Page === 1) {
                this.steps[0].act = true
            } else if (this.Page === 2) {
                this.steps[1].act = true
            } else if (this.Page === 3) {
                this.steps[2].act = true
            } else if (this.Page === 4) {
                this.steps[3].act = true
            }
        },  
        checked() {
            this.month = !this.month
            this.year = !this.year
        },
        onPlanSelected(plan) {
            this.selecteddPlan = plan
            
        },
        planso(plan) {
            this.planss = plan
            
        },
        onAddonSelected(addOn) {
            this.selectedAddon = addOn
            console.log(this.selectedAddon)
        },
        onStepOneComplete() {
            this.infos = this.info
            console.log(this.infos)
        },
       
    },
    computed: {
        isValid() {
            return (
                this.infos.name !== "" && 
                this.infos.email !== "" &&
                /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.infos.email) && 
                this.infos.number !== ""
            );
        }
    },
    
    
}
</script>

<style lang="scss">
.template {
    background-color: hsl(217, 100%, 97%);
    height: 100vh;
}
.dash{
    background-image: url(../assets/bg-sidebar-mobile.svg);
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    .container{
        ul{
            padding: 5px;
            li {
                display: inline-block;
                margin: 0 15px;
                margin-top: 25px;
                margin-bottom: 90px;

                .a {
                    span {
                        font-size: 16px;
                        color: white;
                        outline: 1px solid white;
                        border-radius: 50%;
                        padding: 40% 85%;
                        font-weight: 500;

                        &.active {
                            background-color: hsl(228, 100%, 84%);
                            color: hsl(213, 96%, 18%);
                            outline: none;
                        }
                                       
                    }
                }
                .active {
                    span{
                        background-color: hsl(228, 100%, 84%);
                        outline: none;
                    }
                }
            }
            .description{
                display: none;
            }
        }
    }
}
.content {
    background-color: white;
    box-shadow: 1px 5px 5px 1px rgba(0, 0, 0, 0.1);
    width: 90vw;
    position: absolute;
    top: 15%;
    left: 50%;
    transform: translateX(-50%);
    padding: 25px;
    border-radius: 20px;
    text-align: start;
    .lastc {
        display: none;
    }

}

.last{
    position: absolute;
    bottom: 0;
    background-color: white;
    width: 100vw;
    height: 60px;

    button {
        padding: 9px 14px;
        border-radius: 5px;
        border: none;
        cursor: pointer;
        transition: 0.5s ease;
    }

    .back {
        background-color: transparent;
        color: hsl(231, 11%, 63%);
        float: left;
        margin-left: 10px;
        margin-top: 13px;

        &:hover {
            color: hsl(213, 96%, 18%);
        }
    }
    .forward {
        background-color: hsl(213, 96%, 18%);
        color: white;
        font-weight: 600;
        float: right;
        margin-right: 10px;
        margin-top: 13px;

        &:hover {
            opacity: 0.9;
        }

        &.confirm {
            background-color: hsl(243, 100%, 62%);
        }
    }
}

//responsive 
@media (min-width: 768px) {
    .login {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
        width: 750px;
        display: flex;
        background-color: white;
        padding: 10px;
        border-radius: 10px;
        box-shadow: 1px 5px 5px 1px rgba(0, 0, 0, 0.1);
    }
    .dash{
        background-image: url(../assets/bg-sidebar-desktop.svg);
        height: 60vh;
        border-radius: 10px;
        width: 35vw;
        .container{
            ul{
                
                li {
                    display: block;
                    margin-bottom: 20px;

                    .a {
                        display: grid;
                        grid-template-areas: "sp desc  desc desc"
                                            ". desc  desc desc";
                        span {
                            grid-area: sp;
                            padding: 3px 10%;
                            width: 25px;
                            margin-top: 9px;
                                        
                        }
                        .description {
                            grid-area: desc;
                            display: block;
                            text-align: start;
                            color: white;
                            text-transform: uppercase;
                            font-size: 0.9rem;
                            margin-left: 10px;
                            margin-top: 5px;

                            p {
                                margin-bottom: 0;
                                width: 100%;
                                font-weight: 500;
                                letter-spacing: 0.3px;
                            }
                            .grey {
                                color: hsl(231, 10%, 63%);
                                letter-spacing: -0.5px;
                            }
                        }
                    }
                
                }
                .description{
                    display: block;
                }
            }
        }
    }
    .content {
        margin: 0 50px;
        background-color: transparent;
        box-shadow: none;
        width: 80vw;
        position: relative;
        top: 0;
        left: 0;
        transform: translateX(0);
        padding: 25px;
        input {
            width: 100%;
        }
        .lastc {
        display: block;
        position: absolute;
        bottom: 0;
        background-color: white;
        width: 100%;
        height: 60px;

        button {
            padding: 9px 14px;
            border-radius: 5px;
            border: none;
            cursor: pointer;
            transition: 0.5s ease;
        }

        .back {
            background-color: transparent;
            color: hsl(231, 11%, 63%);
            float: left;
            margin-left: 10px;
            margin-top: 13px;

            &:hover {
                color: hsl(213, 96%, 18%);
            }
        }
        .forward {
            background-color: hsl(213, 96%, 18%);
            color: white;
            font-weight: 600;
            float: right;
            margin-right: 10px;
            margin-top: 13px;

            &:hover {
                opacity: 0.9;
            }

            &.confirm {
                background-color: hsl(243, 100%, 62%);
            }
        }
    }

    }

    .last{
        display: none;
    }

}

</style>
