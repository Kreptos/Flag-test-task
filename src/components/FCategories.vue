<template>
    <a href="#" class="category" :class="{ big: ifBigSize }" >
        <img :src="require(`../assets/img/img-${categories.id}.png`)" />
        <h3 class="category__title">{{categories.name}}</h3>
    </a>
</template>

<script>

export default {
    name: 'FBreadcumbs',
    components: {
    },
    props:{
        categories: Object,
    },
    computed: {
        ifBigSize(){
            return this.categories.size == 2
        }
    }
}
</script>

<style scoped>
.category{
    position: relative;
    height: 200px;
    overflow: hidden;
    cursor: pointer;
    width: 272px;
    margin-bottom: 40px;
    border-radius: 4px;
}
.category.big{
    width: 584px;
}
.category img{
    min-height: 100%;
    min-width: 100%;
    width: auto;
    height: auto;
    max-width: none;
    max-height: none;
    display: block;
    position: relative;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
.category::after{
    content: '';
    background: linear-gradient(180deg, rgba(112, 192, 91, 0) 0%, #70C05B 82.81%);
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    bottom: 0;
    height: 117px;
}
.category:hover::after{
    background: linear-gradient(180deg, rgba(255, 102, 51, 0) 0%, #FF6633 100%);
    z-index: 3;
    height: 177px;
}
.category__title{
    position: absolute;
    bottom: 0;
    color: #fff;
    font-weight: 700;
    font-size: 18px;
    line-height: 150%;
    z-index: 5;
    padding: 0 10px 10px;
}
@media(max-width: 1268px){
    .category, .category.big{
        width: 47%;
    }
    .category img{
        height: auto;
    }
}
@media(max-width: 500px){
    .category, .category.big{
        width: 100%;
        margin-bottom: 30px;
    }
}
</style>
