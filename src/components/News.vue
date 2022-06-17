<template>
	<div class="container">
		<div class="container__left">
			<div>{{ index + 1 }}.</div>
			<img class="up-icon" src="../assets/up-icon.svg" />
		</div>
		<div class="container__right">
			<div class="container__right-top">
				<a :href="url" class="link">
					<span class="title">
						{{ title }}
					</span>
				</a>

				<a :href="url" class="link"> ({{ shorturl.url }}) </a>
			</div>
			<div class="container__right-bottom">
				<span
					>{{ point }} points by<a :href="'/user/' + name">
						{{ name }}</a
					>
					{{ moment(actualTime).fromNow() }} </span
				><span class="hide">hide</span
				><span
					><a class="comment" :href="'/comment/' + id"
						>{{ comments }} comments</a
					></span
				>
			</div>
		</div>
	</div>
</template>

<script>
var moment = require("moment");
export default {
	data() {
		return {
			moment: moment,
			shorturl: {},
			isFetching: true,
			actualTime: 0,
			day: 0,
		};
	},
	created() {
		this.editUrl(this.url);
		this.actualTime = moment.unix(this.time);
		this.day = moment(this.actualTime).format("dddd");
		// console.log(moment(this.actualTime).fromNow());
	},
	methods: {
		editUrl(data) {
			if (this.url) {
				let count = 0;
				let first = data.substring(8);
				let turned = first.split("");
				for (let x = 0; x < turned.length; x++) {
					if (turned[x] != "/" || turned[x] != "/") {
						count++;
					} else {
						break;
					}
				}
				let edited = first.substring(0, count);

				this.shorturl.url = edited;
			}
		},
	},

	// 	// this.hours = hours;
	// },
	props: [
		"title",
		"id",
		"index",
		"url",
		"point",
		"name",
		"comments",
		"no",

		"time",
	],
};
</script>

<style scoped>
a {
	text-decoration: none;
	color: black;
}
.container {
	display: flex;
	padding: 10px 2px;
	height: 35px;
	letter-spacing: 0.5px;
	width: 100%;
}
.container__right {
	width: 80%;
}
.container__left {
	width: 40px;
	display: flex;
	color: #a8a8a8;
	justify-content: flex-end;
	padding-right: 5px;
	font-size: 14px;
	color: rgb(74, 74, 74, 0.7);
}
.container__right-top {
	display: flex;
}
.hide {
	padding: 0px 2px;
	border-right: 2px solid rgb(57, 56, 56);
	border-left: 2px solid rgb(57, 56, 56);
	margin: 3px;
}
.container__right-bottom {
	font-size: 10px;
	line-height: 6px;
	opacity: 0.6;
	cursor: pointer;
}
.title {
	margin: 0 5px 0 0;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
	font-size: 14px;
	cursor: pointer;
}
.up-icon {
	margin-top: 3px;
	height: 10px;
	width: 10px;
}
.comment {
	text-decoration: none;
	color: black;
}
.link {
	opacity: 0.7;
	font-size: 10px;
	line-height: 20px;
	cursor: pointer;
	text-decoration: none;
	color: black;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}
</style>
