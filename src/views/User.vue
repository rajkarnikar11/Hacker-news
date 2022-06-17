<template>
	<div class="container">
		<div class="line__container">
			<p class="line__left">user:</p>
			<p class="line__right">{{ user.id }}</p>
		</div>
		<div class="line__container">
			<p class="line__left">created:</p>
			<p class="line__right">
				{{ moment(date).format("MMMM  Do , YYYY") }}
			</p>
		</div>
		<div class="line__container">
			<p class="line__left">karma:</p>
			<p class="line__right">{{ user.karma }}</p>
		</div>
		<div class="line__container">
			<p class="line__left">about:</p>
			<p class="line__right">{{ user.about }}</p>
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

					this.date = moment.unix(data.created);
					console.log(this.date);
				});
		},
	},
};
</script>

<style scoped>
.line__container {
	display: flex;
	margin: 10px 0;
	color: grey;
	font-size: 14px;
}
.container {
	padding: 4px;
}
.line__left {
	width: 65px;
}
</style>
