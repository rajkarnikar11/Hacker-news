<template>
	<div class="home__container">
		<Navbar />
		<router-view />
		<!-- <Footer /> -->
	</div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
// import Footer from "./components/Footer.vue";
export default {
	name: "Home",
	components: { Navbar },
};
</script>
<style>
* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}
body {
	font-family: Verdana, sans-serif;
}
.home__container {
	max-width: 1277px;
	margin: auto;
	background-color: #f7f7ef;
	margin-top: 7px;
	box-sizing: border-box;
}
</style>
