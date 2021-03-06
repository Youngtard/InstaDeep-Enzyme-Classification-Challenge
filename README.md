Link to competition - https://zindi.africa/competitions/instadeep-enzyme-classification-challenge

My model is a fine-tuned pretrained model (ProtBert) that was trained on billions of protein sequence data (BFD). It is based on the Transformers architecture - BERT  in particular. The pretrained model can be found [here](https://huggingface.co/Rostlab/prot_bert_bfd). There was no need for me to use the given unlabelled sequences. There is a similar pretrained [model](https://huggingface.co/Rostlab/prot_bert) trained on lesser data. Both give good results. As it is integrated into the HuggingFace library, one can easily use them in similar fashion as other popular models like BERT.

There was no need for much fine-tuning as one could get good results of about 90%+ accuracy with little to no tuning. The data is also large enough to learn from various patterns.

### Setup
Due to the number of model parameters (~420M), large data size, and high max sequence length (384), I had to use a TPU (v3-8) for fast model training. 1 epoch runs for ~60 minutes.

### Model parameters
* Max sequence length -  I used 384 so as to boost my score. 256 and below also give good results.
* Epochs - 1 epoch was enough to reach reasonable convergence and generalization. I didn't train for more than that.
* AdamW optimizer.
* 5e-5 Learning rate with scheduling.
* Batch size  - 16 * 8 (TPU cores)

I used TensorFlow as it's more TPU friendly.
