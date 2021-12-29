<template>
    <div class="container" v-if="weatherName.cod != 404 && weatherName.cod != undefined" :style="`background-image: url(${bgImage})`">
    </div>
</template>

<script>
import anime from 'animejs/lib/anime.es.js';
export default {
    name : 'Animation',
    props : {
        weatherName : Object,
        dayOrNight : String
    },
    data() {
        return {
            bgImage : '',
            bgSnowDay : 'https://i.imgur.com/Ut2oCwE.jpg',
            bgSnowNight : 'https://i.imgur.com/0UxlOXW.jpg',
            bgClearDay : 'https://i.imgur.com/7RqQU6w.jpg',
            bgClearNight : 'https://i.imgur.com/oJnLah8.jpg',
            bgCloudNight : 'https://i.imgur.com/IBVGJVt.jpg',
            bgCloudDay : 'https://i.imgur.com/uT1bkiV.jpg',
            bgFogDay : 'https://i.imgur.com/GQxsJmo.jpg',
            bgFogNight : 'https://i.imgur.com/spAgSaA.jpg',
            bgThunderDay : 'https://i.imgur.com/ERbhi2v.jpg',
            bgThunderNight : 'https://i.imgur.com/5r7ZR1H.jpg',
        }
    },
    methods: {
        // Stops the animation when changing from one city to another
        resetAnimation() {
            let container = document.querySelector('.container')
            container.innerHTML = '';
        },
        randomNumberObject() {
            return Math.floor(Math.random() * (50 - 25) ) + 50;
        },
        randomObjectposition() {
            return Math.floor(Math.random() * (100 - 0) ) + 0;
        },
        // Cloud animation
        clouds() {
            this.resetAnimation();
            if ( this.dayOrNight == 'Day') {
                this.bgImage = this.bgCloudDay;
            } else {
                this.bgImage = this.bgCloudNight;
            }
            let container = document.querySelector('.container')
            //creating cloud divs
            // Creating background, middle, foreground layers
            for ( let i = 0; i < 10; i++) {
                let cloud = document.createElement("Div");
                cloud.className = "cloud";
                container.appendChild(cloud);
            }
            // assigning respective classes to all 3 layers
            const cloudList = container.childNodes;
            const cloudNames = ['one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight','nine', 'ten']
            for ( let j = 0; j < cloudList.length; j++) {
                cloudList[j].classList.add(cloudNames[j]);
            }
            anime({
                targets : '.cloud.one',
                left : '105%',
                duration : 10000,
                loop : true,
                easing : 'linear',
                direction : 'normal'
            });
            anime({
                targets : '.cloud.two',
                delay: 500,
                left : '105%',
                duration : 10000,
                loop : true,
                easing : 'linear',
                direction : 'normal'
            });
            anime({
                targets : '.cloud.three',
                delay: 750,
                left : '105%',
                duration : 15000,
                loop : true,
                easing : 'linear',
                direction : 'normal'
            });
            anime({
                targets : '.cloud.four',
                delay: 200,
                left : '105%',
                duration : 10500,
                loop : true,
                easing : 'linear',
                direction : 'normal'
            });
            anime({
                targets : '.cloud.five',
                delay: 1000,
                left : '105%',
                duration : 9000,
                loop : true,
                easing : 'linear',
                direction : 'normal'
            });
            anime({
                targets : '.cloud.six',
                delay: 800,
                left : '105%',
                duration : 20000,
                loop : true,
                easing : 'linear',
                direction : 'normal'
            });
            anime({
                targets : '.cloud.seven',
                delay: 1000,
                left : '105%',
                duration : 41000,
                loop : true,
                easing : 'linear',
                direction : 'normal'
            });
        },
        // Snow animation
        snow() {
            this.resetAnimation();
            // Change background
            if ( this.dayOrNight == 'Day') {
                this.bgImage = this.bgSnowDay;
            } else {
                this.bgImage = this.bgSnowNight;
            }
            let container = document.querySelector('.container')
            // Creating background, middle, foreground layers
            for ( let i = 0; i < 3; i++) {
                let layer = document.createElement("Div");
                layer.className = "layer";
                container.appendChild(layer);
            }
            // assigning respective classes to all 3 layers
            const layerList = container.childNodes;
            const layerNames = ['back', 'middle', 'front']
            for ( let j = 0; j < layerList.length; j++) {
                layerList[j].classList.add(layerNames[j]);
            }
            // creating snowflakes in the background
            const backLayer = document.querySelector('.back')
            for ( let k = 0; k < this.randomNumberObject(); k++) {
                let snowflake = document.createElement("Div");
                backLayer.appendChild(snowflake);
                snowflake.classList.add('snowflake');
                snowflake.style.position = 'absolute';
                snowflake.style.top = `${this.randomObjectposition() - 100}%`;
                snowflake.style.left = `${this.randomObjectposition()}%`;
                snowflake.style.width = '5px';
                snowflake.style.height = '5px';
                snowflake.style.background = '#ffffff';
                snowflake.style.borderRadius = '50%';
            }
            // creating snowflakes in the middle layer
            const middleLayer = document.querySelector('.middle')
            for ( let k = 0; k < this.randomNumberObject(); k++) {
                let snowflake = document.createElement("Div");
                snowflake.classList.add('snowflake');
                middleLayer.appendChild(snowflake);
                snowflake.style.position = 'absolute';
                snowflake.style.top = `${this.randomObjectposition() - 100}%`;
                snowflake.style.left = `${this.randomObjectposition()}%`;
                snowflake.style.width = '10px';
                snowflake.style.height = '10px';
                snowflake.style.background = '#ffffff';
                snowflake.style.borderRadius = '50%';

            }
            // creating snowflakes in the foreground
            const frontLayer = document.querySelector('.front')
            for ( let k = 0; k < this.randomNumberObject(); k++) {
                let snowflake = document.createElement("Div");
                snowflake.classList.add('snowflake');
                frontLayer.appendChild(snowflake);
                snowflake.style.position = 'absolute';
                snowflake.style.top = `${this.randomObjectposition() - 100}%`;
                snowflake.style.left = `${this.randomObjectposition()}%`;
                snowflake.style.width = '20px';
                snowflake.style.height = '20px';
                snowflake.style.background = '#ffffff';
                snowflake.style.borderRadius = '50%';
            }
            // animating snowflakes towards the bottom of the page
            anime({
                targets : '.back .snowflake',
                top : "105%",
                duration : 8000,
                loop : true,
                easing : 'linear',
                direction : 'normal',
                delay : anime.stagger(100)
            });
            anime({
                targets : '.middle .snowflake',
                top : "105%",
                duration : 6000,
                loop : true,
                easing : 'linear',
                direction : 'normal',
                delay : anime.stagger(100)
            });
            anime({
                targets : '.front .snowflake',
                top : "105%",
                duration : 4000,
                loop : true,
                easing : 'linear',
                direction : 'normal',
                delay : anime.stagger(100)
            });
                
        },
        rain() {
            this.resetAnimation();
            if ( this.dayOrNight == 'Day') {
                this.bgImage = this.bgCloudDay;
            } else {
                this.bgImage = this.bgCloudNight;
            }
            let container = document.querySelector('.container')
            // Creating background, middle, foreground layers
            for ( let i = 0; i < 3; i++) {
                let layer = document.createElement("Div");
                layer.className = "layer";
                container.appendChild(layer);
            }
            // assigning respective classes to all 3 layers
            const layerList = container.childNodes;
            const layerNames = ['back', 'middle', 'front']
            for ( let j = 0; j < layerList.length; j++) {
                layerList[j].classList.add(layerNames[j]);
            }
            // creating raindrops in the background
            const backLayer = document.querySelector('.back')
            for ( let k = 0; k < this.randomNumberObject(); k++) {
                let raindrop = document.createElement("Div");
                backLayer.appendChild(raindrop);
                raindrop.classList.add('raindrop');
                raindrop.style.position = 'absolute';
                raindrop.style.top = `${this.randomObjectposition() - 100}%`;
                raindrop.style.left = `${this.randomObjectposition()}%`;
                raindrop.style.width = '1px';
                raindrop.style.height = '6px';
                raindrop.style.background = '#ededed';
                raindrop.style.borderRadius = '25px';
            }
            // creating raindrops in the middle layer
            const middleLayer = document.querySelector('.middle')
            for ( let k = 0; k < this.randomNumberObject(); k++) {
                let raindrop = document.createElement("Div");
                raindrop.classList.add('raindrop');
                middleLayer.appendChild(raindrop);
                raindrop.style.position = 'absolute';
                raindrop.style.top = `${this.randomObjectposition() - 100}%`;
                raindrop.style.left = `${this.randomObjectposition()}%`;
                raindrop.style.width = '2px';
                raindrop.style.height = '12px';
                raindrop.style.background = '#ededed';
                raindrop.style.borderRadius = '25px';

            }
            // creating raindrops in the foreground
            const frontLayer = document.querySelector('.front')
            for ( let k = 0; k < this.randomNumberObject(); k++) {
                let raindrop = document.createElement("Div");
                raindrop.classList.add('raindrop');
                frontLayer.appendChild(raindrop);
                raindrop.style.position = 'absolute';
                raindrop.style.top = `${this.randomObjectposition() - 100}%`;
                raindrop.style.left = `${this.randomObjectposition()}%`;
                raindrop.style.width = '3px';
                raindrop.style.height = '18px';
                raindrop.style.background = '#ededed';
                raindrop.style.borderRadius = '25px';
            }
            anime({
                targets : '.back .raindrop',
                top : "105%",
                duration : 4000,
                loop : true,
                easing : 'linear',
                direction : 'normal',
                delay : anime.stagger(50)
            });
            anime({
                targets : '.middle .raindrop',
                top : "105%",
                duration : 1500,
                loop : true,
                easing : 'linear',
                direction : 'normal',
                delay : anime.stagger(50)
            });
            anime({
                targets : '.front .raindrop',
                top : "105%",
                duration : 1000,
                loop : true,
                easing : 'linear',
                direction : 'normal',
                delay : anime.stagger(50)
            });
        },
        fog() {
            this.resetAnimation();
            if ( this.dayOrNight == 'Day') {
                this.bgImage = this.bgFogDay;
            } else {
                this.bgImage = this.bgFogNight;
            }
            let container = document.querySelector('.container')
            // Creating background, middle, foreground layers
            for ( let i = 0; i < 3; i++) {
                let fogBank = document.createElement("Div");
                fogBank.className = "fogbank";
                container.appendChild(fogBank);
            }
            // assigning respective classes to all 3 layers
            const fogBankList = container.childNodes;
            const layerNames = ['back', 'middle', 'front']
            for ( let j = 0; j < fogBankList.length; j++) {
                fogBankList[j].classList.add(layerNames[j]);
                fogBankList[j].style.position = 'absolute';
                fogBankList[j].style.width = '100%';
                fogBankList[j].style.bottom = '0';
            }
            anime({
                targets : '.back.fogbank',
                height : ['45%', '48%'],
                duration : 7000,
                loop : true,
                easing : 'linear',
                direction : 'alternate',
            });
            anime({
                targets : '.middle.fogbank',
                height : ['45%', '39%'],
                duration : 8000,
                loop : true,
                easing : 'linear',
                direction : 'alternate',
            });
            anime({
                targets : '.front.fogbank',
                height : ['38%', '35%'],
                duration : 6400,
                loop : true,
                easing : 'linear',
                direction : 'alternate',
            });
        },
        clear() {
            this.resetAnimation();
            if ( this.dayOrNight == 'Day') {
                this.bgImage = this.bgClearDay;
            } else {
                this.bgImage = this.bgClearNight;
            }
        },
        thunderstorm() {
            this.resetAnimation();
            if ( this.dayOrNight == 'Day') {
                this.bgImage = this.bgThunderDay;
            } else {
                this.bgImage = this.bgThunderNight;
            }
            let container = document.querySelector('.container')
            // Creating background, middle, foreground layers
            for ( let i = 0; i < 3; i++) {
                let layer = document.createElement("Div");
                layer.className = "layer";
                container.appendChild(layer);
            }
            // assigning respective classes to all 3 layers
            const layerList = container.childNodes;
            const layerNames = ['back', 'middle', 'front']
            for ( let j = 0; j < layerList.length; j++) {
                layerList[j].classList.add(layerNames[j]);
            }
            // creating raindrops in the background
            const backLayer = document.querySelector('.back')
            for ( let k = 0; k < 2000; k++) {
                let raindrop = document.createElement("Div");
                backLayer.appendChild(raindrop);
                raindrop.classList.add('raindrop');
                raindrop.style.position = 'absolute';
                raindrop.style.top = `-5%`;
                raindrop.style.left = `${this.randomObjectposition()}%`;
                raindrop.style.width = '2px';
                raindrop.style.height = '9px';
                raindrop.style.background = '#ffffff';
                raindrop.style.borderRadius = '25px';
            }
            // creating raindrops in the middle layer
            const middleLayer = document.querySelector('.middle')
            for ( let k = 0; k < 200; k++) {
                let raindrop = document.createElement("Div");
                raindrop.classList.add('raindrop');
                middleLayer.appendChild(raindrop);
                raindrop.style.position = 'absolute';
                raindrop.style.top = `-5%`;
                raindrop.style.left = `${this.randomObjectposition()}%`;
                raindrop.style.width = '2px';
                raindrop.style.height = '12px';
                raindrop.style.background = '#ffffff';
                raindrop.style.borderRadius = '25px';

            }
            // creating raindrops in the foreground
            const frontLayer = document.querySelector('.front')
            for ( let k = 0; k < 200; k++) {
                let raindrop = document.createElement("Div");
                raindrop.classList.add('raindrop');
                frontLayer.appendChild(raindrop);
                raindrop.style.position = 'absolute';
                raindrop.style.top = `-5%`;
                raindrop.style.left = `${this.randomObjectposition()}%`;
                raindrop.style.width = '2px';
                raindrop.style.height = '18px';
                raindrop.style.background = '#ededed';
                raindrop.style.borderRadius = '25px';
            }
            // creating lightning
            let lightning = document.createElement("Div");
            lightning.className = "lightning";
            container.appendChild(lightning);
            anime({
                targets : '.back .raindrop',
                top : "105%",
                duration : 200,
                loop : true,
                easing : 'linear',
                direction : 'normal',
                delay : anime.stagger(20)
            });
            anime({
                targets : '.middle .raindrop',
                top : "105%",
                duration : 100,
                loop : true,
                easing : 'linear',
                direction : 'normal',
                delay : anime.stagger(20)
            });
            anime({
                targets : '.front .raindrop',
                top : "105%",
                duration : 50,
                loop : true,
                easing : 'linear',
                direction : 'normal',
                delay : anime.stagger(50)
            });
            anime({
                targets : '.lightning',
                backgroundColor : '#ffffff',
                delay: 5000,
                duration : 50,
                loop : true,
                easing : 'easeOutElastic',
                direction : 'alternate',
            });

        },
    },
    updated() {
            let weatherType = this.weatherName.weather[0].main;
            // let weatherType = 'Clouds'; ///////////////DEBUGGING!!!!!!!!!!!!!!!!
            console.log(weatherType);
            switch (weatherType) {
                case 'Clouds' :
                    this.clouds();
                    break;
                case 'Clear' :
                    this.clear();
                    break;
                case 'Thunderstorm' :
                    this.thunderstorm();
                    break;
                case 'Drizzle' :
                    this.rain();
                    break;
                case 'Rain' :
                    this.rain();
                    break;
                case 'Snow' :
                    this.snow();
                    break;
                case 'Mist' :
                    this.fog();
                    break;
                case 'Smoke' :
                    this.fog();
                    break;
                case 'Haze' :
                    this.fog();
                    break;
                case 'Dust' :
                    this.fog();
                    break;
                case 'Fog' :
                    this.fog();
                    break;
                case 'Sand' :
                    this.fog();
                    break;
                case 'Ash' :
                    this.fog();
                    break;
                case 'Squall' :
                    this.fog();
                    break;
                case 'Tornado' :
                    this.fog();
                    break;
                default: 
                    console.log('No weather event')
            }
        }
}
</script>

<style lang="scss">
.container {
    position: absolute;
    width: 100%;
    height: 100%;
    top:0;
    left: 0;
    z-index: -1;
    overflow: hidden;
    background: rgba(0, 0, 0, 0.1);
    background-blend-mode: multiply;
    background-size: cover;
    background-position: center center;
    background-repeat: no-repeat;
    transition: .4s;
    /* CLOUDS */ 
    .cloud.one {
        background-color: #cecece;
        width: 150px;
        height: 50px;
        border-radius: 100px;
        position: absolute;
        top: 20%;
        left: -105%;
        opacity: .5;
        z-index: 10;
        -webkit-box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55); 
        box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55);
        &::after, 
        &::before{
            content:"";
            position:absolute;
            display:inline-block;
            background:inherit;
            border-radius:inherit;
            -webkit-box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55); 
            box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55);
        }
        &::after{
            width:50px;
            height:50px;
            top:-30px;
            left:30px;
        }
        &::before{
            width:65px;
            height:65px;
            top: -40px;
            left:70px;
        }
    }
    .cloud.two {
        background-color: #cecece;
        width: 259px;
        height: 69px;
        border-radius: 100px;
        position: absolute;
        top: 15%;
        left: -100%;
        opacity: .5;
        z-index: -1;
        -webkit-box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55); 
        box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55);
        &::after, 
        &::before{
            content:"";
            position:absolute;
            display:inline-block;
            background:inherit;
            border-radius:inherit;
            -webkit-box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55); 
            box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55);
        }
        &::after{
            width: 105px;
            height: 105px;
            top: -65px;
            left: 59px;
        }
        &::before{
            width: 90px;
            height: 90px;
            top: -38px;
            left: 148px;
        }
    }
    .cloud.three {
        background-color: #cecece;
        width: 518px;
        height: 138px;
        border-radius: 200px;
        position: absolute;
        top: 5%;
        left: -200%;
        opacity: .5;
        z-index: -2;
        -webkit-box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55); 
        box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55);
        &::after, 
        &::before{
            content:"";
            position:absolute;
            display:inline-block;
            background:inherit;
            border-radius:inherit;
            -webkit-box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55); 
            box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55);
        }
        &::after{
            width: 210px;
            height: 210px;
            top: -130px;
            left: 118px;
        }
        &::before{
            width: 180px;
            height: 180px;
            top: -76px;
            left: 296px;
        }
    }
    .cloud.four {
        background-color: #cecece;
        width: 148px;
        height: 39.42px;
        border-radius: 100px;
        position: absolute;
        top: 25%;
        left: -200%;
        opacity: .5;
        z-index: 3;
        -webkit-box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55); 
        box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55);
        &::after, 
        &::before{
            content:"";
            position:absolute;
            display:inline-block;
            background:inherit;
            border-radius:inherit;
            -webkit-box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55); 
            box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55);
        }
        &::after{
            width: 60px;
            height: 60px;
            top: -38px;
            left: 76px;
        }
        &::before{
            width: 51.42px;
            height: 51.42px;
            top: -29px;
            left: 31px;
        }
    }
    .cloud.five {
        background-color: #cecece;
        width: 397px;
        height: 130px;
        border-radius: 200px;
        position: absolute;
        top: 80%;
        left: -200%;
        opacity: .5;
        z-index: 4;
        -webkit-box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55); 
        box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55);
        &::after, 
        &::before{
            content:"";
            position:absolute;
            display:inline-block;
            background:inherit;
            border-radius:inherit;
            -webkit-box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55); 
            box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55);
        }
        &::after{
            width: 165px;
            height: 165px;
            top: -106px;
            left: 34px;
        }
        &::before{
            width: 128px;
            height: 128px;
            top: -76px;
            left: 176px;
        }
    }
    .cloud.six {
        background-color: #cecece;
        width: 150px;
        height: 70px;
        border-radius: 200px;
        position: absolute;
        top: 40%;
        left: -200%;
        opacity: .5;
        z-index: 5;
        -webkit-box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55); 
        box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55);
        &::after, 
        &::before{
            content:"";
            position:absolute;
            display:inline-block;
            background:inherit;
            border-radius:inherit;
            -webkit-box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55); 
            box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55);
        }
        &::after{
            width: 40px;
            height: 40px;
            top: -24px;
            left: 34px;
        }
        &::before{
            width: 69px;
            height: 69px;
            top: -44px;
            left: 63px;
        }
    }
    .cloud.seven {
        background-color: #cecece;
        width: 518px;
        height: 138px;
        border-radius: 200px;
        position: absolute;
        top: 50%;
        left: -200%;
        opacity: .5;
        z-index: 6;
        -webkit-box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55); 
        box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.55);
        &::after, 
        &::before{
            content:"";
            position:absolute;
            display:inline-block;
            background:inherit;
            border-radius:inherit;
            -webkit-box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55); 
            box-shadow: 11px -15px 15px -9px rgba(0,0,0,0.55);
        }
        &::after{
            width: 210px;
            height: 210px;
            top: -130px;
            left: 118px;
        }
        &::before{
            width: 180px;
            height: 180px;
            top: -76px;
            left: 296px;
        }
    }
    /* SNOW */
    .layer {
        position: absolute;
        width: 100%;
        height: 100%;
    }
    .layer.back{
        z-index: -2;
    }
    .layer.middle{
        z-index: -1;
    }
    .layer.front{
        z-index: 0;
    }
    /* FOG */ 
    .fogbank {
        -webkit-filter: blur(10px);
        -moz-filter: blur(10px);
        -o-filter: blur(10px);
        -ms-filter: blur(10px);
        filter: blur(5px);
    }
    .fogbank.back {
        z-index: -2;
        background-color: #fff;
        height: 50%;
        opacity: .3;
    }
    .fogbank.middle {
        background-color: #fff;
        z-index: -1;
        height: 45%;
        opacity: .2;
    }
    .fogbank.front {
        z-index: 0;
        background-color: #fff;
        height: 30%;
        opacity: .1;
    }
    /* THUNDERSTORM */
    .lightning {
        position: absolute;
        top: 0;
        width: 100%;
        height: 100%;
        z-index: 2;
        opacity: .5;
    }

}
</style>