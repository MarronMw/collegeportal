<script setup lang="ts">
import { Form, Head } from '@inertiajs/vue3';
import InputError from '@/components/InputError.vue';
import PasswordInput from '@/components/PasswordInput.vue';
import TextLink from '@/components/TextLink.vue';
import { Button } from '@/components/ui/button';
import { Checkbox } from '@/components/ui/checkbox';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';
import { Spinner } from '@/components/ui/spinner';
import { register } from '@/routes';
import { store } from '@/routes/login';
import { request } from '@/routes/password';

defineOptions({
    layout: {
        title: 'Log in to your account',
        description: 'Enter your email and password below to log in',
    },
});

defineProps<{
    status?: string;
    canResetPassword: boolean;
    canRegister: boolean;
}>();
</script>

<template>
    <Head title="Log in" />

    <!-- Fixed full‑screen overlay – ignores any parent layout constraints -->
    <div class="fixed inset-0 flex items-center justify-center overflow-auto bg-linear-to-br from-indigo-50 via-white to-sky-50 p-4 sm:p-6 dark:from-gray-950 dark:via-gray-900 dark:to-indigo-950/30">
        <!-- Responsive card – never overflows -->
        <div class="flex w-full max-w-5xl flex-col overflow-hidden rounded-2xl bg-white shadow-xl dark:bg-gray-900/90 md:flex-row">
            <!-- Left column: illustration & branding -->
            <div class="relative flex flex-col items-center justify-center bg-linear-to-br from-indigo-600 to-sky-500 p-6 text-center md:w-5/12 md:p-8">
                <div class="absolute -top-16 -left-16 h-48 w-48 rounded-full bg-white/10 blur-2xl"></div>
                <div class="absolute -bottom-16 -right-16 h-48 w-48 rounded-full bg-white/10 blur-2xl"></div>

                <div class="animate-float mb-6">
                    <svg class="h-20 w-20 text-white drop-shadow-md sm:h-24 sm:w-24" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M50 15 L10 40 L50 65 L90 40 L50 15Z" fill="currentColor" fill-opacity="0.9" stroke="white" stroke-width="2" stroke-linejoin="round"/>
                        <rect x="45" y="40" width="10" height="30" fill="currentColor" fill-opacity="0.7" />
                        <path d="M55 70 L65 75 L60 80 L50 75 Z" fill="currentColor" fill-opacity="0.6" />
                        <path d="M50 65 L50 85" stroke="white" stroke-width="2" stroke-linecap="round" stroke-dasharray="4 4" class="animate-pulse" />
                        <circle cx="50" cy="88" r="4" fill="white" class="animate-bounce" />
                    </svg>
                </div>

                <h2 class="text-2xl font-bold text-white sm:text-3xl">College Central</h2>
                <p class="mt-2 text-indigo-100">Your gateway to academic success</p>

                <div class="mt-6 space-y-3 text-left text-sm text-white/90">
                    <div class="flex items-center gap-2 opacity-0 animate-fadeInUp" style="animation-delay: 0.1s; animation-fill-mode: forwards;">
                        <svg class="h-5 w-5 shrink-0" fill="currentColor" viewBox="0 0 20 20">
                            <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/>
                        </svg>
                        <span>Real‑time grades & attendance</span>
                    </div>
                    <div class="flex items-center gap-2 opacity-0 animate-fadeInUp" style="animation-delay: 0.3s; animation-fill-mode: forwards;">
                        <svg class="h-5 w-5 shrink-0" fill="currentColor" viewBox="0 0 20 20">
                            <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/>
                        </svg>
                        <span>Easy course registration</span>
                    </div>
                    <div class="flex items-center gap-2 opacity-0 animate-fadeInUp" style="animation-delay: 0.5s; animation-fill-mode: forwards;">
                        <svg class="h-5 w-5 shrink-0" fill="currentColor" viewBox="0 0 20 20">
                            <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/>
                        </svg>
                        <span>Campus events & clubs</span>
                    </div>
                </div>
            </div>

            <!-- Right column: login form -->
            <div class="flex items-center p-6 sm:p-8 md:w-7/12 lg:p-10">
                <div class="w-full">
                    <div class="mb-6 text-center md:text-left">
                        <h3 class="text-xl font-semibold text-gray-800 dark:text-white">Welcome back</h3>
                        <p class="mt-1 text-sm text-gray-500 dark:text-gray-400">Sign in to your account</p>
                    </div>

                    <div
                        v-if="status"
                        class="mb-4 rounded-lg bg-green-50 p-3 text-center text-sm font-medium text-green-700 dark:bg-green-950/40 dark:text-green-400"
                    >
                        {{ status }}
                    </div>

                    <Form
                        v-bind="store.form()"
                        :reset-on-success="['password']"
                        v-slot="{ errors, processing }"
                        class="flex flex-col gap-5"
                    >
                        <div class="grid gap-4">
                            <div class="grid gap-1.5">
                                <Label for="email" class="text-sm font-medium text-gray-700 dark:text-gray-300">Email address</Label>
                                <Input
                                    id="email"
                                    type="email"
                                    name="email"
                                    required
                                    autofocus
                                    :tabindex="1"
                                    autocomplete="email"
                                    placeholder="student@college.edu"
                                    class="rounded-lg border-gray-300 bg-white/70 focus:border-indigo-500 focus:ring-indigo-500 dark:border-gray-700 dark:bg-gray-800/70"
                                />
                                <InputError :message="errors.email" />
                            </div>

                            <div class="grid gap-1.5">
                                <div class="flex items-center justify-between">
                                    <Label for="password" class="text-sm font-medium text-gray-700 dark:text-gray-300">Password</Label>
                                    <TextLink
                                        v-if="canResetPassword"
                                        :href="request()"
                                        class="text-sm text-indigo-600 hover:text-indigo-800 dark:text-indigo-400 dark:hover:text-indigo-300"
                                        :tabindex="5"
                                    >
                                        Forgot password?
                                    </TextLink>
                                </div>
                                <PasswordInput
                                    id="password"
                                    name="password"
                                    required
                                    :tabindex="2"
                                    autocomplete="current-password"
                                    placeholder="Enter your password"
                                    class="rounded-lg border-gray-300 bg-white/70 focus:border-indigo-500 focus:ring-indigo-500 dark:border-gray-700 dark:bg-gray-800/70"
                                />
                                <InputError :message="errors.password" />
                            </div>

                            <div class="flex items-center justify-between">
                                <Label for="remember" class="flex cursor-pointer items-center space-x-2 text-sm text-gray-700 dark:text-gray-300">
                                    <Checkbox id="remember" name="remember" :tabindex="3" class="rounded border-gray-300 text-indigo-600 focus:ring-indigo-500 dark:border-gray-600" />
                                    <span>Remember me</span>
                                </Label>
                            </div>

                            <Button
                                type="submit"
                                class="mt-2 w-full rounded-lg bg-indigo-600 py-2.5 font-semibold text-white shadow-md transition-all hover:bg-indigo-700 focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 disabled:opacity-70 dark:bg-indigo-500 dark:hover:bg-indigo-600"
                                :tabindex="4"
                                :disabled="processing"
                                data-test="login-button"
                            >
                                <Spinner v-if="processing" class="mr-2 h-4 w-4 animate-spin" />
                                Log in
                            </Button>
                        </div>

                        <div
                            class="text-center text-sm text-gray-600 dark:text-gray-400"
                            v-if="canRegister"
                        >
                            Don't have an account?
                            <TextLink :href="register()" :tabindex="5" class="font-medium text-indigo-600 hover:text-indigo-800 dark:text-indigo-400 dark:hover:text-indigo-300">
                                Sign up
                            </TextLink>
                        </div>
                    </Form>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
@keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-8px); }
}
.animate-float {
    animation: float 4s ease-in-out infinite;
}
@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(15px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}
.animate-fadeInUp {
    animation-name: fadeInUp;
    animation-duration: 0.5s;
    animation-timing-function: ease-out;
    animation-fill-mode: forwards;
}
</style>