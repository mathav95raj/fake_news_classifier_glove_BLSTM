# fake_news_classifier_glove_BLSTM

A fake news classifier model is built with a Bidirectional LSTM and Glove embeddings of 100 dimension used as feature. 

Reason for choosing
BiLSTM - Vanilla Recurrent neural networks cannot remember long range dependencies in a sentence. A LSTM layer has forget, update and output gates which allow the model to have control on what information is retained and what is discarded. Since the full news text is available beforehand, a bidirectional layer allows us to interpret information from a sentence in both forward and reverse direction

Glove vectors - Traditional way of learning embeddings will result in a huge number of parameters to be learnt and there are high chances that the model might overfit. To avoid this issue, transfer learning was performed by utlizing pre trained embeddings from https://nlp.stanford.edu/projects/glove/
 
The glove vecotrs chosen for this project was learnt from Wikipedia 2014 + Gigaword 5 (6B tokens, 400K vocab, uncased, 100d) 

 Trainable parameters have been substantially reduced from 1 million to about 32 thousand.

A custom embedding layer class is implemented that performs backpropagation training for only a portion of the embedding matrix

Example:

Vocabulary of training set : 10k

words in training set that are also in Glove : 8k  (Non Trainable)

words in training set, not in Glove but each word occurs greather than WORD_FREQUENCY(see config) times : 1k (Trainable)

words in training set, not in Glove, each word occurs less frequently : represented by <other> token (Trainable)

Padding a news title to fixed length(see config): represented by <pad> token (Trainable)

I faced issue in implementing the custom class, a simple keras.concatenate would not do the job because the one hot vector indices were re numbered when I created a separate layer for fixed and variable embeddings.. instead of the embedding matrix looking like {0 1 ..7999 |8000.. 9001} it was like {0 1 ... 7999 | 0 1 .... 1001}
			


Thanks to https://github.com/sachinruk/deepschool.io for the custom class for concatenating fixed and trainable embedding layer..
related query by him in stack overflow: https://stackoverflow.com/questions/46032700/concatenate-embedding-layers/46149153#46149153
