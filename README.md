# MNIST GridSearch Parameter Tuning

## The Final Submission:
The working code for my submission for this task can be found in the "param_tuning.ipynb" notebook. The most complete version of the code is towards the bottom of the notebook.

## Approach
Throughout the optimization process I only used 6 epochs with 3-fold cross validation in order to reduce the training time of the convnet. I also trained each parameter individually and then aggregated the best parameters. This is not optimal because I was not able to capture any of the interactions between the different parameters. I'm certain that I missed out on some performance improvements due to this, but I felt that it was necessary in order to keep the time required to train the algorithm to a reasonable length. 

## Reproducibility Challenges
Sometimes there was such a small difference between the performance of different parameters that I would get different  results for the top performing parameter every time that I ran the code. This is particularly true for the optimization algorithm. Due to this, I chose to stick to the standard gradient descent algorithm and optimize the learn rate and momentum of this optimizer. 

## Code Quality Decisions
The code in the notebook is definitely not DRY. This is intentional. I repeated each section of param tuning as a new iteration so that readers could see the improvement of the test accuracy and the expansion of the param_grid as time went on. I thought it more useful as a learning exercise to be able to view the whole process from start to finish than to spare the user from having to scroll.

# Results

## Test Accuracy
The highest test accuracy that I was able to achieve was 99.66%. I think a more refined approach with more stable cross-validation and a higher number of epochs in each training fold would have allowed me to squeeze more accuracy out of it, but wasn't possible due to computatonal limitations.

## param_grid
The best performing param_grid that I was able to achieve is as follows: 

~~~~
    param_grid = {'epochs': [20],
                  'batch_size': [20, 40, 60],
                  'optimizer': ['SGD'],
                  'learn_rate': [0.1],
                  'momentum': [.4],
                  'init_mode_1': ['glorot_uniform'],
                  'init_mode_2': ['he_normal'],
                  'activation_1': ['softsign'],
                  'activation_2': ['relu'],
                  'activation_3': ['linear'],
                  'activation_4': ['softplus'],
                  'dropout_rate_1': [0.1],
                  'dropout_rate_2': [0.1],
                  'neurons_1': [5],
                  'neurons_2': [25],
                  'neurons_3': [5],
                  'kernel_size': [[5,5]],
                  'pool_size': [[1,1]]
                  }
~~~~
                  
# Takeaways

## 1) It takes a lot of time and computing power to train a convnet.
Even though the scope of the MNIST classification task was greatly simplified. I was surprised how time intensive the task of hand-tuning parameters became even when I greatly reduced the nubmer of epochs that I was working with. 

## 2) Hand tuning parameters is tedious.
Next time I think that I would like to try a bayesian optimization approach to see if I can remove some of the guesswork. I would also like to spend more time creating better visisualizations in order to improve my analysis. 

## 3) Some parameters matter more than others.
From my observations it seemed that things like the number of neurons in a hidden layer, dropout rate, kernel size and number of epochs had the largest impact on accuracy. It was really good to get more familiar with the different parameters and options for those parameters available through the Keras API. 

## 4) My computer's not as fast as sometimes I would like to think that it is. 

