<template>
    <div class="breadcrumbs">
        <a href="#" class="link">Главная</a>
        <img src="../assets/icons/arrow-right.svg">
        <a href="/" class="link active">Каталог</a>
    </div>
</template>

<script>

export default {
    name: 'FBreadcumbs',
    components: {
    },
    props:{
        links: Array,
    }
}
</script>

<style scoped>
.breadcrumbs{ 
    max-width: 1208px;
    margin: 27px auto;
    text-align: left;
    display: flex;
}
.link{
    margin-right: 25px;
    text-decoration: none;
    color: #414141;
    font-weight: 400;
    font-size: 12px;
    line-height: 150%;
}
.link.active{
    color: #8F8F8F;
    margin-right: 0;
    margin-left: 25px;
}
.breadcrumbs img{
    width: 7px;
}
@media(max-width: 1268px){
  .breadcrumbs{
    padding: 0 30px;
  }
}
</style>
