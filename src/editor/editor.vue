<template>
    <div>
        xcvvsdfsdad
    </div>
</template>
<script>
import * as _ from 'lodash';
import { validators } from '_validators';

const { required, jsExpressionNonEmptyString, validateIf } = validators;

export default {
  name: 'editor-test-example',
  props: ['template', 'schema', 'step', 'stepId', 'steps', 'readonly'],
  components: {},
  computed: {},

  created() {
    console.log('!!!!!!!!!!!!!!', this.$v);
  },

  data() {
    return {};
  },

  methods: {},

  validations() {
    return {
      schema: validator(this.template),
    };
  },
};

export const data = template => ({
  //   email: '',
  //   emailPlaceholder: template.emailPlaceholder,
  //   emailLabel: template.emailLabel,
  //   password: '',
  //   passwordPlaceholder: template.passwordPlaceholder,
  //   passwordLabel: template.passwordLabel,
});

export const validator = template => {
  return {};
};

export const meta = {
  name: 'test-shcedule',
  type: 'onereach-studio-form-editor',
  version: '1.0',
};
</script>

<style scoped lang="scss" rel="stylesheet/scss">
// @import '../scss/colors';
</style>
