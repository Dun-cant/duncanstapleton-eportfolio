<script lang='ts'>
	import { T as Threlte } from '@threlte/core';
    import { Float, createTransition } from '@threlte/extras';
    import * as THREE from 'three';
    import gsap from 'gsap';
    import { elasticOut } from 'svelte/easing';

    export let position: [number, number, number] = [0,0,0];
    export let geometry: THREE.BufferGeometry = new THREE.IcosahedronGeometry(3);
    export let rate = 0.5;

    const soundeEffects = [
        new Audio('/sounds/hit1.ogg'),
        new Audio('/sounds/hit2.ogg'),
        new Audio('/sounds/hit3.ogg'),
    ]

    let visable = false;

    const material = new THREE.MeshStandardMaterial();

	const materialParams = [
		{ color: 0xff0000, roughness: 0 },
		{ color: 0xffa500, roughness: 0.4 },
		// { color: 0xffff00, roughness: 0.1 },
		{ color: 0x008000, roughness: 0.1 },
		{ color: 0x0000ff, roughness: 0.1 },
		{ color: 0x4b0082, roughness: 0, metalness: 0.5 },
		{ color: 0xee82ee, roughness: 0.1, metalness: 0.5 }
	];

    function getRandomMaterial(){
        return new THREE.MeshStandardMaterial(gsap.utils.random(materialParams));
    }

    function handleClick(event: MouseEvent) {
        gsap.utils.random(soundeEffects).play();
        if('object' in event && event.object instanceof THREE.Mesh) {
            gsap.to(event.object.rotation, {
                x: `+=${gsap.utils.random(0, 3)}`,
                y: `+=${gsap.utils.random(0, 3)}`,
                z: `+=${gsap.utils.random(0, 3)}`,
                duration: 1.3,
                ease: 'elastic.out(.7,0.3)',
                yoyo: true

            })
            
            event.object.material = getRandomMaterial();
        }
    }

    const bounce = createTransition((ref) => {
        return {
            tick(t) {
                if (t > 0) visable = true;
                ref.scale.set(t, t, t)
            },
            easing: elasticOut,
            duration: gsap.utils.random(800, 1200),
            delay: gsap.utils.random(0,500)
        }
    })

</script>

<Threlte.Group position={position.map((p) => p *2)}>
    <Float 
        speed={5 * rate} 
        rotationSpeed={5 * rate} 
        rotationIntensity={6 * rate} 
        floatIntensity={5 * rate}
    >
        <Threlte.Mesh 
            {visable} 
            {geometry} 
            in={bounce}
            material={getRandomMaterial()}
            interactive
            on:click={handleClick}
        ></Threlte.Mesh>
    </Float>
</Threlte.Group>