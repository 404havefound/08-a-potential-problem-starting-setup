// 父组件中引入子组件
<template>
	<div>
		<active-element
			:topic-title="activeTopic && activeTopic.title"
			:text="activeTopic && activeTopic.fullText"
		></active-element>
		<!-- :topics="topics" -->
		<knowledge-base></knowledge-base>
		<!-- @select-topic="activateTopic" -->
	</div>
</template>

<script>
//provide 和 inject需要父子关系，邻居关系不行
// 在这整个项目中,父子关系如下:APP--> active-element,knowledge-base-->grid-->knowledge-element
//active-element只是普通的被调用了，不是其他组件的父组件
export default {
	data() {
		return {
			topics: [
				{
					id: 'basics',
					title: 'The Basics',
					description: 'Core Vue basics you have to know',
					fullText:
						'Vue is a great framework and it has a couple of key concepts: Data binding, events, components and reactivity - that should tell you something!'
				},
				{
					id: 'components',
					title: 'Components',
					description:
						'Components are a core concept for building Vue UIs and apps',
					fullText:
						'With components, you can split logic (and markup) into separate building blocks and then combine those building blocks (and re-use them) to build powerful user interfaces.'
				}
			],
			activeTopic: null
		};
	},
	// provides data to all the child elements until one injects it (acts as prop wo passing props to middleman componnets)
	// moze bit i provide: ali je onda static data, sama za sebe
	// provide() {
	// 	return {
	// 		topics: this.topics,
	// 		selectTopic: this.activateTopic
	// 	};
	// },
	//在provide和data中都有topics这种情况下是有效的，但它是代码重复，but if we have any logic to change this data stored array, this change will not be refelected in the provided data,beacause it is an brand new array,it's a brand new object in memory therefor, so if we change data in original data in data(),that will no reflex to provide data, 所以provide data 最好写在data()中，以同步获取最后的数据更改。
	//provide: { 因此不再将它作为一个对象，而是一个方法来实现
	provide() {
		return {
			topics: this.topics,
			selectTopic: this.activateTopic
		};
	},
	// topics: [
	// 	{
	// 		id: 'basics',
	// 		title: 'The Basics',
	// 		description: 'Core Vue basics you have to know',
	// 		fullText:
	// 			'Vue is a great framework and it has a couple of key concepts: Data binding, events, components and reactivity - that should tell you something!'
	// 	},
	// 	{
	// 		id: 'components',
	// 		title: 'Components',
	// 		description:
	// 			'Components are a core concept for building Vue UIs and apps',
	// 		fullText:
	// 			'With components, you can split logic (and markup) into separate building blocks and then combine those building blocks (and re-use them) to build powerful user interfaces.'
	// 	}
	// ]
	//},
	methods: {
		activateTopic(topicId) {
			this.activeTopic = this.topics.find(topic => topic.id === topicId);
		}
	},
	//mounted() {
	// setTimeout(() => {
	// 	this.topics.push({
	// 		id: 'crypto',
	// 		title: 'The Crypto Investing',
	// 		description: 'Investing before it is too late',
	// 		fullText:
	// 			'Bitcoin is the future of money and it gonna make you and your mom rich'
	// 	});
	// }, 3000);
	//}
	//为了验证我们的这个写法依然在任何地方都有效，所以我们写一个mount钩子
	mounted() {
		setTimeout(() => {
			this.topics.push({
				id: 'events',
				title: 'Events',
				description: 'events are important in Vue ',
				fullText: 'Events aLLOW YOU to trigger code on demand!'
			});
		}, 3000);
	}
};
</script>

<style>
* {
	box-sizing: border-box;
}
html {
	font-family: sans-serif;
}
body {
	margin: 0;
}
section {
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
	margin: 2rem auto;
	max-width: 40rem;
	padding: 1rem;
	border-radius: 12px;
}

ul {
	list-style: none;
	margin: 0;
	padding: 0;
	display: flex;
	justify-content: center;
}

li {
	border-radius: 12px;
	border: 1px solid #ccc;
	padding: 1rem;
	width: 15rem;
	margin: 0 1rem;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}

h2 {
	margin: 0.75rem 0;
	text-align: center;
}

button {
	font: inherit;
	border: 1px solid #c70053;
	background-color: #c70053;
	color: white;
	padding: 0.75rem 2rem;
	border-radius: 30px;
	cursor: pointer;
}

button:hover,
button:active {
	background-color: #e24d8b;
	border-color: #e24d8b;
}
</style>
