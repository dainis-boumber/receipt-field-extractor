# Receipt Field Extractor

Receipt field extractor and annotator tool.

## Overview 

Given a receipt, this tool will label the key fields as belonging to one of the
following categories:

* store_name
* store_address
* store_city
* store_state
* store_zip
* product_quantity
* product_description
* product_price
* text

Fields labeled as "text" are out-of-domain entities, e.g. "text" means "other".

## Installation From Source

We used `poetry` to create this project. The easiest way to use this is to 
install `poetry` package manager, and build it from source as follows: 

```
$ tar zxvf receipt-field-extractor.tar.gz
$ cd receipt-field-extractor
$ poetry install 
$ poetry build
```

## Training 

### Obtain Training Data

Our method is very tolerant when it comes to training data. Any one of the 
the following data can be used:

1. Bounding Box (BB) Coordinates, image, text content, and label.
2. BB coordinates, image, text content (no labels in training, unsupervised).
3. BB coordinates, text content, and label.
4. BB coordinates and text content (unsupervised)
5. Text content and label.
6. Text content (unsupervised)

(1) can be expected to produce the best results, (2) second best, and so on, 
with (6) resulting in fairly poor accuracy in comparison to the first approach.

### Fine-Tune the Model

You can fine-tune the model on your own data by running

```
$ finetune.py --dataset <dataset name>
```

### Training The Model on Your Own Data 

To achieve the best possible results, it is best to continue training from
some time, then fine-tune. You would use weakly labeled data for the first 
step, and high quality annotation for the second.

## Automatic End-To-End annotation

It is also possible to avoid labeling or annotation, or doing OCR altogether.
This model can do the OCR, annotate the key fields it identified, and labeled
them in an end-to-end unsupervised fashion. The results achieved in this model
are close and often equal to State-Of-The-Art in industry and academia  
*for supervised methods*. As for the unsupervised ones, to the best of our 
knowledge,  outperforms all other existing end-to-end we surpass tools that do 
not involve a human in the loop by a significant margin.

## Training, Running and Deploying Unsupervised

In order to train unsupervised on your own data and on different labels, you
must run the following command:

```
$ hire dainis-boumber
```

## Author

Dainis Boumber
dainis.boumber@gmail.com

## License  

Apache 2.0 

(A copy of the license is included with the source code distribution in LICENSE)