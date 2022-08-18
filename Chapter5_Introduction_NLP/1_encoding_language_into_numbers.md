- The most common way to encode language into numbers is to encode by letters, as is done naturally when strings are stored in your program. In memory, however, you don’t store the letter a but an encoding of it—perhaps an ASCII or Unicode value, or something else. For example, consider the word `listen`. This can be encoded with ASCII into the numbers 76, 73, 83, 84, 69, and 78. This is good, in that you can now use numerics to represent the word. But then consider the word `silent`, which is an antigram of listen. The same numbers represent that word, albeit in a different order, which might make building a model to understand the text a little difficult.


- A better alternative might be to use numbers to encode entire words instead of the letters within them. In that case, silent could be number x and listen number y, and they wouldn’t overlap with each other.
Using this technique, consider a sentence like `“I love my dog.”` You could encode that with the numbers [1, 2, 3, 4]. If you then wanted to encode `“I love my cat.”` it could be [1, 2, 3, 5]. You’ve already gotten to the point where you can tell that the sentences have a similar meaning because they’re similar numerically—[1, 2, 3, 4] looks a lot like [1, 2, 3, 5]. This process is called tokenization.

## 2. Tokenization
- TensorFlow Keras contains a library called preprocessing that provides a number of extremely useful tools to prepare data for machine learning. One of these is a Tokenizer that will allow you to take words and turn them into tokens

```python
import tensorflow as tf
from tensorflow.python import keras
from keras.preprocessing.text import Tokenizer


sentences = [
    'Today is a sunny day',
    'Today is a rainy day'
]

tokenizer = Tokenizer(num_words=100)
tokenizer.fit_on_texts(sentences)
word_index = tokenizer.word_index
print(word_index)
```
In this case, we create a `Tokenizer` object and specify the number of words that it can tokenize. This will be the maximum number of tokens to generate from the corpus of words. We have a very small corpus here containing only six unique words, so we’ll be well under the one hundred specified.

Once we have a tokenizer, calling `fit_on_texts` will create the tokenized word index. Printing this out will show a set of key/value pairs for the words in the corpus, like this:


```console

{'today': 1, 'is': 2, 'a': 3, 'day': 4, 'sunny': 5, 'rainy': 6}
```

This behavior is controlled by the filters parameter to the tokenizer, which defaults
to removing all punctuation except the apostrophe character. So for example, “Today
is a sunny day” would become a sequence containing [1, 2, 3, 4, 5] with the preceding
encodings, and “Is it sunny today?” would become [2, 7, 4, 1]. Once you have the
words in your sentences tokenized, the next step is to convert your sentences into lists
of numbers, with the number being the value where the word is the key.


### 2.2. Using out-of-vocabulary tokens



### 2.3. Understanding padding
When training neural networks you typically need all your data to be in the same
shape. Recall from earlier chapters that when training with images, you reformatted
the images to be the same width and height. With text you face the same issue—once
you’ve tokenized your words and converted your sentences into sequences, they can
all be different lengths. To get them to be the same size and shape, you can use
`padding`
