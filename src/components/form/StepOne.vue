<template>
    <div>
        <div class="container">
            <h2>Personoal info</h2>
            <p class="par">Please provide your name, email, adress, and phone number</p>
            <form action="">
                <label for="">name</label><p v-if="errName" class="err">this field is required</p> <br>
                <input type="text" placeholder="e.g.Stephen King" v-model="info.name"
                :class="{err :  errName}" @keyup="erreurN" required> <br>
                <label for="">Email Address</label><p v-if="errEmail" class="err">this field is required</p>
                <p v-if="errEmailTwo" class="err">Invalid Email Format</p><br>
                <input type="email" placeholder="e.g.stephenking@lorem.com" v-model="info.email"
                :class="{err :  errEmail || errEmailTwo}" @keyup="erreurE" required><br>
                <label for="">Phone number</label><p v-if="errNumber" class="err">this field is required</p><br>
                <input type="number" placeholder="e.g +1 234 567 890" v-model="info.number"
                :class="{err :  errNumber}" @keyup="erreurNu" required><br>
            </form>
        </div>
    </div>
</template>


<script>

export default {
    props: ["infos"],
    data() {
        return {
            info: this.infos,
            errName: false,
            errEmail: false,
            errEmailTwo: false,
            errNumber: false
        }
    },
    watch: {
        info() {
            this.$emit("ifos", this.info)
            console.log(this.info)
        }
    },
    methods: {
        erreurN () {
            if(this.info.name === "") {this.errName = true} else {
                this.errName = false
            } 
        },
        erreurE () {
            if(this.info.email === "") {
                this.errEmail = true
            }else if(this.info.email !== "" && !(/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.infos.email))) {
                this.errEmail = false
                this.errEmailTwo = true
            }else {
                this.errEmail = false
                this.errEmailTwo = false
            }
        },
        erreurNu () {
            if(this.info.number === "") {this.errNumber = true}else {
                this.errNumber = false
            }
        }
        
            
    },
    
}
</script>

<style lang="scss">
.container{
    h2{
        margin-bottom: 15px;
        font-size: 1.2rem;
        font-weight: 700;
        color: hsl(213, 96%, 18%);
    }
    .par{
        margin-bottom: 25px;
        font-size: 0.9rem;
        font-weight: 300;
        color: hsl(231, 11%, 63%);
    }
    form{
        label {
            text-transform: capitalize;
            margin-bottom: 5px;
            font-size: 0.8rem;
            font-weight: 500;
            letter-spacing: -0.5px;
            color: hsl(213, 96%, 18%);
        }
        p.err {
            float: right;
            font-size: 0.8rem;
            color: hsl(354, 84%, 57%);
            font-weight: 500;
            letter-spacing: -0.5px;
        }
        input{
            margin-top: 5px;
            margin-bottom: 10px;
            padding: 8px 15px;
            border-radius: 5px;
            border: none;
            outline: 1px solid hsl(231, 11%, 63%)
;
            font-size: 0.8rem;
            font-weight: 300;
            letter-spacing: -0.5px;
            cursor: pointer;

            &.err {
                outline-color: hsl(354, 84%, 57%);
            }
        }
    }
}

@media (min-width: 768px) {
    .container {
        form {
            input {
                padding: 10px 15px;
            }
        }
    }
}

</style>
