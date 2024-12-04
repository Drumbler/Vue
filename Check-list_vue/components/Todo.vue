<template>
	<template v-if="!isEdit">
		<div
		title="Чтобы пометить выполненным нажать сюда, чтобы вернуть задачу нажми еще раз"	
		class="unit"
		@click="toggleClass()"
		:class="[isActive ? 'start' : 'done']"
		>
			{{ point }}
		</div>
		<br>
		<button @click="edit">
			Редактировать
		</button>
		<br>
	</template>

	<template v-else >
		<input v-model="newPoint" id="input-point">
		<button @click="save" id="input-point">
            Сохранить
        </button>
		<br>

	</template>

	<button @click="remove">
		Удалить
	</button>
	<br>
	<br>
	  

</template>

<script>
	export default {
		emits: ['remove', 'change'], // прописываем эммитс, а именно remove и change
		props: {
			id: Number,
			point: String,
		},
		data() {
			return { // Дата возвращает всю информацию об объекте
				newPoint: this.point,
				isEdit: false,
				isActive: true,
			}
		},
		methods: {
			remove() { // метод замтеки для удаления заметки
				this.$emit('remove', this.id, this.newPoint);
			},
			edit() { // метод заметки для изменения
				this.isEdit = true;
			},
			save() { // метод для сохранения заметки
				this.isEdit = false;
                this.$emit('change', this.id, this.newPoint);
			},
			toggleClass() { // метод изменения состояния заметки (Выполнена/не выполнена)
				this.isActive = !this.isActive;

                
			}
		}
	}
</script>

<style>
	.start{
		cursor: pointer;
		user-select: none;
	}
	.done{
		cursor: pointer;
		user-select: none;
		text-decoration: line-through;
	}
	.unit{
		display: inline-block;
        border: 1px solid black;
        padding: 10px;
    }
	button{
        cursor: pointer;
		background-color: #f3f3f3;
		margin-top: 10px;
		margin-left: 5px;
		border: 1px solid black;
		border-radius: 5px;
		padding: 5px;
		transition: all 0.7s ease;
    }
	button:hover{
        background-color: #cccccc;
    }
	div{
		margin: 15px;
		padding: 5px;
	}
	#input-point{
		margin: 20px;
	}
</style>