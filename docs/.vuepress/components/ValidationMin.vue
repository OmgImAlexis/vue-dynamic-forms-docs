<template>
  <div class="form-composition library-example">
    <div class="col">
      <dynamic-form
        :id="testForm.id"
        :fields="testForm.fields"
        :options="testForm.options"
        @change="updateForm"
      />
      <p class="hint">
        Decrease -1 number and blur to see the validation working 👆🏻
      </p>
    </div>
    <div class="col">
      <pre>{{ formData }}</pre>
    </div>
  </div>
</template>

<script>
import {
  DynamicForm,
  FormField,
  FormOptions,
  FormValidation,
  min,
} from 'vdf-2';

const MIN_VALUE = 5;

export default {
  name: 'ValidationMinDemo',
  components: {
    DynamicForm,
  },
  data: () => ({
    formData: null,
    testForm: {
      id: 'validation-min-demo',
      fields: [
        new FormField({
          type: 'number',
          label: 'Number',
          name: 'minNumber',
          value: 5,
          validations: [
            new FormValidation(
              min(MIN_VALUE),
              `Value should be bigger than: ${MIN_VALUE}`,
            ),
          ],
        }),
      ],
      options: new FormOptions({ autoValidate: true }),
    },
  }),
  methods: {
    updateForm(values) {
      this.formData = values;
    },
  },
};
</script>

<style lang="scss">
@import '@/styles/styles.scss';

.form-composition {
  display: flex;
  justify-content: space-between;
}
.col {
  width: 45%;
}
pre {
  color: white;
  font-size: 12px;
}
</style>
