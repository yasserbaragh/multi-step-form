<template>
    <div>
        <div class="container">
            <h2>Pick add-ons</h2>
            <p class="par">Add-ons help enhance your gaming experience</p>
            <div class="addOns">
                <div class="addOn" :class="{active: addOn.act}" v-for="addOn in addOns" :key="addOn">
                    <input type="checkbox" v-model="selectedAddons" :value="addOn" @change="toggleClass(addOn)">
                    <h5>{{addOn.name}}</h5>
                    <p class="desc">{{ addOn.description }}</p>
                    <p class="mon" v-if="month">+${{ addOn.monthlyPrice }}/mo</p>
                    <p class="year" v-if="year">+${{ addOn.yearlyPrice }}/yr</p>
                </div>
                
            </div>
        </div>
    </div>
</template>

<script>


export default {
    name: "StepThree",
    props:["month", "year"],
    data() {
        return {
            addOns: [
                {
                    name: "Online Service",
                    description: "Access to multiplayer games",
                    monthlyPrice: 1,
                    yearlyPrice: 10,
                    act: false
                },
                {
                    name: "Larger Storage",
                    description: "Extra 1TB of cloud save",
                    monthlyPrice: 2,
                    yearlyPrice: 20,
                    act: false
                },
                {
                    name: "Customizable profile",
                    description: "Custom theme on your profile",
                    monthlyPrice: 2,
                    yearlyPrice: 20,
                    act: false
                }
            ],
            selectedAddons: []
        }
    },
    watch: {
        selectedAddons() {
            this.$emit("selecte", this.selectedAddons)
            console.log(this.selectedAddons)
        }
    },
    methods: {
        toggleClass(addOn) {
            addOn.act = !addOn.act
        }
    },
}

</script>

<style lang="scss">
    .addOns {
        letter-spacing: -0.3px;
        margin-bottom: 40px;
        .addOn {
            outline: 1px solid hsl(229, 24%, 87%);
            border-radius: 7px;
            margin: 13px 0;
            padding: 15px 5px;
            display: grid;
            grid-template-areas: "check title title price"
                                "check desc desc price";

            &.active {
                outline-color: hsl(213, 96%, 18%);
                background-color: hsl(231, 100%, 99%);
            }

            input[type="checkbox"] {
                grid-area: check;
                margin: 8px;
            }
            h5 {
                grid-area: title;
                font-size: 0.8rem;
                font-weight: 700;
            }
            .desc {
                grid-area: desc;
                font-size: 0.65rem;
                color: hsl(231, 11%, 63%);
            }
            .year, .mon {
                margin-left: 5px;
                margin-top: 7px;
                grid-area: price;
                font-size: 0.65rem;
                color: hsl(243, 100%, 62%);
            }
        }
    }
    @media (min-width: 768px) {
        .addOns {
            .addOn {
                grid-template-areas: "check title title title title title title price"
                                    "check desc desc desc desc desc desc price";

                input[type="checkbox"] {
                margin: 5px;
                position: relative;
                left: -5px;
                }
            }
        }
    }
</style>