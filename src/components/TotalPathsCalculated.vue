<script>
import { onSnapshot } from "firebase/firestore";
import { docRef } from '@/firebaseConfig.js';
import gsap from 'gsap';
import { authenticateUser, auth } from "../firebaseConfig";

export default {
    data() {
        return {
            totalPathsCalculated: 0,
            tweened: 0
        }
    },
    async created() {
        if (await authenticateUser(auth)) {
            onSnapshot(docRef, (doc) => {
                this.totalPathsCalculated = doc.data().numberOfPathsCalculated;
            });
        }
    },
    watch: {
        totalPathsCalculated(n) {
            gsap.to(this, { duration: 3, tweened: Number(n) || 0 })
        }
    }
}
</script>

<template>
    <div class="sm:py-20 xl:py-36">
        <h1 class="text-5xl xl:text-7xl uppercase leading-tight text-white text-center py-0 px-10">paths to
            <b>Hikaru</b> calculated so far
        </h1>
        <h1 class="text-8xl xl:text-9xl font-bold text-center py-14 text-[#EA0990]">{{ this.tweened.toFixed(0) }}</h1>
    </div>
</template>