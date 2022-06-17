<template>
	<div class="home__container">
		<Navbar />
		<router-view />
		<Footer />
	</div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";
export default {
	name: "Home",
	components: { Navbar, Footer },
};
</script>
<style>
* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}
body {
	font-family: sans-serif;
}
.home__container {
	max-width: 1280px;
	margin: auto;
	background-color: #f7f7ef;
	margin-top: 10px;
	box-sizing: border-box;
}
</style>
