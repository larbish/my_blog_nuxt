<template>
	<div class="appHeader">
		<div class="content">
			<div class="articleInfo" v-if="isArticle">
				<ContentQuery :path="$route.path" find="one" v-slot="{ data }">
					<p class="articleTitle">{{ data.title }}</p>
					<p class="articleTime">{{ handleTime(data.time) }}</p>
				</ContentQuery>
			</div>
			<nav class="menu">
				<ul class="mainmenu">
					<li class="item">
						<NuxtLink to="/">
							<Icon class="icon" name="icon-park-solid:bachelor-cap-two" />
							<span class="text">Home</span>
						</NuxtLink>
					</li>
					<li class="item spot">·</li>
					<li class="item">
						<NuxtLink to="/article">
							<Icon class="icon" name="icon-park-solid:book-one" />
							<span class="text">article</span>
						</NuxtLink>
					</li>
					<li class="item spot">·</li>
					<li class="item">
						<NuxtLink to="https://www.travellings.cn/go.html" target="_blank">
							<Icon class="icon" name="icon-park-solid:railway" />
							<span class="text">travelling</span>
						</NuxtLink>
					</li>
					<li class="item spot">·</li>
					<li class="item">
						<NuxtLink to="/rss.xml" target="_blank">
							<Icon class="icon" name="typcn:rss" />
							<span class="text">RSS</span>
						</NuxtLink>
					</li>
				</ul>
			</nav>
		</div>
	</div>
</template>

<script setup>
// 判断是否处于文章页面
const route = useRoute();
const isArticle = computed(() => route.path.includes("/articles/"));

// 在文章页时显示文章信息
const config = useRuntimeConfig();

// 格式化时间
const handleTime = (time) => {
	if (time === null) {
		this.updateTime = false;
		return;
	}

	// 使用Date对象解析ISO 8601格式的时间戳
	const date = new Date(time);

	// 解析时间
	const months = date.getMonth();
	const day = date.getDate();
	const year = date.getFullYear();
	const hours = date.getHours().toString().padStart(2, "0"); // 确保两位数
	const minutes = date.getMinutes().toString().padStart(2, "0"); // 确保两位数
	const seconds = date.getSeconds().toString().padStart(2, "0"); // 确保两位数

	// 将月份转换为缩写格式
	const monthArray = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
	const month = monthArray[months];

	// 返回格式化的时间字符串
	return `${month} ${day}, ${year}`;
};
</script>

<style lang="scss" scoped>
@import url("~/assets/css/components/appHeader.scss");
</style>
