<script>
import Twitter from './svg/Twitter.vue';
import RedditShareButton from './svg/RedditShareButton.vue';
import Facebook from './svg/Facebook.vue';
import Copy from './svg/Copy.vue';
import { analytics } from '@/firebaseConfig';
import { logEvent } from '@firebase/analytics';

export default {
    components: {
        Facebook,
        Twitter,
        RedditShareButton,
        Copy
    },
    methods: {
        copyToClipboard(text) {
            navigator.clipboard.writeText(text);
        },
        incrementShareButtonCountHelper(method) {
            !this.shared[method] && logEvent(analytics, "share_on_" + method);
            this.shared[method] = true;
        }
    },
    inject: ['shareableText'],
    data() {
        return {
            shared: {
                twitter: false,
                facebook: false,
                copy: false,
                reddit: false
            }
        }
    }
}
</script>

<template>
    <div class="flex justify-evenly items-center mt-6 mb-3">
        <button @click.stop="incrementShareButtonCountHelper('twitter')"
            class="p-2 bg-[#1DA1F2] rounded-md font-bold aspect-square">
            <a :href="`https://twitter.com/intent/tweet?text=${encodeURIComponent(this.shareableText.text)}&url=${encodeURIComponent(this.shareableText.link)}&hashtags=${encodeURIComponent('chess,kevinbacon,sixdegrees')}`"
                target="_blank">
                <Twitter class="fill-white h-8" />
            </a>
        </button>

        <button @click="incrementShareButtonCountHelper('reddit')"
            class="p-2 bg-[#ff4500] text-white rounded-md font-bold aspect-square">
            <a :href="`http://www.reddit.com/submit?url=https://sixdegreesofhikaru.com&title=${encodeURIComponent('Find the chain of users from you to Hikaru')}`"
                target="_blank">
                <RedditShareButton class="fill-white h-8" />
            </a>
        </button>

        <button @click="incrementShareButtonCountHelper('facebook')"
            class="p-2 bg-[#4267B2] text-white rounded-md font-bold aspect-square">
            <a :href="`http://www.facebook.com/share.php?u=${encodeURIComponent(this.shareableText.link)}`"
                target="_blank">
                <Facebook class="fill-white h-8" />
            </a>
        </button>

        <button @click="incrementShareButtonCountHelper('copy')"
            class="p-2 text-white rounded-md font-bold aspect-square">
            <div @click="this.copyToClipboard(`${this.shareableText.text} ${this.shareableText.link}`)">
                <Copy class="fill-zinc-700 h-8 hover:fill-zinc-900" />
            </div>
        </button>
    </div>
</template>

<style scoped>
button:active {
    transform: scale(0.9);
    transition: cubic-bezier(0.075, 0.82, 0.165, 1);
    transition-duration: 0.06s;
}
</style>