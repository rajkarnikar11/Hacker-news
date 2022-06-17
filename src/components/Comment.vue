<template>
	<div class="container">
		<div class="container__left">
			<!-- <img class="up-icon" src="../assets/up-icon.svg" /> -->
		</div>
		<div class="container__right">
			<div class="info">
				<span>{{ data.by }}</span>
				<span class="info__time">{{
					moment(actualTime).fromNow()
				}}</span>
				<!-- <span class="info__next">next</span>
				<span class="info__collapse">[ - ]</span> -->
			</div>
			<div class="text">
				<div v-if="!body" class="loading"></div>
				{{ body }}
			</div>
			<!-- <p class="comment__reply">reply</p> -->
			<div v-if="data.kids">
				<div v-for="kid in data.kids" :key="kid">
					<Comment :id="kid" />
				</div>
			</div>
		</div>
	</div>
</template>

<script>
var moment = require("moment");

export default {
	name: Comment,
	data() {
		return {
			moment: moment,
			data: {},
			actualTime: 0,
			body: "",
		};
	},
	props: ["id"],
	created() {
		this.fetchComment(this.id);
	},
	methods: {
		fetchComment(id) {
			fetch(`https://hacker-news.firebaseio.com/v0//item/${id}.json`)
				.then((res) => {
					return res.json();
					// console.log(res.body.json());
				})
				.then((res) => {
					console.log(res);
					this.data = res;
					this.body = this.stringToHTML(this.data.text);
					this.actualTime = moment.unix(this.data.time);
				});
		},
		stringToHTML(html) {
			// Create a new div element
			var tempDivElement = document.createElement("div");

			// Set the HTML content with the given value
			tempDivElement.innerHTML = html;

			// Retrieve the text property of the element
			return tempDivElement.textContent || tempDivElement.innerText || "";
		},
	},
};
</script>

<style scoped>
.container {
	display: flex;
	margin-top: 10px;
}
a:host {
	text-decoration: underline;
}
.comment__reply {
	font-size: 12px;
	margin-top: 10px;
	text-decoration: underline;
	cursor: pointer;
}
.info {
}
.info > span {
	font-size: 10px;
	color: rgb(57, 56, 56);
	cursor: pointer;
	opacity: 0.7;
}
.text {
	font-size: 12px;
	margin-top: 5px;
}
.container__left {
	width: 20px;
	display: flex;
	padding-right: 5px;
	margin-left: 15px;
}
.info__time {
	padding: 0 5px;
}
.info__next {
	padding: 0 5px;
}
.container__right {
}
.up-icon {
	height: 9px;
	width: 9px;
	margin-top: 5px;
}
.loading {
	border-radius: 100%;
	border: 2px solid rgb(128, 128, 128, 0.3);
	border-top: 3px solid rgb(255, 102, 0, 0.7);
	height: 20px;
	width: 20px;
	background: #f7f7ef;
	animation: spin 1s linear infinite;
}
@keyframes spin {
	from {
		transform: rotate(0deg);
	}
	30% {
		transform: rotate(660deg);
	}
	50% {
		transform: rotate(750deg);
	}
	to {
		transform: rotate(1080deg);
	}
}
</style>
