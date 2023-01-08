# OpenAI model trained on ENS support docs

## Steps

- Install the [OpenAI CLI](https://beta.openai.com/docs/guides/fine-tuning/cli-data-preparation-tool) with extra dependencies

  ```bash
  pip install --upgrade openai
  pip install openai[datalib]
  ```

- Create a set of training data in [this Google Sheet](https://docs.google.com/spreadsheets/d/1ocByT31GyWlJpAID87ID31K9HgkH6bFgMp3xR-Q8PHE/edit?usp=sharing) based on the [ENS support docs](https://support.ens.domains/docs)
- Download a CSV of the Google Sheet and prepare a JSONL file

  ```bash
  openai tools fine_tunes.prepare_data -f <LOCAL_FILE>
  ```

- Create a fine-tuned model from the training data

  ```bash
  openai api fine_tunes.create -t <TRAIN_FILE_ID_OR_PATH> -m <BASE_MODEL: ada|curie|davinci>
  ```

- View the status of all models

  ```bash
  openai api fine_tunes.list
  ```

- [Make a request](https://beta.openai.com/docs/guides/fine-tuning/use-a-fine-tuned-model) to the new model
  ```bash
  openai api completions.create -m <FINE_TUNED_MODEL> -p <YOUR_PROMPT>
  ```
