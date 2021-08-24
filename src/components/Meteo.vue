<template>

    <div class="container">
        <a href="Meteo.vue"><img class="main-icon" :src="require(`@/assets/main.icon.png`)" /></a>

        <div class="form-groupe mb-5">
                <label class="position" for="position">Météo</label>
                <input id="position" type="text" class="form-control" placeholder="Recherche un pays..." v-model="requete"
                @keypress.enter="goMeteo">
               
        </div>
    <form class="box">
        <div class="w-75 m-auto" v-if="temps">
            <br>
            
                <div class="box-meteo">
                        <h2 class="text-affichage mb-3">{{ temps.name }}, {{ temps.sys.country }}</h2>
                        <br>
                        <br>
                        <img class="temps-icon" :src="`${weather_icon}${temps.weather[0].icon}${'@2x.png'}`"/>
                        <p class="text-affichagee">{{ temps.main.temp.toFixed() }}°</p>                        
                        <p class="text-affichages">{{ temps.weather[0].description }}</p>
                        <p class="text-affichages">{{ temps.main.temp_max.toFixed() }}° / {{ temps.main.temp_min.toFixed() }}°</p>
                        <p class="text-affichages">Ressenti {{ temps.main.feels_like.toFixed() }}°</p>
                <br>
                        <img class="humiditeImage" :src="require(`@/assets/humidite.jpg`)" /><li class="humid1">Humidité</li>
                        <li class="humid">{{ temps.main.humidity }}%</li>
                        <hr>
                        <img class="ventImage" :src="require(`@/assets/vent.jpg`)" /><li class="vent1">Vent</li>
                        <li class="vent">{{ temps.wind.speed.toFixed() }} m/s(↗)</li>
                        <hr>
                        <img class="leverImage" :src="require(`@/assets/lever.png`)" /><li class="leverDuSoleil1">Lever du soleil</li>
                        <li class="leverDusoleil">{{  }}</li>
                        <br>
                        <hr>
                        <img class="coucherImage" :src="require(`@/assets/coucher.png`)" /><li class="coucherDuSoleil1">Coucher du soleil</li>
                        <li class="coucherDuSoleil">{{  }}</li>
                <br>
                        <span class="heure">{{$moment().format('DD MMM HH:mm a')}}</span>

            </div>
        </div>
    </form>
    </div>
</template>
<script>

import axios from 'axios'

export default {
    name: 'Meteo',
    data() {
        return {
            requete: '',
            temps : undefined,
            api_code: '64fd497dee93ada93782c987af391f9f',
            url_recherche: 'https://api.openweathermap.org/data/2.5/weather?',
            weather_icon: "http://openweathermap.org/img/wn/",
            oncall: "https://api.openweathermap.org/data/2.5/onecall?"
        }
    },
    methods: {
        goMeteo() {
                axios.get(`${this.url_recherche}q=${this.requete}&units=metric&APPID=${this.api_code}&lang=fr`).then(reponse => {
                     console.log(reponse);
                    this.temps = reponse.data;
                    // console.log(this.temps);
                })
            },
        mounted() {
            axios.get(`${this.oncall}lat=${this.requete}&lon=exclude&APPID=${this.api_code}&lang=fr`).then(repond => {
                console.log(repond);
                this.temps = repond.data;
            })
            }            
        }
    }

</script>
<style scoped>
@import './Meteo.css';
</style>