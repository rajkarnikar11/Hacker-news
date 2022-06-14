<template>
	<nav>
		<div class="nav__left">
			<router-link class="title__container" to="/">
				<h3 class="title__logo">Y</h3>
				<h1 class="title__name">Hacker News</h1>
			</router-link>
			<router-link class="nav__link" to="/newest">new</router-link>
			<router-link class="nav__link" to="/front">past</router-link>
			<router-link class="nav__link" to="/newcomments"
				>comments</router-link
			>
			<router-link class="nav__link" to="/ask">ask</router-link>
			<router-link class="nav__link" to="/show">show</router-link>
			<router-link class="nav__link" to="/jobs">jobs</router-link>
			<router-link class="nav__link" to="/submit">submit</router-link>
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
	height: 30px;
	padding: 2px;
}
.nav__left .nav__link {
	border-right: 1px solid black;
	padding-right: 10px;
	height: 18 px;
}
.title__container {
	display: flex;
	text-decoration: none;
	align-items: center;
}
.nav__left {
	display: flex;
	width: 45%;
	justify-content: space-between;
	align-items: center;
}
.nav__link {
	text-decoration: none;
	color: black;
}

.title__name {
	font-size: 18px;
	line-height: 25px;
	color: black;
}
.nav__right {
	margin-right: 5px;
}
.title__logo {
	color: white;
	font-size: 15px;
	line-height: 25px;
	justify-content: center;
	align-items: center;
	margin-right: 10px;
	display: flex;
	border: 2px solid white;
	height: 20px;
	box-sizing: border-box;
	width: 20px;
}
.router-link-exact-active {
	color: white;
}
</style>
