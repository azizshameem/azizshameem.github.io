---
layout: post
title: Generative AI
description: Case studies on Generative AI
tags: math genAI
---

With the advent and steep rise in popularity of ChatGPT, people have recently become really interested in Artificial Intelligence in general, and 
generative systems in particular. There are several articles and posts published online, on how such a system comes to be what it is, and what the implications of
advanced in this direction could be in the near future(what with all the code completion softwares coming up, and never before reached directions of advancement of 
intelligent system). In this write-up, I try and describe what such a system is, and then show the some advancements in this field by openAI, the same firm responsible
for chatGPT.  

In general, Machine Learning is sub-divided into two categories : Descriminative modelling and Generative modelling. The former is mainly used for deciding one against
the other, given a set of inputs. If you have ever heard of CLassification(bunching the inputs into one of several classes, think cat-dog classification), regression
(predicting a value from a continuous set, like predicting the lifetime of an individual given his medical background), these come under desciminative ML. The core here
is to get a way to obtain the *probability* of seing a particular output(y), given a particular input(x) (Both x and y can be a bunch of numbers).  
Generative ML, on the other hand, is a different paradigm, in that it tries to learn not just **P(y|x)** (probability of y given x), but also **P(x)**, the probability of 
seeing the input itself. This makes it possible to sample from the learned distribution, thereby *generating* new data similar to the ones already observed. This is 
at the core of all AL generations that have become popular recently, such as text generation(chatGPT), text to image conversions(DALL-E, discussed later), Music generation
(Jukebox, Musenet), Image cpationing etc. This is what I will be majorly focussing on here.  

There are several way, or techniques, to come up wuth models capable of generating data.  

**Gaussian Mixture Models(GMMs)** : Here, the input(a bunch of numbers, called an n-dimensional vector), is assumed to have come from an n-dimensional Gaussian 
Distribution(this is a kind of distribution encountered often in statistics, which looks like a smooth hill(in 2D, 3D), with the highest point lying close to the *mean* of 
the input, and the slope being controlled by another parameter called *Variance*). The parameters of the underlying distribution is learned from the input data, and the
generation simply involves sampling from the learned distribution. This procedure, although fairly straighforward, is not at par with some of the other existing 
techniques, since the gaussian assumption is too naive for most real life data. Further, the choice of features to be included in the model makes it so that the 
number of options available is very large, and obtaining the best among them is a big task in itself.  

**Generative Adversial Networks(GANs)** : This is a class of architecture, introduced and popularised by Ian Goodfellow in 2016, which aims to train two networks : one
that generates the data by learning the distribution of the inputs, and one that tries to tell apart the real datapoints from the fake ones. This has shown to produce
really good outputs, and has therefore sparked research in the recent years. However, as the saying goes, *There's something good in everything bad, and something bad in
everything good*, GANs too have problems, in that they tend to get very unstable during training, and require specific conditions for them to be trained to a level 
where they can produce the desired results. Since the problem in GANs is posed as a *min-max*(or adversarial) game between two networks, the equilibrium may not exist
at all, let alone be one that we desire.  

**Variational Autoencoders** : Here, there are two networks trained, called *Encoder* and *Decoder*. At a basic level, the encoder transforms the input into 
some *Latent Space*, the decoder transforms it back to the input space, and the model tries to make sure the input(to the encoder) and the output(from the decoder) 
resemble each other. This class of functions mainly take pride in that they are able to deal with higher dimensional data better than GMMs or GANs, but suffer from 
other issues. Particularly, they involve assuming prior(or pre-defined set of beliefs about the data in latent space), which may not be accurate and lead to poor
performance, depending on the actual distribution of its inputs.  

**Denoising Diffusion Models(DDMs)** : This is a fairly new concept, emerging as recent as 2020, but shows promise of getting results as good as GANs(if not better), 
with little instability. The core idea here is to add noise(in small steps) to the input, and have the model guess what the noiseless version was. As more and more
noise is added, the result becomes less and less indicative of what the original input was. Eventually, all that is left is some random collection of numbers, but the
model has a way to convert this back to data from the distribution it is trained on.  

Generative modelling has been an active area of research in recent times. Like ChatGPT, openAI(a microsoft backed organisation involved in research in ML) has 
also come up with other systems that are capable of producing jaw-dropping results. Some of which are :  

1) <ins>DALL-E</ins> :  

This was one of the first products capable of producing images, given desciptions in text.  
Text-to-image synthesis has been an active area of research since the pioneering work of Reed et. al, whose approach uses a GAN conditioned on text embeddings.  
Like GPT-3, DALL·E is a transformer(a kind of Deep Learning Architecture) language model. It receives both the text and the image as a single stream of data 
, and is trained using maximum likelihood(what parameters maximize the pribability of seeing the data received as input ?) to generate all of the data, one after
the other. This training procedure allows DALL-E to not only generate images from scratch, but also modify parts of existing images, based on text prompts given by
the user.  
The final trained system has the capability to control attributes in the output image, draw multiple images, visualize perpective and three-dimensionality in its
images(able to produce images of the same object from various angles/perpectives, creating appropraite shadows, lightings, reflections etc), visualizing
internal and external structures, inferring contenxual details(a single caption may mean several things, depending on the context) as well as combining unrelated 
concepts and abstract/fictional ideas. It also depicted geographical and temporal knowledge(when prompted to output image of San Francisco's golden gate bridge, or
phone from the 20's).  

However, like any other model, DALL-E too is not perfect. The success rate of the system depends on how the caption is phrased. For instance,  As more objects are 
introduced, DALL-E is prone to confusing the associations between the objects and their colors, and the success rate decreases sharply. Also,  DALL-E is brittle with 
respect to rephrasing of the caption in some scenarios: alternative, semantically equivalent captions often yield no correct interpretations.  
Another drawback was the DALL-E sometimes was unable to understand the caption, and produced inferior or unrelated images. The developers found that repeating the
caption, sometimes with alternative phrasings, improved the consistency of the results.  
DALL-E is also unable to count past three(fails when prompted to draw an image containing five objects, for instance), and has a hard time understanding relative 
pronouns(The choices “sitting on” and “standing in front of” sometimes appear to work, “sitting below,” “standing behind,” “standing left of,” and 
“standing right of” do not).  

2) <ins>DALL-E 2</ins> :  

This is the next version of Text-to-Image systems that openAI has come up with. The difference lies in the fact that this used *Denoising Diffusion Models* instead of 
just transformers in their encoder-decoder architecture. This is able to outperform DALL-E in several ways. According to the official website, DALL·E 2 is preferred over DALL·E 1 for its caption matching and photorealism when evaluators were asked to compare 1,000 image generations from each model. DALL-E 2 builds on DALL-E 1 , increasing the level of resolution, fidelity, and overall photorealism it is capable of producing.  
Performance of such systems shows how, even *creative* or *design* jobs, that were assumed to be immune to being taken over by AI, are also as much in danger as
any other job. This puts a halt on all individuals who feel that non-humans cannot display the same nature of creativity a human can.  

3) <ins>InstructGPT and ChatGPT</ins> :  

Finaly, lets address the elephant in the room : ChatGPT, and its first ancestor : InstructGPT.  
Both of these systems come under what researchers refer to as Large Language Models(LLMs), and are trained primarily to be able to predict the next words in a 
sentence, given a few words. These are trained over millions of text, in one or more languages, using a class of Neural Networks calles Recurrent Neural Networks(RNNs). Both these models build upon the massive, 175 Billion parameter network, Generative Pre-trained Transformer(GPT) 3, by what is knows as 
Reinforcement Learning through Human Feedback(RLHF). This helps to fine-tune the model to carry out human instructions, with the result that the output of the mere
1.3 Billion parameter InstructGPT has been preferred over the 175 Billion (nearly 100 times as large) GPT 3 by people on a good range of inputs.  
ChatGPT was trained in a similar way as InstructGPT, but with a slightly different data collection set-up.  

The limitations of ChatGPT include sometimes delivering plausible-sounding but factually incorrect information, being more verbose than required and repeating 
certain phrases multiple times in its answers, and responding to harmful or sensitive questions, and/or giving unethical opinions, despite efforts to mitigate
such scenarios. Further, while dealing with ambiguity in questions/prompts, ideally the system should ask for a clarification, however the current model assumes
one of the possible scenarios according to its discretion and provides a result. Also, ChatGPT is really sensitive to minor tweaks in its prompts, and there have
been instances where that model gives two different responses even to the same prompt.  

All these advances, and the speed at which these innovations take place, make following the AI world exciting. Clearly, the advent of ChatGPT has shown the potential
that Artificial Intelligence holds, and the vast scope for research there currently is in this field. Further developements may soon lead us to our ultimate goal, of 
developing a General Intelligence, capable of applications in a wide variety of tasks, and not limited to specializations in a few. Such systems, though of high utility, needs to be developed with caution, since a system more intelligent than the average human is also a system able to outperform humans. Remember that humans
have become the dominant species among the fauna on account of the higher level of IQ we posses, and AI will not have a reason to shy out of undermining the human
race if it sees a strong enough reason to do so.  



References :  
[openai.com](openai.com)


