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
	<head>
		<title>Echo watermarking model</title>
	</head>
	<body>
		<p>
			Our design is an implementation of the echo watermarking technique.The goal of the echo watermarking is to embed the watermark information in the original audio signal resulting in a watermarked audio with a nearly inaudiable watermark. The basic concept behind it is that we introduce a repeated version of a component of the audio signal and manipulating the offset, initial amplitude and decay rate as to produce an imperceptible watermark.
		</p>
		<h5>Block Diagram</h5>
		<p>A simple block diagram for echo watermarking is shown below.</p>
		<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/Echo.PNG?raw=true"  width="500" height="333">

		<!--<h5>Audio Demo</h5>

		<audio src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/Queen(GreatestHitsI)-(3)KillerQueen.mp3?raw=true" type="audio/mp3" controls="controls"></audio>-->

		<h5>Step 1: Dividing audio stream</h5>
		The first step is to divide the audio stream into segments as illustrated in part B of the figure below.

		<h5>Step 2: Echo signals</h5>
		After dividing the audio we then produce two echo signals with different delay times as shown in part C of the figure below. 

		<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/Echo_A.PNG?raw=true"  width="500" height="333">

		<h5>Step 3: Echo creation</h5>
		Part D in the diagram below illustrates the echo creation step.

		<h5>Step 4: Watermarking</h5>
		To embed the watermark bitstream, fade between the two kernels using “mixer” signals as illustrated in part E below.


		<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/Echo_B.PNG?raw=true"  width="500" height="333">
			Images source:"https://www.researchgate.net/publication/2267187_Digital_Music_Distribution_and_Audio_Watermarking"

		<h2>Output of our Design Version 1</h2>
		<p>To read out the value of the delay from the watermarked audio we used Cepstrum Analysis. The cepstrum is defined by:</p>
		<img src="https://github.com/kpisila/AudioWatermarking/blob/master/EchoWatermarking/OutputAudio/ceps.png?raw=true"  width="772" height="146">
		<p>The image below shows the cepstrum of the output audio of our code, which shows 2 output audios with different delays, 256 and 512.</p>
		<img src="https://github.com/kpisila/AudioWatermarking/blob/master/EchoWatermarking/OutputAudio/cepstrumBothDelayEcho.png?raw=true"  width="500" height="333">

		<h5> Determining the location of the Peak </h5>
		<p>
			To determine the location of the peak an average and standard deviation are taken around the expected peak location.
			When the maximum value near the expected peak location is more than a certain number of standard deviations above the average we consider it a peak.
			To determine which value to use to provide the best overall results we ran the same watermarked audio through with different thresholds.
		</p>
		<img src= "https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/CepstrumErrorPercent.png?raw=true"  width="500" height="333">
		<p>Even at the optimal level the error percentage was above 50% so we changed our analysis to the Auto Correlated Cepstrum which is defined by:</p>
		<img src="https://github.com/kpisila/AudioWatermarking/blob/master/EchoWatermarking/OutputAudio/autoceps.png?raw=true"  width="888" height="141">
		<p>Below is the result of determining the optimal threshold for determining a peak.</p>
		<img src= "https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/AutoCepstrumErrorPercent.png?raw=true"  width="500" height="333">
		<p>The optimal value was still not providing good enough results even though the Auto-Cepstrum appears far superior as shown below:</p>
		<img src= "https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/AutoCepstrum512Delay.png?raw=true"  width="500" height="333">

		<p>
			The best solution was to simply assume that there would be a peak at one of the two locations specified and compare the peaks at these locations. 
			The larger peak determined the bit value.
			This produced less than ideal, but usable results. 
			Below is the original audio and watermarked audio with the original watermark message compared to the message read from the watermarked audio.
			The main advantage to the echo watermarking technique is how well the watermark is hidden.
			
		</p>
		<h5>Original Audio:</h5>
		<audio src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/KillerQueen.mp3?raw=true?" type="audio/wav" controls="controls"></audio>
		<h5>Watermarked Audio:</h5>
		<audio src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/KillerQueenWatermarked.wav?raw=true?" type="audio/wav" controls="controls"></audio>

		<h5> Input String (bottom) and Output String (top) </h5>
		<img src= "https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/KillerQueenWatermark.png?raw=true"  width="500" height="333">

		<h5>Second Demo of Watermarked Audio</h5>
		
		<audio src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/128-256EchoWatermarkedHere.wav?raw=true" type="audio/wav" controls="controls"></audio>

		<h5>Original Audio for Second Demo</h5>

		<audio src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/OriginalWAVTHere.wav?raw=true" type="audio/wav" controls="controls"></audio>
		MSE = 0.2729

		<h1> 
			<center>Sample Code Blocks</center>
		</h1>




		<h2> Adding the watermark </h2>
		<pre>
			<code class="language-matlab">
code = input(prompt,'s'); % getting user input and storeing it

b = size(code); % getting the size of user input

if (b <= c)  % checking to make sure its less than 50 characters

	z= double(code); % getting ASCII value

	x = dec2bin(z); % taking ASCII value and turning into binary

	%this turns the code into a [stringLength] by 7 matrix so I resized it into y

	y= reshape(x',[1,numel(x)]); % resize

	a = size(y); %checking the size of which turns out is 1 by 70 not 1 by 80

	Y = mat2cell(y,1,ones(numel(y),1)); % taking the reshaped and creating a cell

	K = convertCharsToStrings(Y); % takes cell on converts to a string

	P = str2double(K); %turns string into double.
	
	bitstream = P;
			</code>
		</pre>
		
		<h2>Add Echo Function </h2>

		<pre>
			<code class="language-matlab">
function [] = AddEchoFunction_v3(bitstream, filepath, delay0, delay1)
spf = 32768;
maxValue = 0;
for i = 1:2	%this code runs twice to create the 2 echo kernels

	%%%%%%%%%%%%%%%%%%%%% Create MATLAB objects to read the audio file %%%%%%%%
	afr1 = dsp.AudioFileReader(filepath, 'SamplesPerFrame', spf);
	afr2 = dsp.AudioFileReader(filepath, 'SamplesPerFrame', spf);

	%%%%%%%%%%%%%%%%%% Create MATLAB objects to write new audio files %%%%%%%%%

	afw1 = dsp.AudioFileWriter('Echo1.wav', 'FileFormat', 'WAV');
	afw2 = dsp.AudioFileWriter('Echo2.wav', 'FileFormat', 'WAV');
	
	%%%%%%%%%%%% every time an audio file reader is called, it %%%%%%%%%%%%%%
	%%%%%%%%%%%% returns the next spf x 2 array of the file    %%%%%%%%%%%%%%
	%%%%%%%%%%%% If one copy is called first before we start   %%%%%%%%%%%%%%
	%%%%%%%%%%%% The loop, it is ahead by spf samples.         %%%%%%%%%%%%%%
	if i == 1
		delay = delay0;    %%%%%%%% Use each input delay for 1 kernel
	end
	if i == 2
		delay = delay1;
	end
	%%%%%%%%%%%% Create temporary variables for use in the loop %%%%%%%%%%%%%
	afterDelay = delay + 1;
	startSecond = spf + 1 - delay;
	endFirst = spf - delay;
	counter = 0;
	audio2 = afr2();
	audio4 = zeros(spf,2);  %initialize temp matrix for splicing
	firsthalf = audio2(afterDelay:end,1:2);%take the second half of the first chunk
	%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

	while ~isDone(afr1)
		
		audio4(1:endFirst,1:2) = firsthalf;  %use it as the first half of the splice

		audio1 = afr1();
		audio2 = afr2();                                    
															%use the first half of the
		audio4(startSecond:end,1:2) = audio2(1:delay,1:2);  %second chunk as the second
															%half of the splice.
													
		firsthalf = audio2(afterDelay:end,1:2);%take the second half of the second 
												%chunk and save it for next time
		audio3 = (audio1 * 0.7) + (audio4 * .3);

		maxValue = max(max(audio3), maxValue);
		if(i == 1)
			afw1(audio3);            %save the audio chunk
		end
		if(i == 2)
			afw2(audio3);            %save the audio chunk
		end
		counter = counter + 1;  %then move to the next chunk
	end
	release(afr1); 
	release(afr2); 
	release(adw);
	release(afw1);
	release(afw2);
end

%%%%% read back in the two created echo kernels 4096 samples at a time 	%%%%%%%
%%%%% and create a MATLAB object to write the watermarked audio 		%%%%%%%
spf2 = 4096;
afr3 = dsp.AudioFileReader('Echo1.wav', 'SamplesPerFrame', spf2);
afr4 = dsp.AudioFileReader('Echo2.wav', 'SamplesPerFrame', spf2);
totalFrames = counter * 8; %defines the total number of bits to be encoded
afw2 = dsp.AudioFileWriter('EchoWatermarked.wav', 'FileFormat', 'WAV');

%%%%% Set up counters to repeat the given string through the entire audio %%%%%%
mixCounter = 1;
lengthb = length(bitstream);
repeat = 0;

%%%%% Mix the two echo kernels by writing from one or the other depending 	%%%%%
%%%%% on the value of the current bit in the input bitstream 				%%%%%
while mixCounter <= totalFrames
	audio1 = afr3();
	audio2 = afr4();
	
	if(bitstream(mixCounter - repeat*lengthb) == 0) %Mix
		afw2(audio1);
	end
	if(bitstream(mixCounter - repeat*lengthb) == 1)
		afw2(audio2);
	end
	
	mixCounter = mixCounter + 1;
	if(mixCounter > lengthb * (repeat + 1)) %Repeat
		repeat = repeat + 1;
	end
end
			</code>
		</pre>

		<h5> ReadWatermarkedAudio </h5>
		<pre>
		  <code>
while ~isDone(afr) 
	audio = afr();
	%%%%%%%%%%% Take the Auto-Correlated Cepstrum %%%%%%%%%%%%%%%%%%
	oneChannel = audio(1:4096,1:1);
	AutoCepstrum = real((ifft(log(fft(oneChannel)).^2)).^2);
	c = AutoCepstrum;

	%parameters to define areas around expected peak locations
	RD0a = Delay0 - 50;
	RD0b = Delay0 - 5;
	RD0c = Delay0 + 5;
	RD0d = Delay0 + 50;
	RD1a = Delay1 - 50;
	RD1b = Delay1 - 5;
	RD1c = Delay1 + 5;
	RD1d = Delay1 + 50;

	%get mean and standard deviation around the peak, 
	%but not including the peak
	avgDelay0 = mean(mean([c(RD0a:RD0b), c(RD0c:RD0d)]));
	Delay0StdDev = mean(std([c(RD0a:RD0b), c(RD0c:RD0d)]));
	avgDelay1 = mean(mean([c(RD1a:RD1b), c(RD1c:RD1d)]));
	Delay1StdDev = mean(std([c(RD1a:RD1b), c(RD1c:RD1d)]));
	
	%Get the peak value at each of the expected peak locations
	%in terms of standard deviations above the mean
	Delay0value = (max(c(RD0b:RD0c)) - avgDelay0) / Delay0StdDev;
	Delay1value = (max(c(RD1b:RD1c)) - avgDelay1) / Delay1StdDev;
	
	%assuming that there is a peak at one of the locations
	%the location with the higher relative peak determines
	%the output bit value. Peak height varries so no single
	%threshold was sufficient
	if Delay0value >= Delay1value
			bitstream = [bitstream, 0];
	end
	if Delay1value > Delay0value
			bitstream = [bitstream, 1];
	end
end
			</code>
		</pre>
		<h2>
			Converting Bitstream Back to String
		</h2>

		<pre>
		  <code>
%%%%%% First clip the bitstream to whole 7-bit chars
BitLength = numel(opBit);
numChars = floor(BitLength / 7);
numUsableBits = floor(numChars * 7);
truncated = opBit(1:numUsableBits);

%%%%%% Then convert the stream of bits into a character array
reshaped = (reshape(truncated,7,[]).'); %place each group of 7 bits in 1 row
opBitTemp = num2str(reshaped);% convert the rows of 1s and 0s to strings
i = num2cell(opBitTemp, 2);% covert the array to a cell array(required by bin2dec)
decoded = char(bin2dec(i).');% converts into characters
		  </code>
		</pre>
		<h2>Least significant bit watermarking </h2>

		Least significant bid watermarking (LSB) is one of the simplest techniques there are out there for audio signals. Essentially what is does is it allows the hidden message to be embedded in the signal so it can not be detected via audio or visual. By changing the LSB in any chunk of data, the watermark can be hidden without changing the original audio file.

		<h3> Image in Audio</h3>
		By using the LSB technique, we are trying to embed an image in an audio signal. Most of the prior works have used one major operation to achieve this, the Discrete Cosine Transform (DCT). What this does is take an image which is in N by M pixels, then separated into 8 by 8 or 16 by 16 array of integers. Basically, this is used to break down the image into small parts. This can be mathematically expressed as:

		<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/cm.PNG?raw=true"  width="200" height="333">
			  Once the image is broken down into binary bits, you divide the audio into equal parts, apply LSB, and add the image and audio together.By using the Mean Squared Erro to check the difference between the two audio files. It gave an error of .0025. Which is exceptionally good conisdering 0 correlates to identical signals.

		<h2>Extracting the image:</h2>
		Essentially, extracting the image from the watermarked file is a very similar process. Divide the audio file with embedded image into equal parts and subtract the original signal. Once that is down apply the inverse of the DCT which can be described mathematically as:

		<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/fn.PNG?raw=true"  width="300" height="360">
		The result should be the embedded image.

		Below is sample of the image in and image out:

		<h5>In Image: </h5>

		<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/ball.PNG?raw=true"  width="200" height="200">

		<h5> Out Image: </h5>

		<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/ball_out.PNG?raw=true"  width="200" height="200">


		   

		<h3>Text in Audio LSB</h3>
		<h5>Example:</h5>
		To hide the letter A whose binary value is 01000001, we would replace the LSBs of the original audio with the binary value of A.
			1001011<mark>0</mark> 1000110<mark>1</mark> 1101001<mark>0</mark> 0100101<mark>0</mark> 0010011<mark>0</mark> 0100001<mark>0</mark> 0001010<mark>0</mark> 0101011<mark>1</mark>
		<h5>Original Audio </h5>

		<audio src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/w.wav?raw=true" type="audio/wav" controls="controls"></audio>

		<h5> Output Audio </h5>
		<audio src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/outputfile.wav?raw=true?" type="audio/wav" controls="controls"></audio>


		   
		 Mean-square error = 0.1830 

		<h2> Amplitude of input audio</h2>

		<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/input_amplitude.png?raw=true"  width="700" height="400">

		<h2> Output Amplitude </h2>
		<img src="https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/output_amplitude.png?raw=true"  width="700" height="400">
	</body>
</html>
