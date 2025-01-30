<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>微信版-飞翔的小鸟</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            touch-action: none; /* 禁止手机缩放 */
        }
        #game {
            width: 100%;
            height: 100vh;
            background: skyblue;
            position: relative;
        }
        #bird {
            width: 40px;
            height: 40px;
            position: absolute;
            left: 100px;
            background: url('https://img.icons8.com/color/48/bird.png') center/cover;
        }
        .pipe {
            width: 60px;
            background: green;
            position: absolute;
        }
        #score {
            position: fixed;
            top: 20px;
            left: 20px;
            font-size: 24px;
            color: white;
            font-family: Arial;
        }
    </style>
</head>
<body>
    <div id="game">
        <div id="bird"></div>
        <div id="score">0</div>
    </div>

    <script>
        const bird = document.getElementById('bird');
        const game = document.getElementById('game');
        const scoreElement = document.getElementById('score');
        let birdY = 200; // 初始位置
        let velocity = 0; // 小鸟下落速度
        let score = 0;
        let isGameOver = false;

        // 触屏/鼠标点击控制跳跃
        document.addEventListener('touchstart', jump);
        document.addEventListener('mousedown', jump);

        function jump() {
            if (isGameOver) return;
            velocity = -10; // 点击后小鸟向上跳
        }

        // 游戏主循环
        function gameLoop() {
            if (isGameOver) return;

            // 更新小鸟位置
            velocity += 0.5; // 模拟重力
            birdY += velocity;
            bird.style.top = birdY + 'px';

            // 碰撞检测（简化版）
            if (birdY < 0 || birdY > game.clientHeight - 40) {
                gameOver();
            }

            requestAnimationFrame(gameLoop);
        }

        function gameOver() {
            isGameOver = true;
            alert('游戏结束！得分：' + score);
            location.reload(); // 刷新页面重新开始
        }

        // 开始游戏
        gameLoop();
    </script>
</body>
</html>
