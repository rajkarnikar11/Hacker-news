<template>
	<div class="container">
		<div class="container__left">
			<div>{{ index + 1 }}.</div>
			<!-- <img class="up-icon" src="../assets/up-icon.svg" /> -->
		</div>
		<div class="container__right">
			<div class="container__right-top">
				<a :href="url" class="link">
					<span class="title">
						{{ title }}
					</span>
				</a>

				<a :href="url" class="link link-url"> ({{ shorturl.url }}) </a>
			</div>
			<div class="container__right-bottom">
				<span
					>{{ point }} points by<a
						class="name"
						:href="'/user/' + name"
					>
						{{ name }}</a
					>
					{{ moment(actualTime).fromNow() }}
				</span>
				<!-- <span class="hide">hide</span> -->
				<span
					><router-link class="comment" :to="'/comment/' + id"
						>{{ comments }} comments</router-link
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
a:hover {
	text-decoration: underline;
}
.link-url:hover {
	text-decoration: underline !important;
}
.container {
	display: flex;
	padding: 8pt 2px;
	height: 35px;
	width: 100%;
}
.container__right {
	width: 80%;
}
.container__left {
	display: flex;
	color: #a8a8a8;
	justify-content: flex-end;
	font-size: 10pt;
	color: #828282;
	margin-right: 5px;
	min-width: 22px;
}
.container__right-top {
	display: flex;
}
.name {
	color: #a8a8a8;
	margin: 0 5px;
}
.hide {
	padding: 0px 2px;
	border-right: 2px solid rgb(57, 56, 56);
	border-left: 2px solid rgb(57, 56, 56);
	margin: 3px;
}
.container__right-bottom {
	font-size: 8pt;
	line-height: 6px;
	color: #a8a8a8;
	cursor: pointer;
}
.title {
	text-decoration: none;
	margin: 0 5px 0 0;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
	font-size: 10pt;
	cursor: pointer;
}
.title:hover {
	text-decoration: none !important;
}

.comment {
	text-decoration: none;
	margin: 0 5px;
	color: #a8a8a8;
}
.link {
	font-size: 8pt;

	line-height: 20px;
	cursor: pointer;
	text-decoration: none;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}
.link:hover {
	text-decoration: none;
}
.link:visited {
	color: #828282;
}
</style>
