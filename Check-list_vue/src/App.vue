<template>  <!--Шаблон вывода-->
	<h1>Список запланированных дел</h1>
	<br>

	<Todo   
		v-for="todo in todos"
		:id="todo.id"
		:point="todo.point"
		:key="todo.id"
		@remove="remove"
		@change="change"
	/>
	
	<TodoForm @add="add"/>
</template>

<script>
	import Todo from '../components/Todo.vue'; // Импотры
	import TodoForm from '../components/TodoForm.vue';
	export default {
		components: { // прописываем компоненты
			Todo, TodoForm
		},
		// В дата нужно прописать массив объектов todos
		data() {
			return {
				todos: [
					{
						id: 1,
						point: 'Проснуться',

					},
					{
						id: 2,
						point: 'Умыться'

					},
					{
						id: 3,
						point: 'Почистить зубы'
					}
				]
			}
		},
		methods: {

			remove(id) { // метод удаления заметки
				this.todos = this.todos.filter((todo) => { // для удаления сначала отфильтровываем объект
					return todo.id!== id;
				});
			},

			change(id, point) { // метод изменения заметки, позволяет изменять заметку
				this.todos = this.todos.map((todo) => { // с помощью стрелочной функции проверяем айди и присваиваем новое значение
					if (todo.id === id) {
						todo.point = point;
					}
					return todo;
				});
			},

			add(point) { // метод добавления новой заметки
				let id = this.todos.length + 1; // айди подбираем исходя из длины массива и прибавляем 1
				this.todos.push({ // и с помощью метода push добавляем объект в массив
					id,
					point 
					});
			}

		}
	}
</script>

<style>
	h1 {
		text-align: center;
		font-size: 26px;

	}
</style>