<template>
    <h2>(1) Vue의 ComboBox</h2>
    <div>
        <div id="content">
            <p class="title">ID</p><p>{{animal === '' ? '-' : animal.animalID}}</p>
            <p class="title">NAME</p><p>{{animal === '' ? '-' : animal.animalName}}</p>
        </div>
        <div id="searchBox">
                <select v-model="animal">
                        <option disabled value="">선택해주세요</option>
                        <option v-for="(item, index) in animals" :value="item" :key="index">
                            {{item.animalName}}
                        </option>
                </select>
        </div>  
    </div>
</template>

<script>
export default{
        props: ['animals'],
        data(){
                return{
                        animal: '',//선택된 동물
                };
        },
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
