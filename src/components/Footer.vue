<script>
import Reddit from './svg/Reddit.vue';
import Github from './svg/Github.vue';

export default {
    components: {
        Reddit,
        Github
    }
}
</script>

<template>
    <div class="p-10 flex items-center justify-items-center justify-center">
        <h4 class='text-white font-bold font-RobotoCondensed text-center text-lg lg:text-2xl 2xl:text-3xl mx-5'>
            Patrick Edwards 2022 ©
        </h4>
        <a href="https://www.reddit.com/r/chess/comments/x30op1/i_made_a_website_to_find_the_chain_of_wins_from/"
            target="_blank" class="cursor-pointer">
            <Reddit class=' mx-2 h-11' />
        </a>
        <a href="https://github.com/FuzzyLogic123/six-degrees-of-hikaru-vue" target="_blank" class="cursor-pointer">
            <Github class='mx-2 h-11' />
        </a>
    </div>
</template>
