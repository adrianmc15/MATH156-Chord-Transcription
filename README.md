# Chord Transcription with CNNs and RNNs

## Strategy

Goal: based on a recording, get the chords at the correct times transcribed.

## Options for Dataset

- **jazznet Dataset**: a bunch of midi-generated piano audio files including scales, chord progressions and arpeggios (with annotation ofc)

    Link: https://github.com/tosiron/jazznet/tree/main


- **POP909 Dataset**: A bunch of piano versions of pop songs with chord annotations based on time

    Link: https://paperswithcode.com/dataset/pop909

- **C4DM**: Annotated Pop music recordings database
        
    Link: https://citeseerx.ist.psu.edu/viewdoc/download;jsessionid=48A228C90AD010F76AB98DA6820E2CC0?doi=10.1.1.207.4076&rep=rep1&type=pdf

I think I will try to use each of these in order to work with more and more complexity to see how far we can go. I think starting off with the jazznet dataset, we could get something working with the chord progressions at least, and then the POP909 would be more challenging bc it has real recordings

## Model

Based on preliminary reading, the approach needs to involve several parts:

1. Timesplicing - finding the changes in chords from an audio file or chord sequence
2. Preprocessing and transformation of the data -> for example, taking the DFT (or CQT) of the spliced chords
3. Classification. This involves both a sequence and pattern matching components -> which will likely combine both an RNN and a CNN to take both of these into account

Some papers to reference the model from:
1. https://arxiv.org/pdf/2008.12710.pdf
2. https://arxiv.org/pdf/1612.05082.pdf
3. https://archives.ismir.net/ismir2015/paper/000096.pdf
4. https://ieeexplore.ieee.org/abstract/document/7738895?casa_token=AsXqhmXafx8AAAAA:WpMlyNZeF78m3_YHIXm7XkVhP3HAbkZr-5ksJN2waLlXzE7FlimAA2DWDAJbAEHa_QrZKTFPOw
5. https://ismir2013.ismir.net/wp-content/uploads/2013/09/243_Paper.pdf
6. https://ieeexplore.ieee.org/abstract/document/7738895?casa_token=AsXqhmXafx8AAAAA:WpMlyNZeF78m3_YHIXm7XkVhP3HAbkZr-5ksJN2waLlXzE7FlimAA2DWDAJbAEHa_QrZKTFPOw
7. https://ieeexplore.ieee.org/abstract/document/8523662?casa_token=yq_8-_722icAAAAA:RPQpKZMGXdPIynDRWBJ4TyMOocaPRa_Q1EFdEE1XttZb4q2d8nPoyY-YY8x6uo-sPu0JE3IVXw 
8. https://www.kaggle.com/code/davidbroberts/chord-progression-maker/notebook



I will read these papers to get an idea of a good system

Additional Reading:
- https://towardsdatascience.com/conditional-random-fields-explained-e5b8256da776 

## Stages of Development
Development will need to happen in a few stages so that I have real results to show in the presentation. The stages will be as follows:

Edit (2 Dec): goals have been changed slighty: just to explore chord recognition with CNN + signal processing (maybe compare different methods)

#### Attempt 1: Exploration
Plan:
Do a CNN for just the chord recognition - on the separated chords from jazznet to demonstrate
-  Preprocessing idea: extract the most prominent frequencies from the CQT of the chord and their respective magnitudes
- rearrange them, and extract the differences between them
- add these into the training dataframe
- train the model with and without the spectograms

Results:
- the model for the manual chord extraction didn't work super well
- the pure CNN on the spectograms didn't work super well. Now going to attempt a slightly different approach, based on some papers online

#### Attempt 2: Building blocks
Plan:
- start with just major/minor model similar to kaggle
- try to expand to diminished and augmented


#### (Not in plan any more)

2. Try to do a RNN or a CRF on the chord sequence
3. Try a combined model