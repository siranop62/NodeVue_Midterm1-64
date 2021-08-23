<template>
<div>
    <h1>แก้ไขข้อมูล</h1>
    <form v-on:submit.prevent = "editUser">
        <p>ชื่อ: <input type="text" v-model="user.name"></p>
        <p>ชื่อทางวิทยาศาสตร์: <input type="text" v-model="user.lastname"></p>
        <p>ชื่อวงศ์: <input type="text" v-model="user.email"></p>
        <p>วิธีการปลูก: <input type="text" v-model="user.password"></p>
        <p><button type="submit">แก้ไขข้อมูล</button></p>
    </form>
    <hr>
    <div>
        <p>ชื่อ: {{user.name}}</p>
        <p>ชื่อทางวิทยาศาสตร์: {{user.lastname}}</p>
        <p>ชื่อวงศ์: {{user.email}}</p>
        <p>วิธีการปลูก: {{user.password}}</p>
    </div>
</div>
</template>
<script>import UsersService from '@/services/UsersService'

export default {
    data(){
        return{
            user:{
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods:{
        async editUser(){
            try{
                await UsersService.put(this.user)
                this.$router.push({
                    name: 'users'
                })

            }catch(error){
                console.log(error)
            }
        }
    }, 
    async created(){
        try{
            let userId = this.$route.params.userId
            this.user = (await UsersService.show(userId)).data
        }catch(error){
            console.log(error)
        }
    }
}
</script>
<style scoped>


</style>