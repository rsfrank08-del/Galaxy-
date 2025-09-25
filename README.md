```html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Galaxia de Amor</title>
<style>
  body, html {
    margin: 0; padding: 0; overflow: hidden; background: black;
    height: 100vh; display: flex; justify-content: center; align-items: center;
    color: white; font-family: Arial, sans-serif;
  }
  canvas {
    display: block;
  }
</style>
</head>
<body>
<canvas id="galaxy"></canvas>

<script>
const canvas = document.getElementById('galaxy');
const ctx = canvas.getContext('2d');
let width, height;

function resize() {
  width = window.innerWidth;
  height = window.innerHeight;
  canvas.width = width;
  canvas.height = height;
}
resize();
window.addEventListener('resize', resize);

class Heart {
  constructor() {
    this.reset();
  }
  reset() {
    this.x = Math.random() * width;
    this.y = Math.random() * height;
    this.size = 5 + Math.random() * 10;
    this.speed = 0.5 + Math.random();
    this.angle = Math.random() * 2 * Math.PI;
    this.orbitRadius = 50 + Math.random() * 150;
    this.centerX = width / 2;
    this.centerY = height / 2;
  }
  update() {
    this.angle += this.speed * 0.01;
    this.x = this.centerX + this.orbitRadius * Math.cos(this.angle);
    this.y = this.centerY + this.orbitRadius * Math.sin(this.angle);
  }
  draw() {
    ctx.fillStyle = 'pink';
    ctx.beginPath();
    // Dibujar pequeño corazón (simplificado con un path)
    ctx.moveTo(this.x, this.y);
    ctx.bezierCurveTo(this.x - this.size / 2, this.y - this.size / 2,
                      this.x - this.size, this.y + this.size / 3,
                      this.x, this.y + this.size);
    ctx.bezierCurveTo(this.x + this.size, this.y + this.size / 3,
                      this.x + this.size / 2, this.y - this.size / 2,
                      this.x, this.y);
    ctx.fill();
  }
}

const hearts = [];
for(let i=0; i<40; i++){
  hearts.push(new Heart());
}

function animate() {
  ctx.clearRect(0, 0, width, height);
  hearts.forEach(h => {
    h.update();
    h.draw();
  });
  requestAnimationFrame(animate);
}
animate();
</script>
</body>
</html>
```
