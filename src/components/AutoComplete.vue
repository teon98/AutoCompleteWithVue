<template>
    <h2>(2) Vue의 AutoComplete</h2>
    <div>
        <div id="content">
            <p class="title">ID</p><p>{{animal === '' ? '-' : animal.animalID}}</p>
            <p class="title">NAME</p><p>{{animal === '' ? '-' : animal.animalName}}</p>
        </div>
        <div id="autocompleteBox">
            <input type="text" placeholder="선택해주세요"
              :value="searchAnimal" @input="setSearchAnimal"
              @blur="handleListOpen(false)" @focus="handleListOpen(true)"/>
            <img :class="['caret', isListOpen ? 'openCaret' : 'closeCaret']" src="../components/icons/caret-down-solid.svg" alt="caretImg" />
            <img :class="['xmark', searchAnimal == '' ? 'xmarkhide' : 'xmarkshow']" src="../components/icons/circle-xmark-solid.svg"
              @click="handleRemove"/>
            <ul v-if="isListOpen">
                <li v-if="filterAnimals.length == 0">검색결과가 없습니다</li>
                <li v-for="(item, index) in filterAnimals" @mousedown="setAnimal(item)">
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
          if(event.target.value == ''){
            this.animal = '';
          }
          this.searchAnimal = event.target.value;  
        },
        setAnimal(itemObj){
            this.animal = itemObj;
            this.searchAnimal = itemObj.animalName;
        },
        handleRemove(){
          this.animal = '';
          this.searchAnimal = '';
        }
    },
    computed:{
      filterAnimals(){
        if(this.searchAnimal == ''){
          return this.animals;
        }
        return this.animals.filter(animal => {
          if(animal.animalName.includes(this.searchAnimal)){
            return animal;
          }
        })
      }
    }
};
</script>

<style scoped>
    #content{ display: grid; grid-template-columns: 100px 200px; }
    .title{ font-weight: bold; }
    #autocompleteBox{ display:inline-block; position: relative; }
    #autocompleteBox > ul{ position: absolute; list-style: none;
      padding-left:0px; width: 100%; max-height: 194px;
      border: 1px solid black; overflow: scroll; overflow-x: hidden;
      border-radius: 5px; }
  
    #autocompleteBox > ul::-webkit-scrollbar{ width: 6px;}
    #autocompleteBox > ul::-webkit-scrollbar-thumb{ background: #BED1CF; border-radius: 3px; }
    #autocompleteBox > ul::-webkit-scrollbar-track{background: #FFE4C9}
  
    #autocompleteBox > ul > li{ padding: 0px 5px; }
    #autocompleteBox > ul > li:hover{ background-color: #E78895; color: #FFF7F1;}
    #autocompleteBox > input{ padding-right: 44px; }
    .caret{ width: 10px; position: absolute; top: 50%; right: 8px;
      transition: 0.2s ease; pointer-events: none; }
    .closeCaret{ transform: translateY(-50%) rotate(0deg); }
    .openCaret{ transform: translateY(-40%) rotate(180deg);}
    .xmark{ position: absolute; top: 50%; cursor:pointer; z-index:1;
      width: 12px; transition: 0.3s ease; transform: translateY(-40%);}
    .xmarkhide{ visibility:hidden; right: 8px; opacity: 0; }
    .xmarkshow{ visibility:show; right: 28px; opacity: 1;}
</style>