---
layout: post
title: Using TensorBoard to Visualize Image Classification Retraining in TensorFlow
---

**tl;dr** I [contributed code][pr] to the Google [TensorFlow][tflow] project on GitHub that adds [TensorBoard][tboard] visualizations to the existing TensorFlow ["How to Retrain Inception's Final Layer for New Categories" tutorial][tutorial]. My additions make it easier to understand, debug, and optimize the retraining process. Check it out by walking through the [updated tutorial][tutorial], specifically the "Visualizing the Retraining with TensorBoard" section I added, or use the [source code][source] as a starting point to visualize your own TensorFlow code with TensorBoard.

# Quick start

Follow the steps in [this tutorial][tutorial]. The specific section I added is "Visualizing the Retraining with TensorBoard."

# Retraining a state-of-the-art image classification Neural Network to classify your own images in TensorFlow

A major part of [my final Metis project]({% post_url 2016-08-31-final-project %}) was modifying and retraining the state-of-the-art [Google Inception v3](http://arxiv.org/abs/1512.00567) Deep Convolutional Neural Network to classify images. The Google TensorFlow project has a great [tutorial][tutorial] which shows you how to quickly get started retraining the Inception v3 model to classify images of flowers and then repurpose the code for your own image classification needs.

# Challenges optimizing Inception v3 model retraining

Before I added TensorBoard summaries to the TensorFlow image classification [tutorial][tutorial], it was not possible to visualize the model architecture or compare model training performance over many training steps.

## Analyzing model training performance over time

The stock TensorFlow tutorial code did a great job of printing model performance to the console such as accuracy and cross entropy. However, it was difficult to understand how the model was performing over time, especially when you trained the model for thousands of steps. Is the model converging? Is the model overfitting the data? It was difficult to select the optimal model parameters without answers to those questions. Additionally, those questions got even more difficult to answer when comparing the model performance across different parameter combinations!

<!-- <amp-img width="650" height="216" layout="responsive" src="/assets/images/image_retraining/text_stats.png"></amp-img> -->

{% include image.html width="650" height="216" src="/assets/images/image_retraining/text_stats.png" caption="It's difficult to analyze model training performance over time when the output is only text." %}

<!-- [Show before pics comparing text for multiple runs] -->

## Understanding the Inception v3 retraining model architecture

What about if you wanted to add TensorFlow code that modifies the Inception v3 model architecture to fit your own image classification problem? Sure, you can find some images of the Inception v3 architecture online, but understanding how it's actually implemented in TensorFlow is a whole separate beast.

Wouldn't it be great to visualize the model training performance and architecture to more easily understand, debug, and optimize the retraining process?

# Visualizing model performance and architecture with TensorBoard

Luckily, TensorFlow includes a complementary tool for model performance and architecture visualization called [TensorBoard][tboard].

To take advantage of the TensorBoard visualization capabilities, I added code to the retraining script that allows you to visualize the model training statistics and overall model architecture.

Once you execute the retraining according to the [tutorial][tutorial], visualizing the retrain process and model architecture is as simple as:

    tensorboard --logdir /tmp/retrain_logs

<!-- Add Docker alternative??? -->

## Viewing model performance in TensorBoard

Once TensorBoard is running, selecting the `EVENTS` tab allows you to visualize the change in model statistics such as accuracy and cross entropy.

<!-- <amp-img width="650" height="609" layout="responsive" src="/assets/images/image_retraining/events.png"></amp-img> -->

{% include image.html width="650" height="609" src="/assets/images/image_retraining/events.png" caption="TensorBoard EVENTS tab." %}

<!-- Show screenshots of before (with only text) and after (with TensorBoard)
- screenshot of overfitting?
- screenshot of convergence? -->

You can select the `HISTOGRAMS` tab to visualize the retraining layer weights, biases, activations, etc.

<!-- <amp-img width="650" height="431" layout="responsive" src="/assets/images/image_retraining/histograms.png"></amp-img> -->

{% include image.html width="650" height="431" src="/assets/images/image_retraining/histograms.png" caption="TensorBoard HISTOGRAMS tab." %}

## Comparing model training performance across multiple model parameter combinations

Want to easily compare model training performance across multiple parameter combinations? Change the TensorBoard summary directory for each model training run, keeping the same base directory (`/tmp/retrain_logs` in the example below).

> NOTE: The following examples are run from the `tensorflow/examples/image_retraining` directory of the TensorFlow GitHub project

**Example run 1**

In this training run, let's set the `learning_rate` to 0.01.

    $ python retrain.py --image_dir ~/Downloads/flower_photos --learning_rate 0.01 --summaries_dir /tmp/retrain_logs/run1

**Example run 2**

In this training run, let's set the `learning_rate` to 0.001.

    $ python retrain.py --image_dir ~/Downloads/flower_photos --learning_rate 0.001 --summaries_dir /tmp/retrain_logs/run2

**Launch TensorBoard**

    $ tensorboard --logdir /tmp/retrain_logs/

In the image below, you can easily see how changing the `learning_rate` from 0.01 to 0.001 affects the model training.

<!-- <amp-img width="650" height="584" layout="responsive" src="/assets/images/image_retraining/compare.png"></amp-img> -->

{% include image.html width="650" height="584" src="/assets/images/image_retraining/compare.png" caption="TensorBoard EVENTS tab comparing a learning rate of 0.01 (run 1) to 0.001 (run 2)." %}

## Viewing model architecture in TensorBoard

Selecting the `GRAPH` tab allows you to view an interactive diagram of the Inception v3 model architecture that was modified for retraining.

<!-- <amp-img width="650" height="588" layout="responsive" src="/assets/images/image_retraining/graph.png"></amp-img> -->

{% include image.html width="650" height="588" src="/assets/images/image_retraining/graph.png" caption="TensorBoard GRAPH tab." %}


# Visualizing other TensorFlow models with TensorBoard

Want to visualize other models you create in TensorFlow? You can use the [source code I added][source] as a starting point to visualizing your own TensorFlow code with TensorBoard!

# Wrapping up

I hope [my TensorBoard additions][pr] to the TensorFlow image classification retraining [tutorial][tutorial] make it easier for you to optimize the retraining process or build your own TensorBoard visualizations! If you have any comments or questions, please feel free to email me at [maxmelnick@gmail.com](mailto:maxmelnick@gmail.com).

[pr]: https://github.com/tensorflow/tensorflow/pull/2887
[tflow]: https://github.com/tensorflow/tensorflow
[tboard]: https://www.tensorflow.org/versions/master/how_tos/summaries_and_tensorboard/index.html
[tutorial]: https://www.tensorflow.org/versions/master/how_tos/image_retraining/index.html
[source]: https://github.com/tensorflow/tensorflow/pull/2887/files


<!-- # Other notes

- Use the code to visualize retraining yourself
- Use the code as starter code to help you visualize your own TensorFlow model with TensorBoard
- Contribute to TensorFlow or other open source projects

- used MNIST with summaries as model

Challenges

- maintaining operability with label_image script (i.e., name of final tensor)

# Benefits

- visualizing the training process allowed me to more easily diagnose issues with my model such as overfitting and tweak the model parameters and architecture accordingly
- easier to visualize complicated models
- debug issues with your code (e.g., my issue with the name of final tensor) -->




