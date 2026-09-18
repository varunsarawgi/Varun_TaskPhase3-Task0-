# Task 0.4: ML Fundamentals and Data Preprocessing

These are my notes on Task 0.4, written the way I'd actually explain the ideas to myself if I were revising the night before a quiz on this.

## 1. Overview of AI and ML

### 1.1 What AI actually means
Artificial Intelligence is the big umbrella term for getting a machine to do things that normally need human intelligence. That could be recognizing a face, understanding a sentence, or deciding the best move in chess. AI itself isn't one technique, it's more of a goal.

## 2. Supervised and Unsupervised Learning

### 2.1 Supervised learning explained
In supervised learning, every example you give the model already comes with the correct answer attached, called a label. If you're training a model to recognize handwriting, every image of a digit comes tagged with which digit it actually is. The model's whole job is to learn the mapping from input to that known output, so that later it can predict the label for something it has never seen.

### 2.2 Unsupervised learning explained
Unsupervised learning removes the labels entirely. You just hand the model a pile of data and ask it to find structure on its own, things like natural groupings or patterns. A classic example is clustering customers into segments based on their shopping behavior, without ever telling the model what those segments should be beforehand.

### 2.3 SL vs USL
If there's an answer key involved during training, it's supervised. If the model is left to explore the data with no answer key at all, it's unsupervised. That single question settles it almost every time.

## 3. Training, Validation and Test Sets

### 3.1 Why we split data at all
If a model is trained and then judged on the exact same data, it's basically taking an exam it already memorized the answers to. To actually know if it learned something useful, we have to test it on data it has never touched.

### 3.2 The training set
This is the portion the model actually learns from. It sees these examples repeatedly and adjusts itself based on them.

### 3.3 The validation set
While building and tuning the model, we check its performance against the validation set. This helps decide things like how complex the model should be, without ever letting it peek at the final test data.

### 3.4 The test set
This chunk is set aside and left completely untouched until the very end. Once the model is finished, it's evaluated on the test set exactly once, giving an honest picture of how it would perform in the real world.

### 3.5 Typical split ratios
A common approach is something like seventy percent training, fifteen percent validation, and fifteen percent test, though the exact numbers shift depending on how much data you actually have available.

## 4. What a Model Is and How Training Works

### 4.1 Defining a model
Underneath all the buzzwords, a model is just a mathematical function that takes an input and produces an output. What makes it useful is that this function has adjustable internal numbers that can be tuned so the output gets closer and closer to correct.

### 4.2 Parameters and weights
Those adjustable internal numbers are called parameters or weights. Training a model really just means finding good values for these numbers.

### 4.3 The training loop
The process usually goes like this. First, the model looks at an input and makes a prediction. Second, that prediction is compared against the actual correct answer. Third, the size of the mistake is calculated. Fourth, the model's internal numbers are nudged slightly in a direction that would have reduced that mistake. This whole cycle repeats thousands or even millions of times.

### 4.4 Loss and why it matters
The measurement of how wrong the model currently is gets a specific name, the loss. Training is essentially the process of gradually pushing that loss value down as far as it will reasonably go.

## 5. Why Data Needs Cleaning and Preprocessing

### 5.1 The garbage in garbage out idea
A model can only ever be as good as the data it learns from. If the data fed into it is messy or wrong, the model will confidently learn the wrong things, and no amount of clever algorithm design can fix that afterward.

### 5.2 Common problems in raw data
Real datasets almost never arrive clean. There are missing entries, inconsistent formatting, duplicate rows, typos, mismatched units, and values that are just plain wrong due to human or sensor error.

### 5.3 What good preprocessing achieves
Cleaning and preprocessing turns messy raw data into something consistent and trustworthy, so that whatever pattern the model ends up learning actually reflects reality instead of noise or errors in the dataset.

## 6. Handling Missing Data

### 6.1 Why data goes missing
Values can be missing for all sorts of reasons. A sensor might fail, a survey question might get skipped, or a record might simply never have been entered in the first place.

### 6.2 Deletion
When only a small number of rows or columns are affected, sometimes the simplest fix is to just remove them, as long as doing so doesn't throw away too much useful information.

### 6.3 Mean median and mode imputation
Often it's better to fill the gap instead of deleting it. Using the mean works fine for fairly symmetric numeric data. The median is a safer choice when the data is skewed, since it isn't dragged around by extreme values. The mode, meaning the most frequent value, is used for categorical columns where an average doesn't even make sense.

### 6.4 Predictive imputation
A more advanced option is to use the other columns in the dataset to actually predict what the missing value probably was, essentially treating the missing value itself as a small prediction problem.

### 6.5 Flagging missingness
Sometimes the fact that a value is missing carries information on its own. In those cases, it can help to add a new column that simply marks whether the original value was missing, so the model can learn from that pattern too.

## 7. Handling Outliers

### 7.1 What counts as an outlier
An outlier is a value that sits way outside the normal range of the rest of the data, like someone's recorded age showing up as two hundred and fifty.

### 7.2 Detecting outliers with IQR
One common method looks at the interquartile range, which covers the middle fifty percent of the data. Anything sitting far outside that middle range gets flagged as a potential outlier.

### 7.3 Detecting outliers with SD
Another method measures how many standard deviations a value sits away from the mean. A value that's unusually far from the mean in either direction gets flagged the same way.





## 8. Feature Scaling

### 8.1 Why scale matters to a model
Different features in a dataset often live on completely different scales, like age ranging up to a hundred while income ranges into the millions. Some models mistakenly treat the feature with bigger numbers as more important, simply because its numbers are larger.

### 8.2 Normalization
Normalization, often called min max scaling, squeezes every value in a feature into a fixed range, typically between zero and one.

### 8.3 Standardization
Standardization instead reshapes a feature so that its average becomes zero and its spread becomes one standard deviation, which is especially useful when the data roughly follows a normal distribution.

### 8.4 When scaling is not necessary
Not every model actually needs this step. Tree based models generally don't care about the scale of the input, while distance based models like K nearest neighbors depend on it heavily.

## 10. Overfitting and Underfitting

### 10.1 What overfitting looks like
Overfitting happens when a model learns the training data so thoroughly that it starts memorizing its noise and quirks along with the real pattern. It ends up performing great on the training data but noticeably worse once it sees anything new.

### 10.2 What underfitting looks like
Underfitting is the opposite problem. The model is too simple to even capture the real pattern in the first place, so it performs poorly everywhere, including on the very data it trained on.


## 10. Evaluation Metrics

### 10.1 Accuracy
Accuracy simply measures the percentage of predictions that turned out correct. It sounds like the obvious metric to use, but it can be misleading, especially when one class is far more common than another.

### 10.2 Precision
Precision looks only at the cases the model predicted as positive, and asks how many of those were actually positive. This matters a lot when a false alarm is costly.

