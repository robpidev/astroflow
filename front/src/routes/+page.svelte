<script lang="ts">
	import Scene from './Scene.svelte';
	import { Canvas } from '@threlte/core';

	import { type CameraControlsRef } from '@threlte/extras';
	import Controls from './Controls.svelte';

	let controls = $state.raw<CameraControlsRef>();
</script>

<Canvas>
	<Scene bind:controls />
</Canvas>
<!---->
<!-- <div> -->
<!-- </div> -->
<Controls bind:controls />
