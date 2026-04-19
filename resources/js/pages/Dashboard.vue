<script setup lang="ts">
import { Head } from '@inertiajs/vue3';
import { dashboard } from '@/routes';
import { 
  BookOpen, 
  GraduationCap, 
  CalendarDays, 
  FileText, 
  BarChart3, 
  Megaphone,
  Calendar,
  MapPin,
  Clock
} from 'lucide-vue-next';

defineOptions({
    layout: {
        breadcrumbs: [
            {
                title: 'Dashboard',
                href: dashboard(),
            },
        ],
    },
});

// Sample data
const stats = [
    { title: 'Enrolled Courses', value: '6', change: '+1 this sem', icon: BookOpen, color: 'bg-indigo-100 text-indigo-700 dark:bg-indigo-900/40 dark:text-indigo-300' },
    { title: 'Current GPA', value: '3.72', change: '+0.08 from last term', icon: GraduationCap, color: 'bg-emerald-100 text-emerald-700 dark:bg-emerald-900/40 dark:text-emerald-300' },
    { title: 'Attendance Rate', value: '94%', change: '↑ 2% vs average', icon: CalendarDays, color: 'bg-sky-100 text-sky-700 dark:bg-sky-900/40 dark:text-sky-300' },
];

const recentActivities = [
    { id: 1, title: 'Completed assignment: Calculus II', course: 'BMAT101', time: '2 hours ago', type: 'submission', icon: FileText },
    { id: 2, title: 'Grade posted: Physics Lab Report', course: 'BICT103', grade: '92/100', time: 'yesterday', type: 'grade', icon: BarChart3 },
    { id: 3, title: 'New announcement: Midterm schedule', course: 'CS 305', time: '2 days ago', type: 'announcement', icon: Megaphone },
    { id: 4, title: 'Registered for Spring 2025 courses', course: 'Registration', time: '3 days ago', type: 'registration', icon: Calendar },
];

const upcomingEvents = [
    { id: 1, title: 'Career Fair', date: 'Apr 22, 2025', time: '10:00 AM - 3:00 PM', location: 'Student Union' },
    { id: 2, title: 'Guest Lecture: AI Ethics', date: 'Apr 25, 2026', time: '2:00 PM - 3:30 PM', location: 'Virtual' },
    { id: 3, title: 'Final Exam: Data Structures', date: 'May 5, 2026', time: '9:00 AM - 12:00 PM', location: 'Hall 204' },
    { id: 4, title: 'Hackathon 2026', date: 'May 10-12, 2026', time: 'All day', location: 'Innovation Lab' },
];
</script>

<template>
    <Head title="Dashboard" />

    <div class="flex h-full flex-1 flex-col gap-6 overflow-x-auto rounded-xl p-4">
        <!-- Stats Cards -->
        <div class="grid gap-5 md:grid-cols-3">
            <div
                v-for="stat in stats"
                :key="stat.title"
                class="group relative overflow-hidden rounded-2xl border border-gray-200 bg-white p-5 shadow-sm transition-all hover:shadow-md dark:border-gray-800 dark:bg-gray-900/80"
            >
                <div class="flex items-start justify-between">
                    <div>
                        <p class="text-sm font-medium text-gray-500 dark:text-gray-400">{{ stat.title }}</p>
                        <p class="mt-1 text-3xl font-bold text-gray-900 dark:text-white">{{ stat.value }}</p>
                        <p class="mt-1 text-xs text-gray-500 dark:text-gray-400">{{ stat.change }}</p>
                    </div>
                    <div :class="['flex h-10 w-10 items-center justify-center rounded-xl', stat.color]">
                        <component :is="stat.icon" class="h-5 w-5" />
                    </div>
                </div>
                <!-- Decorative gradient line -->
                <div class="absolute bottom-0 left-0 h-1 w-0 bg-linear-to-r from-indigo-500 to-sky-500 transition-all duration-300 group-hover:w-full"></div>
            </div>
        </div>

        <!-- Main Content: Two Columns -->
        <div class="grid gap-6 lg:grid-cols-2">
            <!-- Recent Activities -->
            <div class="rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-gray-900/80">
                <div class="mb-4 flex items-center justify-between">
                    <h3 class="text-lg font-semibold text-gray-800 dark:text-white">Recent Activity</h3>
                    <span class="text-xs text-indigo-600 dark:text-indigo-400">Last 7 days</span>
                </div>
                <div class="space-y-4">
                    <div
                        v-for="activity in recentActivities"
                        :key="activity.id"
                        class="flex items-start gap-3 border-b border-gray-100 pb-3 last:border-0 last:pb-0 dark:border-gray-800"
                    >
                        <div class="flex h-8 w-8 shrink-0 items-center justify-center rounded-full bg-gray-100 text-gray-600 dark:bg-gray-800 dark:text-gray-400">
                            <component :is="activity.icon" class="h-4 w-4" />
                        </div>
                        <div class="flex-1">
                            <p class="text-sm font-medium text-gray-800 dark:text-white">{{ activity.title }}</p>
                            <p class="text-xs text-gray-500 dark:text-gray-400">
                                {{ activity.course }} • {{ activity.time }}
                                <span v-if="activity.grade" class="ml-1 font-semibold text-emerald-600 dark:text-emerald-400">({{ activity.grade }})</span>
                            </p>
                        </div>
                    </div>
                </div>
                <!-- View all link -->
                <div class="mt-4 text-center">
                    <a href="#" class="text-sm text-indigo-600 hover:underline dark:text-indigo-400">View all activity →</a>
                </div>
            </div>

            <!-- Upcoming Events -->
            <div class="rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-gray-900/80">
                <div class="mb-4 flex items-center justify-between">
                    <h3 class="text-lg font-semibold text-gray-800 dark:text-white">Upcoming Events</h3>
                    <span class="text-xs text-indigo-600 dark:text-indigo-400">Next 30 days</span>
                </div>
                <div class="space-y-4">
                    <div
                        v-for="event in upcomingEvents"
                        :key="event.id"
                        class="flex items-start gap-3 border-b border-gray-100 pb-3 last:border-0 last:pb-0 dark:border-gray-800"
                    >
                        <div class="flex h-10 w-10 shrink-0 flex-col items-center justify-center rounded-lg bg-indigo-50 text-indigo-700 dark:bg-indigo-950/60 dark:text-indigo-300">
                            <span class="text-sm font-bold">{{ event.date.split(',')[0].split(' ')[1] }}</span>
                            <span class="text-[10px] uppercase">{{ event.date.split(',')[0].split(' ')[0].slice(0,3) }}</span>
                        </div>
                        <div class="flex-1">
                            <p class="text-sm font-medium text-gray-800 dark:text-white">{{ event.title }}</p>
                            <div class="flex flex-wrap items-center gap-x-3 gap-y-1 text-xs text-gray-500 dark:text-gray-400">
                                <span class="flex items-center gap-1">
                                    <Clock class="h-3 w-3" />
                                    {{ event.time }}
                                </span>
                                <span class="flex items-center gap-1">
                                    <MapPin class="h-3 w-3" />
                                    {{ event.location }}
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="mt-4 text-center">
                    <a href="#" class="text-sm text-indigo-600 hover:underline dark:text-indigo-400">View full calendar →</a>
                </div>
            </div>
        </div>

        <!-- Course Progress (full width) -->
        <div class="rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-gray-900/80">
            <h3 class="mb-3 text-lg font-semibold text-gray-800 dark:text-white">Course Progress</h3>
            <div class="grid gap-4 sm:grid-cols-2 lg:grid-cols-3">
                <div class="space-y-1">
                    <div class="flex justify-between text-sm">
                        <span class="text-gray-700 dark:text-gray-300">Calculus II</span>
                        <span class="text-gray-500 dark:text-gray-400">78%</span>
                    </div>
                    <div class="h-2 w-full overflow-hidden rounded-full bg-gray-200 dark:bg-gray-700">
                        <div class="h-full w-[78%] rounded-full bg-indigo-500"></div>
                    </div>
                </div>
                <div class="space-y-1">
                    <div class="flex justify-between text-sm">
                        <span class="text-gray-700 dark:text-gray-300">Physics 101</span>
                        <span class="text-gray-500 dark:text-gray-400">92%</span>
                    </div>
                    <div class="h-2 w-full overflow-hidden rounded-full bg-gray-200 dark:bg-gray-700">
                        <div class="h-full w-[92%] rounded-full bg-emerald-500"></div>
                    </div>
                </div>
                <div class="space-y-1">
                    <div class="flex justify-between text-sm">
                        <span class="text-gray-700 dark:text-gray-300">Data Structures</span>
                        <span class="text-gray-500 dark:text-gray-400">65%</span>
                    </div>
                    <div class="h-2 w-full overflow-hidden rounded-full bg-gray-200 dark:bg-gray-700">
                        <div class="h-full w-[65%] rounded-full bg-sky-500"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>