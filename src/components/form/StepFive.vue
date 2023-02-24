<template>
    <div class="thanks">
        <div class="container">
            <span><img src="../../assets/icon-thank-you.svg" alt=""></span>
            <h2>Thank you!</h2>
            <p class="par">Thanks for confirming your subscription! We hop you have fun using our platform. if you ever need support, please feel free to eamil us at support@loremgaming.com.</p>
        </div>
    </div>
</template>

<script>

export default {
    name: "StepFive",
    
   
}

</script>

<style lang="scss">

.thanks {
    text-align: center;
    margin: 50px 0;

    span {
        img {
            width: 50px;
        }
    }
    h2 {
        margin-top: 20px;
        letter-spacing: -0.5px;
    }

    .par {
        letter-spacing: -0.5px;
    }
}

@media(min-width: 768px) {
    .thanks {
        text-align: center;
        position: absolute;
        top: 40%;
        left: 50%;
        transform: translate(-50%,-50%);
        width: 90%;

        .container {
            h2 {
                margin-top: 20px;
                font-size: 1.8rem;
                font-weight: 700;
                letter-spacing: -0.5px;
            }

            .par {
                letter-spacing: -0.5px;
            }
        }
        

    }
}
    
</style>