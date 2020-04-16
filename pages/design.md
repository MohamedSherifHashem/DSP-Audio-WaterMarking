---
layout: page
show_meta: false
title: "Design"
teaser: "In this section we discuss different parts of our design and how we implement it."
header: 
    image_fullwidth: "d.PNG"
permalink: "/design/"
---
<html>
<body>
<h2>Echo watermarking model</h2>
<body>Our design is an implementation of the echo watermarking technique.The goal of the echo watermarking is to embed the watermark information in the original audio signal resulting in a watermarked audio with a nearly inaudiable watermark. The basic concept behind it is that we introduce a repeated version of a component of the audio signal and manipulating the offset, initial amplitude and decay rate as to produce an imperceptible watermark. </body>
    
 <h5>Block Diagram</h5>
<body>A simple block diagram for echo watermarking is shown below.</body>
<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/Echo.PNG?raw=true"  width="500" height="333">

<h5>Step 1: Dividing audio stream</h5>
<body>The first step is to divide the audio stream into segments as illustrated in part B of the figure below.</body>

<h5>Step 2: Echo signals</h5>
<body>After dividing the audio we then produce two echo signals with different delay times as shown in part C of the figure below. </body>

<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/Echo_A.PNG?raw=true"  width="500" height="333">

<h5>Step 3: Echo creation</h5>
<body>Part D in the diagram below illustrates the echo creation step.</body>

<h5>Step 4: Watermarking</h5>
<body>To embed the watermark bitstream, fade between the two kernels using “mixer” signals as illustrated in part E below.</body>


<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/Echo_B.PNG?raw=true"  width="500" height="333">
    <body>Images source:"https://www.researchgate.net/publication/2267187_Digital_Music_Distribution_and_Audio_Watermarking"</body>
<h2>Output of our Design</h2>
<body>The image below shows the output audio of our code, which shows a 2 output audios with different delay, 256 and 512.</body>
<img src="https://github.com/kpisila/AudioWatermarking/blob/master/EchoWatermarking/OutputAudio/cepstrumBothDelayEcho.png?raw=true"  width="500" height="333">

<h5> 512 Peaks </h5>
<img src= " https://github.com/kpisila/AudioWatermarking/blob/master/Ben/peeks%20and%20peek512.png?raw=true"  width="500" height="333">
