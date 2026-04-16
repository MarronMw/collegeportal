<script setup lang="ts">
import { Head, Link } from '@inertiajs/vue3';
import { dashboard, login, register } from '@/routes';

withDefaults(
    defineProps<{
        canRegister: boolean;
    }>(),
    {
        canRegister: true,
    },
);
</script>

<template>
    <Head title="College Portal | Your Academic Hub">
        <link rel="preconnect" href="https://rsms.me/" />
        <link rel="stylesheet" href="https://rsms.me/inter/inter.css" />
    </Head>
    <div
        class="flex min-h-screen flex-col items-center bg-gradient-to-b from-sky-50 via-white to-indigo-50 p-6 text-[#1b1b18] lg:justify-center lg:p-8 dark:from-gray-950 dark:via-gray-900 dark:to-indigo-950/40"
    >
        <header
            class="mb-8 w-full max-w-[335px] text-sm not-has-[nav]:hidden lg:max-w-5xl"
        >
            <nav class="flex items-center justify-end gap-4">
                <Link
                    v-if="$page.props.auth.user"
                    :href="dashboard()"
                    class="inline-block rounded-full border border-indigo-200 bg-white/70 px-5 py-1.5 text-sm font-medium leading-normal text-indigo-700 shadow-sm backdrop-blur-sm transition-all hover:border-indigo-300 hover:bg-indigo-50 dark:border-gray-700 dark:bg-gray-800/70 dark:text-indigo-300 dark:hover:border-indigo-600 dark:hover:bg-indigo-950/40"
                >
                    Dashboard
                </Link>
                <template v-else>
                    <Link
                        :href="login()"
                        class="inline-block rounded-full px-5 py-1.5 text-sm font-medium leading-normal text-gray-700 transition-all hover:bg-gray-100 dark:text-gray-300 dark:hover:bg-gray-800"
                    >
                        Log in
                    </Link>
                    <Link
                        v-if="canRegister"
                        :href="register()"
                        class="inline-block rounded-full bg-indigo-600 px-5 py-1.5 text-sm font-medium leading-normal text-white shadow-md transition-all hover:bg-indigo-700 dark:bg-indigo-500 dark:hover:bg-indigo-600"
                    >
                        Register
                    </Link>
                </template>
            </nav>
        </header>
        <div
            class="flex w-full items-center justify-center opacity-100 transition-opacity duration-750 lg:grow starting:opacity-0"
        >
            <main
                class="flex w-full max-w-[335px] flex-col-reverse overflow-hidden rounded-2xl shadow-2xl lg:max-w-5xl lg:flex-row"
            >
                <!-- Left column: Portal info & features -->
                <div
                    class="flex-1 rounded-b-2xl bg-white/80 p-6 pb-12 text-[13px] leading-[20px] backdrop-blur-sm lg:rounded-l-2xl lg:rounded-br-none lg:p-10 lg:pl-12 dark:bg-gray-900/80 dark:text-[#EDEDEC]"
                >
                    <div class="mb-2 flex items-center gap-2">
                        <div class="rounded-full bg-indigo-100 p-1.5 dark:bg-indigo-900/60">
                            <svg class="h-5 w-5 text-indigo-600 dark:text-indigo-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.042A8.967 8.967 0 006 3.75c-1.052 0-2.062.18-3 .512v14.25A8.987 8.987 0 016 18c2.305 0 4.408.867 6 2.292m0-14.25a8.966 8.966 0 016-2.292c1.052 0 2.062.18 3 .512v14.25A8.987 8.987 0 0018 18a8.967 8.967 0 00-6 2.292m0-14.25v14.25" />
                            </svg>
                        </div>
                        <span class="text-xs font-semibold uppercase tracking-wider text-indigo-600 dark:text-indigo-400">Student Portal</span>
                    </div>
                    <h1 class="mb-3 text-3xl font-bold tracking-tight text-gray-900 dark:text-white lg:text-4xl">
                        Welcome to<br />College Central
                    </h1>
                    <p class="mb-5 text-base text-gray-600 dark:text-gray-300">
                        Your unified platform for academics, campus life, and success. Access courses, grades, resources, and community — all in one place.
                    </p>

                    <!-- Features list -->
                    <ul class="mb-6 space-y-3">
                        <li class="flex items-start gap-3">
                            <span class="mt-0.5 flex h-5 w-5 shrink-0 items-center justify-center rounded-full bg-indigo-100 text-indigo-600 dark:bg-indigo-900/60 dark:text-indigo-400">
                                <svg class="h-3 w-3" fill="currentColor" viewBox="0 0 20 20">
                                    <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                                </svg>
                            </span>
                            <span class="text-sm text-gray-700 dark:text-gray-300"><strong class="font-semibold text-gray-900 dark:text-white">Smart Dashboard</strong> — Real-time grades, attendance, and notifications.</span>
                        </li>
                        <li class="flex items-start gap-3">
                            <span class="mt-0.5 flex h-5 w-5 shrink-0 items-center justify-center rounded-full bg-indigo-100 text-indigo-600 dark:bg-indigo-900/60 dark:text-indigo-400">
                                <svg class="h-3 w-3" fill="currentColor" viewBox="0 0 20 20">
                                    <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                                </svg>
                            </span>
                            <span class="text-sm text-gray-700 dark:text-gray-300"><strong class="font-semibold text-gray-900 dark:text-white">Course Registration</strong> — Enroll in classes with ease.</span>
                        </li>
                        <li class="flex items-start gap-3">
                            <span class="mt-0.5 flex h-5 w-5 shrink-0 items-center justify-center rounded-full bg-indigo-100 text-indigo-600 dark:bg-indigo-900/60 dark:text-indigo-400">
                                <svg class="h-3 w-3" fill="currentColor" viewBox="0 0 20 20">
                                    <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                                </svg>
                            </span>
                            <span class="text-sm text-gray-700 dark:text-gray-300"><strong class="font-semibold text-gray-900 dark:text-white">Campus Life</strong> — Events, clubs, and announcements.</span>
                        </li>
                        <li class="flex items-start gap-3">
                            <span class="mt-0.5 flex h-5 w-5 shrink-0 items-center justify-center rounded-full bg-indigo-100 text-indigo-600 dark:bg-indigo-900/60 dark:text-indigo-400">
                                <svg class="h-3 w-3" fill="currentColor" viewBox="0 0 20 20">
                                    <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                                </svg>
                            </span>
                            <span class="text-sm text-gray-700 dark:text-gray-300"><strong class="font-semibold text-gray-900 dark:text-white">Library & Resources</strong> — 24/7 access to digital materials.</span>
                        </li>
                    </ul>

                    <!-- CTA buttons -->
                    <div class="flex flex-wrap gap-3">
                        <Link
                            v-if="canRegister"
                            :href="register()"
                            class="inline-flex items-center rounded-full bg-indigo-600 px-6 py-2.5 text-sm font-semibold text-white shadow-md transition-all hover:bg-indigo-700 dark:bg-indigo-500 dark:hover:bg-indigo-600"
                        >
                            Get Started
                            <svg class="ml-2 h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M13 7l5 5m0 0l-5 5m5-5H6" />
                            </svg>
                        </Link>
                        <Link
                            :href="login()"
                            class="inline-flex items-center rounded-full border border-indigo-200 bg-white/60 px-6 py-2.5 text-sm font-medium text-indigo-700 transition-all hover:bg-indigo-50 dark:border-indigo-800 dark:bg-gray-800/60 dark:text-indigo-300 dark:hover:bg-indigo-950/40"
                        >
                            Sign In
                        </Link>
                    </div>
                    <p class="mt-5 text-xs text-gray-500 dark:text-gray-400">
                        🔒 Secure access for students, faculty, and staff.
                    </p>
                </div>

                <!-- Right column: Hero Illustration -->
                <div
                    class="relative -mb-px aspect-[335/364] w-full shrink-0 overflow-hidden rounded-t-2xl bg-gradient-to-br from-indigo-100 via-white to-sky-100 lg:mb-0 lg:-ml-px lg:aspect-auto lg:w-[480px] lg:rounded-t-none lg:rounded-r-2xl dark:from-indigo-950 dark:via-gray-900 dark:to-sky-950"
                >
                    <!-- Academic illustration SVG -->
                    <div class="relative flex h-full w-full items-center justify-center p-8">
                        <svg
                            class="w-full max-w-[320px] text-indigo-600 drop-shadow-xl transition-all duration-750 dark:text-indigo-400 lg:max-w-md"
                            viewBox="0 0 400 350"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <!-- Background decorative circles -->
                            <circle cx="200" cy="175" r="140" fill="currentColor" fill-opacity="0.05" />
                            <circle cx="200" cy="175" r="110" fill="currentColor" fill-opacity="0.08" />
                            
                            <!-- Graduation cap (mortarboard) -->
                            <g transform="translate(120, 80)">
                                <!-- Base -->
                                <rect x="30" y="70" width="100" height="12" rx="4" fill="currentColor" fill-opacity="0.2" />
                                <rect x="45" y="82" width="70" height="40" rx="6" fill="currentColor" fill-opacity="0.15" />
                                <!-- Top platform -->
                                <polygon points="0,70 80,30 160,70 80,110" fill="currentColor" fill-opacity="0.85" />
                                <polygon points="0,70 80,30 160,70 80,110" stroke="currentColor" stroke-width="2" stroke-linejoin="round" />
                                <!-- Tassel -->
                                <path d="M80 35 L110 55 L115 95" stroke="currentColor" stroke-width="2.5" fill="none" stroke-linecap="round" />
                                <circle cx="115" cy="98" r="4" fill="currentColor" />
                            </g>

                            <!-- Book stack -->
                            <g transform="translate(220, 150)">
                                <rect x="0" y="20" width="70" height="12" rx="3" fill="currentColor" fill-opacity="0.7" transform="rotate(-10)" />
                                <rect x="8" y="8" width="70" height="12" rx="3" fill="currentColor" fill-opacity="0.85" transform="rotate(-5)" />
                                <rect x="15" y="-4" width="70" height="12" rx="3" fill="currentColor" transform="rotate(0)" />
                                <path d="M20 10 L20 30" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" />
                                <path d="M50 5 L50 25" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" />
                            </g>

                            <!-- Diploma with ribbon -->
                            <g transform="translate(60, 200)">
                                <rect x="0" y="0" width="90" height="60" rx="6" fill="currentColor" fill-opacity="0.1" stroke="currentColor" stroke-width="2" />
                                <path d="M20 15 L70 15 M20 30 L70 30 M20 45 L50 45" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" />
                                <path d="M90 10 L110 20 L90 30" fill="currentColor" fill-opacity="0.6" stroke="currentColor" stroke-width="1.5" />
                            </g>

                            <!-- Floating stars / sparkles -->
                            <g fill="currentColor" fill-opacity="0.6">
                                <path d="M310 90 L314 100 L324 104 L314 108 L310 118 L306 108 L296 104 L306 100 Z" />
                                <path d="M60 280 L62 286 L68 288 L62 290 L60 296 L58 290 L52 288 L58 286 Z" />
                                <path d="M340 230 L342 236 L348 238 L342 240 L340 246 L338 240 L332 238 L338 236 Z" />
                            </g>

                            <!-- Decorative lines -->
                            <path d="M40 160 L120 130" stroke="currentColor" stroke-width="1.5" stroke-dasharray="4 4" fill-opacity="0.4" />
                            <path d="M280 260 L360 240" stroke="currentColor" stroke-width="1.5" stroke-dasharray="4 4" fill-opacity="0.4" />
                            
                            <!-- Laptop / device icon -->
                            <g transform="translate(240, 260)">
                                <rect x="0" y="0" width="50" height="35" rx="4" fill="currentColor" fill-opacity="0.1" stroke="currentColor" stroke-width="1.5" />
                                <rect x="5" y="5" width="40" height="20" fill="currentColor" fill-opacity="0.2" />
                                <path d="M15 30 L35 30 L25 40 Z" fill="currentColor" fill-opacity="0.5" />
                            </g>

                            <!-- Abstract network nodes (digital learning) -->
                            <circle cx="170" cy="240" r="6" fill="currentColor" fill-opacity="0.3" />
                            <circle cx="210" cy="260" r="4" fill="currentColor" fill-opacity="0.4" />
                            <circle cx="140" cy="280" r="5" fill="currentColor" fill-opacity="0.25" />
                            <path d="M170 240 L210 260 L140 280" stroke="currentColor" stroke-width="1" stroke-dasharray="3 3" fill-opacity="0.3" />
                        </svg>
                    </div>
                    
                    <!-- Overlay shadow border -->
                    <div
                        class="pointer-events-none absolute inset-0 rounded-t-2xl shadow-[inset_0px_0px_0px_1px_rgba(0,0,0,0.05)] lg:rounded-t-none lg:rounded-r-2xl dark:shadow-[inset_0px_0px_0px_1px_rgba(255,255,255,0.1)]"
                    ></div>
                </div>
            </main>
        </div>
        <div class="hidden h-14.5 lg:block"></div>
    </div>
</template>