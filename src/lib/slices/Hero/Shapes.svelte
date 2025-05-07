<script lang='ts'>
    import { T as Threlte } from "@threlte/core";
    import * as THREE from 'three';
    import Geometry from './Geometry.svelte';
    import { ContactShadows, Environment, interactivity, transitions } from '@threlte/extras';

    interactivity();
    transitions();
</script>

<Threlte.PerspectiveCamera
    makeDefault
    position={[0,0,25]}
    aspect={1}
    fov={30}
    near={1}
    far={40}
/>

<Threlte.DirectionalLight position = {[0, 10, 30]} intensity={2}></Threlte.DirectionalLight>
<ContactShadows position={[0, -3.5, 0]} opacity={0.65} scale={40} blur={1} far={9} />

<Environment files="smallroom.hdr" path="/" format="hdr" />

<!-- Icosahedron -->
<Geometry 
    position={[0, 0, 0,]} 
    rate={0.3} 
    geometry={new THREE.IcosahedronGeometry(3)}
/>

<!-- Dodecahedron -->
<Geometry 
    position={[1, -0.75, 4]} 
    rate={0.4} 
    geometry={new THREE.DodecahedronGeometry(1)}
/>

<!-- Octahedron -->
<Geometry 
    position={[-1.4, 2, -4]} 
    rate={0.6} 
    geometry={new THREE.OctahedronGeometry(1)}
/>

<!-- Torus -->
<Geometry 
    position={[-.8, -0.75, 5]} 
    rate={0.6} 
    geometry={new THREE.TorusGeometry(0.6, 0.25, 16, 32)}
/>

<!-- Icosahedron -->
<Geometry 
    position={[1.6, 1.6, -4]} 
    rate={0.7} 
    geometry={new THREE.TetrahedronGeometry(1.5)}
/>