<template>
    <div>
        <div class="container mx-auto">
            <div class="flex justify-center px-6 my-12">
                <div class="w-full xl:w-3/4 lg:w-11/12 flex">
                    <div class="w-full h-auto bg-gray-400 hidden lg:block lg:w-1/2 bg-cover rounded-l-lg"
                        style="background-image: url('https://source.unsplash.com/YuJokOHODF0/')"></div>
                    <div class="w-full lg:w-1/2 bg-slate-100 p-5 rounded-lg lg:rounded-l-none">
                        <div class="px-8 mb-4 text-center">
                            <h3 class="pt-4 mb-2 text-2xl">Forgot Your Password?</h3>
                            <p class="mb-4 text-sm text-gray-700">
                                We get it, stuff happens. Just enter your email address below and we'll send you a
                                link to reset your password!
                            </p>
                        </div>
                        <div class="flex flex-col px-8 pt-6 pb-8 mb-4  rounded">
                            <label class="block mb-2 text-sm font-bold text-gray-700" for="email">
                                Email
                            </label>
                            <input
                                class="mb-4 w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded shadow appearance-none focus:outline-none focus:shadow-outline"
                                type="email" placeholder="Enter Email Address..." v-model="userEmail" />


                            <button
                                class="self-center w-[200px] h-[50px] px-4 mb-3 py-2 font-bold text-white bg-red-500 rounded-full hover:bg-red-700  hover:scale-105 hover:shadow-md active:bg-red-500 active:scale-100"
                                type="submit" @click="sendResetLink()">Submit</button>
                            <hr class="mb-6 border-t" />
                            <div class="text-center">
                                <router-link
                                    class="inline-block text-sm text-blue-500 align-baseline hover:text-blue-800"
                                    to="/register">
                                    Create an Account!
                                </router-link>
                            </div>
                            <div class="text-center">
                                <router-link
                                    class="inline-block text-sm text-blue-500 align-baseline hover:text-blue-800"
                                    to="/login">
                                    Already have an account? Login!
                                </router-link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';
import { sendPasswordResetEmail } from '@firebase/auth';
import { auth } from '@/firebase'
export default {

    setup() {
        const userEmail = ref()
        console.log(userEmail.value);


        const sendResetLink = async () => {

            await sendPasswordResetEmail(auth, userEmail.value).then(
                alert('Reset email send successfully ')
            )
            userEmail.value = ''
        }
        return { sendResetLink, userEmail }
    }
}


</script>

<style lang="scss" scoped>
</style>