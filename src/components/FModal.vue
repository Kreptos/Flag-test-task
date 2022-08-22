<template>
    <div class="modal__wrapper" :class="{active: isActive}">
        <div class="modal" :style="{display: isModal}">
            <button class="modal__close" @click="$emit('closeModal')"></button>
            <form action="" class="modal__form" @submit.prevent='createProductItem'>
                <h2 class="modal__title">Регистрация</h2>
                <h3 class="modal__subtitle">Обязательные поля</h3>

                <div class="modal__fields">
                    <div class="modal__left-fields modal__block">
                        <label for="number">Телефон</label>
                        <input 
                            type="text" 
                            id="number" 
                            name="number" 
                            ref="number" 
                            @focus="numInput" 
                            v-model="phone">
                        
                        <label for="surname">Фамилия</label>
                        <input 
                            type="text" 
                            id="surname" 
                            name="surname"
                            v-model="surname">

                        <label for="name">Имя</label>
                        <input 
                            type="text" 
                            id="name" 
                            name="name"
                            v-model="name">
                        
                        <div class="password-wrapper">
                            <label for="password">Пароль</label>
                            <input 
                                type="password" 
                                id="password" 
                                name="password" 
                                ref="password"
                                v-model="password">
                            <i class="togglePassword" id="password" @click="togglePassword"></i>
                        </div>
                        <div class="password-wrapper">
                            <label for="confirm-password">Повторите пароль</label>
                            <input 
                                type="password" 
                                id="confirm-password" 
                                name="confirm-password" 
                                ref="confirm-password"
                                v-model="confirmPassword">
                            <i class="togglePassword" id="confirm-password" @click="togglePassword"></i>
                        </div>
                    </div>
                    <div class="modal__right-fields modal__block">
                        <label for="date">Дата рождения</label>
                        <input 
                            type="date" 
                            id="date" 
                            name="date"
                            v-model="date">

                        <div class="modal__city">
                            <label for="city">Населенный пункт</label>
                            <input 
                                type="text" 
                                id="city" 
                                name="city"
                                ref="city"
                                v-model="city"
                                @change="changeCity">
                            <i></i>
                        </div>
                        <label for="gender">Пол</label>
                        <div class="modal__gender">
                        <input
                            label="Мужской"
                            value="male"
                            type="radio"
                            v-model="gender">
                        <input
                            label="Женский"
                            value="female"
                            type="radio"
                            v-model="gender">
                        </div>
                    </div>
                </div>

                <h3 class="modal__subtitle">Необязательные поля</h3>

                <div class="modal__fields">
                    <div class="modal__block">
                        <label for="card">Номер карты</label>
                        <input 
                            type="text" 
                            id="card" 
                            name="card" 
                            @focus="numInput" 
                            v-model="card">

                        <div class="loyalty">
                            <input 
                                type="checkbox" 
                                id="loyalty" 
                                name="loyalty"
                                v-model="loyalty">
                            <label for="loyalty">У меня нет карты лояльности</label>
                        </div>
                    </div>
                    <div class="modal__block">
                        <label for="email">E-mail</label>
                        <input 
                            type="email" 
                            id="email" 
                            name="email"
                            v-model="email">
                    </div>
                </div>
                <div class="modal__btn"><button class="btn" :disabled="!requiredFields" @click="success">Продолжить</button></div>
            </form>
        </div>
        <div class="success" :style="{display: isSuccess}" @click="clearForm">
            <button class="modal__close" @click="$emit('closeModal')"></button>
            <div class="success__inner">
                <h1 class="success__title">Вы успешно зарегистрировались!</h1>
                <button class="success__btn btn">К покупкам</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'FModal',
    components: {
    },
    props:{
        links: Array,
        isActive: Boolean,
    },
    data(){
        return {
            surname: '',
            name: '',
            password: '',
            confirmPassword: '',
            date: '',
            city: '',
            gender: '',
            email: '',
            phone: '',
            card: '',
            phoneMask: "+7 (###) ### ####",
            cardMask: "##-######",
            keyCode: '',

            ifSurname: '',
            ifName: '',
            ifPassword: '',
            ifConfirmPassword: '',
            ifDate: '',
            ifCity: '',
            ifGender: '',
            ifPhone: '',

            requiredFields: false,

            isSuccess: 'none',
            isModal: 'block',
        }
    },
    mounted(){
        if(this.isActive == false){
            this.isSuccess = 'none'
            this.isModal = 'block'
        }
    },  
    watch:{
        'this.$refs.city.value': function(val){
            // console.log(this.$refs.city)
            // this.city = val
            console.log(val)
        },  
        'surname': function(val){
            val.length >= 3 ? this.ifSurname = true : this.ifSurname = false
            this.ifRequiredFields()
        },
        'name': function(val){
            val.length >= 3 ? this.ifName = true : this.ifName = false
            this.ifRequiredFields()
        },
        'password': function(val){
            if(val.length > 5 && val.match(/[0-9]/) != null && val.match(/[A-Z]/) != null && val.match(/[a-z]/) != null) this.ifPassword = true
            else this.ifPassword = false

            this.ifRequiredFields()
        },
        'confirmPassword': function(val){
            val == this.password ? this.ifConfirmPassword = true : this.ifConfirmPassword = false
            this.ifRequiredFields()
        },
        'date': function(val){
            val != '' ? this.ifDate = true : this.ifDate = false
            this.ifRequiredFields()
        },
        'phone': function(val){
            val.length == 17 ? this.ifPhone = true : this.ifPhone = false
            this.ifRequiredFields()
        },
        'city': function(val){
            val != '' ? this.ifCity = true : this.ifCity = false
            this.ifRequiredFields()
        },
        'gender': function(val){
            val != '' ? this.ifGender = true : this.ifGender = false
            this.ifRequiredFields()
        }
    }, 
    methods: {
        clearForm(){
            this.isSuccess = 'none'
            this.isModal = 'block'
            this.surname = ''
            this.name = ''
            this.password = ''
            this.confirmPassword = ''
            this.date = ''
            this.city = ''
            this.gender = ''
            this.email = ''
            this.phone = ''
            this.card = ''

            this.$emit('closeModal')
        },  
        success(){
            this.isModal = 'none'
            this.isSuccess = 'block'
        },  
        changeCity(event){
            this.city = event.target.value
        },  
        ifRequiredFields(){
            if(this.ifSurname && this.ifName && this.ifPassword && this.ifConfirmPassword && this.ifDate && this.ifPhone && this.ifCity && this.ifGender) this.requiredFields = true
            else this.requiredFields = false
        },
        togglePassword(e){
            let id = e.target.id
            let el = this.$refs[id]
            el.type == 'text' ? el.type = 'password' : el.type = 'text'
        },
        numInput(event){
            if(this.phone == '' && event.target.id == 'number')
                this.phone = '+7 '
            if(this.card == '' && event.target.id == 'card')
                this.card == ''
            event.target.addEventListener("input", this.mask, false);
            event.target.addEventListener("focus", this.mask, false);
            event.target.addEventListener("blur", this.mask, false);
            event.target.addEventListener("keydown", this.mask, false);
        },  
        mask(event) {
            event.keyCode && (this.keyCode = event.keyCode);
            let pos = this.selectionStart;
            if (pos < 3) event.preventDefault();

            let matrix, value = ''
            if(event.target.id == 'number'){
                matrix = this.phoneMask
                value = this.phone
            }
               
            if(event.target.id == 'card'){
                matrix = this.cardMask
                value = this.card
            }

            let i = 0,
                def = matrix.replace(/\D/g, ""),
                val = value.replace(/\D/g, ""),
                new_value = matrix.replace(/[#\d]/g, function(a) {
                    return i < val.length ? val.charAt(i++) || def.charAt(i) : a
                });
            i = new_value.indexOf("#");
            if (event.target.id == 'number' && i != -1) {
                i < 5 && (i = 3);
                new_value = new_value.slice(0, i)
            }
            if (event.target.id == 'card' && i != -1) {
                i < 3;
                new_value = new_value.slice(0, i)
            }
            let reg = matrix.substr(0, value.length).replace(/#+/g,
                function(a) {
                    return "\\d{1," + a.length + "}"
                }).replace(/[+()]/g, "\\$&");
            reg = new RegExp("^" + reg + "$");
            if (!reg.test(value) || value.length < 5 || this.keyCode > 47 && this.keyCode < 58) value = new_value;
            if (event.type == "blur" && value.length < 5)  value = ""

            if(event.target.id == 'number'){
                this.phone = value
            }
               
            if(event.target.id == 'card'){
                this.card = value
            }
        }
    }
}
</script>

<style scoped>
.modal__close{
    position: absolute;
    width: 40px;
    height: 40px;
    background: #F3F2F1;
    border-radius: 4px;
    right: 0;
    cursor: pointer;
}
.modal__close::before{
    content: '';
    width: 18px;
    height: 1px;
    border-radius: 1px;
    background: #414141;
    position: absolute;
    transform: rotate(45deg);
    left: 11px;
}
.modal__close::after{
    content: '';
    width: 18px;
    height: 1px;
    border-radius: 1px;
    background: #414141;
    position: absolute;
    transform: rotate(-45deg);
    left: 11px;
}
.modal__wrapper.active{
    display: block;
}
.modal__wrapper{
    display: none;
    width: 100vw;
    height: 100vh;
    background: rgba(252, 213, 186, 0.8);
    position: fixed;
    z-index: 10;
}
.modal{
    position: absolute;
    width: 687px;
    height: 926px;
    background: #fff;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    z-index: 10;
    border-radius: 4px;
}
.modal__form{
    padding: 72px 67.5px 40px;
}
.modal__title{
    font-size: 24px;
    font-weight: 700px;
    line-height: 150%;
    text-align: center;
    margin-bottom: 40px;
}
.modal__subtitle{
    font-size: 18px;
    font-weight: 700;
    line-height: 150%;
    text-align: center;
    margin-bottom: 24px;
}
.modal__fields{
    position: relative;
    display: flex;
    justify-content: space-between;
    margin-bottom: 40px;
}
.modal input{
    border: 1px solid #BFBFBF;
    border-radius: 4px;
    margin-bottom: 16px;
    position: relative;
    overflow: visible;
    width: 214px;
    height: 40px;
    padding: 0 30px 0 16px;
    font-weight: 400;
    font-size: 16px;
    line-height: 150%;
    outline: none;
    caret-color: #70C05B;
    font-family: 'Rubik';
    box-sizing: content-box!important;
}
.modal input:focus{
    box-shadow: 4px 8px 16px rgba(112, 192, 91, 0.2);
    outline: 1px solid #70C05B;
}
.modal .modal__gender{
    display: flex;
    background: #F3F2F1;
    border-radius: 4px;
    max-height: 40px;
    padding: 4px;
}
.modal .modal__gender input{
    -webkit-appearance: none;
	-moz-appearance: none;
	appearance: none;
    outline: none;
    cursor: pointer;
    border: none;
    height: 32px;
    margin-bottom: 0;
}
.modal .modal__gender input::before{
    content: attr(label);
    color: #414141;
    font-size: 12px;
    font-weight: 400;
    line-height: 150%;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}
.modal .modal__gender input:checked{
    background: #70C05B;
}
.modal .modal__gender input:checked::before{
    color: #fff;
}
.modal .password-wrapper{
    position: relative;
}
.modal .togglePassword{
    background-image: url('../assets/icons/eye-off.svg');
    width: 24px;
    height: 24px;
    position: absolute;
    top: 33px;
    right: 6px;
    cursor: pointer;
}
.modal .modal__city{
    position: relative;
}
.modal .modal__city i{
    background-image: url('../assets/icons/arrow-down.svg');
    width: 13px;
    height: 7px;
    position: absolute;
    top: 42px;
    right: 11px;
}
.modal #loyalty{
    width: 20px;
    height: 20px;
    outline: none;
    box-shadow: none;
    cursor: pointer;
    margin: 0;
    margin-right: 8px;
    vertical-align: middle;
}
.modal #loyalty:checked{
    background: #fff;
}
.modal .loyalty label{
    vertical-align: top;
}
.modal label{
    font-weight: 400;
    font-size: 16px;
    line-height: 150%;
    color: #8F8F8F;
}
.modal__block{
    display: flex;
    flex-direction: column;
    width: 260px;
}
.modal__btn{
    display: flex;
}
.btn{
    font-weight: 400;
    font-size: 24px;
    line-height: 150%;
    color: #FF6633;
    background: #FCD5BA;
    border-radius: 4px;
    width: 260px;
    height: 68px;
    margin: 0 auto;
    cursor: pointer;
}
.btn:hover{
    background: #ebc2a5;
}
.btn:active{
    background: #d8ae90;
}
.btn:disabled{
    background: #c2c2c2;
    color: #fff;
    cursor: default;
}

.success{
    position: absolute;
    width: 687px;
    height: 292px;
    background: #fff;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    z-index: 10;
    border-radius: 4px;
}

.success__inner{
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.success__title{
    font-weight: 700;
    font-size: 24px;
    line-height: 150%;
    text-align: center;
    color: #70C05B;
    width: 315px;
    align-self: center;
    margin-top: 72px;
}

.success__btn{
    margin-bottom: 40px;
}

@media(max-width: 1208px){
    .modal{
        height: 100%;
    }
    .modal__form{
        padding: 20px 67.5px;
    }
}

@media(max-width: 687px){
    .modal{
        width: 100%;
        overflow-y: scroll;

    }
    .modal__fields{
        flex-direction: column;
    }
    .modal__block{
        width: 100%;
    }
    .modal input{
        width: 90%;
    }
    .success{
        width: 100%;
    }
}

@media(max-width: 687px){
    .modal__form{
        padding: 20px 30px;
    }
}
</style>
