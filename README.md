# Basic named entity recognition with BERT

This repo contains a bare-bones deployment of a named entity recognition model (NER) with BERT, using Docker and FastAPI. The model is fine-tuned on the Kaggle [generic NER dataset](https://www.kaggle.com/abhinavwalia95/entity-annotated-corpus) following [this tutorial](https://www.depends-on-the-definition.com/named-entity-recognition-with-bert/).  


## Model finetuning

* To fine-tune a model, open the `BERT_NER_training.ipynb` notebook in Google Colab and run through the cells in the `Model training` section. You will need to place the dataset csv found [here](https://www.kaggle.com/abhinavwalia95/entity-annotated-corpus) into a location of your choice in Google Drive and change the path accordingly in the `os.chdir` cell. To report model metrics, we used `seqeval`. 
* Once the finetuning is done, the model checkpoint should be dropped to your local directory in Drive. 
* Copy the model checkpoint file to (a) `finetuned_models/` and (b) `docker/finetuned_models/`. Due to git's file size requirements, we are unable to upload the actual models. 

## Inference

Once the models are in the correct places, you can simply perform inference on your local computer (make sure you load the dependencies specified in `environment.yml`). The example text specified there outputs (upon running `python inference.py`):

```
{
	'extracted_entities': "[('Divy', 'B-per'), ('Murli', 'I-per'), ('United', 'B-geo'), ('States', 'I-geo'), ('UCSB', 'B-org'), ('June', 'B-tim'), ('2014', 'I-tim'), ('6pm', 'B-tim')]", 
	'BERT_tokenized': ['[CLS]', 'Di', '##vy', 'Mu', '##rl', '##i', 'lives', 'in', 'the', 'United', 'States', 'and', 'went', 'to', 'college', 'at', 'UC', '##SB', 'in', 'June', '2014', 'at', '6', '##pm', '.', '[SEP]'], 
	'predicted_labels': ['O', 'B-per', 'B-per', 'I-per', 'I-per', 'I-per', 'O', 'O', 'O', 'B-geo', 'I-geo', 'O', 'O', 'O', 'O', 'O', 'B-org', 'B-org', 'O', 'B-tim', 'I-tim', 'O', 'B-tim', 'I-tim', 'O', 'O']
}
```

