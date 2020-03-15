# プレイヤー

## hls.jsを利用したWeb版プレイヤー

`player.html`

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <meta charset="utf-8">
    <title>Live streaming player(HLS) - Demo</title>
</head>
<body>
<h1>PC/Android</h1>

<script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
<video id="video" crossorigin controls></video>
<script>
    if (Hls.isSupported()) {
        var video = document.getElementById('video');
        var hls = new Hls();
        hls.loadSource('https://*****/*****.m3u8' + query);
        hls.attachMedia(video);
        hls.on(Hls.Events.MANIFEST_PARSED, function () {
            video.play();
        });
    }
</script>

<script>
    function back() {
        let video = document.getElementById('video');
        video.currentTime = video.currentTime - 10;
        video.addEventListener("canplaythrough", function () {
            video.play();
        }, false);
    }

    function forward() {
        let video = document.getElementById('video');
        video.currentTime = video.currentTime + 10;
        video.addEventListener("canplaythrough", function () {
            video.play();
        }, false);
    }

    function pause() {
        let video = document.getElementById('video');
        video.pause();
    }

    function play() {
        let video = document.getElementById('video');
        video.addEventListener("canplaythrough", function () {
            video.play();
        }, false);
    }
</script>

<button onclick="back()">←</button>
<button onclick="forward()">→</button>
<button onclick="pause()">■</button>
<button onclick="play()">Play</button>

<script>
    document.getElementById("video").width = window.parent.screen.width;
</script>

</body>
</html>

```

