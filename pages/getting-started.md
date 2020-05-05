---
layout: page
show_meta: false
title: "Getting Started"
subheadline: "A Step-by-Step Guide"
teaser: "This step-by-step guide helps you run the program and watermark your audio."
header:
   image_fullwidth: "start.PNG"
permalink: "/getting-started/"
---
<html>
   <a href=" https://github.com/kpisila/AudioWatermarking">Go to Github Repository.</a>
   <h2>
      For Echo Watermarking
   </h2>
   <ul>
      <li>Step 1: There are two folders on the <a href=" https://github.com/kpisila/AudioWatermarking">Github repository,</a> open the one for Echo Watermarking.
      </li>
      <li>Step 2: There are multiple versions, so make sure to select the folder with the highest number (i.e. the current version) and download all of the MATLAB script files in that folder.
      </li>
      <li>Step 3: Watermark your audio file by running INPUT_v(x).m and following the prompts. Be sure to use two different delay values between 100 and 500 as smaller delays do not persist as well when the watermark is read, and longer delays become increasingly audible. Record the values used for delay0 and delay1 as these provide a key to reading the watermark later. The watermarked version of your audio will be saved in the default MATLAB filepath as EchoWatermarkedTest.wav.
      </li>
      <li>Step 4: Read the watermark in your audio file by running OUTPUT_v(x).m and following the prompts. To correctly read your watermark you must input the same delay0 and delay1 values used to create the watermark. In the current state, the output will not exactly match the input.
      </li>
      <li>Step 5: Record the string produced by the OUTPUT_v(x).m for later verification. If changes are made to the file, this string will also change or the output will generate an error. If your audio has not been modified, the output should remain the same every time you run it so you can use the original output as a key to validate the audio's state.
      </li>
   </ul>
   
   <h2>
      For Least Significant Bit Watermarking
   </h2>
   <ul>
      <li>
         In Progress .......
      </li>
   </ul>
</html>

