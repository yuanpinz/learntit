# Your Daily(or maybe monthly) Dose of ML

## 2021.09.15

### Google AI: [Revisiting Mask-Head Architectures for Novel Class Instance Segmentation](http://ai.googleblog.com/2021/09/revisiting-mask-head-architectures-for.html)

[[project page]](https://google.github.io/deepmac/) [[paper]](https://arxiv.org/pdf/2104.00613.pdf) [[partially supervised segmentation paper]](https://arxiv.org/pdf/1711.10370.pdf)

**Keywords**: instance segmentation; partially supervised instance segmentation

**Summary**: **Instance segmentation** is an important task to many downstream applications. Collecting large labeled instance segmentation dataset is time consuming. **Partially supervised instance segmentation** target to tackle the challenge but requires a **stronger form of model generalization** to handle **novel classes not seen at training time**. This paper proposed two easy-to-implement fixes (one **training protocol fix**, one **mask-head architecture fix**) based on Mask R-CNN like network that work in tandem to close the gap to fully supervised performance. ***While neither of these ingredients have a large impact on the classes for which masks are available during training, employing both leads to significant improvement on novel classes for which masks are not available during training.*** In a nutshell, **cropping exclusively to ground true boxes during training** and **using deep hourglass mask heads with 50 or more layers** brought significant performance improvement to unseen classes.

**Comment**: I haven't read the paper yet. I hope there will be more discussion about why these two fix would bring better performance to unseen classes. Otherwise it's just a technical report.

## 2021.09.09

### Google AI: [Personalized ASR Models from a Large and Diverse Disordered Speech Dataset](http://ai.googleblog.com/2021/09/personalized-asr-models-from-large-and.html)

[[paper1]](https://www.isca-speech.org/archive/interspeech_2021/macdonald21_interspeech.html) [[paper2]](https://www.isca-speech.org/archive/interspeech_2021/green21_interspeech.html)

**Keywords**: 

**Related Paper**: 

**Summary**:

## 2021.09.02

### Google AI: [Discovering Anomalous Data with Self-Supervised Learning](http://ai.googleblog.com/2021/09/discovering-anomalous-data-with-self.html)

**Keywords**: 

**Related Paper**: 

**Summary**:

## 2021.05.06

### DeepMind: [Game theory as an engine for large-scale data analysis](https://deepmind.com/blog/article/EigenGame)

**Keywords**: 

**Related Paper**: 

**Summary**:

## 2021.01.05

### OpenAI: [CLIP: Connecting Text and Images](https://openai.com/blog/clip/)

**Keywords**: 

**Related Paper**: 

**Summary**:

### OpenAI: [DALL·E: Creating Images from Text](https://openai.com/blog/dall-e/)

**Keywords**: 

**Related Paper**: 

**Summary**:

## 2020.06.17

### OpenAI: [Image GPT](https://openai.com/blog/image-gpt/)

**Keywords**: 

**Related Paper**: 

**Summary**: