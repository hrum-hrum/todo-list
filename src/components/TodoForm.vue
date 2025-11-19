<script setup>
import { ref, defineEmits } from 'vue'
import { Form, Field, ErrorMessage } from 'vee-validate'
import * as yup from 'yup'

const todoTitle = ref('')
const $emit = defineEmits(['add-todo'])

const formValidationSchema = yup.object({
  todoTitleInput: yup.string().required('Введите название todo'),
})

const formSubmitHandler = (values) => {
  console.log(values)
  if (todoTitle.value) {
    $emit('add-todo', todoTitle.value)
    todoTitle.value = ''
  }
  //form.reset()
}
</script>

<template>
  <Form class="form" :validation-schema="formValidationSchema" @submit="formSubmitHandler">
    <div class="form__group form__group--todo">
      <Field
        class="form-control"
        name="todoTitleInput"
        type="text"
        placeholder="Новая задача"
        v-model.trim="todoTitle"
      />
      <button class="btn btn--add-todo" type="submit">Добавить</button>
    </div>
    <ErrorMessage name="todoTitleInput" class="message message--error" />
  </Form>
</template>

<style setup>
.form {
  display: block;
  margin-bottom: 2rem;
}

.form__group {
  display: flex;
  width: 100%;
}

.form-control {
  flex: 1;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px 0 0 5px;
}

.form-control:focus {
  outline: none;
  border-color: #6574cd;
}

.btn--add-todo {
  border-radius: 0 5px 5px 0;
}

.message {
  display: block;
  margin: 0;
  font-size: 0.75rem;
  position: relative;
  left: 0;
  margin-bottom: -1rem;
}

.message--error {
  color: #f44336;
}
</style>
