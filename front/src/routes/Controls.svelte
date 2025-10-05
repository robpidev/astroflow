<script lang="ts">
	import { Button } from '@svar-ui/svelte-core';

	import type { CameraControlsRef } from '@threlte/extras';
	//
	import { MathUtils } from 'three';

	let { controls = $bindable() }: { controls?: CameraControlsRef } = $props();

	let enabled = $state(true);

	$effect(() => {
		if (controls !== undefined) {
			controls.enabled = enabled;
		}
	});
</script>

<div class="Movement">
	<Button
		onclick={() => {
			controls?.setPosition(5, 5, 5, true);
			// controls?.reset(true);
		}}>Reset</Button
	>

	<Button
		onclick={() => {
			controls?.truck(1, 0, true);
			console.log(controls);
		}}>Truck</Button
	>

	<Button
		onclick={() => {
			controls?.rotate(45 * MathUtils.DEG2RAD, 0, true);
		}}
	>
		Rotate
	</Button>

	<Button
		onclick={() => {
			controls?.rotate(0, 45 * MathUtils.DEG2RAD, true);
		}}
	>
		Rotate
	</Button>
</div>
