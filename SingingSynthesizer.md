# Singing Synthesizer

## Knowledge

+ PyWorld

	PyWorld wrappers WORLD, which is a free software for high-quality speech analysis, manipulation and synthesis. It can estimate fundamental frequency (F0), aperiodicity and spectral envelope and also generate the speech like input speech with only estimated parameters.

+ MFCC

	在语音识别（SpeechRecognition）和话者识别（SpeakerRecognition）方面，最常用到的语音特征就是梅尔倒谱系数（Mel-scaleFrequency Cepstral Coefficients，简称MFCC）。根据人耳听觉机理的研究发现，人耳对不同频率的声波有不同的听觉敏感度。从200Hz到5000Hz的语音信号对语音的清晰度影响对大。两个响度不等的声音作用于人耳时，则响度较高的频率成分的存在会影响到对响度较低的频率成分的感受，使其变得不易察觉，这种现象称为掩蔽效应。由于频率较低的声音在内耳蜗基底膜上行波传递的距离大于频率较高的声音，故一般来说，低音容易掩蔽高音，而高音掩蔽低音较困难。在低频处的声音掩蔽的临界带宽较高频要小。所以，人们从低频到高频这一段频带内按临界带宽的大小由密到疏安排一组带通滤波器，对输入信号进行滤波。将每个带通滤波器输出的信号能量作为信号的基本特征，对此特征经过进一步处理后就可以作为语音的输入特征。由于这种特征不依赖于信号的性质，对输入信号不做任何的假设和限制，又利用了听觉模型的研究成果。因此，这种参数比基于声道模型的LPCC相比具有更好的鲁邦性，更符合人耳的听觉特性，而且当信噪比降低时仍然具有较好的识别性能。
	
	梅尔倒谱系数（Mel-scale Frequency Cepstral Coefficients，简称MFCC）是在Mel标度频率域提取出来的倒谱参数，Mel标度描述了人耳频率的非线性特性.
	
+ harmonoc

+ Cepstral

	语音的产生用源、滤波器模型来表示，即把声带振动看作激励源e(n)，把声道看成一个滤波器h(n)，两者在时域进行卷积，得到语音信号s(n)。为了更好地处理语音，则需要分析s(n)以分别得到e(n)和h(n)，这个过程称为解卷过程。倒谱计算本质上为同态处理，就是解卷的一种方法，称为“非参数解卷”，而LPC分析则为另一种方法，称为“参数解卷”，两者的作用都是解卷，这个概念一定要有。

	用数字说明：
考虑浊音,其激励源e(n)是一个周期序列，周期为N（基音周期与采样率的乘积），其倒谱e'(n)只有当n为N的倍数时才有值，在其他点都为0，而基音周期一般在2.5ms到20ms之间，如果采样率为8KHz，则N的范围是20到160之间。

而h'(n)随n的增大而迅速减小，当采样率为8KHz时在n大于20的时候已经很小，可以忽略不计，这样通过倒滤波器就可以分开激励源与信道，n小于20的低频部分可认为是信道，而n大于20的高频部分则认为是激励源。

+ F0

	Also known as the fundamental frequency, f0 is a property of the source and is perceived by the ear as pitch. The f0 of the adult human voice ranges from 100-300 Hz.

[不同元音辅音在声音频谱的表现是什么样子](https://www.zhihu.com/question/27126800/answer/35376174)

[Fundamental Frequency, Harmonics, and Formant Frequencies](https://underlingsosu.wordpress.com/2013/03/08/phonetics-phriday-fundamental-frequency-harmonics-and-formant-frequencies/)



## Singing synthesizer


### Abbreviation

+ Lyrics-to-Singing (LTS)
+ Speech-to-Singing (STS)
+ Automatic Speech Recognition (ASR)
+ signal-to-noise-ratio (SNR)

+ Words segmentation
	+ Hidden Markov model (HMM)
	+ Maximum Entropy (Maent)
	+ Conditional Random Field (CRF) 
	+ Dynamic Time Warping (DTW) [动态时间规整](https://www.jianshu.com/p/4c905853711c)

+ STS stage
	1. Learning
	2. Transformation
	3. Synthesis

+ [Sinsy](http://www.sinsy.jp/)
+ [NPSS](https://github.com/seaniezhao/torch_npss)
+ [CSound](https://github.com/csound/csound/issues/658)






