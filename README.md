# fake_news_classifier_glove_BLSTM

A fake news classifier model is built with a Bidirectional LSTM and Glove embeddings of 100 dimension used as feature. 

Reason for choosing
BiLSTM - Vanilla Recurrent neural networks cannot remember long range dependencies in a sentence. A LSTM layer has forget, update and output gates which allow the model to have control on what information is retained and what is discarded. Since the full news text is available beforehand, a bidirectional layer allows us to interpret information from a sentence in both forward and reverse direction

Glove vectors - Traditional way of learning embeddings will result in a huge number of parameters to be learnt and there are high chances that the model might overfit. To avoid this issue, transfer learning was performed by utlizing pre trained embeddings from https://nlp.stanford.edu/projects/glove/
 
The glove vecotrs chosen for this project was learnt from Wikipedia 2014 + Gigaword 5 (6B tokens, 400K vocab, uncased, 100d) 

 Trainable parameters have been substantially reduced from 1 million to about 32 thousand.

When a training set is passed, a custom embedding layer class separates out 
words present in glove
frequent words present in the training set (frequency adjusted in config)
			
The nonfrequent words are designated a common <other> token. The sequence length is padded according to the maximum news title length (adjusted in config)

Thanks to https://github.com/sachinruk/deepschool.io for the custom class for concatenating fixed and trainable embedding layer..
related query by him in stack overflow: https://stackoverflow.com/questions/46032700/concatenate-embedding-layers/46149153#46149153
