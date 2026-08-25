<script setup>
import { NMarquee } from 'naive-ui'

const skillGroups = [
    {
        title: "Laravel",
        logo: "/logo/p1.png",
        items: ["Backend", "REST APIs", "Auth", "Services"],
    },
    {
        title: "Vue.js",
        logo: "/logo/p2.png",
        items: ["SPA", "Components", "Dashboards", "Vuex"],
    },
    {
        title: "MySQL",
        logo: "/logo/p3.png",
        items: ["Schema", "Queries", "Relations", "Tuning"],
    },
    {
        title: "cPanel",
        logo: "/logo/p4.png",
        items: ["Hosting", "Domains", "Email", "Server Tools"],
    },
    {
        title: "Stripe",
        logo: "/logo/p5.png",
        items: ["Payments", "Checkout", "Webhooks", "States"],
    },
    {
        title: "AdonisJS",
        logo: "/logo/p6.png",
        items: ["Backend", "REST APIs", "Auth", "Services"],
    },
    {
        title: "Node.js",
        logo: "/logo/p7.png",
        items: ["Backend", "REST APIs", "Auth", "Services"],
    },
    {
        title: "Git",
        logo: "/logo/p8.png",
        items: ["Version Control", "Branches", "Merges", "CI/CD"],
    },
];
</script>

<template>
    <div class="trust-strip">
        <n-marquee auto-fill>
            <div v-for="(group, index) in skillGroups" :key="index" class="skill-group">
                <img :src="group.logo" :alt="group.title" class="skill-img" />
            </div>
        </n-marquee>
    </div>
</template>