### Which is CameraRtmpSDK

CameraRtmpSDK is an audio and video based on ffmpeg SDK, is committed to creating a cross-platform audio and video sampling, encoding, mixing, protocol upload program.
But all current creation is based on the iOS platform and CameraRtmpSDK was coded by c++.

### Blog to Introduction

[利用FFmpeg 开发音视频流（三）——将视频 YUV 格式编码成 H264](http://simplecodesky.com/2016/08/18/%E5%88%A9%E7%94%A8FFmpeg-%E5%BC%80%E5%8F%91%E9%9F%B3%E8%A7%86%E9%A2%91%E6%B5%81-3/)

[深入浅出理解视频编码H264结构](http://simplecodesky.com/2016/11/15/%E6%B7%B1%E5%85%A5%E6%B5%85%E5%87%BA%E7%90%86%E8%A7%A3%E8%A7%86%E9%A2%91%E7%BC%96%E7%A0%81H264%E7%BB%93%E6%9E%84/)

i did write a blog to introduce this project , hope it can help you to comprehend it.

### How to Use
**If you want to test Vido (H.264编码)**

```object-c
self.session = [[ABSSimpleSession alloc] initWithVideoSize:CGSizeMake(640, 480)
                                                       fps:30
                                                   bitrate:1000000
                                   useInterfaceOrientation:true
                                               cameraState:ABSCameraStateFront previewFrame:self.view.bounds];
self.session.delegate = self;
[self.view addSubview:self.session.previewView];

[self.session startVideoRecord];

// close it 
[self.session endVidoeRecord];
```

**if you want to test audio for AAC (AAC编码)**

```object-c
self.session = [[ABSSimpleSession alloc] initWithAudioSampleRate:16000 bitRate:16000
                                                      channelCount:2 encode:ABSEncodeTypeAAC];
self.session.delegate = self;
[self.session startAudioRecord];

// close it 
[self.session endAudioRecord];
```

**if you want to test audio for Opus (Opus编码)**
```
self.session = [[ABSSimpleSession alloc] initWithAudioSampleRate:16000 bitRate:16000
                                                      channelCount:2 encode:ABSEncodeTypeOpus];
self.session.delegate = self;
[self.session startAudioRecord];

// close it 
[self.session endAudioRecord];
```


**if you want to test amix（混音） of ffmpeg**
```
NSString* path1 = [[NSBundle mainBundle] pathForResource:@"audio1.wav" ofType:nil];
NSString* path2 = [[NSBundle mainBundle] pathForResource:@"audio2.wav" ofType:nil];
NSString* outputPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, true).lastObject 
stringByAppendingPathComponent:@"audio127.wav"];

const char* input1 = [path1 cStringUsingEncoding:NSUTF8StringEncoding];
const char* input2 = [path2 cStringUsingEncoding:NSUTF8StringEncoding];
const char* output = [outputPath cStringUsingEncoding:NSUTF8StringEncoding];

std::vector<std::string> inputs{std::string(input1), std::string(input2)};

PushSDK::ffmpeg::audio_mixer mixer(inputs, output);
mixer.StartMixAudio();
```

### Update
2017.11.1 Update project to runnable and and modify test API, enjoy it.

2018.1.2 Fix audio encode bug, make it encode correctly，enjoy it.

### Feature
As far as this moment, This project looks very confusing，i will take more time make it more usable. hope you can supports me, leaving you stars, Thanks.
