## 视频解说项目拆解

### 在YouTube查找相关视频
keyword: `recaps`,`explanation`,`commentary`,`analysis`,`breakdown`,`explained`

### 使用yt-dlp下载视频、字幕、封面 并保留音视频文件
使用yt-dlp从YouTube下载视频、字幕、封面 并保留音视频文件

```bash
yt-dlp -f bestvideo+bestaudio --write-sub --write-thumbnail --write-description -k  https://www.youtube.com/watch?v=OF4IJPy5tFo
```

### bilibili视频下载
```bash
./BBDown -tv  https://b23.tv/pZ9XNMS  -q "8K 超高清, 1080P 高码率, HDR 真彩, 杜比视界"
```

### 使用whisper生成字幕文件
```bash
whisper abc.mkv --language en --model tiny --output_format srt 
```
### 提取srt中的文字
```Python
def extract_text_from_srt(file_path):
    with open(file_path, 'r') as file:
        lines = file.readlines()

    subtitle_text = ""
    for line in lines:
        line = line.strip()
        if line.isdigit() or '-->' in line or not line:
            continue
        subtitle_text += line + "\n"

    return subtitle_text.strip()

# 用法示例
subtitle_file = 'audio.srt'
text = extract_text_from_srt(subtitle_file)
print(text)
```
### 这里尝试使用srt中的文字逐行翻译


### 使用chatGPT翻译成中文 
> 遇到如下问题
> * 翻译成中文后文稿字数减少 会导视频和音频不同步
> * 翻译质量需要改进 并且朗读停顿也需要优化

逐行翻译成中文 请保持换行 其中人、动物、地名都不要翻译

作为一名中文写作改进助理，你的任务是改进所提供文本的拼写、语法、清晰、简洁和整体可读性，同时分解长句，减少重复，并提供改进建议。请只提供文本的更正版本，避免包括解释, 请保持原有的换行格式。请从编辑以下文本开始：


### 将翻译成的中文文本转换成语音
```bash
edge-tts -f zh.txt --write-media audio.mp3 --write-subtitles a.srt --voice zh-CN-YunxiNeural
```
### 使用ffmpeg将音频和视频合并
```bash
ffmpeg -i audio.mp3 -i video.mp4 -c:v copy -c:a aac -strict experimental output.mp4
```
