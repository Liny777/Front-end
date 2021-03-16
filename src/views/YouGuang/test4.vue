<template>
  <body>
    <!-- partial:index.partial.html -->
    <section class="buttons">
      <h1>CSS3鼠标滑过按钮动画</h1>
      <div class="container">

        <a href="#" class="btn btn-1">
          <svg>
            <rect x="0" y="0" fill="none" width="100%" height="100%" />
          </svg>
          路径分析功能
        </a>
      </div>
    </section>

  </body>

</template>
<script>
export default {
}
</script>
<style scoped>
@import url(https://fonts.googleapis.com/css?family=Roboto:400,100,900);
* {
  box-sizing: inherit;
  transition-property: all;
  transition-duration: 0.6s;
  transition-timing-function: ease;
}

html,
body {
  box-sizing: border-box;
  height: 100%;
  width: 100%;
}

body {
  background: #E1332D;
  font-family: "Roboto", sans-serif;
  font-weight: 400;
}

.buttons {
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content: center;
  text-align: center;
  width: 100%;
}

.container {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 1em;
  text-align: center;
}
@media (min-width: 600px) {
  .container {
    flex-direction: row;
    justify-content: space-between;
  }
}

h1 {
  color: #fff;
  font-size: 1.25em;
  font-weight: 900;
  margin: 0 0 2em;
}
@media (min-width: 450px) {
  h1 {
    font-size: 1.75em;
  }
}
@media (min-width: 760px) {
  h1 {
    font-size: 3.25em;
  }
}
@media (min-width: 900px) {
  h1 {
    font-size: 5.25em;
    margin: 0 0 1em;
  }
}

p {
  color: #fff;
  font-size: 12px;
}
@media (min-width: 600px) {
  p {
    left: 50%;
    position: absolute;
    transform: translate(-50%, 0);
    top: 90%;
  }
}
@media (max-height: 500px) {
  p {
    left: 0;
    position: relative;
    top: 0;
    transform: translate(0, 0);
  }
}
p a {
  background: rgba(255, 255, 255, 0);
  border-bottom: 1px solid;
  color: #fff;
  line-height: 1.4;
  padding: 0.25em;
  text-decoration: none;
}
p a:hover {
  background: white;
  color: #E1332D;
}

.btn {
  color: #fff;
  cursor: pointer;
  font-size: 16px;
  font-weight: 400;
  line-height: 45px;
  margin: 0 0 2em;
  max-width: 160px;
  position: relative;
  text-decoration: none;
  text-transform: uppercase;
  width: 100%;
}
@media (min-width: 600px) {
  .btn {
    margin: 0 1em 2em;
  }
}
.btn:hover {
  text-decoration: none;
}

.btn-1 {
  background: #e02c26;
  font-weight: 100;
}
.btn-1 svg {
  height: 45px;
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
}
.btn-1 rect {
  fill: none;
  stroke: #fff;
  stroke-width: 2;
  stroke-dasharray: 422, 0;
  transition: all 0.35s linear;
}

.btn-1:hover {
  background: rgba(225, 51, 45, 0);
  font-weight: 900;
  letter-spacing: 1px;
}
.btn-1:hover rect {
  stroke-width: 5;
  stroke-dasharray: 15, 310;
  stroke-dashoffset: 48;
  transition: all 1.35s cubic-bezier(0.19, 1, 0.22, 1);
}
</style>
