<template>
    <Mainframe>
        <div class="settings-wrapper">
            <div class="settings-content">
            <Loader />
            <div class="title">
                <div class="title-content">
                    <div class="avatar">
                        <img src="../assets/avatar.jpg" alt="">
                    </div>
                    <div class="edit-icon">
                        <svg style="width: 15px" class="w-5 h-5" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20">
                        <path d="M13.586 3.586a2 2 0 112.828 2.828l-.793.793-2.828-2.828.793-.793zM11.379 5.793L3 14.172V17h2.828l8.38-8.379-2.83-2.828z"></path>
                    </svg>
                    </div>
                </div>
            </div>
            <table>
                <tr>
                    <td class="highlight">Full name:</td>
                    <td>
                        <input class="form-control non-editable" type="text" v-model="userInfo.fullname" readonly>
                    </td>
                </tr>
                <tr>
                    <td class="highlight">Email:</td>
                    <td>
                        <input class="form-control non-editable" type="text" v-model="userInfo.email" readonly>
                    </td>
                </tr>
                <tr>
                    <td class="highlight">Phone:</td>
                    <td>
                        <input class="form-control non-editable" type="text" v-model="userInfo.phone" readonly>
                    </td>
                </tr>
                <tr>
                    <td class="highlight">Username:</td>
                    <td>
                        <input class="form-control" type="text" v-model="userInfo.username">
                    </td>
                </tr>
                <tr>
                    <td class="highlight">Password:</td>
                    <td>
                        <div class="password form-control">
                            <input class="" type="password" v-model="userInfo.password">
                            <span class="visible" @click="toggleVisibility">show</span>
                        </div>
                    </td>
                </tr>
                <tr>
                    <td>
                        <button @click="updateUserInfo">Save</button>
                    </td>
                </tr>
            </table>
        </div>
        </div>
    </Mainframe>
</template>

<script>
import Mainframe from '@/components/MainFrame.vue'
import store from '../store'

export default {
    name: "settings",
    components: {
        Mainframe,
    },
    data(){
        return {
            userInfo:{
                email: this.$store.state.user.email,
                password: this.$store.state.user.pass,
                fullname: this.$store.state.user.name,
                username: this.$store.state.user.username,
                phone: this.$store.state.user.phone,
            }
        }
    },
    methods: {
        updateUserInfo(){
            store.dispatch('updateUsernamePassword', {
                'id': store.state.user.id,
                'username': this.userInfo.username,
                'password': this.userInfo.password,
            })
        },
        toggleVisibility(){
            let pass = document.querySelector('.password input');
            let span = document.querySelector('.password span');
            if(pass.type == 'password'){
                pass.type = 'text'
                span.textContent = 'hide'
            }
            else {
                pass.type = 'password'
                span.textContent = 'show'
            }
        }
    }
}
</script>


<style scoped>
.non-editable {
    opacity: .5;
}
.non-editable:hover {
    cursor: pointer;
}
button {
    border: none;
    background: #08248c;
    color: #fff;
    padding: 2px 15px;
    border-radius: 3px;
}
.form-control {
    width: 260px;
    border: .5px solid rgba(0,0,0,.1);
    border-radius: 5px;
}
.password {
    width: 260px;
    border: .5px solid rgba(0,0,0,.1);
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
}
.password input {
    border: none;
}
.password input:focus {
    border:none;
    outline: none;
}
.password span {
    width: 32px;
    color: #08248c;
}
.password .visible:hover {
    cursor: pointer;
}
.title {
    display: flex;
    justify-content: center;
    align-items: center;
}
.title-content {
    position: relative;
}
.edit-icon {
    position: absolute;
    background: #08248c;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    right: 3px;
    bottom: 3px;
}
.edit-icon svg {
    width: 10px;
    height: 10px;
    fill: #fff;
}
.avatar {
    width: 80px;
    height: 80px;
    border-radius: 50%;
}
.avatar img {
    width: 100%;
    height: 100%;
    border-radius: inherit;
    object-fit: cover;
}
.settings-wrapper {
    height: Calc(100vh - 80px);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
.settings-content {
    display: flex;
    flex-direction: column;
    padding: 40px 5px;
    height: 100%;
}
.title {
    margin-bottom: 40px;
    color: #08248c;
}
td {
    text-align: left;
    padding: 10px 20px;
}
.highlight {
    font-weight: 600 !important;
}
.edit {
    transition: 300ms ease-in-out;
}
.edit svg:hover {
    cursor: pointer;
    fill: #08248c;
    transform: scale(1.1);
}
</style>