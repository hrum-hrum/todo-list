<script setup>
import { defineEmits } from 'vue'
import { Form, Field, ErrorMessage } from 'vee-validate'
import * as yup from 'yup'

defineProps({
  todoTitle: String,
})

const todoTitle2 = defineModel()

const formValidationSchema = yup.object({
  todoTitleInput: yup.string().required('Введите название todo'),
  todoTitleInput2: yup.string().required('Введите название todo'),
})

const emit = defineEmits(['submit:todo-form'])

const formSubmitHandler = (values, { form }) => {
  console.log(form)
  emit('submit:todo-form')
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
        :value="todoTitle"
        @input="$emit('update:todo-title-input', $event.target.value.trim())"
      />
    </div>
    <ErrorMessage name="todoTitleInput" class="message message--error" />

    <div class="form__group form__group--todo">
      <Field
        class="form-control"
        name="todoTitleInput2"
        type="text"
        placeholder="Новая задача"
        v-model="todoTitle2"
      />
      <button class="btn btn--add-todo" type="submit">Добавить</button>
    </div>
    <ErrorMessage name="todoTitleInput2" class="message message--error" />
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
  margin: 0;
  font-size: 0.75rem;
  text-align: center;
  position: relative;
  left: 0;
}

.message--error {
  color: #f44336;
}
</style>
