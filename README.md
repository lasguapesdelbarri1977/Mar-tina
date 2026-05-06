<!DOCTYPE html>
<html>
<body style="margin:0; background:black;">
<canvas id="c"></canvas>

<script>
let canvas = document.getElementById("c");
let ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let particulas = [];
let T = 1;

for (let i = 0; i < 50; i++) {
    particulas.push({
        x: Math.random()*canvas.width,
        y: Math.random()*canvas.height,
        vx: Math.random()*4-2,
        vy: Math.random()*4-2
    });
}

function loop(){
    ctx.fillStyle = "black";
    ctx.fillRect(0,0,canvas.width,canvas.height);

    for (let p of particulas){
        p.x += p.vx * T;
        p.y += p.vy * T;

        if (p.x < 0 || p.x > canvas.width) p.vx *= -1;
        if (p.y < 0 || p.y > canvas.height) p.vy *= -1;

        ctx.fillStyle = "white";
        ctx.beginPath();
        ctx.arc(p.x,p.y,3,0,Math.PI*2);
        ctx.fill();
    }

    requestAnimationFrame(loop);
}

loop();

// controles
window.addEventListener("keydown", e=>{
    if (e.key === "ArrowUp") T += 0.2;
    if (e.key === "ArrowDown") T -= 0.2;
});
</script>
</body>
</html>
