<template>
	<nav>
		<div class="nav__left">
			<router-link class="title__container" to="/">
				<h3 class="title__logo">Y</h3>
				<h1 class="title__name">Hacker News</h1>
			</router-link>
			<router-link class="nav__link" to="/newest">new</router-link>
			<!-- <router-link class="nav__link" to="/front">past</router-link>
			<router-link class="nav__link" to="/comment">comments</router-link>
			<router-link class="nav__link" to="/ask">ask</router-link>
			<router-link class="nav__link" to="/show">show</router-link>
			<router-link class="nav__link" to="/jobs">jobs</router-link>
			<router-link class="nav__link" to="/submit">submit</router-link> -->
		</div>
		<div class="nav__right">
			<router-link class="nav__link" to="/submit">login</router-link>
		</div>
	</nav>
</template>

<script>
export default {
	name: "Navbar",
};
</script>

<style scoped>
nav {
	background: #ff6600;
	display: flex;
	align-items: center;
	justify-content: space-between;
	height: 24px;
}
.nav__left .nav__link {
	border-right: 1px solid black;
	padding: 0px 10px;
	height: 18 px;
}
.title__container {
	display: flex;
	text-decoration: none;
	align-items: center;
}
.nav__left {
	display: flex;
	max-width: 45%;
	font-size: 13.5px;

	justify-content: space-between;
	align-items: center;
}
.nav__link {
	text-decoration: none;
	color: black;
	align-self: center;
}

.title__name {
	font-size: 10pt;
	line-height: 25px;
	color: black;
	min-width: 100px;
}
.nav__right {
	margin-right: 5px;
	font-size: 10pt;
}
.title__logo {
	color: white;
	font-size: 14px;
	font-weight: normal;
	line-height: 25px;
	justify-content: center;
	align-items: center;
	margin-right: 5px;
	display: flex;
	border: 1px solid white;
	height: 20px;
	box-sizing: border-box;
	width: 20px;
	margin-left: 1px;
}
.router-link-exact-active {
	color: white;
}
</style>
