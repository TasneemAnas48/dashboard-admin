<template>
    <div class="login">
        <div class="side-left col-lg-4 d-none d-lg-block">
            <div class="image">
                <img src="../../assets/img/login.png" class="img-thumbnail img" />
            </div>
        </div>
        <div class="side-right col-lg-9 ">
            <div class="top-button">
                    <div class="button-add create button-login" >أهلا بعودتك، </div>
                    <div class="button-add create button-login" > الرجاء قم بإدخال بياناتك</div>
            </div>
            
            <v-app>
                <form class="form-input" style="margin-top: -35px;">

                    <div class="form-row" style="justify-content: center;margin-top: 100px">
                        <div class="my-input col-lg-12 row" style="margin-top: -12px">
                            <label for="email" class="col-lg-3 label-input">البريد الالكتروني</label>
                            <b-form-input class="col-lg-6 col-md-11 input-field" v-model.trim="email"
                                name="email" type="email" style="padding-left: 30px;"></b-form-input>
                            <v-tooltip color="error" right v-if="v$.email.$error">
                                <template v-slot:activator="{ on, attrs }">
                                    <v-icon color="red" dark v-bind="attrs" v-on="on">
                                        mdi-exclamation
                                    </v-icon>
                                </template>
                                <span>{{v$.email.$errors[0].$message}}</span>
                            </v-tooltip>
                            <v-tooltip color="error" right v-if="!valid_email">
                                <template v-slot:activator="{ on, attrs }">
                                    <v-icon color="red" dark v-bind="attrs" v-on="on">
                                        mdi-exclamation
                                    </v-icon>
                                </template>
                                <span> الايميل غير موجود </span>
                            </v-tooltip>
                            
                        </div>
                    </div> 


                    <div class="form-row" style="justify-content: center;">
                        <div class="my-input col-lg-12 row" style="margin-top: -12px">
                            <label for="password" class="col-lg-3 label-input">كلمة السر</label>
                            <b-form-input class="col-lg-6  col-md-11 input-field" v-model="password"
                                name="password" type="password"></b-form-input>
                            <v-tooltip color="error" right v-if="v$.password.$error">
                                <template v-slot:activator="{ on, attrs }">
                                    <v-icon color="red" dark v-bind="attrs" v-on="on">
                                        mdi-exclamation
                                    </v-icon>
                                </template>
                                <span>{{v$.password.$errors[0].$message}}</span>
                            </v-tooltip>
                            <v-tooltip color="error" right v-if="!validate_">
                                <template v-slot:activator="{ on, attrs }">
                                    <v-icon color="red" dark v-bind="attrs" v-on="on">
                                        mdi-exclamation
                                    </v-icon>
                                </template>
                                <span>كلمة السر غير صحيحة </span>
                            </v-tooltip>
                        </div>

                    </div> 

                    <div class="buttons form-row " style="margin-top:50px;justify-content: flex-end;margin-left: 40px;">
                        <b-button type="button" class="button-add" v-on:click="submitForm" style="margin-left: 55px;">
                            <font-awesome-icon icon="fas fa-arrow-left" class="icon-button-left" />تسجيل دخول
                        </b-button>
                    </div>
                </form>
            </v-app>
        </div>
    </div>
</template>


<script>
import useVuelidate from '@vuelidate/core'
import { required, helpers } from '@vuelidate/validators'

export default {
    name: "Login",
    setup () {
        return { v$: useVuelidate() }
    },
    data() {
        return {
            valid_email: true,
            email:'',
            password:'',
            validate_: true,

        };
    },
    validations () {
        return {
                
                email: {  required: helpers.withMessage('هذا الحقل مطلوب', required),},
                password: {  required: helpers.withMessage('هذا الحقل مطلوب', required), },
                
            }
    },

    methods: {
        validateEmail() {
            this.v$.$validate()
            // if (this.email != ''){
            //     this.axios.post("http://"+this.$store.state.ip+"api/settings/person/unique", {email : this.email})
            //     .then((res) =>{
            //         if (res.data.data != "error")
            //             this.valid_email = false
            //         else 
            //             {
            //                 this.valid_email = true
            //                 this.validateLogin()
            //             }
            //     })
            // }
        },
        validateLogin(){
            // this.axios.post("http://"+this.$store.state.ip+"api/settings/storeManager/login", {email : this.email, password : this.password})
            //     .then((res) =>{
            //         // console.log(res.data)
            //         if (res.data.message != "success")
            //             this.validate_ = false
            //         else 
            //             {
            //                 this.validate_ = true
            //                 this.addlocalStorage(res.data.store_id, res.data.manager_id)
            //                 this.submitForm()
            //             }
            //     })
        },
        submitForm(){
            this.v$.$validate()
            if (!this.v$.$error){
                this.$router.replace({ name: 'dashboard' })
            }
        },
        addlocalStorage(store, manager){
            // console.log(store)
            // console.log(manager)
            // localStorage.setItem("id_store", store);
            // localStorage.setItem("id_manager", manager);
            // this.$store.state.id_store = store
            // this.$store.state.id_manager = manager
        }
    },
};
</script>

<style lang="scss">
@import '@/assets/css/Login/Login.css';
</style>

