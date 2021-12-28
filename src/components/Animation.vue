<template>
    <div class="container" v-if="weatherName.cod != 404 && weatherName.cod != undefined">
    </div>
</template>

<script>
import anime from 'animejs/lib/anime.es.js';
export default {
    name : 'Animation',
    props : {
        weatherName : Object
    },
    data() {
    },
    methods: {
        resetAnimation() {
            let container = document.querySelector('.container')
            container.innerHTML = '';
        },
        clouds() {
            this.resetAnimation();
            let container = document.querySelector('.container')
            let cloud = document.createElement("Div");
            cloud.className = "cloud";
            container.appendChild(cloud);
            let cloud2 = document.createElement("Div");
            cloud2.className = "cloud-2";
            container.appendChild(cloud2);
            let cloud3 = document.createElement("Div");
            cloud3.className = "cloud-3";
            container.appendChild(cloud3);
            anime({
                targets : '.cloud',
                left : '105%',
                duration : 6000,
                loop : true,
                easing : 'linear',
                direction : 'normal'
            });
            anime({
                targets : '.cloud-2',
                left : '105%',
                duration : 10000,
                loop : true,
                easing : 'linear',
                direction : 'normal'
            });
            anime({
                targets : '.cloud-3',
                left : '105%',
                duration : 18000,
                loop : true,
                easing : 'linear',
                direction : 'normal'
            });
        },
        clear() {
            this.resetAnimation();
            alert('clear');
        },
        thunderstorm() {
            this.resetAnimation();
            alert('thunderstorm');
        },
        drizzle() {
            this.resetAnimation();
            alert('drizzle');
        },
        rain() {
            this.resetAnimation();
            alert('rain');
        },
        snow() {
            this.resetAnimation();
            alert('snow');
        },
        mist() {
            this.resetAnimation();
            alert('mist');
        },
        smoke() {
            this.resetAnimation();
            alert('smoke');
        },
        haze() {
            this.resetAnimation();
            alert('haze');
        },
        dust() {
            this.resetAnimation();
            alert('dust');
        },
        fog() {
            this.resetAnimation();
            alert('fog');
        },
        sand() {
            this.resetAnimation();
            alert('sand');
        },
        ash() {
            this.resetAnimation();
            alert('ash');
        },
        squall() {
            this.resetAnimation();
            alert('squall');
        },
        tornado() {
            this.resetAnimation();
            alert('tornado');
        }

    },
    updated() {
            let weatherType = this.weatherName.weather[0].main;
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
                    this.drizzle();
                    break;
                case 'Rain' :
                    this.rain();
                    break;
                case 'Snow' :
                    this.snow();
                    break;
                case 'Mist' :
                    this.mist();
                    break;
                case 'Smoke' :
                    this.smoke();
                    break;
                case 'Haze' :
                    this.haze();
                    break;
                case 'Dust' :
                    this.dust();
                    break;
                case 'Fog' :
                    this.fog();
                    break;
                case 'Sand' :
                    this.sand();
                    break;
                case 'Ash' :
                    this.ash();
                    break;
                case 'Squall' :
                    this.squall();
                    break;
                case 'Tornado' :
                    this.tornado();
                    break;
                default: 
                    console.log('Okay')
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
    overflow-x: hidden;
    /* CLOUDS */ 
    .cloud {
        background-color: #d8d8d8;
        width: 150px;
        height: 50px;
        border-radius: 100px;
        position: absolute;
        top: 20%;
        left: -105%;
        opacity: .5;
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
    .cloud-2 {
        background-color: #e2e2e2;
        width: 259px;
        height: 69px;
        border-radius: 100px;
        position: absolute;
        top: 15%;
        left: -105%;
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
    .cloud-3 {
        background-color: #c9c9c9;
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
}
</style>