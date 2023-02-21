<template>
	<section>
		<h2>Select a Topic</h2>
		<!-- :topics="topics" -->
		<knowledge-grid></knowledge-grid>
	</section>
	<!-- @select-topic="$emit('select-topic', $event)" -->
	<!-- base 是 grid 的父组件，在这里，返回的是事件对象 -->
</template>

<script>
export default {
	//props: ['topics'],
	//emits: ['select-topic']
};
</script>
