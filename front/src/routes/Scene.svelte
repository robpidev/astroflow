<script lang="ts">
	import { T, useTask } from '@threlte/core';
	import {
		CameraControls,
		MeshLineMaterial,
		Grid,
		MeshLineGeometry,
		type CameraControlsRef
	} from '@threlte/extras';
	import { Spring } from 'svelte/motion';
	import { Mesh, Vector3 } from 'three';

	const scale = new Spring(1);

	let t = 0;
	let x = $state(0);
	let y = $state(0);
	let z = $state(0);

	const points: Vector3[] = $state([]);

	let {
		controls = $bindable()
	}: {
		controls?: CameraControlsRef;
	} = $props();

	useTask((delta) => {
		t += delta;
		x = Math.cos(t) * 10;
		y = Math.sin(t) * 5;
		// z = Math.sin(t) * 5;

		points.push(new Vector3(x, z, -y));
		if (points.length > 150) {
			points.shift();
		}
	});
</script>

<T.PerspectiveCamera makeDefault>
	<CameraControls
		bind:ref={controls}
		oncreate={(ref) => {
			ref.setPosition(5, 5, 5);
		}}
	/>
</T.PerspectiveCamera>

<T.DirectionalLight position={[-1, 10, 0]} />
<T.AmbientLight intensity={-1.5} />
<T.Mesh position={[x, z, -y]}>
	<T.BoxGeometry />
	<T.MeshBasicMaterial color="hotpink" />
</T.Mesh>
<Grid></Grid>

<!-- Trayectory -->
<T.Mesh position={[0, 0, 0]}>
	<MeshLineGeometry {points} shapeFunction={(p) => 1 - p} />
	<MeshLineMaterial width={0.05} color="#fe3d00" />
</T.Mesh>
