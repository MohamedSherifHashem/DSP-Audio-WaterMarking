---
layout: page
show_meta: false
title: "Background"
subheadline: "DSP concepts behind our desing."
teaser: "In this section we discuss different DSP concepts that we used and implemented in our design."
header: 
    image_fullwidth: "background.PNG"
permalink: "/background/"
---

<h2>What is Audio Watermarking and What Makes a Good One? </h2>
<body>  Audio watermakring is the process of embedding information into a singal in a way that makes it difficult to remove. This is extremly important when identifying proof of ownership. If we think about a watermark on a picture, it is very similar to watermarking an audio singal but now, the watermark isnt seen.The are multiple attributes that we consider when considering a watermarking technique and we need to understand each one of them to be able to judge and choose which technique is more suitable for our purposes.</body>

<h5> Inaudiability: </h5>
<body>Inadiability is sometimes considered one of the most important attributes of a watermarking technique, it is simply concerned with whether or not your watermark can be detected or heard by the end receiver.But this is not an absolute scale, it depends on the audio quality of the signal and the desired quality of output audio. So for example if the target output quality is low;then the watermark does not have to achieve absolute inadiability and hence giving a little flexability in the design. In summary, it is a balance between the required output quality and the noise that the watermark will introduce, the need for a higher quality will result in the need for the noise introduced by the watermark to be as insignificant as possible. </body>

<h5> Robustness: </h5>
<body>Robustness is an important aspect in audio watermarking, simply a watermark that is considered robust means that any intentional or unintentional modification or extraction of the watermark is successful if and only if the audio signal get destroyed or loses significant quality.This does not mean that the watermark is impossible to remove or detect it just means that an attempt to remove the watermakr will essentially cauase the destruction of the original audio or render it useless,hence protecting the audio.  </body>

<h5> Data Rate: </h5>
<body>The data rate is the number of bits per seconds that can be transmitted by the watermarking system as a whole.</body>

<h5>Operational Domain: </h5>
<body>Operational domain is concerned with the type or format of the input and output audio  , we have 2 domains compressed and uncompresses audio format. Therefore, a watermarking technique could have uncompressed audio as it's input and output or compressed audio as input and output or a combination of both where we can have an uncompressed input and the output is a compressed audio file also called combined compression watermarking.</body>

<h5> Interoperatability: </h5>
<body>Interoperatability is concerned of whether or not a watermark can be extracted using a generic watermark extractor with no prior knowledge of the underlying processes of the system.To acquire interoperatability the system has to follow the same signal representation that other systems use.</body>

<h5> Complexity: </h5>
<body>This is the maximum tolerable complexity of a system whether in embedding the watermark or the extraction it, this is important due to the existance of a tradeoff between complexity and the inaudiability property.</body>

<h5>Blind vs. Non-Blind Watermark Detection: </h5>
<body>Blind detection means that the watermarking system can detect and extract the watermark without prior knowledge of the unwatermarked audio signal.Of course a non-blind watermark extraction would result in a more efficient watermark extraction but tha knowledge of the original is not always available.</body>

<h5>Tradeoffs: </h5>
<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/tradeoff.PNG?raw=true" width="500" height="333">
<body>
    All the above characteristics are desirable in any system, but there exists a tradeoff between three of them. As a result w have to balance these propertiess to match the requirments of our application,for example if we want our technique to be robust we have to be ready to give up the inaudiability property and vice versa, so it depends on the functions,priorities and requirments.</body>


<h2>Types of audio watermarking </h2>

<h5>Audio in Audio: </h5>
<body>Hiding an audio message inside the original audio signal.</body>

<h5>Image in Audio: </h5>
<body>Hiding an image inside the original audio signal.</body>

<h5>Text in Audio: </h5>
<body>Hiding a text message inside the original audio signal.</body>

<h2>How to measure effiency of watermarking technique</h2>

<h5> Mean Square Error: </h5>
<body>Described as a signal fidelity measure, the goal of to compare two signals by providing a
quantitative score that describes the level of error/distortion between them.</body>

<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/MSE.PNG?raw=true" width="333" height="200">

<body>
    
    X represents the original signal while Y represents the watermarked signal.
    
</body>

