<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Comic Runner 🕷️</title>
<style>
  body {
    margin: 0;
    background: #f5f5dc;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    overflow: hidden;
  }
  canvas {
    border: 4px solid #000;
    background: linear-gradient(to top, #87ceeb, #ffffff);
  }
</style>
</head>
<body>
<canvas id="gameCanvas" width="600" height="200"></canvas>
<script>
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");

const player = { x: 50, y: 150, width: 30, height: 30, dy: 0, jumping: false };
const gravity = 0.7;
const jumpPower = -14; // saut un peu plus fort pour plus de réactivité

let obstacles = [];
let frame = 0;
let score = 0;
let gameOver = false;
const speed = 3; // vitesse plus lente

// Créer un obstacle
function createObstacle() {
  const height = Math.floor(Math.random() * 20) + 20;
  obstacles.push({ x: canvas.width, y: 200 - height, width: 20, height });
}

// Collision
function collision(p, o) {
  return p.x < o.x + o.width && p.x + p.width > o.x &&
         p.y < o.y + o.height && p.y + p.height > o.y;
}

// Fonction pour faire sauter l’araignée
function jump() {
  if(!player.jumping){
    player.dy = jumpPower;
    player.jumping = true;
  }
}

// Événements clavier et clic/tap
document.addEventListener("keydown", e => {
  if(e.code === "Space" || e.key === " ") jump();
});
canvas.addEventListener("click", jump);
canvas.addEventListener("touchstart", jump);

// Boucle de jeu
function update() {
  if(gameOver) return;

  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Appliquer gravité
  player.dy += gravity;
  player.y += player.dy;

  if(player.y + player.height >= 200){
    player.y = 200 - player.height;
    player.dy = 0;
    player.jumping = false;
  }

  // Dessiner le joueur avec emoji
  ctx.font = "30px Arial";
  ctx.fillText("🕷️", player.x, player.y + player.height);

  // Créer obstacles toutes les 100 frames
  if(frame % 100 === 0) createObstacle();

  // Déplacer et dessiner obstacles
  ctx.fillStyle = "green";
  for(let i = 0; i < obstacles.length; i++){
    obstacles[i].x -= speed;
    ctx.fillRect(obstacles[i].x, obstacles[i].y, obstacles[i].width, obstacles[i].height);

    if(collision(player, obstacles[i])) gameOver = true;
  }

  // Score
  score = Math.floor(frame / 10);
  ctx.fillStyle = "black";
  ctx.font = "20px Comic Sans MS";
  ctx.fillText("Score: " + score, 10, 30);

  frame++;
  if(!gameOver) requestAnimationFrame(update);
  else {
    ctx.fillStyle = "red";
    ctx.font = "40px Comic Sans MS";
    ctx.fillText("BOOM!", 220, 100);
  }
}

update();
</script>
</body>
</html>
