<template>
	<li>
		<h3>{{ topicName }}</h3>
		<p>{{ description }}</p>
		<button @click="selectTopic(id)">Learn More</button>
		<!-- 直接将点击事件写在了 绑定事件中 这个id既是从父组件中获取的又是要向父组件返回的 -->
		<!-- $emit('selectTopic', id) -->
	</li>
</template>

<script>
// props获取来自父组件的数据
export default {
	inject: ['selectTopic'],
	emits: ['select-topic'],
	props: ['id', 'topicName', 'description']
};
</script>
