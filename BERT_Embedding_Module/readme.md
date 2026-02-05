# Co-Speech Gesture Generator (BERT Version)

This is a modified implementation of *Robots learn social skills: End-to-end learning of co-speech gesture generation for humanoid robots* ([Paper](https://arxiv.org/abs/1810.12541)).

While the original paper used the TED dataset and FastText, this repository has been adapted to use the [Talking With Hands 16.2M](https://github.com/facebookresearch/TalkingWithHands32M) dataset and **BERT embeddings** for text processing.

## Environment

The code was developed using Python 3.8 on Ubuntu 18.04. PyTorch 1.5.0 was used.

## Installation & Preparation

1. **Install dependencies**
    ```bash
    pip install -r requirements.txt
    ```

2. **Generate BERT Embeddings**
    Before training, you must generate the BERT embeddings for the dataset.
    
    * Navigate to the `scripts/text_bert` directory.
    * Open `embedding.py` and **manually update the dataset paths** to match your local environment.
    * Run the script:
        ```bash
        cd scripts/text_bert
        python embedding.py
        ```

3. **Make LMDB** (If not already done via the embedding step or previous processing)
    ```bash
    cd scripts
    python twh_dataset_to_lmdb.py [PATH_TO_DATASET]
    ```

## Train

To train the model using the BERT configuration:

1. Update paths and parameters in `config/seq2seq_bert.yml` if necessary.
2. Run the training script:
    ```bash
    python train_bert.py --config=../config/seq2seq_bert.yml
    ```

## Inference

To generate gestures from speech text (TSV files) using a trained checkpoint:

```bash
python inference_bert.py [PATH_TO_MODEL_CHECKPOINT] [PATH_TO_TSV_FILE_FOLDER]
