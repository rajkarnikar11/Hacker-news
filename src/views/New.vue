<template>
	<div class="home">
		<div v-if="loading " class="loading"></div>

		<div v-for="(data, index) in news" :key="data.id">
			<News
				v-if="index >= pageCounter && index < pageCounter + 30"
				:index="index"
				
				:id="data.id"
				
				>i++</News
			>
			<!-- <div>{{ data.id }} {{ data.title }}</div> -->
		</div>
		<button @click="incrementPage" class="more-button">More</button>
	</div>
</template>

<script>
import News from "@/components/News.vue";
// @ is an alias to /src

export default {
	name: "HomeView",
	components: { News },

	data() {
		return {
			news: [],
			titles: [],
			shorturl: [],
			fetcher:30,
			i: 0,
			arrayFlag: 0,
			pageCounter: 0,

			// url: "https://hacker-news.firebaseio.com/v0/item/%7Bitem-id%7D.json?print=pretty",
		};
	},
	created() {
		this.loading = true;
		this.fetchId(this.fetcher);
		console.log("started");
		console.log(this.pageCounter);
	},
	methods: {
		incrementPage() {
			console.log("clicked");
			console.log(this.pageCounter);
			this.fetcher=this.fetcher+30;
			this.pageCounter = this.pageCounter + 30;
			this.fetchId(this.fetcher);
		},
		fetchId(fetcher	) {
			fetch("https://hacker-news.firebaseio.com/v0/newstories.json")
				.then((res) => {
					return res.json();
					
				})
				.then((data) => {
					data.forEach((element) => {
						this.fetchStory(element,fetcher);
						console.log(fetcher)
					});
				});
		},

		fetchStory(id,fetcher) {
			if(this.i<(fetcher)){
			fetch(
				`https://hacker-news.firebaseio.com/v0/item/${id}.json?print=pretty`,
			)
				.then((res) => {
					return res.json();
				})
				.then((data) => {
					this.news.push(data);

					
				}).finally(() => {
					this.fetcher=this.fetcher +30;
					this.loading = false;
				});	
			}
			this.i++;
			
		},
	},
};
</script>
<style scoped>

.more-button {
	color: #a8a8a8;
	background: none;
	border: none;
	margin: 20px 0;
	cursor: pointer;
	font-size: 10pt;
	margin-left: 25px;
}
.loading {
	border-radius: 100%;
	border: 2px solid rgb(128, 128, 128, 0.3);
	border-top: 3px solid rgb(255, 102, 0, 0.7);
	height: 20px;
	width: 20px;
	background: #f7f7ef;
	margin: 10px auto;
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
