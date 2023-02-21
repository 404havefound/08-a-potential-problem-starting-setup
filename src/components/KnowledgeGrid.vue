<template>
	<ul>
		<knowledge-element
			v-for="topic in topics"
			:key="topic.id"
			:id="topic.id"
			:topic-name="topic.title"
			:description="topic.description"
		></knowledge-element>
	</ul>
	<!-- @select-topic="$emit('select-topic', $event)" -->
	<!-- grid是 knowledge-element的父组件 从app.vue的数组中获取id 将id传给子组件element，又返回回来-->
</template>

<script>
// $emit()的第一个参数是定义的事件名，第二个参数是要传入的数据
export default {
	// incect data provided by higher up component
	//you provide an array,and now you reference all the provided data you want to use in this component
	//you can only inject what has been provided,on a higher up level,which bascilly means in a parent component or an ancestor(祖先) component of KnowledgeGrid
	//so we can inject topics here because it provided from AppVue
	inject: ['topics']
	//props: ['topics'],

	//emits: ['select-topic']
};
</script>
