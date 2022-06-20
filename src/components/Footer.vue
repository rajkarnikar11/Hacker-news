<template>
	<div>
		<div class="home__line" />
		<ul class="list">
			<li class="list-item list-item--faded">
				<a href="https://news.ycombinator.com/newsguidelines.html"
					>Guideline</a
				>
			</li>
			<li class="list-item">
				<router-link to="https://news.ycombinator.com/newsfaq.html">FAQ</router-link>
			</li>
			<li class="list-item">
				<router-link to="https://news.ycombinator.com/lists">Lists</router-link>
			</li>
			<li class="list-item">
				<a to="https://news.ycombinator.com/lists">API</a>
			</li>
			<li class="list-item">
				<router-link to="https://news.ycombinator.com/security.html"
					>Security</router-link
				>
			</li>
			<li class="list-item">
				<router-link to="https://www.ycombinator.com/legal/">Legal</router-link>
			</li>
			<li class="list-item">
				<router-link to="https://www.ycombinator.com/apply/">Apply to YC</router-link>
			</li>
			<li class="list-item">Contact</li>
		</ul>
		<div class="search">
			<p class="search__title">Search:</p>
			<input class="search__field" type="text" />
		</div>
	</div>
</template>

<script>
export default {};
</script>

<style scoped>
* {
	list-style: none;
	text-decoration: none;
}
a {
	color: black;
	padding: 0 5px;
	border-right: 1px solid black;
}
a:visited {
	color: #a8a8a8;
	border-right: 1px solid #a8a8a8;
}
.search {
	display: flex;
	justify-content: center;
	height: 70px;
	align-items: center;
	cursor: pointer;
}
.list {
	display: flex;
	justify-content: center;
	margin-top: 25px;
}
.search__title {
	color: #a8a8a8;
	font-size: 10pt;
}
.search__field {
	margin: 0 10px;
}
.home__line {
	height: 1.5px;
	margin-bottom: 10px;
	background-color: #ff6600;
}
.list-item {
	font-size: 8pt;
	cursor: pointer;
}
.list-item:last-of-type {
	border: none;
}
</style>
