<!--

#################################################
### THIS FILE WAS AUTOGENERATED! DO NOT EDIT! ###
#################################################
# file to edit: index.ipynb
# command to build the docs after a change: nbdev_build_docs

-->

# online_triplet_loss

> PyTorch conversion of the excellent post on the [same topic in Tensorflow](https://omoindrot.github.io/triplet-loss). Simply an implementation of a triple loss with online mining of candidate triplets used in semi-supervised learning.


## Install

`pip install online_triplet_loss`

Then import with:
`from online_triplet_loss.losses import *`

## How to use

In these examples I use a really large margin, since the embedding space is so small. A more realistic margins seems to be between `0.1 and 2.0`
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```
from torch import nn
import torch

model = nn.Embedding(10, 10)
```

</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```
#from online_triplet_loss.losses import *
labels = torch.randint(high=10, size=(5,)) # our five labels

embeddings = model(labels)
print('Labels:', labels)
print('Embeddings:', embeddings)
loss = batch_hard_triplet_loss(labels, embeddings, margin=100)
print('Loss:', loss)
loss.backward()
```

</div>
<div class="output_area" markdown="1">

    Labels: tensor([8, 2, 5, 4, 5])
    Embeddings: tensor([[-0.8817, -1.0785, -0.3578, -0.0837,  0.2544, -0.8937,  1.4421,  0.2820,
              0.2439,  0.4424],
            [ 0.8939, -1.9193,  0.2663, -0.1702, -0.7696,  1.3117,  1.0242, -1.0406,
              0.2643,  0.2774],
            [ 0.9621, -3.1509,  0.3539,  1.3979, -0.9992,  0.4069,  0.7399,  0.2953,
              0.1055,  1.6277],
            [-0.6303, -0.6868, -0.3235,  1.2629,  0.1715, -0.8287, -0.0056,  0.0165,
             -0.6142,  0.9858],
            [ 0.9621, -3.1509,  0.3539,  1.3979, -0.9992,  0.4069,  0.7399,  0.2953,
              0.1055,  1.6277]], grad_fn=<EmbeddingBackward>)
    Loss: tensor(97.3276, grad_fn=<MeanBackward0>)


</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```
#from online_triplet_loss.losses import *
embeddings = model(labels)
print('Labels:', labels)
print('Embeddings:', embeddings)
loss, fraction_pos = batch_all_triplet_loss(labels, embeddings, squared=False, margin=100)
print('Loss:', loss)
loss.backward()
```

</div>
<div class="output_area" markdown="1">

    Labels: tensor([8, 2, 5, 4, 5])
    Embeddings: tensor([[-0.8817, -1.0785, -0.3578, -0.0837,  0.2544, -0.8937,  1.4421,  0.2820,
              0.2439,  0.4424],
            [ 0.8939, -1.9193,  0.2663, -0.1702, -0.7696,  1.3117,  1.0242, -1.0406,
              0.2643,  0.2774],
            [ 0.9621, -3.1509,  0.3539,  1.3979, -0.9992,  0.4069,  0.7399,  0.2953,
              0.1055,  1.6277],
            [-0.6303, -0.6868, -0.3235,  1.2629,  0.1715, -0.8287, -0.0056,  0.0165,
             -0.6142,  0.9858],
            [ 0.9621, -3.1509,  0.3539,  1.3979, -0.9992,  0.4069,  0.7399,  0.2953,
              0.1055,  1.6277]], grad_fn=<EmbeddingBackward>)
    tensor(96.4817, grad_fn=<DivBackward0>) tensor(1.)
    Loss: tensor(96.4817, grad_fn=<DivBackward0>)


</div>

</div>

## References
* [Triplet Loss and Online Triplet Mining in Tensorflow](https://github.com/omoindrot/tensorflow-triplet-loss)
* [Facenet paper](https://arxiv.org/abs/1503.03832)
* [adambielski's nice implementation](https://github.com/adambielski/siamese-triplet) (unfortunately context switches between CPU / GPU)
