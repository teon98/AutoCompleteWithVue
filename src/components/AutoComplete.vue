<template>
    <h2>(2) Vue의 AutoComplete</h2>
    <div>
        <div id="content">
            <p class="title">ID</p><p>{{animal === '' ? '-' : animal.animalID}}</p>
            <p class="title">NAME</p><p>{{animal === '' ? '-' : animal.animalName}}</p>
        </div>
        <div id="autocompleteBox">
            <input type="text" placeholder="선택해주세요"
              @blur="handleListOpen(false)" @focus="handleListOpen(true)"/>
            <ul v-if="isListOpen">
                <li v-for="(item, index) in animals" @mousedown="setAnimal(item)">
                    {{item.animalName}}
                </li>
            </ul>
        </div>  
    </div>
</template>

<script>
export default{
    props: ['animals'],
    data(){
        return{
            animal: '',//선택된 동물
            searchAnimal: '',//검색할 동물 이름
            isListOpen: false, //리스트 열림/닫힘 여부
        }
    },
    methods:{
        handleListOpen(isopen){
          this.isListOpen = isopen;
        },
        setSearchAnimal(event){
          this.searchAnimal = event.target.value;  
        },
        setAnimal(itemObj){
            this.animal = itemObj;
        }
    }
};
</script>

<style scoped>
    #content{
        display: grid;
        grid-template-columns: 100px 200px;
    }
    .title{
        font-weight: bold;
    }
</style>