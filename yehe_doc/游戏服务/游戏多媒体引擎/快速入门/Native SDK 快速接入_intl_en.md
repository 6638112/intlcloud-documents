This document provides a detailed description that makes it easy for Native project developers to debug and integrate the APIs for Game Multimedia Engine (GME).

This document only provides the main APIs to help you get started with GME to debug and integrate the APIs.

## Key Considerations for Using GME

GME provides two services: Voice chat service and voice messaging and speech-to-text service, both of which rely on key APIs such as Init and Poll.

<dx-alert infotype="notice" title="Note on Init API">
If you need to use voice chat and voice messaging services at the same time, **you only need to call `Init` API once**.
</dx-alert>

### API call flowchart

![image](https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg)

### Directions

#### Core APIs


<dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
<dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>

#### Voice Chat

<dx-steps>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Entering a voice chat room</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Turning on or off the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Turning on or off the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exiting a voice room</dx-tag-link>
</dx-steps>

#### Voice Message

<dx-steps>
-<dx-tag-link link="#ApplyPtt" tag="API: ApplyPTTAuthbuffer">Initializing authentication</dx-tag-link>
-<dx-tag-link link="#StartRWSR" tag="API: StartRecordingWithStreamingRecognition">Starting streaming speech recognition</dx-tag-link>
-<dx-tag-link link="#Stop" tag="API: StopRecording">Stop recording</dx-tag-link>
</dx-steps>

- <dx-tag-link link="#Init" tag="API: UnInit">Uninitializing GME</dx-tag-link>

## Core API Integration

### 1. Download the SDK 

On the SDK download guide page, download the appropriate <dx-tag-link link="https://intl.cloud.tencent.com/document/product/607/18521" tag="DownLoad">client SDK</dx-tag-link>.


### 2. Importing the header file

<dx-codeblock>
::: Java Java
import com.tencent.TMG.ITMGContext;
import com.tencent.av.sig.AuthBuffer;
import com.tencent.bugly.crashreport.CrashReport;
:::
::: Object-C objetctive-c
#import "GMESDK/TMGEngine.h"
#import "GMESDK/QAVAuthBuffer.h"
:::
::: C++ C++
#include "auth_buffer.h"
#include "tmg_sdk.h"
#include "AdvanceHeaders/tmg_sdk_adv.h"
#include <vector>
:::
</dx-codeblock>


### 3. Getting singleton

To use the voice feature, get the `ITMGContext` object first.

#### Function prototype 

<dx-codeblock>
::: Java Java
public static ITMGContext GetInstance(Context context)
:::
::: Object-C objetctive-c

+ (ITMGContext*) GetInstance;
  :::
  ::: C++ C++
  __UNUSED static ITMGContext* ITMGContextGetInstance(){
  return ITMGContextGetInstanceInner(TMG_SDK_VERSION);
  }
  :::
  </dx-codeblock>

#### Sample code  


<dx-codeblock>
::: Java Java
//MainActivity.java
import com.tencent.TMG.ITMGContext; 
ITMGContext tmgContext = ITMGContext.GetInstance(this);
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
ITMGContext* _context = [ITMGContext GetInstance];
:::
::: C++ C++
ITMGContext* context = ITMGContextGetInstance();
:::
</dx-codeblock>

### 4. Setting callback

The API class uses the `Delegate` method to send callback notifications to the application. Register the callback function to the SDK for receiving callback messages before room entry.

#### Function prototype and sample code

Register the callback function to the SDK for receiving callback messages before room entry.

<dx-codeblock>
::: Java Java
//ITMGContext
public abstract int SetTMGDelegate(ITMGDelegate delegate);

//MainActivity.java
tmgContext.SetTMGDelegate(TMGCallbackDispatcher.getInstance());
:::
::: Object-C objetctive-c
ITMGDelegate < NSObject >

//TMGSampleViewController.m
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate = [DispatchCenter getInstance];
:::
::: C++ C++
// When initializing the SDK
m_pTmgContext = ITMGContextGetInstance();
m_pTmgContext->SetTMGDelegate(this);
// In the destructor
CTMGSDK_For_AudioDlg::~CTMGSDK_For_AudioDlg()
{
    ITMGContextGetInstance()->SetTMGDelegate(NULL);
}
:::
</dx-codeblock>

#### Callback examples  

Override this callback function in the constructor to process the parameters of the callback.


<dx-codeblock>
::: Java Java
//MainActivity.java
tmgContext.SetTMGDelegate(TMGCallbackDispatcher.getInstance());

//RealTimeVoiceActivity.java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
        if (type == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
		{
			// Processing callbacks
		}
}

// Refer to TMGCallbackDispatcher.java, TMGCallbackHelper.java, and TMGDispatcherBase.java
:::
::: Object-C Object-C
//TMGRealTimeViewController.m
TMGRealTimeViewController ()< ITMGDelegate >


- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
  NSString *log = [NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
  [self showLog:log];
  NSLog(@"====%@====", log);
  switch (eventType) {
      // Step 6/11 : Perform the enter room event
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM: {
          int result = ((NSNumber *)[data objectForKey:@"result"]).intValue;
          NSString *error_info = [data objectForKey:@"error_info"];

          [self showLog:[NSString stringWithFormat:@"OnEnterRoomComplete:%d msg:(%@)", result, error_info]];
      
          if (result == 0) {
              [self updateStatusEnterRoom:YES];
          }
      }
      break;

  }
  }

// Refer to DispatchCenter.h and DispatchCenter.m
:::
::: C++ C++
// Declaration in the header file
virtual void OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data);
// Sample code
void CTMGSDK_For_AudioDlg::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data)
{
    switch(eventType)
    {
    case ITMG_MAIN_EVENT_TYPE_XXXX_XXXX:
        {
            // Process the callback
        }
        break;
    }
}
:::
</dx-codeblock>


| Parameter | Type | Description |
| ---- | :------------------------------: | ------------------------ |
| type | ITMGContext.ITMG_MAIN_EVENT_TYPE | Event type in the callback response |
| data | Intent message type | Callback message, i.e., event data |

### [5. Initializing SDK](id:Init)

**You need to initialize the SDK through the `Init` API** before you can use the real-time voice, voice message, and speech-to-text services. The `Init` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.

#### API prototype

<dx-codeblock>
::: Java Java
public abstract int Init(String sdkAppId, String openId);
:::
::: Object-C objetctive-c
-(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID;
:::
::: C++ C++
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
:::
</dx-codeblock>


| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | `AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme), which can be obtained as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782). |
| openID   | string | `openID` can only be in `Int64` type, which is passed in after being converted to a string. You can customize its rules, and it must be unique in the application. To pass in `openID` as a string, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application. |

#### Sample code 

<dx-codeblock>
::: Java Java
//MainActivity.java
int nRet = tmgContext.Init(appId, openId);
if (nRet == AV_OK )
{
    GMEAuthBufferHelper.getInstance().setGEMParams(appId, key, openId);
    // Step 4/11: Poll to trigger callback
    //https://www.tencentcloud.com/document/product/607/40860
    EnginePollHelper.createEnginePollHelper();
    showToast("Init success");
}else if (nRet == AV_ERR_HAS_IN_THE_STATE) // SDK has been initialized. This operation is successful.
{
    showToast("Init success");
}else
{
    showToast("Init error errorCode:" + nRet);
}
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
QAVResult result = [_context InitEngine:self.appIDTF.text openID:self.openIDTF.text];
if (result == QAV_OK) {
    self.isSDKInit = YES;
}
:::
::: C++ C++
#define SDKAPPID3RD "14000xxxxx"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
:::
</dx-codeblock>


### [6. Triggering event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API is GME's message pump and should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run abnormally. For more information, see the `EnginePollHelper` file in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).

#### Sample code

<dx-codeblock>
::: Java Java
//MainActivity.java
[EnginePollHelper createEnginePollHelper];

//EnginePollHelper.java
private Handler mhandler = new Handler();
    private Runnable mRunnable = new Runnable() {
        @Override
        public void run() {
            if (s_pollEnabled) {
                if (ITMGContext.GetInstance(null) != null)
                    ITMGContext.GetInstance(null).Poll();
            }
            mhandler.postDelayed(mRunnable, 33);
        }
    };
// For the code of calling Poll periodically, see EnginePollHelper.java.
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
[EnginePollHelper createEnginePollHelper];
// Refer to EnginePollHelper.m and EnginePollHelper.h
:::
::: C++ C++
void TMGTestScene::update(float delta)
{
  ITMGContextGetInstance()->Poll();
}
:::
</dx-codeblock>

### 7. Calculating the local authentication key

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    

#### API prototype

<dx-codeblock>
::: Java Java
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String openId, String key)
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
[EnginePollHelper createEnginePollHelper];
// Refer to EnginePollHelper.m and EnginePollHelper.h
:::
::: C++ C++
void TMGTestScene::update(float delta)
{
  ITMGContextGetInstance()->Poll();
}
:::
</dx-codeblock>

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId | int | `AppId` from the Tencent Cloud console.|
| roomId | string | Room ID, which can contain up to 127 characters (For voice message, enter "null".) |
| openId | string | User ID, which is the same as `openId` during initialization. |
| key | string | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |


#### Sample code  

<dx-codeblock>
::: Java Java
//GMEAuthBufferHelper.java
import com.tencent.av.sig.AuthBuffer;// Header file
public byte[] createAuthBuffer(String roomId)
    {
        byte[] authBuffer;
        // Generate AuthBuffer for encryption and authentication of relevant features. For release in the production environment,
        // please use the backend deployment key as detailed in https://intl.cloud.tencent.com/document/product/607/12218
        if (TextUtils.isEmpty(roomId))
        {
            authBuffer =  AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(mAppId), "0", mOpenId, mKey);
        }else
        {
            authBuffer =  AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(mAppId), roomId, mOpenId, mKey);
        }
        return authBuffer;
    }
:::
::: Object-C objetctive-c
// Voice chat authentication 
NSData* authBuffer = [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomID:self.roomIdTF.text openID:_openId key:_key];
// Voice message authentication
NSData* authBuffer =  [QAVAuthBuffer GenAuthBuffer:(unsigned int)SDKAPPID3RD.integerValue roomID:nil openID:self.openId key:AUTHKEY];
:::
::: C++ C++
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
:::
</dx-codeblock>


## Voice Chat Access

###  [1. Entering a room](id:EnterRoom)

This API is used to enter a room with the generated authentication information. The mic and speaker are not turned on by default after room entry. The returned value of `AV_OK` indicates successful API call but not successful room entry.

#### API prototype

<dx-codeblock>
::: Java Java
public abstract int EnterRoom(String roomID, int roomType, byte[] authBuffer);
:::
::: Object-C objetctive-c
-(int)EnterRoom:(NSString*) roomId roomType:(int)roomType authBuffer:(NSData*)authBuffer;
:::
::: C++ C++
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen);
:::
</dx-codeblock>

| Parameter | Type | Description |
| ---------- | :----: | ----------------------- |
| roomId | String | Room ID, which can contain up to 127 characters |
| roomType | int | Use `FLUENCY` sound quality to enter the room |
| authBuffer | byte[] | Authentication code |

#### Sample code  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
byte[] authBuffer =  GMEAuthBufferHelper.getInstance().createAuthBuffer(roomId);
ITMGContext.GetInstance(this).EnterRoom(roomId, roomType, authBuffer);
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[ITMGContext GetInstance] EnterRoom:self.roomIdTF.text roomType:(int)self.roomTypeControl.selectedSegmentIndex + 1 authBuffer:authBuffer];
:::
::: C++ C++
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_FLUENCY, (char*)retAuthBuff,bufferLen);
:::
</dx-codeblock>

### Callback for room entry

After the user enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function for callback and processing. A successful callback means that the room entry is successful, and the billing starts.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009)
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will Voice Chat still be charged when client is offlined?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

- **Sample code**  
Sample code for processing the callback, including room entry and network disconnection events.
<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
    if (type == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
    {
        // Step 6/11 : Perform the enter room event
        int nErrCode = TMGCallbackHelper.ParseIntentParams2(data).nErrCode;
        String strMsg = TMGCallbackHelper.ParseIntentParams2(data).strErrMsg;
        if (nErrCode == AV_OK)
        {
            appendLog2MonitorView("EnterRomm success");
        }else
        {
            appendLog2MonitorView(String.format(Locale.getDefault(), "EnterRomm errCode:%d errMsg:%s", nErrCode, strMsg));
        }
    }
}		
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m

- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
  NSString *log = [NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
  [self showLog:log];
  NSLog(@"====%@====", log);
  switch (eventType) {
      // Step 6/11 : Perform the enter room event
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM: {
          int result = ((NSNumber *)[data objectForKey:@"result"]).intValue;
          NSString *error_info = [data objectForKey:@"error_info"];

          [self showLog:[NSString stringWithFormat:@"OnEnterRoomComplete:%d msg:(%@)", result, error_info]];
      
          if (result == 0) {
              [self updateStatusEnterRoom:YES];
          }
      }
      break;

  }
  :::
  ::: C++ C++
  void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
  switch (eventType) {
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
      {
          ListMicDevices();
          ListSpeakerDevices();
              std::string strText = "EnterRoom complete: ret=";
          strText += data;
          m_EditMonitor.SetWindowText(MByteToWChar(strText).c_str());
          }
  }
  }
  :::
  </dx-codeblock>
- **Error code**
<table>
<thead>
<tr>
<th>Error Code Value</th>
<th>Cause and Suggested Solution</th>
</tr>
</thead>
<tbody><tr>
<td>7006</td>
<td>Authentication failed. Possible causes:<ul><li>The `AppID` does not exist or is incorrect.</li><li>An error occurred while authenticating the `authbuff`.</li><li>Authentication expired.</li><li>The `openId` does not meet the specification.</li></ul></td>
</tr>
<tr>
<td>7007</td>
<td>Already in another room.</td>
</tr>
<tr>
<td>1001</td>
<td>The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned.</td>
</tr>
<tr>
<td>1003</td>
<td>The user was already in the room and called the room entering API again.</td>
</tr>
<tr>
<td>1101</td>
<td>Make sure that the SDK is initialized, `openId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally.</td>
</tr>
</tbody></table>





### [2. Turning on or off the microphone](id:EnableMic)

This API is used to turn on or off the mic. Mic and speaker are not enabled by default after room entry.

#### Sample code  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
:::
::: C++ C++
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
:::
</dx-codeblock>

### [3. Turning on or off the speaker](id:EnableSpeaker)

This API is used to turn on/off the speaker.

#### Sample code  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
:::
::: C++ C++
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
:::
</dx-codeblock>


### [4. Exiting the room](id:ExitRoom)

This API is called to exit the current room. It needs to wait for and process the callback for exit.

#### Sample code  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
ITMGContext.GetInstance(this).ExitRoom();
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[ITMGContext GetInstance] ExitRoom];
:::
::: C++ C++
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();
:::
</dx-codeblock>


#### Callback for room exit

After the user exits a room, a callback will be returned with the message being `ITMG_MAIN_EVENT_TYPE_EXIT_ROOM`. The sample code is shown below:
<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM == type)
        {
            // Receive the event of successful room exit
        }
}
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
switch (eventType) {
    case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
    {
        // Receive the event of successful room exit
    }
        break;
	}
}
:::
::: C++ C++
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
switch (eventType) {
    case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
    {
        // Process
        break;
        }
    }
}
:::
</dx-codeblock>



## Voice Message Access


### [1. Initializing authentication](id:ApplyPtt)

Call authentication initialization after initializing the SDK. For more information on how to get the `authBuffer`, please see `genAuthBuffer` (the voice chat authentication information API).

#### API prototype  

<dx-codeblock>
::: Java Java
public abstract int ApplyPTTAuthbuffer(byte[] authBuffer);
:::
::: Object-C objetctive-c
-(QAVResult)ApplyPTTAuthbuffer:(NSData *)authBuffer;
:::
::: C++ C++
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
:::
</dx-codeblock>

| Parameter       |  Type  | Description                    |
| ---------- | :----: | ---- |
| authBuffer | String | Authentication |

#### Sample code  

<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
byte[] authBuffer = GMEAuthBufferHelper.getInstance().createAuthBuffer("");
ITMGContext.GetInstance(this).GetPTT().ApplyPTTAuthbuffer(authBuffer);
:::
::: Object-C objetctive-c
//TMGPTTViewController.m
NSData* authBuffer =  [QAVAuthBuffer GenAuthBuffer:(unsigned int)SDKAPPID3RD.integerValue roomID:nil openID:self.openId key:AUTHKEY];
[[[ITMGContext GetInstance] GetPTT] ApplyPTTAuthbuffer:authBuffer];
:::
::: C++ C++
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
:::
</dx-codeblock>

### [2. Starting streaming speech recognition](id:StartRWSR)

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. **To stop recording, call `StopRecording`**. The callback will be returned after the recording is stopped.

#### API prototype  

<dx-codeblock>
::: Java Java
public abstract int StartRecordingWithStreamingRecognition (String filePath);

public abstract int StopRecording();
:::
::: Object-C objetctive-c
-(int)StartRecordingWithStreamingRecognition:(NSString *)filePath;

-(QAVResult)StopRecording;
:::
::: C++ C++
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 

ITMGPTT virtual int StopRecording()
:::
</dx-codeblock>


| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath | String | Path of stored audio file |


#### Sample code  

<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
ITMGContext.GetInstance(this).GetPTT().StartRecordingWithStreamingRecognition(recordfilePath);
:::
::: Object-C objetctive-c
//TMGPTTViewController.m
QAVResult ret = [[[ITMGContext GetInstance] GetPTT] StartRecordingWithStreamingRecognition:[self pttTestPath]];
if (ret == 0) {
    self.currentStatus = @"Start streaming recording";
} else {
    self.currentStatus = @"Failed to start streaming recording";
}
:::
::: C++ C++
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath);
:::
</dx-codeblock>

#### Callback for streaming speech recognition

After streaming speech recognition is started, you need to listen for callback messages in the callback function `onEvent`. The event message is `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE`, namely returns text after the recording is stopped and the recognition is completed, which is equivalent to returning the recognized text after a paragraph of speech.

The event message will be identified in the `OnEvent function` based on the actual needs. The passed parameters include the following four messages.

| Message Name | Description |
| --------- | :-----------------------------------------: |
| result | A return code for judging whether the streaming speech recognition is successful. |
| text | Text converted from speech |
| file_path | Local path of stored recording file |
| file_id | Backend URL address of recording file, which will be retained for 90 days |

- **Sample code**  
<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
import static com.tencent.TMG.ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE;
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (type == ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE)
        {
            // Step 1.3/3 handle ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE event
            mIsRecording = false;
            if (nErrCode ==0)
            {
                String recordfilePath = data.getStringExtra("file_path");
                mRecFilePathView.setText(recordfilePath);

                String recordFileUrl = data.getStringExtra("file_id");
                mRecFileUrlView.setText(recordFileUrl);
            }
            else
            {
                appendLog2MonitorView("Record and recognition fail errCode:" + nErrCode);
            }
        }

}
:::
::: Object-C objetctive-c
//TMGPTTViewController.m

- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
  {
  NSNumber *number = [data objectForKey:@"result"];
  switch (eventType)
  {
  	case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
  	{
            if (data != NULL &&[[data objectForKey:@"result"] intValue]== 0)
            {
                self.translateTF.text = [data objectForKey:@"text"] ;
                 self.currentStatus = @"Streaming conversion completed";
            }
        }
  	break;
  }
  :::
  ::: C++ C++
  void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
        {
            HandleSTREAM2TEXTComplete(data,true);
            break;
        }
        ...
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING:
        {
            HandleSTREAM2TEXTComplete(data, false);
            break;
        }
    }
  }
  void CTMGSDK_For_AudioDlg::HandleSTREAM2TEXTComplete(const char* data, bool isComplete)
  {
    std::string strText = "STREAM2TEXT: ret=";
    strText += data;
    m_EditMonitor.SetWindowText(MByteToWChar(strText).c_str());
    Json::Reader reader;
    Json::Value root;
    bool parseRet = reader.parse(data, root);
    if (!parseRet) {
        ::SetWindowText(m_EditInfo.GetSafeHwnd(),MByteToWChar(std::string("parse result Json error")).c_str());
    }
        else
        {
            if (isComplete) {
                                ::SetWindowText(m_EditUpload.GetSafeHwnd(), MByteToWChar(root["file_id"].asString()).c_str());
                            }
                            else {
                                    std::string isruning = "STREAMINGRECOGNITION_IS_RUNNING";
                                    ::SetWindowText(m_EditUpload.GetSafeHwnd(), MByteToWChar(isruning).c_str());
                                 }
    }
  }
  :::
  </dx-codeblock>
- **Error code**
<table>
<thead>
<tr>
<th>Error Code</th>
<th align="center">Description</th>
<th align="center">Suggested Solution</th>
</tr>
</thead>
<tbody><tr>
<td>32775</td>
<td align="center">Streaming speech-to-text conversion failed, but recording succeeded.</td>
<td align="center">Call the `UploadRecordedFile` API to upload the recording file and then call the `SpeechToText` API to perform speech-to-text conversion.</td>
</tr>
<tr>
<td>32777</td>
<td align="center">Streaming speech-to-text converting failed, but recording and upload succeeded</td>
<td align="center">The message returned contains a backend URL after successful upload. Call the `SpeechToText` API to perform speech-to-text conversion.</td>
</tr>
<tr>
<td>32786</td>
<td align="center">Streaming speech-to-text conversion failed.</td>
<td align="center">During streaming recording, wait for the execution result of the streaming recording API to return.</td>
</tr>
</tbody></table>



### [3. Stopping recording](id:Stop)

This API is used to stop recording. It is async, and a callback for recording completion will be returned after recording stops. A recording file will be available only after recording succeeds.

#### API prototype  

<dx-codeblock>
::: Java Java
public abstract int StopRecording();
:::
::: Object-C objetctive-c
-(QAVResult)StopRecording;
:::
::: C++ C++
ITMGPTT virtual int StopRecording();
:::
</dx-codeblock>


#### Sample code  

<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
ITMGContext.GetInstance(this).GetPTT().StopRecording();
:::
::: Object-C objetctive-c
//TMGPTTViewController.m

- (void)stopRecClick {
  // Step 3/12 stop recording,  need handle ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE event
  // https://www.tencentcloud.com/document/product/607/15221
  QAVResult ret =  [[[ITMGContext GetInstance] GetPTT] StopRecording];
   if (ret == 0) {
       self.currentStatus = @"Stop recording";
   } else {
        self.currentStatus = @"Failed to stop recording";
   }
  }
  :::
  ::: C++ C++
  ITMGContextGetInstance()->GetPTT()->StopRecording();
  :::
  </dx-codeblock>

	
