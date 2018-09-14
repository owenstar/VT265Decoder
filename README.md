# H265硬解码


自己项目中使用的VT265硬解，针对裸流数据，几句代码就可以搞定，不需要再百度、Google了，需要源码的朋友加微信 nihuo2016

## 使用方法：

#### 判断是否支持硬解HEVC 

#### 调用解码的方法，如果需要截图，传YES，图片会通过代理回调出来，请在主线程刷新图片;


```
typedef struct VTDecodeData{
    unsigned int  decodeStatus;   //解码状态
    unsigned int  uiChannelID;    //[out] 通道ID，用于标识通道信息
    unsigned int  uiDecWidth;    // 解码宽
    unsigned int  uiDecHeight;   //解码高
    unsigned int  uiYStride;     // Y数据大小
    unsigned int  uiUVStride;    // UV数据大小
    unsigned char *pucOutYUV;   // YUV地址
}VTDecodeData_t;


@protocol VTDecoderDelegate<NSObject>
-(void)screenShotImage:(UIImage *)image;
@end

@interface VTDecoder : NSObject
@property (nonatomic,assign) id<VTDecoderDelegate>  delegate;

/**
 是否支持硬解码

 @return YES NO
 */
-(BOOL)supportVTDecode;

/**
 解码视频帧

 @param data 数据流
 @param size 大小
 @param shot 是否截图
 */
-(VTDecodeData_t)decodeData:(uint8_t*)data size:(uint32_t)size channel:(uint32_t)channel screenShot:(BOOL)shot;

/**
 销毁
 */
-(void)destory;
@end


```
