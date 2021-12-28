<template>
    <div class="container" v-if="weatherName != null">
        
    </div>
</template>

<script>
// import anime from 'animejs/lib/anime.es.js';
export default {
    name : 'Animation',
    props : {
        weatherName : Object
    },
    methods: {
        animation() {
            let weatherType = this.weatherName.weather[0].main;
            console.log(weatherType)
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
            // if (this.weatherName.weather[0].main == 'Clouds') {
            //     this.clouds();
            // }
        },
        clouds() {
            alert('clouds');
        },
        clear() {
            alert('clear');
        },
        thunderstorm() {
            alert('thunderstorm');
        },
        drizzle() {
            alert('drizzle');
        },
        rain() {
            alert('rain');
        },
        snow() {
            alert('snow');
        },
        mist() {
            alert('mist');
        },
        smoke() {
            alert('smoke');
        },
        haze() {
            alert('haze');
        },
        dust() {
            alert('dust');
        },
        fog() {
            alert('fog');
        },
        sand() {
            alert('sand');
        },
        ash() {
            alert('ash');
        },
        squall() {
            alert('squall');
        },
        tornado() {
            alert('tornado');
        }

    }
}
</script>

<style lang="scss" scoped>
.container {
    position: absolute;
    width: 100%;
    height: 100%;
    top:0;
    left: 0;
    z-index: -1;
    canvas{
        width: 100vw;
        height: 100vh;
}
    .square {
        width: 50px;
        height: 50px;
        background-color: blue;
    }
}
</style>