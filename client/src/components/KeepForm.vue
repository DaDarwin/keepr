<template>
	<div
		class="modal fade"
		id="create-keep"
		tabindex="-1"
		aria-hidden="true">
		<div class="modal-dialog">
			<div class="modal-content">
				<div class="modal-header">
					<h1 class="modal-title">Post your Keep!</h1>
					<button
						type="button"
						class="btn-close"
						data-bs-dismiss="modal"
						aria-label="Close"></button>
				</div>
				<div class="modal-body">
					<form @submit.prevent="createKeep()">
						<div>
							<label for="keep-name">Name</label>
							<input
								v-model="keepData.name"
								id="keep-name"
								class="form-control"
								name="keep-name"
								type="text" />
						</div>
						<div>
							<label for="keep-img">Img</label>
							<input
								v-model="keepData.img"
								id="keep-img"
								class="form-control"
								name="keep-img"
								type="text" />
						</div>
						<div>
							<label for="keep-description">Name</label>
							<textarea
								v-model="keepData.description"
								id="keep-description"
								class="form-control"
								name="keep-description"
								cols="10"
								rows="5"></textarea>
						</div>
						<button class="btn btn-secondary mt-1">Post</button>
					</form>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import { AppState } from "../AppState";
import { computed, ref, onMounted } from "vue";
import Pop from "../utils/Pop";
import { keepService } from "../services/KeepService";
export default {
	setup() {
		const keepData = ref({});
		return {
			keepData,
			async createKeep() {
				try {
					await keepService.createKeep(keepData.value);
				} catch (error) {
					Pop.error(error);
				}
			},
		};
	},
};
</script>

<style lang="scss" scoped></style>
