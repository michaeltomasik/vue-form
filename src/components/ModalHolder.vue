<template>
	<section>
		<button class="button is-primary"
			@click="isComponentModalActive = true">
			Open modal
		</button>

		<b-modal :active.sync="isComponentModalActive" has-modal-card>
			<MultiStepModal :steps="steps"/>
		</b-modal>
	</section>
</template>

<script>
import MultiStepModal from "./MultiStepModal.vue";

export default {
  components: {
    MultiStepModal
  },
  props: ["steps"],
  data() {
    return {
      isComponentModalActive: false
    };
  }
};
</script>
