<script setup>
import { onMounted, ref } from "vue";
import NavBar from "./components/index/NavBar.vue";
import Loader from "./components/utility/Loader.vue";
import ContactFooter from "./components/index/ContactFooter.vue";
import { useRouter } from "vue-router";


const router = useRouter();
const loading = ref(true);
const currentRoute = ref(null);

onMounted(() => {
	setTimeout(() => {
		currentRoute.value = router.currentRoute.value.name;
		loading.value = false;
		
	}, 2000);
});
</script>

<template>
	<header
		v-if="currentRoute !== 'payment'"
		v-show="!loading"
		class="px-4 md:px-10 py-5 bg-[wheat] pt-6 transition-all duration-200">
		<NavBar />
	</header>

	<Transition>
		<Loader v-if="loading" />
	</Transition>
	<main v-show="!loading">
		<router-view></router-view>
	</main>
	<footer
	v-if="currentRoute !== 'payment'"
		v-show="!loading"
		class="px-2 py-5 pt-6 bg-[#f5deb3]"
		style="box-shadow: 0px -6px 6px -2px rgba(128, 128, 128, 0.438)">
		<ContactFooter />
	</footer>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
	transition: opacity 1s ease;
}

.v-enter-from,
.v-leave-to {
	opacity: 0;
}
</style>
