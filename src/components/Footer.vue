<template>
	<div>
		<div class="home__line" />
		<ul class="list">
			<li class="list-item list-item--faded">Guideline</li>
			<li class="list-item">FAQ</li>
			<li class="list-item">Lists</li>
			<li class="list-item list-item--faded">API</li>
			<li class="list-item">Security</li>
			<li class="list-item">Legal</li>
			<li class="list-item">Apply to YC</li>
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
.list-item--faded {
	opacity: 0.8;
}
.search__title {
	color: #a8a8a8;
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
	padding: 0 5px;
	border-right: 1px solid black;
	font-size: 12px;
	cursor: pointer;
	letter-spacing: 0.2px;
}
.list-item:last-of-type {
	border: none;
}
</style>
