# First Architecture

The first model consists of three convolutional layers, one fully connected
layer, and an output layer for binary classification.

## Feature Extraction

The convolutional layers learn increasingly complex visual features:

1. **First convolutional layer:** learns simple edges, colors, and textures.
2. **Second convolutional layer:** combines these features into shapes and
   patterns, such as food surfaces.
3. **Third convolutional layer:** learns higher-level patterns associated with
   the overall appearance of a hotdog.

Each convolution uses a $3 \times 3$ kernel with padding of 1. Each max-pooling
operation uses a stride of 2, halving the spatial dimensions.

## Architecture

The input images are resized to $128 \times 128$ pixels and have three color
channels (RGB).

```text
Input: 128 x 128 x 3
    |
    | Convolution: 32 feature maps
    | Max pooling: stride = 2
    v
64 x 64 x 32
    |
    | Convolution: 64 feature maps
    | Max pooling: stride = 2
    v
32 x 32 x 64
    |
    | Convolution: 128 feature maps
    | Max pooling: stride = 2
    v
16 x 16 x 128
    |
    | Flatten
    v
128 x 16 x 16 = 32,768 values
    |
    | Fully connected layer
    v
128 neurons
    |
    | Output layer
    v
2 values: hotdog or not hotdog
```

The number of feature maps increases from 32 to 64 and then to 128. This gives
the deeper layers more capacity to represent complex features while pooling
gradually reduces the spatial resolution.

## First Results

| Epoch | Loss | Accuracy |
|---:|---:|---:|
| 1 | 0.7086 | 0.5423 |
| 2 | 0.5959 | 0.6991 |
| 3 | 0.5414 | 0.7391 |
| 4 | 0.5181 | 0.7523 |
| 5 | 0.5027 | 0.7631 |
| 6 | 0.4852 | 0.7802 |
| 7 | 0.4627 | 0.7929 |
| 8 | 0.4370 | 0.8046 |
| 9 | 0.4115 | 0.8236 |
| 10 | 0.3775 | 0.8383 |

The training loss decreased consistently, while the training accuracy increased
from 54.23% to 83.83% over the ten epochs.

