<template>
  <body>
    <div class="blank" />
    <div class="cube-container">

      <div class="cube initial-position">

        <img class="cube-face-image image-1" src="@/assets/Visulization/Path1.jpg">

        <img class="cube-face-image image-2" src="@/assets/Visulization/Relation1.jpg">

        <img class="cube-face-image image-3" src="@/assets/Visulization/Search1.jpg">

        <img class="cube-face-image image-4" src="@/assets/Visulization/Path1.jpg">

        <img class="cube-face-image image-5" src="@/assets/Visulization/Relation1.jpg">

        <img class="cube-face-image image-6" src="@/assets/Visulization/Search1.jpg">

      </div>

    </div>

    <h2>Click the images below to rotate the cube</h2>

    <div class="image-buttons">
      <!-- <button class="show-image-1">路径分析功能</button> -->

      <!-- <button class="show-image-2">关联分析功能</button> -->

      <!-- <button class="show-image-3">搜索查询功能</button> -->

      <button class="show-image-1"><svg><rect x="0" y="0" fill="none" width="100%" height="100%" /></svg>路径分析功能</button>

      <button class="show-image-2"><svg><rect x="0" y="0" fill="none" width="100%" height="100%" /></svg>关联分析功能</button>

      <button class="show-image-3"><svg><rect x="0" y="0" fill="none" width="100%" height="100%" /></svg>搜索查询功能</button>

      <button class="show-image-4" />

      <button class="show-image-5" />

      <button class="show-image-6" />

    </div>
  </body>
</template>
<script>
export default {
  data() {
    return {
    }
  },
  created() {
    // this.load()
  },
  mounted() {
    this.load()
  },
  methods: {
    load() {
      var cube = document.querySelector('.cube')
      var imageButtons = document.querySelector('.image-buttons')
      var cubeImageClass = cube.classList[1]
      // Add click event listener to image buttons container
      imageButtons.addEventListener('click', function(e) {
        // Get node type and class value of clicked element
        var targetNode = e.target.nodeName
        var targetClass = e.target.className
        // Check if image input has been clicked and isn't the currently shown image
        if (targetNode === 'BUTTON' && targetClass !== cubeImageClass) {
          console.log('Show Image: ' + targetClass.charAt(11))

          // Replace previous cube image class with new class
          cube.classList.replace(cubeImageClass, targetClass)

          // Update cube image class variable with new class
          cubeImageClass = targetClass
        }
      })
    }

  }
}
</script>
<style scoped>
@import url(https://fonts.googleapis.com/css?family=Montserrat:500);
:root {
	/* Base font size */
	font-size: 10px;

	/* Border color variable */
	--border-color: #e70;
}

* {
	box-sizing: border-box;
}
.blank {
  height: 100px;
}
body {
	font-family: "Montserrat", Arial, sans-serif;
	font-weight: 500;
	/* line-height: 1.5; */
	text-align: center;
	min-height: 100vh;
	/* padding: 40px 20px; */
	color: #fafafa;
	background-color: #339999;
}

.cube-container {
	position: relative;
	width: 300px;
	height: 300px;
	margin: 0px auto 100px;
	perspective: 100rem;
}

.cube {
	position: absolute;
	width: 100%;
	height: 100%;
	transform-style: preserve-3d;
	transition: transform 1s cubic-bezier(0.32, 0.05, 0.35, 1.6);
}

.cube-face-image {
	display: block;
	position: absolute;
	opacity: 0.95;
	border: 0.2rem solid rgb(11, 234, 235);
  box-shadow: rgb(11, 234, 235) 0px 0px 10px inset
	/* box-shadow: 0 0 100px #e70,
				0 0 300px var(--border-color),
				0 0 900px var(--border-color); */
}

.image-buttons {
	display: grid;
	grid-template-columns: repeat(3, auto);
	grid-gap: 1.5rem;
	justify-content: center;
}

/* .image-buttons input {
	border: 0.2rem solid #fafafa;
} */
/* .image-buttons button { */
	/* border: 5px solid #fafafa; */
/* } */

/* .image-buttons button:focus {
	outline: none;
	border: 50px solid var(--border-color);
} */
/* .image-buttons input:focus {
	outline: none;
	border: 0.2rem solid var(--border-color);
} */

/* Transform images to create cube */

.image-1 {
	transform: translateZ(190px);
}

.image-2 {
	transform: rotateX(-180deg) translateZ(190px);
}

.image-3 {
	transform: rotateY(90deg) translateZ(190px);
}

.image-4 {
	transform: rotateY(-90deg) translateZ(190px);
}

.image-5 {
	transform: rotateX(90deg) translateZ(190px);
}

.image-6 {
	transform: rotateX(-90deg) translateZ(190px);
}

/* Transform cube to show correct image */

.cube.initial-position {
	transform: translateZ(-190px) translateY(-100px) rotateX(-15deg) rotateY(18deg) rotateZ(2deg);
}

.cube.show-image-1 {
	transform: translateZ(-190px);
}

.cube.show-image-2 {
	transform: translateZ(-190px) rotateX(180deg);
}

.cube.show-image-3 {
	transform: translateZ(-190px) rotateY(-90deg);
}

.cube.show-image-4 {
	transform: translateZ(-190px) rotateY(90deg);
}

.cube.show-image-5 {
	transform: translateZ(-190px) rotateX(-90deg);
}

.cube.show-image-6 {
	transform: translateZ(-190px) rotateX(90deg);
}
.show-image-1 {
  /* visibility:hidden */
  color: #fff;
  cursor: pointer;
  font-size: 18px;
  /* font-weight: 400; */
  line-height: 45px;
  margin: 0 0 2em;
  max-width: 350px;
  position: relative;
  text-decoration: none;
  text-transform: uppercase;
  width: 100%;
  background: #336699;
  font-weight: bold;
}
.show-image-1:hover {
  text-decoration: none;
   background: rgba(225, 51, 45, 0);
  font-weight: 900;
  letter-spacing: 1px;
}
.show-image-1 svg {
  height: 45px;
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
}
.show-image-1 rect {
  fill: none;
  stroke: #fff;
  stroke-width: 2;
  stroke-dasharray: 422, 0;
  transition: all 0.35s linear;
}
.show-image-1:hover rect {
  stroke-width: 5;
  stroke-dasharray: 15, 310;
  stroke-dashoffset: 48;
  transition: all 1.35s cubic-bezier(0.19, 1, 0.22, 1);
}
.show-image-2 {
  /* visibility:hidden */
  color: #fff;
  cursor: pointer;
  font-size: 18px;
  /* font-weight: 400; */
  line-height: 45px;
  margin: 0 0 2em;
  max-width: 350px;
  position: relative;
  text-decoration: none;
  text-transform: uppercase;
  width: 100%;
  background: #336699;
  font-weight: bold;
}
.show-image-2:hover {
  text-decoration: none;
   background: rgba(225, 51, 45, 0);
  font-weight: 900;
  letter-spacing: 1px;
}
.show-image-2 svg {
  height: 45px;
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
}
.show-image-2 rect {
  fill: none;
  stroke: #fff;
  stroke-width: 2;
  stroke-dasharray: 422, 0;
  transition: all 0.35s linear;
}
.show-image-2:hover rect {
  stroke-width: 5;
  stroke-dasharray: 15, 310;
  stroke-dashoffset: 48;
  transition: all 1.35s cubic-bezier(0.19, 1, 0.22, 1);
}
.show-image-3 {
  /* visibility:hidden */
  color: #fff;
  cursor: pointer;
  font-size: 18px;
  /* font-weight: 400; */
  line-height: 45px;
  margin: 0 0 2em;
  max-width: 350px;
  position: relative;
  text-decoration: none;
  text-transform: uppercase;
  width: 100%;
  background: #336699;
  font-weight: bold;
}
.show-image-3:hover {
  text-decoration: none;
   background: rgba(225, 51, 45, 0);
  font-weight: 900;
  letter-spacing: 1px;
}
.show-image-3 svg {
  height: 45px;
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
}
.show-image-3 rect {
  fill: none;
  stroke: #fff;
  stroke-width: 2;
  stroke-dasharray: 422, 0;
  transition: all 0.35s linear;
}
.show-image-3:hover rect {
  stroke-width: 5;
  stroke-dasharray: 15, 310;
  stroke-dashoffset: 48;
  transition: all 1.35s cubic-bezier(0.19, 1, 0.22, 1);
}
.show-image-4 {
  visibility:hidden
}
.show-image-5 {
  visibility:hidden
}
.show-image-6 {
  visibility:hidden
}
/* .show-image-4 {
  color: #fff;
  font-size: 18px;
  line-height: 45px;
  max-width: 300px;
  position: relative;
  text-decoration: none;
  text-transform: uppercase;
  width: 100%;
  background: #336699;
  font-weight: bold;
}
.show-image-4:hover {
  text-decoration: none;
   background: rgba(225, 51, 45, 0);
  font-weight: 900;
  letter-spacing: 1px;
}
.show-image-4 svg {
  pointer-events:none;
  height: 45px;
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
}
.show-image-4 rect {
  fill: none;
  stroke: #fff;
  stroke-width: 2;
  stroke-dasharray: 422, 0;
  transition: all 0.35s linear;
}
.show-image-4:hover rect {
  stroke-width: 5;
  stroke-dasharray: 15, 310;
  stroke-dashoffset: 48;
  transition: all 1.35s cubic-bezier(0.19, 1, 0.22, 1);
} */
/* html,body,div,span,applet,object,iframe,h1,h2,h3,h4,h5,h6,p,blockquote,pre,a,abbr,acronym,address,big,cite,code,del,dfn,em,img,ins,kbd,q,s,samp,small,strike,strong,sub,sup,tt,var,b,u,i,center,dl,dt,dd,ol,ul,li,fieldset,form,label,legend,table,caption,tbody,tfoot,thead,tr,th,td,article,aside,canvas,details,embed,figure,figcaption,footer,header,hgroup,menu,nav,output,ruby,section,summary,time,mark,audio,video{margin:0;padding:0;border:0;font-size:100%;font:inherit;vertical-align:baseline}article,aside,details,figcaption,figure,footer,header,hgroup,menu,nav,section{display:block}body{line-height:1}ol,ul{list-style:none}blockquote,q{quotes:none}blockquote:before,blockquote:after,q:before,q:after{content:'';content:none}table{border-collapse:collapse;border-spacing:0} */
</style>

