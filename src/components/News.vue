<template>
	<div>
		<div v-if="loading" class="loading"> </div>
		<div  class="container">			
			<div class="container__left">
				<div>{{ index + 1 }}.</div>
			</div>
			<div class="container__right">
				<div class="container__right-top">
					<a :href="news.url" class="link">
						<span class="title">
							{{ news.title }}
						</span>
					</a>

					<a :href="news.url" class="link link-url"> ({{ shorturl.url }}) </a>
				</div>
				<div class="container__right-bottom">
					<span
						>{{ point }} points by<a
							class="name"
							:href="'/user/' + news.by"
						>
							{{ news.by }}</a
						>
						{{ moment(actualTime).fromNow() }}
					</span>
					<span
						><router-link class="comment" :to="'/comment/' + id"
							>{{ news.descendants }} comments</router-link
						></span
					>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
var moment = require("moment");
export default {
	data() {
		return {
			news:[],
			moment: moment,
			shorturl: {},
			isFetching: true,
			actualTime: 0,
			day: 0,
		};
	},
	created() {
		this.fetchNews(this.id)
		this.editUrl(this.news.url);
		this.actualTime = moment.unix(this.news.time);
		this.day = moment(this.actualTime).format("dddd");
		// console.log(moment(this.actualTime).fromNow());
	},
	methods: {
		
		fetchNews(id){
			this.loading=true;
			fetch(
				`https://hacker-news.firebaseio.com/v0/item/${id}.json?print=pretty`,
			)
				.then((res) => {
					return res.json();
				})
				.then((data) => {
					this.news=data;
						this.loading = false;
					this.i++;
				});
		
		},
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
		
		"id",
		"index",
		
	],
};
</script>

<style scoped>
.loading {
	border-radius: 100%;
	border: 2px solid rgb(128, 128, 128, 0.3);
	border-top: 3px solid rgb(255, 102, 0, 0.7);
	height: 20px;
	width: 20px;
	background: #f7f7ef;
	margin: 10px ;
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
