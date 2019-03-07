[参考视频资料:Canvas 绘制时钟](http://www.php.cn/course/253.html)



>  最近复习到Canvas,先准备来段有趣的代码，用Canvas绘制出一个动态的时钟。然后后续再对Canvas进行进一步学习。以下代码均来自以上链接所属的视频教程。 **【侵删】**



**完整代码：**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style type="text/css">
        div {
            text-align: center;
            margin-top: 250px;
        }
    </style>
</head>

<body>
    <div>
        <canvas id="clock" height="200px" width="200px">你的浏览器不支持canvas</canvas>
    </div>

    <script>
        var dom = document.getElementById('clock');
        var ctx = dom.getContext('2d');
        var width = ctx.canvas.width;
        var height = ctx.canvas.height;
        var r = width / 2;


        //绘制表盘
        function drawBackground() {
            ctx.save();
            ctx.translate(r, r);
            ctx.beginPath();
            ctx.lineWidth = 10;

            ctx.arc(0, 0, r - 5, 0, 2 * Math.PI, false);
            ctx.stroke();

            var hourNumbers = [3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 1, 2];
            ctx.font = '18px Arial';
            ctx.textAlign = 'center';

            ctx.textBaseline = 'middle';

            //小时数字
            hourNumbers.forEach(function (number, i) {
                var rad = 2 * Math.PI / 12 * i;
                var x = Math.cos(rad) * (r - 30);
                var y = Math.sin(rad) * (r - 30);
                ctx.fillText(number, x, y);
                // console.log(x)
            })

            //绘制分刻度
            for (var i = 0; i < 60; i++) {
                var rad = 2 * Math.PI / 60 * i;
                var x = Math.cos(rad) * (r - 18);
                var y = Math.sin(rad) * (r - 18);
                ctx.beginPath();
                if (i % 5 == 0) {
                    ctx.fillStyle = '#000';
                    ctx.arc(x, y, 2, 0, 2 * Math.PI, false);
                } else {
                    ctx.fillStyle = '#ccc';
                    ctx.arc(x, y, 2, 0, 2 * Math.PI, false);
                }

                ctx.fill();
            }

        }



        //绘制时针
        function drawHour(hour, minute) {
            ctx.save();
            ctx.beginPath();
            var rad = 2 * Math.PI / 12 * hour;
            var mrad = 2 * Math.PI / 12 / 60 * minute;
            ctx.rotate(rad + mrad);
            ctx.lineWidth = 6;
            ctx.lineCap = 'round';
            ctx.moveTo(0, 10);
            ctx.lineTo(0, -r / 2);
            ctx.stroke();
            ctx.restore();
        }


        //绘制分针
        function drawMinute(minute) {
            ctx.save();
            ctx.beginPath();
            var rad = 2 * Math.PI / 60 * minute;
            ctx.rotate(rad);
            ctx.lineWidth = 3;
            ctx.lineCap = 'round';
            ctx.moveTo(0, 10);
            ctx.lineTo(0, -r + 30);
            ctx.stroke();
            ctx.restore();
        }


        //绘制秒针
        function drawSecond(second) {
            ctx.save();
            ctx.beginPath();
            ctx.fillStyle = 'red'
            var rad = 2 * Math.PI / 60 * second;
            ctx.rotate(rad);
            ctx.moveTo(-2, 20);
            ctx.lineTo(2, 20);
            ctx.lineTo(1, -r + 18);
            ctx.lineTo(-1, -r + 18);
            ctx.fill();
            ctx.restore();
        }

        //绘制指针的端点
        function drawDot() {
            ctx.beginPath();
            ctx.fillStyle = 'white';
            ctx.arc(0, 0, 3, 0, 2 * Math.PI, false);
            ctx.fill();
        }

        //动起来
        function draw() {
            //清除之前所绘制的
            ctx.clearRect(0, 0, width, height);

            var now = new Date();
            var hour = now.getHours();
            var minute = now.getMinutes();
            var second = now.getSeconds();
            drawBackground();
            drawHour(hour, minute);
            drawMinute(minute);
            drawSecond(second)
            drawDot();
            ctx.restore();
        }
        //draw();

        setInterval(draw, 1000);
    </script>
</body>

</html>
```

