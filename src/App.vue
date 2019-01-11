<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div id="section_0" class="section">
      <div id="section_0-card_0" class="card">

      </div>
    </div>
  </div>
</template>

<script>
import interact from 'interactjs';
// import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'app',
  // components: {
  //   HelloWorld,
  // },
};

document.addEventListener('DOMContentLoaded', () => {
  let x = 0;
  let y = 0;

  interact('.card').draggable(
    {
      origin: 'parent',
      snap: {
        targets: [
          interact.createSnapGrid({
            x: 200,
            y: 250,
          }),
        ],
        range: 200,
        relativePoints: [{ x: 0, y: 0 }],
        endOnly: true,
      },
      inertia: true,
      restrict: {
        restriction: 'parent',
        elementRect: {
          top: 0,
          left: 0,
          bottom: 1,
          right: 1,
        },
        endOnly: true,
      },
    },
  ).resizable({
    snapSize: {
      targets: [
        interact.createSnapGrid({
          x: 200,
          y: 250,
        }),
      ],
      range: 200,
      relativePoints: [{ x: 0, y: 0 }],
      endOnly: true,
    },
    edges: {
      left: true,
      right: true,
      bottom: true,
      top: true,
    },
    restrictSize: {
      min: { width: 200, height: 250 },
    },
    restrictEdges: {
      outer: 'parent',
      endOnly: true,
    },
  }).on('resizemove', (event) => {
    console.log('resizemove');
    const { target } = event;
    x = (parseFloat(target.getAttribute('data-x')) || 0);
    y = (parseFloat(target.getAttribute('data-y')) || 0);

    target.style.width = `${event.rect.width}px`;
    target.style.height = `${event.rect.height}px`;

    x += event.deltaRect.left;
    y += event.deltaRect.top;

    target.style.webkitTransform = `translate(${x}px, ${y}px)`;
    target.style.transform = `translate(${x}px, ${y}px)`;

    target.setAttribute('data-x', x);
    target.setAttribute('data-y', y);
  }).on('dragmove', (event) => {
    const { target } = event;
    x = (parseFloat(target.getAttribute('data-x')) || 0) + event.dx;
    y = (parseFloat(target.getAttribute('data-y')) || 0) + event.dy;

    target.style.webkitTransform = `translate(${x}px, ${y}px)`;
    target.style.transform = `translate(${x}px, ${y}px)`;

    target.setAttribute('data-x', x);
    target.setAttribute('data-y', y);
  });
});

</script>

<style lang="scss">

$teal: #576C6E;
$blue: #1B293D;
$grey: #505050;
$light-teal: rgba($teal, .4);
$light-blue: rgba($blue, .4);


body {
  margin: 0;
}

#app {
  background-color: ghostwhite;
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
}

.section {
  width: 800px;
  height: 500px;
  background-color: $light-teal;
}

.card {
  width: 200px;
  height: 250px;
  background-color: $light-blue;
  user-select: none;
  -webkit-transform: translate(0px, 0px);
          transform: translate(0px, 0px);
}

</style>
