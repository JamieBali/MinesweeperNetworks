# Minesweeper CNN

I've been entertaining myself on the way to and from work for the last couple months and I'd like to say I'm geteting good at it. This made me think of how we could make some neural system learn how to play Minesweeper (because it would make anyone think that, obviously).

Minesweeper is unique in the way that a game can be generated with a tiny amount of processing power, and the win condition is very easily defined.
Minesweeper is also very abstractable. We can take a grid of tiles, let's say a 3x3 area to start with, and we can predict the whether or not the middle tile is a mine or not based on the surrounding tiles. I predict that a 3x3 area won't be particularly effective, a 5x5 area will work well, but a 7x7 grid area will begin to overfit the data, likely causing issues when predicting around unrevealed tiles.

## Design

I plan on constructing a Convolution Neural Network which will be able to provide a probability of a tile containing a bomb. My network will search through full Minesweeper grid, working in segments to predict a given tile.
The network structure will be 2 convolution layers, followed by 2 fully-connected layers, and ending in a single node as a classifier (providing a probability of "bomb", where 1 means absolutely there is a bomb, and 0 means there is absolutely not a bomb).

I will create my network using Keras, as this is the CNN library I am most confident with.

## Dataset

We will artificially create a training dataset to run this network. For each epoch of training, I will create a certain number of minesweeper grids and reveal a random selection of tiles, and take random segments from them (making sure that we feature selections of both covered and uncovered tiles, and some edge and corner areas).

In our training, we can provide the "error" of a prediction as how close they were to the correct answer (i.e. if the network predicts 0.67 when the correct answer is 1, then the error is 0.33). Training will happen via backpropogation.

## Experiments / Optimisation

In order to optimise out network, we can run some brief experiments.

Firstly, we can see the impact of varying the size of the segments. As mentioned earlier, I expect 3x3 to be fairly inaccurate, 5x5 to be much better, and 7x7 to potentially start reaching into overfitting territory, possibly reducing the accuracy again.

Secondly, we can investigate varying the amount of data - both the amount per epoch and the number of epochs.

Third, we can investigate varying the data itself - increasing and decreasing the number of bombs. I think this will have the least impact, as the completely random data means that the number of bombs in each segment will vary a fair amount anyway.
