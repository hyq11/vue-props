<template>
    <div>
        <Login :phone="phone" :pwd="pwd" @on-chang-phone="getValue"></Login>
        <p>{{phone}}</p>
        <p>{{pwd}}</p>
        <Login2 :phone="phone" v-model="pwd"></Login2>
        <Login3 :phone.sync="phone"></Login3>
    </div>
</template>

<script>
// 三种方式实现组件之间的双向数据绑定
import Login from './components/Login'
import Login2 from './components/Login2'
import Login3 from './components/Login3'

export default {
    data(){
        return {
            phone:'18256983812',
            pwd: '123456'
        }
    },
    methods:{
        getValue(value){
            this.phone = value
        }
    },
    components:{
        Login,
        Login2,
        Login3
    }
}
</script>

<style>

</style>
