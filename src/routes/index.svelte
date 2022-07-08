<script>
  import * as SC from "svelte-cubed";
  import * as THREE from "three";

  let width = 1;
  let height = 1;
  let depth = 1;

  let spin = 0;

  SC.onFrame(() => {
    spin += 0.01;
  });
</script>

<h1>why is there cube???????</h1>

<SC.Canvas
  antialias
  background={new THREE.Color("white")}
  fog={new THREE.FogExp2("white", 0.1)}
  shadows
>
  <SC.Group position={[0, -height / 2, 0]}>
    <SC.Mesh
      geometry={new THREE.PlaneGeometry(50, 50)}
      material={new THREE.MeshStandardMaterial({ color: "black" })}
      rotation={[-Math.PI / 2, 0, 0]}
      receiveShadow
    />
    <SC.Primitive
      object={new THREE.GridHelper(50, 50, "gray", "gray")}
      position={[0, 0.001, 0]}
    />
  </SC.Group>

  <SC.Mesh
    geometry={new THREE.BoxGeometry()}
    material={new THREE.MeshStandardMaterial({ color: "white" })}
    scale={[width, height, depth]}
    rotation={[0, spin, 0]}
    castShadow
  />

  <SC.PerspectiveCamera position={[1, 1, 3]} />
  <SC.OrbitControls enableZoom={false} maxPolarAngle={Math.PI * 0.51} />
  <SC.AmbientLight intensity={0.4} />
  <SC.DirectionalLight
    intensity={0.6}
    position={[-2, 3, 2]}
    shadow={{ mapSize: [2048, 2048] }}
  />
</SC.Canvas>

<style>
  h1 {
    position: absolute;
    top: 10px;
    width: 100%;
    text-align: center;
    z-index: 100;
    display: block;
  }
</style>
