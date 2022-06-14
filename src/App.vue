<template>
	<div class="home__container">
		<Navbar />
		<router-view />
	</div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
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
	font-family: sans-serif;
	margin: 10px;
}
.home__container {
	max-width: 1280px;
	margin: auto;
	background-color: #f7f7ef;
}
</style>
