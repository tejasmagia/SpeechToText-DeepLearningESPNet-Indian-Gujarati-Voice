# SpeechToText-DeepLearningESPNet-Indian-Gujarati-Voice

This project has 2 parts to it,
1] Data Creation for Model training
2] Using generated data implement Indian Gujarati ASR model

Steps 1] Data Creation for Model training – Project Completed

Google Sppech2Text Gujarati Text conversion

What we are doing
I have used client Google Speech to Text api (https://cloud.google.com/speech) using following variation to find high accuracy of Gujarati text. For running the conversion used google.cloud_speech_v1p1beta1 library using python language.
Speech Recognition for Indian Language – Gujarati using google api
• Adjusting Audio speed (playback speed)
• Adjusting Audio Bit Rate
• Adjust different audio type (like flac, wav)
• Adjust Audio slicing 
• Detect and slice silence portion 
• Adjust Rewind for Slicing audio

Measured Accuracy %
To understand how much manual efforts will be required for user we have generated accuracy % between Google generated text and manually corrected the google generated text by user. The 30 mins audio file shows 69% accuracy which means to correct the 30 mins file user need to spend 3-4 hrs of manual efforts. The attached excel file analysis was performed on Feb 2019.  Currently if user listen to audio and type it on computer then 30 mins will take 6 hrs.
Attached 30 mins Audio Accuracy Analysis_Feb2019.xlsx

For accessing google api and project, used Google Id: XXXXXXX@gmail.com.
Accuracy% not Improving
Recently we have started using google SpeechToText api where few audio text we have compared between Google generated text and User corrected google generated text which is as follows,
Attached Original File from Cloud Service.txt 	
Attached Manually corrected by User.pdf
 
In the above audio text speech starts from 00:03:22 - 00:03:48 timestamp onwards. 


Step 2] Using ESPNet model implementing SpeechToText for Indian language Gujarati
ASR

Next Steps:
1.	Explore ESPnet (https://github.com/espnet/espnet) - get it running on some local setup (laptop)
2.	Confirm that our annotated Gujarati dataset can be converted to ESPnet’s data format
3.	Identfiy other datasets which can be of help (LibriSpeech, Wall Street Journal etc.)

What we need
Automatic Speech Recognition (ASR) which works for Gujarati (with some English) spoken in Gujarati voice. Word-Error-Rate (WER) needs to be at 15 or less.

ASR methods
There are two distinct ways of doing it:
1.	Cascade Models
a.	Acoustic Model - converts audio inputs to individual phonemes
b.	HMM model - converts phonemes to characters
(with reps… “CCCCATTTTT” instead of “CAT”)
c.	CTC Loss - resolves repeating characters
d.	Language Model - makes sure that generated sentences are grammatical
2.	End-to-End Models
a.	single model which converts audio input to written sentences
Cascade Models get better performance but have a lot more moving parts, each of which requires effort. Using them would need multiple people who have a lot of experience in AI. We should not go for Cascade Models, because we won’t be able to track the effort.
End-to-End Models, do get competitive performances and are much easier to handle. Further, since we have a very narrow domain (one speaker one language), the choice of method might not matter much.

End-to-End Models
Some frameworks exist, which are pretty good. Of them, ESPnet (https://github.com/espnet/espnet) is the one that was strongly suggested.

Data
Just 10 hours of data in Gujarati is not enough data to train these models. So the suggestion is to either:
1.	get a pretrained model (trained on bigger public datasets) and finetune them for our prupose
2.	get hold of bigger public datsets ourselves to do the pretraining of the model
a.	Wall Street Journal (WSJ) dataset https://catalog.ldc.upenn.edu/LDC93S6A
b.	LibriSpeech http://www.openslr.org/12/
c.	https://towardsdatascience.com/a-data-lakes-worth-of-audio-datasets-b45b88cd4ad

