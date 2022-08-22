<template>
  <FModal :isActive="isModalActive" @closeModal="isModalActive = false"/>
  <FHeader @openModal="isModalActive = true"/>
  <FBreadcrumbs/>
  <div class="wrapper">
    <h1 class="catalog">Каталог</h1>
    <div class="categories">
      <FCategories 
        v-for="(item, index) in categories" 
        :key="item.id"
        :categories='categories[index]'/>
    </div>
  </div>
</template>

<script>
import FHeader from './components/FHeader.vue'
import FBreadcrumbs from './components/FBreadcrumbs.vue';
import FCategories from './components/FCategories.vue';
import FModal from './components/FModal.vue';

export default {
  name: 'App',
  components: {
    FHeader,
    FBreadcrumbs,
    FCategories,
    FModal,
},
  data(){
    return{
      isModalActive: false,
      categories:[
        {
          name: 'Молоко, сыр, яйцо',
          size: 2,
          id: 1,
        },
        {
          name: 'Хлеб',
          size: 1,
          id: 2,
        },
        {
          name: 'Фрукты и овощи',
          size: 1,
          id: 3,
        },
        {
          name: 'Бакалея',
          size: 1,
          id: 4,
        },
        {
          name: 'Здоровое питание',
          size: 1,
          id: 5,
        },
        {
          name: 'Зоотовары',
          size: 2,
          id: 6,
        },
        {
          name: 'Детское питание',
          size: 1,
          id: 7,
        },
        {
          name: 'Мясо, птицы, колбасы',
          size: 2,
          id: 8,
        },
        {
          name: 'Непродовольственные товары',
          size: 1,
          id: 9,
        }
      ],
    }
  },
}
</script>

<style>
body{
  background: #E5E5E5;
}

#app {
  font-family: 'Rubik', sans-serif;
  color: #414141;
}

.wrapper{
  max-width: 1208px;
  margin: 0 auto;
}

.catalog{
  font-weight: 700;
  font-size: 64px;
  line-height: 150%;
  text-align: left;
  margin-bottom: 60px;
}

.categories{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
@media(max-width: 1268px){
  .wrapper{
    padding: 0 30px;
  }
}
@media(max-width: 500px){
  .catalog{
    margin-bottom: 30px;
  }
}



/* rubik-regular - cyrillic */
@font-face {
  font-family: 'Rubik';
  font-style: normal;
  font-weight: 400;
  src: url('./fonts/rubik-v21-cyrillic-regular.eot'); /* IE9 Compat Modes */
  src: local(''),
       url('./fonts/rubik-v21-cyrillic-regular.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('./fonts/rubik-v21-cyrillic-regular.woff2') format('woff2'), /* Super Modern Browsers */
       url('./fonts/rubik-v21-cyrillic-regular.woff') format('woff'), /* Modern Browsers */
       url('./fonts/rubik-v21-cyrillic-regular.ttf') format('truetype'), /* Safari, Android, iOS */
       url('./fonts/rubik-v21-cyrillic-regular.svg#Rubik') format('svg'); /* Legacy iOS */
}
/* rubik-600 - cyrillic */
@font-face {
  font-family: 'Rubik';
  font-style: normal;
  font-weight: 600;
  src: url('./fonts/rubik-v21-cyrillic-600.eot'); /* IE9 Compat Modes */
  src: local(''),
       url('./fonts/rubik-v21-cyrillic-600.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('./fonts/rubik-v21-cyrillic-600.woff2') format('woff2'), /* Super Modern Browsers */
       url('./fonts/rubik-v21-cyrillic-600.woff') format('woff'), /* Modern Browsers */
       url('./fonts/rubik-v21-cyrillic-600.ttf') format('truetype'), /* Safari, Android, iOS */
       url('./fonts/rubik-v21-cyrillic-600.svg#Rubik') format('svg'); /* Legacy iOS */
}
/* rubik-700 - cyrillic */
@font-face {
  font-family: 'Rubik';
  font-style: normal;
  font-weight: 700;
  src: url('./fonts/rubik-v21-cyrillic-700.eot'); /* IE9 Compat Modes */
  src: local(''),
       url('./fonts/rubik-v21-cyrillic-700.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('./fonts/rubik-v21-cyrillic-700.woff2') format('woff2'), /* Super Modern Browsers */
       url('./fonts/rubik-v21-cyrillic-700.woff') format('woff'), /* Modern Browsers */
       url('./fonts/rubik-v21-cyrillic-700.ttf') format('truetype'), /* Safari, Android, iOS */
       url('./fonts/rubik-v21-cyrillic-700.svg#Rubik') format('svg'); /* Legacy iOS */
}
</style>
