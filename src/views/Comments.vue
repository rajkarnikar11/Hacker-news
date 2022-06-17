<template>
	<div>
		<div class="container">
			<div class="container__left">
				<!-- <img class="up-icon" src="../assets/up-icon.svg" /> -->
			</div>
			<div class="container__right">
				<div class="container__right-top">
					<span class="title title--comment">
						{{ news.title }}
					</span>
					<a :href="url" class="link"> ({{ shorturl }}) </a>
				</div>
				<div class="container__right-bottom">
					<span
						>{{ news.score }} points by {{ news.by }}
						{{ moment(actualTime).fromNow() }}
					</span>
					<!-- <span class="hide">hide</span>
					<span class="">past</span>
					<span class="hide">favourite</span> -->
					<span
						><router-link
							class="comment"
							:to="'/comment/' + $route.params.id"
							>{{ news.descendants }} comments</router-link
						></span
					>
				</div>
				<div class="container__right--text-field">
					<textarea></textarea>
				</div>
				<button>add comment</button>
			</div>
		</div>
		<div class="comments-container">
			<div v-for="kid in news.kids" :key="kid">
				<Comment :id="kid" />
			</div>
		</div>
	</div>
</template>

<script>
var moment = require("moment");
import Comment from "../components/Comment.vue";

export default {
	components: { Comment },
	data() {
		return { moment: moment, news: {}, actualTime: 0, shorturl: "" };
	},
	created() {
		this.fetchStory(this.$route.params.id);

		// this.actualTime = moment.unix(this.news.time);
	},

	methods: {
		editUrl(data) {
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

			this.shorturl = edited;
		},
		fetchStory(id) {
			fetch(
				`https://hacker-news.firebaseio.com/v0/item/${id}.json?print=pretty`,
			)
				.then((res) => {
					return res.json();
				})
				.then((data) => {
					this.news = data;
					console.log(data);
					this.actualTime = moment.unix(this.news.time);
					this.editUrl(data.url);
				});
		},
	},
};
</script>

<style scoped>
.container {
	display: flex;
	padding: 10px 2px;
	width: 100%;
	margin-top: 10px;
}
.comments-container {
}
button {
	margin-top: 13px;
	padding: 2px 4px;
}
.container__right {
	width: 80%;
}
.container__left {
	width: 20px;
	display: flex;
	color: #a8a8a8;
	justify-content: flex-end;
	padding-right: 5px;
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
	color: #a8a8a8;
	cursor: pointer;
}
.title {
	margin: 0 5px 0 0;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
	font-size: 10pt;
	color: #a8a8a8;
}
.up-icon {
	height: 9px;
	width: 9px;
}
textarea {
	margin-top: 15px;
	height: 124px;
	width: 608px;
}
.comment {
	text-decoration: none;
	color: #a8a8a8;
	margin: 0 5px;
}
.link {
	font-size: 10px;
	line-height: 20px;
	cursor: pointer;
	text-decoration: none;
	color: #a8a8a8;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}
.title--comment {
	color: #a8a8a8 !important;
}
</style>
