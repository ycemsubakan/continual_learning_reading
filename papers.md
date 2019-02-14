# Continual Learning

## [Self-Supervised GAN to counter forgetting](https://marcpickett.com/cl2018/CL-2018_paper_23.pdf)

* [Longer version](https://arxiv.org/pdf/1811.11212.pdf). 
	In this paper, main argument is based on the fact in GANs, the discriminator training involves training a classifier with non-stationary label distribution. (The generator changes, therefore the label distribution changes also) The authors name this problem as *Discriminator forgetting*. While I agree that this is a non-stationary set-up in terms of labels, I am not sure how this is a scenario where we need to avoid catastrophic forgetting. (We actually want to forget what the happened earlier with the generator, right? - at least remembering everthing about the earlier states of the generator seems wrong  - This being said, I see that the generator explore the space, and we probably would not want to forget the areas visited - so some notion of memory seems to be good idea)
	Authors state that there exists multiple papers which takes into account the sequential aspect of discriminator training. Then, they cite few papers on this ([2, 15, 17, 19]). What is proposed in the paper to combat the non-stationarity is to artificially rotate the genearted and real images, and estimate the rotation angle with an extra head coming out of the discriminator. The results propose that what they suggest does something substantial. But I am not sure how much continual learning there is in the proposed solution.  
	All this being said, I enjoyed reading this paper because it made me look at GAN training as an online / continual learning problem. (Although the solution proposed in the paper is not really continual learning, or is it? ) 

## [A Proposal for Learning Compositional Problem-Solvers](https://marcpickett.com/cl2018/CL-2018_paper_84.pdf)

* They propose learning transformations by composing smaller transformation *routines*. One example they have in the paper is mapping arithmetic in words in different languages to numbers (e.g. one plus two, un plus deux). They do the composition by considering a markov decision process which involves making decisions for each composition. The preliminary experiments show that instead of using an RNN to do a big *flat learning*, if you do compositional learning, it appears to learn faster.

## [Closed-Loop GAN for continual Learning](https://marcpickett.com/cl2018/CL-2018_paper_17.pdf)

* First of all, this paper is about catastrophic forgetting. The paper has a review in the introduction on methods to alleviate catastrophic forgetting (second and third paragraphs), I suggest you check it out. They do generative replay with a conditional GAN. The novelty seems to be the fact that they use the same network for the GAN generator and the continually trained classifier. They also don't use a copy of the existing model to generate data. They say that making a copy of the existing model is not biologically plausible - I am not sure how important this argument is. Sure we use extra memory, but I don't think it is that bad - Furthermore, as they claim in the paper we don't need to train from scratch when the task changes, we can keep on using the old weights. The experimental section is little difficult to follow, but it seems like they have used the actual training data as buffer, and they say that they good performances only if they use some real data buffer. 


## [GEM](https://arxiv.org/pdf/1706.08840.pdf) 

* This paper uses this thing called the *task descriptor*: Each datapoint consists of a triple $$(x_n, y_n, t_n)$$, where $$x_n$$ is the feature, $$y_n$$ is the label, and $$t_n$$ is the task descriptor. They say that the task descriptor can be an integer label, or something like a feature vector to ``describe`` the task. I think they used integers to describe tasks (as they say so in the beginning of chapter 3). But the thing is, I don't understand why they say that forward transfer is unlikely if we use integer task descriptors? Is transfer learning accomplished only via task descriptors? One way they differ from something like `generative replay` is that, they only provide one example at a time for the learner. (In generative replay and so on, we have a much larger batch..). Something I also like about the paper is that they define measures for quantifying forward and backward transfer in learning (equations 3-4).  
* Regarding the algorithm: The algorithm stores a subset of the observed samples to avoid forgetting. They accumulate samples that correspond to each task, but it is still unclear to me as to how do they choose the representative samples. (Denoted by calligraphic M) The idea is to project the gradient so that the performance on the earlier tasks, do not at least deteriorate.  
* An important point that is being brought up to my attention is that they only use a data item once (judging from algorithm 1). 
* It also seems the tasks are ordered in training. Then what is the point of having a task descriptor? 

## [iCaRL:Incremental Classifier and Representation Learning](https://arxiv.org/pdf/1611.07725.pdf)

* This paper considers incremental class learning where we add one class at a time to a dataset. The method is based on using ``examplars`` to avoid forgetting earlier classes. They try to approximate the average representation learnt for the class with a set of selected input data. After selecting these examplars, they use them to avoid forgetting when they add a new class. They only thing that confuses me is that, after learning the representation via a neural net, they pass this representation through a linear layer, and the results of the linear layer is passed through sigmoids. As far as I can understand, they are not doing multiclass classification. So could they be using a softmax, at the end of the output layer? From what I understand, the reason they use sigmoids is because they want to be able to add output units each time there is a new class observed.

* In the experiments they used cifar100 with 100 classes. 

## [Few-shot self reminder to overcome catastrophic forgetting](https://marcpickett.com/cl2018/CL-2018_paper_65.pdf)


# Meta Learning

## [MAML](https://arxiv.org/pdf/1703.03400.pdf)
