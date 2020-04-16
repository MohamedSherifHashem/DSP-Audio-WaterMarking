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
<img src= "https://github.com/MohamedSherifHashem/DSP-Audio-WaterMarking/blob/gh-pages/images/peak512.png?raw=true"  width="500" height="333">

<h2> Taking Watermark as input from User </h2>

<pre>
  <code>
   bitstream = addwatermark();
   AddEchoFunction(bitstream);
    
    %disp('Error, Must be 10 characters!');% if user input is not exactly 10, error pops up
  </code>
</pre>


<h2> Adding the watermark </h2>

<pre>
  <code>
   function bitstream=addwatermark()


    c = [1,50]; % setting a limit on input length
    phrase = [ 'Please enter any word:' newline];
    prompt = phrase;
    code = input(prompt,'s'); % getting user input and storeing it

    b = size(code); % getting the size of user input


    if (b<=c )  % checking to make sure its only 10 characters
    
     z= double(code); % getting ASCII value
   
     x = dec2bin(z); % taking ASCII value and turning into binary
     
     %this turns the code into a 10 by 7 matrix so I resized it into y
 
     y= reshape(x',[1,numel(x)]); % resize
     
     a = size(y); %checking the size of which turns out is 1 by 70 not 1 by 80
     
      Y = mat2cell(y,1,ones(numel(y),1)); % taking the reshaped and creating a cell
      
       K = convertCharsToStrings(Y); % takes cell on converts to a string
       
        P = str2double(K); %turns string into double.
        bitstream = P;
       
        
        
        
      disp('Thank you, your word is stored'); 

    end
    end
  </code>
</pre>

<h2>Add Echo Function </h2>

<pre>
  <code>
  function [] = AddEchoFunction(bitstream)
spf = 32768;
for i = 1:2
    %%%%%%%%%%%%%%%%%%%%% Create MATLAB objects to read the audio file %%%%%%%%
    afr1 = dsp.AudioFileReader('C:\Program Files\MATLAB\AudioFiles\TheCarSong.mp3', 'SamplesPerFrame', spf);
    afr2 = dsp.AudioFileReader('C:\Program Files\MATLAB\AudioFiles\TheCarSong.mp3', 'SamplesPerFrame', spf);

    %%%%%%%%%%%%%%%%%% Create MATLAB objects to write new audio files %%%%%%%%%

    afw1 = dsp.AudioFileWriter('Echo1.wav', 'FileFormat', 'WAV');
  
    afw2 = dsp.AudioFileWriter('Echo2.wav', 'FileFormat', 'WAV');
   
    %%%%%%%%%%% Create MATLAB object to play the altered audio %%%%%%%%%%%%%%%%
    adw = audioDeviceWriter('SampleRate', afr2.SampleRate);

    %%%%%%%%%%%% every time an audio file reader is called, it %%%%%%%%%%%%%%%
    %%%%%%%%%%%% returns the next 1024 x 2 array of the file   %%%%%%%%%%%%%%
    %%%%%%%%%%%% If one copy is called first before we start   %%%%%%%%%%%%%%
    %%%%%%%%%%%% The loop, it is ahead by one step.             %%%%%%%%%%%%%%

    delay = 256*i;    %%%%%%%% Alter this value to change the added delay

    afterDelay = delay + 1;
    startSecond = spf + 1 - delay;
    endFirst = spf - delay;

    counter = 0;
    audio2 = afr2();
    audio4 = zeros(spf,2);  %initialize temp matrix for splicing

    firsthalf = audio2(afterDelay:end,1:2);%take the second half of the first chunk

    while ~isDone(afr1)%counter < 500
        audio4(1:endFirst,1:2) = firsthalf;  %use it as the first half of the splice

        audio1 = afr1();
        audio2 = afr2();

                                                    %use the first half of the
        audio4(startSecond:end,1:2) = audio2(1:delay,1:2);    %second chunk as the second
                                                    %half of the splice.

        firsthalf = audio2(afterDelay:end,1:2);%take the second half of the second 
                                        %chunk and save it for next time

        audio3 = (audio1 * 1) + (audio4 * .3);
    %     if counter == 1       This is an alternate way of creating echo,
    %        afr2.reset();      reset starts the second copy at the beginning
    %     end                   It is limited to multiples of the chunk size

        %adw(audio3);            %play the audio chunk
        
        if(i == 1)
            afw1(audio3);            %save the audio chunk
        end
        if(i == 2)
            afw2(audio3);            %save the audio chunk
        end
        counter = counter + 1;  %then move to the next chunk
    end
    %afr1.reset();
    %counter = 0;
    %while counter < 500
     %   audio1 = afr1();
      %  adw(audio1);
       % counter = counter +1;
    %end
    release(afr1); 
    release(afr2); 
    release(adw);
    release(afw1);
    release(afw2);
end
spf2 = 4096;
afr3 = dsp.AudioFileReader('Echo1.wav', 'SamplesPerFrame', spf2);
afr4 = dsp.AudioFileReader('Echo2.wav', 'SamplesPerFrame', spf2);
totalFrames = counter * 8;

afw2 = dsp.AudioFileWriter('EchoWatermarkedTest.wav', 'FileFormat', 'WAV');

mixCounter = 1;
lengthb = length(bitstream);
repeat = 0;

while mixCounter <= totalFrames
    audio1 = afr3();
    audio2 = afr4();
    
    if(bitstream(mixCounter - repeat*lengthb) == 0)
        afw2(audio1);
    end
    if(bitstream(mixCounter - repeat*lengthb) == 1)
        afw2(audio2);
    end
    
    mixCounter = mixCounter + 1;
    if(mixCounter > lengthb * (repeat + 1))
        repeat = repeat + 1;
    end
end
  </code>
</pre>
