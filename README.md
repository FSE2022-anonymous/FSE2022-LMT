## Achieving Last-Mile Functional Coverage in Chip Design Verification.

### Introduction

This is the webpage of our FSE 2022 submission: Achieving Last-Mile Functional Coverage in Testing Chip Design Implementations.

 Due to the limited space of the paper, we show the specific implementation details and parameter experiment results of LMT here.

### Details of Random Forest
We use `sklearn.ensemble.RandomForestClassifier` to implement the random forest component. The main hyperparameters used in LMT are as follows:

- `n_estimators`: 10
  - The number of trees in the forest.

- `max_depth`:24
  - The maximum depth of the tree. 

- `max_features`:auto
  - The number of features to consider when looking for the best split. If "auto", then max_features=sqrt(n_features).

- `n_jobs`:10
  - The number of jobs to run in parallel. 

The remaining parameters are set to be default .

### Details of GAN

We use  the state-of-the-art Generative Adversarial Network , WGAN-GP[1],  to implement our constraint learning component. The details are shown below: 

*Generator*: The generator is composed of four Linear Layers. The input dimension is 100 and the output dimension is the same as the input dimension of the chip design. RELU is used as the activation function of the hidden layer. The activation function of the output layer is `Sigmoid`.

*Discriminator* :The discriminator is composed of five linear layers, and its input dimension is the same as that of the chip design, and the output dimension is 1.

The Learning rate and optimizer used in LMT are `1e-3` and `Adam` respectively. 

### Parameterized experiment results:

We conducted an experiment to investigate its influence by setting 𝐾 to 10, 30, 50, and 100 respectively (In LMT, we set K to be 50.) We found that the influence of 𝐾 is relatively small under these studied settings, and LMT with each studied setting of
𝐾 significantly outperforms all the compared approaches on both subjects.

**The experimental results of chip design A:**
![all_dfu](https://user-images.githubusercontent.com/74804893/142853519-6dcf8f70-2307-4873-95f9-7ffd21aa7343.png)

**The experimental results of chip design B:**

![all_tfe](https://user-images.githubusercontent.com/74804893/142853753-b6244307-7d0e-4771-b81d-9aaf3fb71192.png)

### Reference
[1] Gulrajani, I., Ahmed, F., Arjovsky, M., Dumoulin, V., & Courville, A. (2017). Improved training of wasserstein gans. *arXiv preprint arXiv:1704.00028*.
