arecord | aplay 
arecord 录音
aplay 播放

查看播放设备: aplay -l
查看录音设备: arecord -l


首先说一下alsa的配置文件。alsa的配置文件是alsa.conf位于/usr/share/alsa目录下，通常还有/usr/share/alsa/card和/usr/share/alsa/pcm两个子目录用来设置card相关的参数，别名以及一些PCM默认设置。以上配置文件，我等凡夫从不用修改，修改它们是大神的工作。
还有两个配置文件/etc/asound.conf和~/.asoundrc，它俩有效是因为它俩被alsa.conf引用
asound.conf示例

pcm.!default {
    type asym
    playback.pcm "playback" 播放
    capture.pcm "ac108" 录音
}

pcm.playback {
    type plug
    slave.pcm "hw:1,0" #参数说明 hw:1,0 第一个参数1是指你的声卡ID,第二个参数0,是声卡的子设备id
#    slave.pcm "hw:ALSA"
}

# pcm.dmixed {
#     type dmix
#     slave.pcm "hw:0,0"
#     ipc_key 555555 
# }

pcm.ac108 {
    type plug
    slave.pcm "hw:seeed4micvoicec"
}
