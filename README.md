# AVMuST-TED

The first Audio-Visual Multi-lingual Speech Translation dataset.

Paper: [MixSpeech: Cross-Modality Self-Learning with Audio-Visual Stream Mixup for Visual Speech Translation and Recognition](https://arxiv.org/abs/2303.05309)

## Introduction


AVMuST-TED contains over 706 hours of videos and the translation text of 4 different languages.

| Target Language | Hours | Sents | Vocab | Tokens |       Labeling Type       |
|-----------------|:-----:|:-----:|:-----:|:------:|:-------------------------:|
| Spanish (Es)    |  198h |  258K |  95K  |  2.0M  | Machine Translation + Manual Review |
| French (Fr)     |  185h |  244K |  91K  |  1.9M  | Machine Translation + Manual Review |
| Italian (It)    |  165h |  218K |  95K  |  1.6M  | Machine Translation + Manual Review |
| Portuguese (Pt) |  158h |  205K |  84K  |  1.5M  | Machine Translation + Manual Review |

## Acquisition of AVMuST-TED
- **Transcription & Translation**

    The transcription and translations in the AVMuST-TED dataset are taken directly from the high reliability translated subtitles in TED. All translations and transcriptions are performed strictly in accordance with the [TED Translation Guidelines](https://www.ted.com/participate/translate/guidelines). The transcription and translations go through the following steps before publication:

    ![./resource/TED.png](./resource/TED.png)
    
    1. Transcription
        
        TED provides an original transcript for all TED and TED-Ed content. For TEDx talks, volunteers are able to utilize auto-generated transcriptions as a base, or create their own from scratch.
    
    2. Translation
    
        Subtitles are translated from the original language into the target language, using a dynamic subtitle editor. Note that TEDx transcripts must be reviewed and published before any translations can be created.
    
    3. Review
    
        Before publication, subtitles are reviewed by an experienced volunteer. Once reviewed, subtitles publish directly to the TED.com video player and YouTube for the world to enjoy.

- **Audio and Visual Speech Preparation**

    We follow [the previous audio-video speech dataset](https://arxiv.org/pdf/1809.02108) acquisitions pipeline to extract audio speech and visual speech (i.e., talking head). The visual speech corpus is provided as face-centered video in __.avi__ files with a resolution of 224\*224 and a frame rate of 25fps. The audio speech corpus is provided as the single-track, 16-bit 16kHz __.wav__ files.
    
- **AV Synchronization and Active Speaker Detection**
    
    To detect active speakers, [SyncNet](https://github.com/joonson/syncnet_python) is further used to determine which face's lip movements match the audio, and if there is no match, the clip is rejected as being a voice-over.
    
## Tasks on AVMuST-TED

- Visual Speech Translation (Lip Translation)

| Method          | M         | En-Es    |   En-Fr  |   En-It  |   En-Pt  |
|-----------------|-----------|----------|:--------:|:--------:|:--------:|
| Cascaded        | V         |   12.7   |   11.3   |   11.5   |   13.2   |
| AV-Hubert       | V         |   14.2   |   12.6   |   12.9   |   14.8   |
| Cascaded        | A(+Noise) |   16.0   |   12.9   |   12.6   |   15.5   |
| AV-Hubert       | A(+Noise) |   17.6   |   14.5   |   14.1   |   17.1   |
| MixSpeech(ours) | V         | **18.5** | **15.1** | **14.3** | **17.2** |

- Audio Speech Translation

| **Src-Tgt** | **Method** | **M** |  **-20db**  |  **-10db**  |    **0db**   |   **10db**   |   **20db**   | **Avg.** | **Clean** |
|:-----------:|:----------:|:-----:|:-----------:|:-----------:|:------------:|:------------:|:------------:|:--------:|:---------:|
|  **En-Es**  |  Cascaded  |   A   |   1.4±0.1   |   5.8±0.2   |   21.1±0.3   |   25.5±0.3   |   26.3±0.2   |   16.0   |     26.6  |
|             |  AV-Hubert |   A   | **1.5±0.2** | **6.7±0.2** | **22.3±0.4** | **27.7±0.2** | **28.6±0.3** | **17.6** |  **28.9** |
|  **En-Fr**  |  Cascaded  |   A   |   1.3±0.2   |   4.5±0.3   |   16.6±0.4   |   20.9±0.3   |   21.3±0.1   |   12.9   |    21.7   |
|             |  AV-Hubert |   A   | **1.4±0.2** | **5.5±0.3** | **18.5±0.4** | **23.2±0.2** | **23.6±0.1** | **14.5** |  **23.9** |
|  **En-It**  |  Cascaded  |   A   |   0.9±0.3   |   4.0±0.3   |   16.1±0.2   |   20.7±0.1   |   21.2±0.2   |   12.6   |    21.5   |
|             |  AV-Hubert |   A   | **1.0±0.2** | **5.1±0.5** | **18.3±0.3** | **22.7±0.2** | **23.6±0.2** | **14.1** |  **23.8** |
|  **En-Pt**  |  Cascaded  |   A   |   1.1±0.3   |   5.4±0.5   |     20.1±0.4 |     24.9±0.2 |   26.0±0.1   |   15.5   |    26.2   |
|             |  AV-Hubert |   A   | **1.2±0.2** | **6.3±0.4** | **22.2±0.3** | **27.4±0.3** | **28.4±0.1** | **17.1** |  **28.6** |

- Audio-Visual Speech Translation

| **Src-Tgt** | **Method** | **M** |  **-20db**  |   **-10db**  |    **0db**   |   **10db**   |   **20db**   | **Avg.** | **Clean** |
|:-----------:|:----------:|:-----:|:-----------:|:------------:|:------------:|:------------:|:------------:|:--------:|:---------:|
|  **En-Es**  |  Cascaded  |   AV  |   6.7±0.2   |   15.3±0.4   |   24.6±0.4   |   26.3±0.2   |   26.7±0.2   |   19.9   |   26.9    |
|             |  AV-Hubert |   AV  | **6.9±0.3** | **16.4±0.5** | **26.6±0.3** | **28.7±0.1** | **28.9±0.2** | **21.5** |  **29.1** |
|  **En-Fr**  |  Cascaded  |   AV  |   4.6±0.1   |   11.4±0.5   |   19.4±0.3   |   21.5±0.2   |   22.0±0.2   |   15.8   |   22.3    |
|             |  AV-Hubert |   AV  | **4.9±0.2** | **12.1±0.3** | **21.6±0.4** | **23.7±0.3** | **24.3±0.1** | **17.3** |  **24.6** |
|  **En-It**  |  Cascaded  |   AV  |   4.8±0.3   |   11.8±0.4   |   19.5±0.3   |   21.4±0.2   |   22.1±0.1   |   15.9   |   22.3    |
|             |  AV-Hubert |   AV  | **5.0±0.4** | **12.4±0.6** | **21.9±0.3** | **23.7±0.1** | **24.1±0.2** | **17.4** |  **24.5** |
|  **En-Pt**  |  Cascaded  |   AV  |   5.8±0.4   |   13.8±0.6   |   23.5±0.4   |   25.8±0.2   |   26.3±0.1   |   19.0   |   26.4    |
|             |  AV-Hubert |   AV  | **6.1±0.3** | **15.5±0.4** | **26.0±0.3** | **28.2±0.3** | **28.6±0.2** | **20.9** |  **28.8** |

- Other Cross-Lingual Audio-Visual Speech Tasks

AVMuST-TED can also be used for quantitative verification of cross-lingual multimodal generation tasks, such as [Cross-lingual Talking Head Generation](https://developer.nvidia.com/maxine).

## Download
   **BaiduDisk** 链接: https://pan.baidu.com/s/1Yr6tm56ygEJpCCKe37cAQg?pwd=b9up 

## License
CC-BY-NC 4.0

## Citation
```BibTeX
@article{cheng2023mixspeech,
  title={MixSpeech: Cross-Modality Self-Learning with Audio-Visual Stream Mixup for Visual Speech Translation and Recognition},
  author={Cheng, Xize and Li, Linjun and Jin, Tao and Huang, Rongjie and Lin, Wang and Wang, Zehan and Liu, Huangdai and Wang, Ye and Yin, Aoxiong and Zhao, Zhou},
  journal={arXiv preprint arXiv:2303.05309},
  year={2023}
}
```
