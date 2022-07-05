### How do I connect to ASR?
ASR currently supports connection via API and SDK (recommended). For more information, see [Quick Server API Access](https://intl.cloud.tencent.com/document/product/1118/43356) and [Real-Time Speech Recognition](https://intl.cloud.tencent.com/document/product/1118/43383).

### How do I update a file over 5 MB in size to the ASR console to try ASR out?
You can try ASR out by using an audio URL in the feature trial section in the [ASR console](https://console.cloud.tencent.com/asr/demonstrate). **We recommend you upload the audio file to a URL and keep the audio length below five hours.**

### Which ASR service should I choose in different scenarios?
- Real-time speech recognition is applicable to scenarios with requirements for real-timeness, such as voice input method, voice robot, and meeting recording.

### Are far-field and offline speech recognition features supported?
Real-time speech recognition doesn't support far-field and offline speech recognition features.

### Does ASR support recognizing speeches in Chinese-English mix and dialects?
- Real-time speech recognition supports Mandarin, English, Cantonese, Korean, Japanese, Thai, and Shanghainese.

>?If you want to recognize other dialects such as Sichuan, Nanjing, or Nanchang dialect, fill out the [form](https://cloud.tencent.com/apply/p/75h8nunsh9) for application.

### How long can an ASR input audio be?
- In real-time speech recognition, each audio segment of a data packet in the audio stream is 200 ms in length.

### What should I do if HTTP requests to ASR APIs return an authentication failure?
You can check whether your parameters are uploaded correctly against the parameter table. For quick connection, we recommend you use the SDK provided at our official website.

### Do ASR APIs have restrictions on the sample rate of audio files?
APIs don't restrict the sample rate of audio files, but if the sample rate is non-compliant, the recognition effect will be compromised.

