# kotlin轮播，重叠1秒
```
    class LoopMediaPlayer(context: Context, resId: Int) {

        private val mediaPlayer1: MediaPlayer = MediaPlayer.create(context, resId)
        private val mediaPlayer2: MediaPlayer = MediaPlayer.create(context, resId)

        private var isPlaying = false
        private var currentPlayer = mediaPlayer1
        private val timer = Timer()
        fun start() {
            if (isPlaying) {
                return
            }

            isPlaying = true


            timer.schedule(object : TimerTask() {
                override fun run() {
                    currentPlayer.stop()
                    currentPlayer =
                        if (currentPlayer == mediaPlayer1) mediaPlayer2 else mediaPlayer1
                    currentPlayer.start()
                }
            }, 0, mediaPlayer1.duration - 1000L)
        }

        fun stop() {
            if (!isPlaying) {
                return
            }
            timer.cancel()
            currentPlayer.stop()
            isPlaying = false
        }
    }
```
