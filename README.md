# Trigger Word Detection
Trigger word detection is the technology that allows devices like Amazon Alexa, Google Home, Apple Siri, etc to wake up upon hearing a certain word. Here trigger word will be "activate". Every time it hears you say "activate", it will make a "chiming" sound.

Audio of word 'activate' is mixed with audio of background noise of different environments and different words other than activate to create training set. Output is 1 after you finish saying activate, else output is 0. 

### From Audio Recordings to Spectrograms

What really is an audio recording? 
* A microphone records little variations in air pressure over time, and it is these little variations in air pressure that your ear also perceives as sound. 
* You can think of an audio recording as a long list of numbers measuring the little air pressure changes detected by the microphone. 
* We will use audio sampled at 44100 Hz (or 44100 Hertz). 
    * This means the microphone gives us 44,100 numbers per second. 
    * Thus, a 10 second audio clip is represented by 441,000 numbers (= $10 \times 44,100$). 

#### Spectrogram
* It is quite difficult to figure out from this "raw" representation of audio whether the word "activate" was said. 
* In  order to help our sequence model more easily learn to detect trigger words, we will compute a *spectrogram* of the audio. 
* The spectrogram tells us how much different frequencies are present in an audio clip at any moment in time. 


### Building the Model

Our goal is to build a network that will ingest a spectrogram and output a signal when it detects the trigger word. This network will use 4 layers:

    * A convolutional layer
    
    * Two GRU layers
    
    * A dense layer. 

Here is the architecture we will use.

<img src="images/model.png" style="width:600px;height:600px;">

Output at each timestamp is probability of output being 1.

#### Insert a chime to acknowledge the "activate" trigger
* Once we've estimated the probability of having detected the word "activate" at each output step, we can trigger a "chiming" sound to play when the probability is above a certain threshold. 
