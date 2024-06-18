<script setup>
import Submit from "./Form/Submit.vue";
import Input from "./Form/Input.vue";
import Requirement from "./Form/Requirement.vue";
</script>

<template>
    <form action="index.html" class="bg-green-900 p-4 rounded-2xl border-2 border-black">
        <h1 class="mb-5 text-4xl text-center"><b>Create Account</b></h1>
        <div class="flex gap-5 flex-col mb-5">
            <div class="flex gap-5">
                <Input name="Username" type="text" @input="validateForm" v-model:value="value.username">
                <Requirement v-if="value.username.length" v-for="requirement in requirements.username"
                    :text="requirement.text" :status="requirement.filter"></Requirement>
                </Input>
                <Input name="Email" type="text" @input="validateForm" v-model:value="value.email">
                <Requirement v-if="value.email.length" v-for="requirement in requirements.email"
                    :text="requirement.text" :status="requirement.filter"></Requirement>
                </Input>
            </div>
            <div class="flex gap-5">
                <Input name="Password" type="password" @input="validateForm" v-model:value="value.password">
                <Requirement v-if="value.password.length" v-for="requirement in requirements.password"
                    :text="requirement.text" :status="requirement.filter"></Requirement>
                </Input>
                <Input name="Verify Password" type="password" @input="validateForm"
                    v-model:value="value.verifyPassword">
                <Requirement v-if="value.verifyPassword.length" v-for="requirement in requirements.verifyPassword"
                    :text="requirement.text" :status="requirement.filter"></Requirement>
                </Input>
            </div>
        </div>
        <Submit class="m-auto w-1/4 flex justify-center" :disabled="checkRequirement"></Submit>
    </form>
</template>

<script>
export default {
    data() {
        return {
            value: {
                password: new String,
                verifyPassword: new String,
                username: new String,
                email: new String,
            },

            status: [null]
        }
    },

    computed: {
        requirements() {
            return {
                password: [
                    {
                        text: "Be atleast 5 characters",
                        filter: this.value.password.length >= 5
                            ? true : false
                    },
                    {
                        text: "Include a capital letter",
                        filter: /[A-Z]/.test(this.value.password)
                            ? true : false
                    },
                    {
                        text: "Include a special character",
                        filter: /[`!@#$%^&*()_+\-=\[\]{};':"\\|,.<>\/?~]/.test(
                            this.value.password
                        )
                            ? true : false
                    },
                    {
                        text: "Cannot contain spaces",
                        filter: !/\s/.test(
                            this.value.password
                        )
                            ? true : false
                    }
                ],

                username: [
                    {
                        text: "No special characters",
                        filter: !/[ `!@#$%^&*()_+\-=\[\]{};':"\\|,.<>\/?~]/.test(
                            this.value.username
                        )
                            ? true : false
                    },
                    {
                        text: "Cannot be empty",
                        filter: this.value.username.length
                            ? true : false
                    }
                ],

                email: [
                    {
                        text: "Must be a valid email",
                        filter: /^\S+@\S+\.\S+$/.test(this.value.email)
                            ? true : false
                    }
                ],

                verifyPassword: [
                    {
                        text: "Passwords must match",
                        filter: this.value.password == this.value.verifyPassword
                            ? true : false
                    }
                ],
            }
        },

        checkRequirement() {
            return this.status.map(e => e).every(i => i) ? false
                : true
        },
    },

    methods: {
        validateForm() {
            this.status = []
            Object.values(this.requirements).forEach(e => e.map(i => this.status.push(i.filter)))
        }
    }
}
</script>