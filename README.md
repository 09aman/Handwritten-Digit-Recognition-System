# MNIST Handwritten Digit Recognition — Streamlit App

A small web app for the three Keras models in `Handwritten_Digit_Recognition.ipynb`:
- Dense baseline
- ANN
- CNN

The app lets you draw a digit or upload an image, select a trained model, and view the predicted digit and class probabilities.

## 1. Train and save the models

1. Open `Handwritten_Digit_Recognition.ipynb` in Jupyter.
2. Select the `Python (tensorflow_env)` kernel.
3. Make sure `mnist_train.csv` and `mnist_test.csv` are available where the notebook expects them.
4. Run the notebook from top to bottom so that `perceptron`, `ann`, and `cnn` are trained.
5. Run the model-saving cell at the end of the notebook. It creates:
   - `models/mnist_dense_model.keras`
   - `models/mnist_ann_model.keras`
   - `models/mnist_cnn_model.keras`

**Important:** The notebook currently uses raw pixel values in the 0–255 range (it does not divide the pixel values by 255). The app preprocesses input images to the same range. If you change the notebook's preprocessing later, update `preprocess_image()` in `app.py` to match.

## 2. Install the app dependencies

Open Terminal and move into this folder:

```bash
cd path/to/mnist_digit_app
```

Activate the environment that has TensorFlow:

```bash
conda activate tensorflow_env
```

Install the app packages:

```bash
python -m pip install -r requirements.txt
```

If TensorFlow 2.21.0 is already installed in this environment, pip will normally leave it in place.

## 3. Run the app

```bash
python -m streamlit run app.py
```

Streamlit will print a local URL, usually:

```text
http://localhost:8501
```

Open that URL in your browser.

## 4. Project structure

```text
mnist_digit_app/
├── app.py
├── requirements.txt
├── README.md
├── Handwritten_Digit_Recognition.ipynb
└── models/
    ├── README.txt
    ├── mnist_dense_model.keras   # generated after training
    ├── mnist_ann_model.keras     # generated after training
    └── mnist_cnn_model.keras     # generated after training
```

The `.keras` files are trained Keras models. They are the deep-learning equivalent of saved model artifacts such as `.pkl` files often used with scikit-learn.

## Troubleshooting

### `ModuleNotFoundError: No module named 'tensorflow'`

Check that the active environment is the TensorFlow environment:

```bash
conda activate tensorflow_env
python -c "import tensorflow as tf; print(tf.__version__)"
```

Then launch Streamlit from that same Terminal window.

### Model file not found

Run the model-saving cell in the notebook. Confirm that the three `.keras` files are inside the app's `models/` folder.

### The app predicts the wrong digit for a photo

MNIST images normally have a dark background and a bright digit. The app attempts to invert white-background images and centre the digit. Clear, high-contrast images containing one digit work best. Predictions on camera photos may be less accurate than predictions on MNIST-like images.
