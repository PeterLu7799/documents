# Singing Synthesizer

## Knowledges

+ Cepstral: 语音的产生用源、滤波器模型来表示，即把声带振动看作激励源e(n)，把声道看成一个滤波器h(n)，两者在时域进行卷积，得到语音信号s(n)。为了更好地处理语音，则需要分析s(n)以分别得到e(n)和h(n)，这个过程称为解卷过程。倒谱计算本质上为同态处理，就是解卷的一种方法，称为“非参数解卷”，而LPC分析则为另一种方法，称为“参数解卷”，两者的作用都是解卷，这个概念一定要有。用数字说明：考虑浊音,其激励源e(n)是一个周期序列，周期为N（基音周期与采样率的乘积），其倒谱e'(n)只有当n为N的倍数时才有值，在其他点都为0，而基音周期一般在2.5ms到20ms之间，如果采样率为8KHz，则N的范围是20到160之间。而h'(n)随n的增大而迅速减小，当采样率为8KHz时在n大于20的时候已经很小，可以忽略不计，这样通过倒滤波器就可以分开激励源与信道，n小于20的低频部分可认为是信道，而n大于20的高频部分则认为是激励源。

+ F0

	Also known as the fundamental frequency, f0 is a property of the source and is perceived by the ear as pitch. The f0 of the adult human voice ranges from 100-300 Hz.

+ [不同元音辅音在声音频谱的表现是什么样子](https://www.zhihu.com/question/27126800/answer/35376174)

+ [Fundamental Frequency, Harmonics, and Formant Frequencies](https://underlingsosu.wordpress.com/2013/03/08/phonetics-phriday-fundamental-frequency-harmonics-and-formant-frequencies/)


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

### Open source
+ [Sinsy](http://www.sinsy.jp/)
+ [NPSS](https://github.com/seaniezhao/torch_npss)


### Library
+ [CSound](https://github.com/csound/csound/issues/658)
+ [MFCC](https://blog.csdn.net/class_brick/article/details/82743741)
+ [WORLD](http://www.sohu.com/a/219420730_723464)

### Papers

+ [Speech-to-Singing Synthesis System: Vocal Conversion from Speaking Voices to Singing Voices by Controlling Acoustic Features Unique to Singing Voices](https://pdfs.semanticscholar.org/f5cd/a53068f0c436c2bd72abdcd02c626b55e39b.pdf)
+ [A Neural Parametric Singing Synthesizer Modeling Timbre and Expression from Natural Songs](https://www.mdpi.com/2076-3417/7/12/1313)






