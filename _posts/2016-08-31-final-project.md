---
layout: post
title: Final Project - Improving Brand Analytics with an Image Logo Detection Convolutional Neural Net in TensorFlow
---

For my final Metis project, I developed an application that can improve brand analytics through logo detection in images. The core of my solution leverages a Deep Convolutional Neural Network developed and trained using Google's Deep Learning library, [TensorFlow](https://www.tensorflow.org/). Since my presentation was constrained to only four minutes, I'll use this post to elaborate on the slides I presented (provided as screenshots throughout this post). My hope is this post will be useful to you if you're trying to build your own image detection model or just trying to understand more about deep learning!

>**Note:** while I focus on detecting Patagonia's logo, this project was in no way associated with [Patagonia](http://www.patagonia.com/home). I just really like their gear and their logo!

<!-- What reader can get out of it:

- process
- understanding of the challenges and improve on my work -->


{% include image.html width="650" height="344" src="/assets/images/final_project/file-page1.jpg" caption="Title slide of my presentation." %}


### Why image logo detection?

> *“A picture is worth a thousand words”* – almost everyone ever


{% include image.html width="650" height="344" src="/assets/images/final_project/file-page2.jpg" %}


{% include image.html width="650" height="344" src="/assets/images/final_project/file-page3.jpg" %}

It's not easy for brands to understand who is using their products and how they're using them. One method brands use is surveys. But surveys can be time-consuming, expensive, and have somewhat biased results. Another more scalable solution is text analytics on social media posts, specifically on the captions, comments, tags, and other metadata such as location and user information. However, text analytics rely on manual data entry from users and can miss out on posts that only include the people using the brand's products in an image. To capture these additional image-only posts, a brand can pay someone to manually sift through the torrent of social media image posts and pick out ones that are relevant. Unfortunately, that kind of manual search is expensive and doesn't scale! One way we can create a scalable solution is with a logo detection Convolutional Neural Net model...


{% include image.html width="650" height="344" src="/assets/images/final_project/file-page4.jpg" %}

<!-- Advertisers such as Kraft Foods Group Inc. pay Ditto Labs to find their products’ logos in photos on Tumblr and Instagram. The Cambridge, Mass., company’s software can detect patterns in consumer behavior, such as which kinds of beverages people like to drink with macaroni and cheese, and whether or not they are smiling in those images. Ditto Labs places users into categories, such as “sports fans” and “foodies” based on the context of their images. http://www.wsj.com/articles/smile-marketing-firms-are-mining-your-selfies-1412882222

The problem:

For brands: Brand analytics
Questions they’re asking:
How can I identify my target demographic?
Reaching target audience
Who fits my target demographic?
Want to increase probability
Less waste on people who aren’t interested
What are people saying about my brand? (sentiment)
How are people REALLY using my brand?
Surveys are expensive and responses are somewhat artificial
Understand opportunities to expand to new products and/or improve existing products
How do I save money on marketing?
Current solutions and shortcomings:
Text mining and tagging
Dependent on manual data entry by people
Misses a lot of information that’s only shared visually (show example and also venn diagram to make this point)
Brands only know when people are using their product on social media through tagging/tags/text
Manual visual analysis isn’t scalable

The answer:

Visual analytics = new frontier of social analytics
Significant supply of untapped data
We’re now posting 1.8 billion pics per day http://www.businessinsider.com/were-now-posting-a-staggering-18-billion-photos-to-social-media-every-day-2014-5
Create a visual that combines this slide and the problem slide?
Existing approaches + visual analytics = profit
People like to show their best selves in pictures on social media – if your brand is part of that, that says something important
Don’t have to depend on people for manual data entry
Deep Convolutional Neural Networks (DCNNs) have recently set state-of-the-art accuracy results on image classification problems -->



<!-- ### Existing work?? -->


### Designing the logo detector model and app

{% include image.html width="650" height="344" src="/assets/images/final_project/file-page5.jpg" %}

The core of the image logo detection model I developed uses the state-of-the-art Deep Convolutional Neural Net developed by Google, [Inception v3][inception]. Instead of training the Inception v3 model from scratch, I used a technique called [transfer learning](http://www.kdnuggets.com/2015/08/recycling-deep-learning-representations-transfer-ml.html) to retrain the model to classify if an image has a Patagonia `logo` vs. `no-logo`. I used transfer learning because it took significantly less time to train the model and I didn’t need as many training images.

To make the retraining easier, I started with this great [TensorFlow retraining tutorial][retrain] and [associated script][retrain-script]. As I'll explain in the _Model development_ section below, I had to make custom changes to the script, but it allowed me to get up and running quickly!

Next, let's explore the end-to-end design of the logo detection model and associated web app, including the technical details.

{% include image.html width="650" height="344" src="/assets/images/final_project/file-page6.jpg" %}

##### Data collection

I chose to focus my data collection (i.e., image collection) efforts on Instagram given the platform's image-centered nature and popularity among brands. Unfortunately, the Instagram API recently underwent some major changes that greatly limit access. Therefore, I chose to manually scrape images from the Instagram accounts of many Patagonia-sponsored athletes and Patagonia stores. To do the manual scraping, I used JavaScript in a Google Chrome console. Not ideal, but it allowed me to quickly gather images and start training my model!

Because this was a supervised problem, I also manually went through all the images I downloaded and grouped them into two folders: 1) has a Patagonia logo (`logo`), or 2) doesn't have a Patagonia logo (`no-logo`).

##### Model development

The majority of my time was spent iterating on developing the logo detection model. The main steps included modifying the out-of-the-box Inception v3 model and associated [retraining script][retrain] in TensorFlow, retraining the modified model, analyzing model performance, and tuning model parameters accordingly.

Some of the major modifications to the out-of-the-box Inception v3 model and associated [retraining script][retrain-script] in TensorFlow I made were:

- **Retrained the final model layer** to categorize `logo` vs. `no-logo`
- **Added a dropout layer** to minimize overfitting. If you've never heard of dropout before, check out [this great short video](https://www.youtube.com/watch?v=NhZVe50QwPM) from the Google Udacity Deep Learning course.
- **Up-sampled** `logo` class of images to improve precision and recall for the unbalanced class.
- **Removed random sampling for validation and test sets** from the script which originally distorted the results.
- **Added TensorBoard summaries** to be able to visualize model training. See my other [post]({% post_url 2016-07-04-visualizing-tensorflow-retrain %}) for more details.

As far as tuning model parameters, I experimented with different hyper-parameters and image distortions. Hyper-parameters included the learning rate, number of training steps, testing/validation percentage, and training batch size. Distortions included random image cropping, scale, and brightness. While I found distortions to improve model performance somewhat, they came at a major performance cost so I did not end up using them in my final model.

##### Web app

The web app is a simple prototype that allows a user to upload an image (either from a desktop or mobile phone) and test whether or not there is a Patagonia logo in the image, as determined by the TensorFlow logo detection model I trained and tested.

Check out the _Live app prototype!_ section below for a screencast and link to the live web app.

#### Technical architecture

Here’s the technical view, highlighted by TensorFlow and several AWS services:

{% include image.html width="650" height="344" src="/assets/images/final_project/file-page7.jpg" %}

A few notes about the technical architecture:

- **Speeding up model training** – Training the TensorFlow image detection model can require a lot of computing power. To speed things up, I used AWS [EC2 GPU instances](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using_cluster_computing.html) (g2.2xlarge instance type) and automated the instance setup to run multiple model trainings in parallel.
- **Reducing costs** – on-demand AWS EC2 GPU instances can be expensive ($0.65 per hour). However, I used [AWS spot instances](https://aws.amazon.com/ec2/spot/) to take advantage of the significantly reduced costs (e.g., ~$0.10 per hour vs. $0.65 per hour for a regular on-demand GPU EC2 instance). The main downside was that a lot of times my servers were terminated without any warning when the spot prices increased above my bid price. Luckily I always saved everything to [AWS S3](https://aws.amazon.com/s3/) so I could spin up a new spot instance and continue training the model once the spot prices went back down!


### Evaluating the logo detector model

{% include image.html width="650" height="344" src="/assets/images/final_project/file-page8.jpg" %}

The major challenge with this `logo` vs. `no-logo` classification problem is the class imbalance (i.e., most images don't have a Patagonia logo in it). Initially, my trained models had much poorer `logo` precision and recall than the final model. In order to improve these metrics, I experimented with up-sampling the `logo` class, as well as down-sampling the `no-logo` class, each of which improved the precision and recall on the `logo` class. In the end, the model achieved 77% precision and 40% recall on the `logo` class. There's definitely room for improvement in the next iteration, but still a good start!

>Need a refresher on the difference between precision and recall? Take a look at [this post](https://www.quora.com/What-is-the-best-way-to-understand-the-terms-precision-and-recall) on Quora.

Curious which test images the model correctly and incorrectly predicted? Let's take a look:

{% include image.html width="650" height="344" src="/assets/images/final_project/file-page9.jpg" %}


{% include image.html width="650" height="344" src="/assets/images/final_project/file-page10.jpg" %}

As you can see, the model struggled dealing with:

- Logo scale differences
- Multiple logos for the same brand
- Other images with text and other logos

However, sometimes the model was even smarter than me...

{% include image.html width="650" height="344" src="/assets/images/final_project/file-page11.jpg" %}


### App Screencast!

<amp-youtube
    data-videoid="3ZyQaA58DLY"
    layout="responsive"
    width="560" height="315"></amp-youtube>

### Contributing to the Google TensorFlow project

{% include image.html width="650" height="344" src="/assets/images/final_project/file-page15.jpg" %}

One of the most exciting parts of my project was being able to contribute code I developed back to the Google TensorFlow project so others can benefit from it. For more information, take a look at my other [post]({% post_url 2016-07-04-visualizing-tensorflow-retrain %}) for more details.

<!-- ### Key takeaways -->

### Future work

I was very happy with the results of my initial model and the basic functionality of the web app. However, that was just the tip of the iceberg! Here are some of the potential next steps for this project I've been thinking about:

- Better understanding how a solution like this could be successful while still protecting people's privacy.
- Pitch use-cases to brands/marketers to determine product/market fit
- Expand prototype of product and collect feedback
    - Enable batch image processing via a RESTful API
    - Integrate with Instagram (and other social media image services) API to automatically collect images
- Improve and optimize model/process
    - Improve recall on "has logo" class by adding class weights to loss function similar to what's suggested in [this StackOverflow post](http://stackoverflow.com/questions/35155655/loss-function-for-class-imbalanced-binary-classifier-in-tensor-flow).
    - Improve ability to generalize to broader set of images by training model on more data.
    - Localization of logo detection (i.e., where in this picture is a logo, if any?)
    - Combine logo detection with existing textual analytics
    - Automate model selection / hyper-parameter tuning process
    - Explore other model architectures
    - Compare model performance to existing logo-detection services



<!-- Key considerations for future work:

Cultural
Consumer privacy
Lead to new trends in logo design and placement
Brands optimizing their logos for detection to gain an edge in data analysis
Demographics of brands – inclination to post on social media
Lack of control over what people are posting / Dealing with cases of negative context -> this could actually be a good use-case
Brands without prevalent logos
Technical
Data access
Speed of modeling
Managing model lifecycle as algorithms evolve
Scalability
Images processed per minute + number of logo-classes supported + high accuracy
Building multi-class classifier to classify images against multiple logos at once
Reducing false-positives and true-negatives
Ensemble multiple methods
Depending on use-case, tune model to optimize precision or recall -->

### Conclusion

{% include image.html width="650" height="344" src="/assets/images/final_project/file-page14.jpg" %}

Combining the power of Deep Convolutional Neural Networks, like the logo detector model I developed, with existing text analytics capabilities presents an opportunity for brands to discover new insights about their customers and how customers use their products.

### Additional References

I did a lot of research on computer vision and neural networks during this project. Here are the sources I found most useful:

- [_Rethinking the Inception Architecture for Computer Vision_ (Inception v3)][inception]
- [_How to Retrain Inception's Final Layer for New Categories_][retrain] and associated [script][retrain-script]
- [_Udacity Deep Learning course (in partnership with Google)_](https://classroom.udacity.com/courses/ud730)
- [_DeepLogo: Hitting Logo Recognition with the Deep Neural Network Hammer_](http://arxiv.org/pdf/1510.02131.pdf)
- [_Scalable Logo Recognition in Real-World Images_](http://www.multimedia-computing.de/mediawiki//images/3/34/ICMR2011_Scalable_Logo_Recognition_in_Real-World_Images.pdf)
- [_ImageNet Large Scale Visual Recognition Challenge_](http://image-net.org/challenges/LSVRC/)


<!-- ### Footnotes -->


[inception]: http://arxiv.org/pdf/1512.00567v3.pdf
[retrain]: https://www.tensorflow.org/versions/master/how_tos/image_retraining/index.html
[retrain-script]: https://github.com/tensorflow/tensorflow/blob/master/tensorflow/examples/image_retraining/retrain.py