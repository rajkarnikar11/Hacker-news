<template>
	<div class="container">
		<div class="line__container">
			<p class="line__left">user:</p>
			<p class="line__right">{{ user.id }}</p>
		</div>
		<div class="line__container">
			<p class="line__left">created:</p>
			<p class="line__right date">
				{{ moment(date).format("MMMM  D , YYYY") }}
			</p>
		</div>
		<div class="line__container">
			<p class="line__left">karma:</p>
			<p class="line__right">{{ user.karma }}</p>
		</div>
		<div class="line__container">
			<p class="line__left">about:</p>
			<p class="line__right">{{ about }}</p>
			<!-- <a class="comment" :href="'/comment/' + user.id"> comments</a> -->
		</div>
	</div>
</template>

<script>
var moment = require("moment");

export default {
	data() {
		return {
			moment: moment,
			user: [],
			date: 0,
			about: "",
		};
	},
	created() {
		this.fetchUser(this.$route.params.id);
	},
	methods: {
		fetchUser(user) {
			fetch(
				`https://hacker-news.firebaseio.com/v0/user/${user}.json?print=pretty`,
			)
				.then((res) => {
					return res.json();
				})
				.then((data) => {
					this.user = data;
					console.log(this.user);
					this.stringToHTML(this.user.about);
					this.date = moment.unix(data.created);
					console.log(this.date);
				});
		},
		stringToHTML(html) {
			// Create a new div element
			var tempDivElement = document.createElement("div");

			// Set the HTML content with the given value
			tempDivElement.innerHTML = html;

			// Retrieve the text property of the element
			this.about =
				tempDivElement.textContent || tempDivElement.innerText || "";
		},
	},
};
</script>

<style scoped>
* {
	color: #828282;
	font-size: 10pt;
}
.line__container {
	display: flex;
	margin: 4px 0;

	font-size: 14px;
}
.date {
	color: black;
}
.container {
	padding: 4px;
	margin-top: 8px;
}
.line__left {
	width: 58px;
}
</style>
