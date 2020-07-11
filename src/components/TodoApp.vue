<template>
	<div>
		<div class="item">
			<p>Nowe todo: {{ newItem }}</p>
			<input type="text" placeholder="todo" v-model="newItem" />
			<button @click="addItem">Dodaj</button>
		</div>

		<div
			class="item"
			v-bind:class="{
				complited: item.completed,
			}"
			v-for="item in items"
			v-bind:key="item.id"
		>
			<h2>{{ item.title }}</h2>
			<button v-if="!item.completed" @click="removeItem(item.id)">
				Zrobione
			</button>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			newItem: "",
			items: [
				{ title: "Zrobic zakupy", completed: false, id: 1 },
				{ title: "Nauka programowania", completed: true, id: 2 },
			],
		};
	},

	methods: {
		addItem() {
			this.items.push({
				title: this.newItem,
				completed: false,
				id: Math.random(),
			});

			this.newItem = "";
		},

		removeItem(id) {
			const index = this.items.findIndex((el) => el.id === id);
			this.items[index].completed = true;
		},
	},
};
</script>

<style>
.item {
	border: 1px solid black;
	margin: 8px;
	padding: 10px;
}

.complited {
	opacity: 0.5;
}

.complited h2 {
	text-decoration: line-through;
}
</style>
