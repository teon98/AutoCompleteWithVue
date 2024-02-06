<template>
        <div>
            <h1>Vue에서 AutoComplete 직접 구현하기</h1>
            <div id="child">
                <combo-box v-bind:animals = "animalList"></combo-box>
                <auto-complete v-bind:animals = "animalList"></auto-complete>
            </div>
        </div>
</template>

<script>
import ComboBox from './components/ComboBox.vue';
import AutoComplete from './components/AutoComplete.vue';
import axios from 'axios';
    
export default{
        data(){
                return{
                        animalList: [],
                };
        },
        components:{
                'combo-box': ComboBox,
                'auto-complete': AutoComplete,
        },
        mounted(){
            this.load();
        },
        methods:{
            load(){//load animal list
                    let _this = this;
                    axios.get('https://my-json-server.typicode.com/teon98/demo/animalList')
                    .then((res) => {
                            _this.animalList = res.data;
                    }).catch((err) => {
                            console.log(err)
                    });
            },
        }
}
        
</script>

<style scoped>
</style>
