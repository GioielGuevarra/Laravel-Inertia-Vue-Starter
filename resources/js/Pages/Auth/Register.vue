<script setup>
import Container from "../../components/Container.vue";
import Title from "../../components/Title.vue";
import TextLink from "../../components/TextLink.vue";
import InputField from "../../components/InputField.vue";
import PrimaryBtn from "../../components/PrimaryBtn.vue";
import ErrorMessages from "../../components/ErrorMessages.vue";
import { useForm } from "@inertiajs/vue3";

const form = useForm({
    name: "",
    email: "",
    password: "",
    password_confirmation: "",
});

const submit = () => {
    form.post(route("register"), {
        onFinish: () => form.reset("password", "password_confirmation"),
    });
};
</script>

<template>
    <Head title="- Login" />
    <Container class="w-1/2">
        <div class="mb-8 text-center">
            <Title class="text-3xl font-bold mb-2"
                >Register a new account</Title
            >
            <p>
                Already have an account?
                <TextLink routeName="login" label="Login" />
            </p>
        </div>

        <!-- Error Messages -->
        <ErrorMessages :errors="form.errors"/>

        <form @submit.prevent="submit" class="space-y-6">
            <InputField label="Name" icon="user" v-model="form.name" />

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

            <InputField
                label="Confirm Password"
                type="password"
                icon="key"
                v-model="form.password_confirmation"
            />

            <p class="text-slate-500 text-sm dark:text-slate-400">
                By creating an account, you agree to our Terms of Services and
                Privacy Policy.
            </p>

            <PrimaryBtn :disabled="form.processing">Register</PrimaryBtn>
        </form>
    </Container>
</template>
