<script setup>
import Container from "../../components/Container.vue";
import Title from "../../components/Title.vue";
import TextLink from "../../components/TextLink.vue";
import InputField from "../../components/InputField.vue";
import PrimaryBtn from "../../components/PrimaryBtn.vue";
import ErrorMessages from "../../components/ErrorMessages.vue";
import Checkbox from "../../components/Checkbox.vue";
import { useForm } from "@inertiajs/vue3";

const form = useForm({
    email: "",
    password: "",
    remember: null,
});

const submit = () => {
    form.post(route("login"), {
        onFinish: () => form.reset("password"),
    });
};
</script>

<template>
    <Head title="- Login" />
    <Container class="w-1/2">
        <div class="mb-8 text-center">
            <Title class="text-3xl font-bold mb-2">Login to your account</Title>
            <p>
                Need an account?
                <TextLink routeName="register" label="Register" />
            </p>
        </div>

        <!-- Error Messages -->
        <ErrorMessages :errors="form.errors"/>

        <form @submit.prevent="submit" class="space-y-6">
            
            <InputField
                label="Email"
                type="email"
                icon="at"
                v-model="form.email"
            />

            <InputField
                label="Password"
                type="password"
                icon="key"
                v-model="form.password"
            />

            <div class="flex items-center justify-between">
                <Checkbox name="remember" v-model="form.remember">
                    Remember me
                </Checkbox>

                <TextLink routeName="home" label="Forgot Password?" />
            </div>

            <PrimaryBtn :disabled="form.processing">Login</PrimaryBtn>
        </form>
    </Container>
</template>
