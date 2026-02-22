# Analyzing Text Data -- Week 4
### Checking for missing or duplicate values and removing them 
```
data.isnull().sum()
# checking for duplicate values
data.duplicated().sum()
# keeping only the first occurence of duplicate values and dropping the rest
data = data.drop_duplicates(keep = 'first')
# reseting the index of the dataframe
data = data.reset_index(drop = True)
```

## Text Preporcessing
### Why Remove Special Characters in Text Preprocessing?
* Special characters can introduce unnecessary elements, complicating text analysis.
* Clean text is simpler to work with and understand.
* However, as text become larger and contain various patterns of special characters, manually handling like use of **replace()** becomes tedious.
* In such cases, we need more flexible methods to efficiently identify and remove multiple patterns at once - **this is where advanced tools like regular expressions come in handy**.
* Suppose you have a string, and you are interested in adding a character between each of its characters
  * This is where the **join method** comes to rescue.
    * The **join()** method takes all characters in a string and joins them into one string with a sepataror.
    * A string must be specified as the separator.
    *  Syntax : string.join(list)
```
import re
string = "Regular expressions"
' '.join(string)
# As we can observe, the string 'space' has been added between each character in the string
# output - R e g u l a r   e x p r e s s i o n s
```
### Regular Expressions
#### 1. Pattern: [a-z] 
* Use Case: Extracting lowercase letters from usernames.
* Description: This pattern matches any single lowercase letter from 'a' to 'z'. It can be used to ensure usernames contain only lowercase letters.
```
pattern = r'[a-z]'
# Finding the specified pattern and replacing lowercase characters with a blank string
new_text = ''.join(re.sub(pattern, ' ', text))
```
* The **r prefix** creates a raw string, preventing Python from interpreting backslashes as escape characters, which is essential when working with regular expressions that often use backslashes.
* [] define a character set, which matches any one character from a specified set of characters inside the brackets.
* If you put a hyphen between characters like [a-z], it matches any character in that range, so [a-z] matches any lowercase letter from a to z.
* The **re** library in Python includes many built-in functions, one of which is **re.sub**, used for substituting occurrences of a specified regex pattern in a string.
  * **re.sub(pattern, replacement, string)** -- This function is used to replace occurrences of a pattern in a string.
    * **pattern**: The regular expression that defines the sequence of characters you want to search for in the string.
    * **replacement**: The string that will replace each occurrence of the pattern found in the original string.
    * **string**: The input string where the search and replacement will occur
* same logic mentioned above for pattern [A-Z] or [0-9]
#### 2. Pattern: [^]
* The **^ character is used as a negation operator** in regular expressions.
* **Any pattern mentioned after the ^ character will be excluded from consideration.**
* **Use Case:** Removing all non-numeric characters from a string of digits.
* Description: The pattern [^0-9] matches any character that is not a digit. It can be used to clean up strings that should only contain numbers.
```
pattern = r'[^0-9]'
# Finding the specified pattern and replacing non-digit characters with a blank string
new_text = ''.join(re.sub(pattern, ' ', text))
```
#### 3. Pattern: [^A-Za-z]
* Use Case: Sanitizing input fields to allow only letters.
* Description: **This pattern matches any character that is not a letter** (either uppercase or lowercase). It can be used to sanitize user input in forms to ensure it only contains alphabetic characters.
```
pattern = r'[^A-Za-z]'
# Finding the specified pattern and replacing non-letter characters with a blank string
new_text = ''.join(re.sub(pattern, ' ', text))
```
#### 4. Pattern: []+
* The **+ character** is used to indicate that the **preceding element must occur one or more times**.
* **Any pattern mentioned before the +** character will be matched as long as it appears at least once.
* **Use Case**: Validating hexadecimal color codes.
  * Description: The pattern [a-fA-F0-9]+ matches one or more characters in the range 'a' to 'f' (lowercase) or 'A' to 'F' (uppercase) or 0-9. It can be used to extract or validate parts of hexadecimal color codes.
```
pattern = r'[a-fA-F]+'
# Finding the specified pattern and replacing non-hexadecimal characters with a blank string
new_text = ''.join(re.sub(pattern, ' ', text))
```
* To make our process faster and easier, we want to clean all reviews in the DataFrame at once instead of handling them individually.
* By using the **apply function** in Pandas, we can quickly apply our cleaning function, remove_special_characters, to every review in the DataFrame in one go.
* We will define the remove_special_characters function to remove special characters from the text. Then, we will apply this function to the review column, ensuring all reviews are clean and ready for analysis.
```
# defining a function to remove special characters
def remove_special_characters(text):
    # Defining the regex pattern to match non-alphanumeric characters
    pattern = '[^A-Za-z0-9]+'

    # Finding the specified pattern and replacing non-alphanumeric characters with a blank string
    new_text = ''.join(re.sub(pattern, ' ', text))
    return new_text

# Applying the function to remove special characters
data['cleaned_text'] = data['review'].apply(remove_special_characters)
```
### Lowercasing
#### Why is Lowercasing Important in Text Preprocessing?
* It ensures that all words are in the same format, which helps maintain consistency across the dataset.
* This means "Dog" and "dog" are treated as the same word.
* Converting text to lowercase simplifies the data, making it easier to process and analyze.
#### How to Implement Lowercasing?
* The **lower() method** is a built-in string method in Python that converts all uppercase characters in a string to lowercase. This is useful for standardizing text data.
```
input_string = "Hello, World!"
lowercased_string = input_string.lower()
print(lowercased_string)
```
* To streamline our process, we want to convert all reviews in the DataFrame to lowercase at once instead of handling each one separately.
* By using the **str.lower() method** in Pandas, we can efficiently apply the **lowercase transformation to every review in the DataFrame in a single operation**.
* We will apply the **str.lower()** method to the review column, ensuring that all reviews are standardized and ready for analysis.
```
# changing the case of the text data to lower case
data['cleaned_text'] = data['cleaned_text'].str.lower()
```
### Removing extra whitespace
* Why is Removing Extra Spaces Important in Text Preprocessing?
* Removing extra spaces ensures uniformity in the text, making it easier to analyze and process.
* Extra spaces can unnecessarily increase the size of the text data. By eliminating them, the overall storage requirements are reduced, leading to more efficient data handling and processing.
* How to Implement Lowercasing?
  * The **strip() method** is a built-in string method in Python that removes leading and trailing whitespace from a string.
```
string = " johan@gmail.com "
stripped_string = string.strip()
print(stripped_string)
```
* By utilizing the **str.strip() method** in Pandas, we can easily **eliminate leading and trailing whitespace from every review in the DataFrame in a single operation**.
```
# We will apply the str.strip() method to the review column, ensuring that all reviews are cleaned and formatted consistently for analysis.
data['cleaned_text'] = data['cleaned_text'].str.strip()
```
### Removing Stopwords
* **Stop words are common words (like "and," "the," and "is")** that are often excluded from text analysis because they add little meaning to the content.
* Excluding frequently occurring words helps emphasize the more significant terms in the text, improving analysis quality.
* Removing pronouns and articles, commonly categorized as stop words, minimizes irrelevant information, allowing algorithms to better identify patterns.
#### How to implement stop word removal?
* **NLTK (Natural Language Toolkit)** is a Python library designed for working with human language data (text) and provides tools for various natural language processing tasks.
* NLTK is widely used in academic and research settings, supported by an active community that contributes to its development and documentation, making it a valuable resource for learning and experimentation in NLP.
* It is imported using the statement `import nltk`
* **NLTK has a module called stopwords** that provides a list of common stop words based on the English language.
* **This list includes frequently used words that typically do not add significant meaning to text analysis.**
* We can download this stop words list using the statement **nltk.download('stopwords')**
```
import nltk
nltk.download('stopwords')
```
* Once we have downloaded the list, **we can use the corpus module from nltk to load the stopwords**
`from nltk.corpus import stopwords`
* To access the stopwords in the english language, we can use the **words method** from the stopwords module and pass 'english' as the argument.
* Using the **NLTK stop words list**, we can filter reviews by keeping only the words not in this list, allowing us to focus on meaningful content and enhance the quality of our analysis.
#### 1. Splitting the Text
* The first step involves splitting the input text into individual words using the **split() method**. This method separates the text at each space and creates a list of words.
  * **words = text.split()**
#### 2. Removing Stop Words
* Next, we remove the English stop words from the list of words. We use a list comprehension to iterate through each word in the words list and check if it is not present in the stop words list obtained from stopwords.words('english').
  * [word for word in **words** if word not in stopwords.words('english')]
#### 3. Creating the New Text
* Finally, the remaining words (those not in the stop words list) are joined back together into a single string using the join() method. This creates a new text string that contains only the meaningful words.
  * **new_text = ' '.join([word for word in words if word not in stopwords.words('english')])**
  * **Performance Tip** -- If you are processing a very large dataset, convert the stopwords list into a set first. Looking up a word in a set is much faster than looking it up in a list:
#### 4. Result
* The resulting new_text variable now holds the filtered text, free of common English stop words, which allows for a more relevant analysis of the content. 
* To streamline our process, **we want to remove stop words from all reviews in the DataFrame at once** instead of handling each one separately.
* **By defining a function called remove_stopwords** using the NLTK library, we can efficiently apply the stop word removal to every review in the DataFrame in a single operation.
* This function splits the text into separate words, removes English language stop words, and then joins the remaining words back into a single string, ensuring that all reviews are cleaned and ready for analysis.
* To implement this, we will apply the remove_stopwords function to the review column in our DataFrame using the Pandas **apply() method**, allowing us to filter out common stop words from each review and enhance the quality of our text analysis.
```
# defining a function to remove stop words using the NLTK library
def remove_stopwords(text):
    # Split text into separate words
    words = text.split()
    # Removing English language stopwords
    new_text = ' '.join([word for word in words if word not in stopwords.words('english')])
    return new_text

# Applying the function to remove stop words using the NLTK library
data['cleaned_text_without_stopwords'] = data['cleaned_text'].apply(remove_stopwords)
```
### Stemming
* Why is Stemming Important?
  * **Stemming** transforms different forms of a word (e.g., "running," "ran," "runs") into a single root (e.g., "run"), **making data more uniform**.
  * Fewer unique words mean simpler data, which helps in processing and analyzing text more efficiently.
  * It helps in identifying key topics and sentiments by focusing on the core meaning of words rather than their variations.
* How to implement?
  * The **Porter Stemmer** is one of the widely-used algorithms for stemming, and it shorten words to their root form by removing suffixes.
  * This is particularly useful in NLP tasks where you want to analyze the underlying meaning of text without being misled by different grammatical forms of the same word.
  * **NLTK module supports Porter Stemmer algorithm**.
* Before proceeding, we need to download the wordnet database.
   * WordNet is a large lexical database of English words that groups words into sets of synonyms called synsets, providing definitions and semantic relationships between them.
   * By using **nltk.download('wordnet')**, we can download the WordNet dataset directly into their NLTK environment, enabling easy access to its rich linguistic resources.
```
nltk.download('wordnet')
# Next, we can import the PorterStemmer module from stem.porter module available in the nltk library
from nltk.stem.porter import PorterStemmer

# Creating an instance of the Porter Stemmer class, which is used to stem words by reducing them to their root form.
ps = PorterStemmer()

# Specifying the input word that needs to be stemmed.
word = 'Running'

# Applying the stemming process to the input word (in this case, 'Running'), and assigns the resulting stemmed form to the variable stemmed_word.
stemmed_word = ps.stem(word)

# Now, let's try to use this pattern to manipulate one of the reviews in the data.
review = data['review'][21]
words = review.split(' ')
stemmed_text = ' '.join([ps.stem(word) for word in words])
```
* By defining a function called apply_porter_stemmer using the NLTK library, we can efficiently apply the Porter stemming algorithm to every word in the text in a single operation.
    * This function splits the input text into separate words, applies the Porter Stemmer to each word, and then joins the stemmed words back into a single string, ensuring that the text is uniformly stemmed and ready for further analysis.
```
# Loading the Porter Stemmer
ps = PorterStemmer()

# defining a function to perform stemming
def apply_porter_stemmer(text):
    # Split text into separate words
    words = text.split()

    # Applying the Porter Stemmer on every word of a message and joining the stemmed words back into a single string
    new_text = ' '.join([ps.stem(word) for word in words])

    return new_text

# Applying the function to perform stemming
data['final_cleaned_text'] = data['cleaned_text_without_stopwords'].apply(apply_porter_stemmer)
```
### Text Vectorization
* Why is Text Vectorization Important?
  * It **transforms words and sentences into numerical formats** that mathematical algorithms can understand, making it essential for processing text data.
  * By representing text as vectors, it helps capture important patterns and relationships in the data, leading to better insights and analysis in text-related tasks.
* **Definition**:
A document-term matrix is a mathematical representation of a collection of documents, where each document is represented as a row, and each unique word (or term) across all documents is represented as a column. The cells in the matrix contain values that indicate the frequency or presence of the corresponding word in the corresponding document.

* **Usage in Text Preprocessing:**
The document-term matrix is essential in text preprocessing as it converts unstructured text data into a structured numerical format. This transformation allows for efficient analysis and processing of textual information. By representing documents as matrices, it facilitates the extraction of important features and patterns, making it easier to prepare text data for further analysis and understanding.

* Example: Consider three short documents:
    * Document 1: "I love programming"
    * Document 2: "Programming is fun"
    * Document 3: "I love fun programming"

* Steps to Create the Document-Term Matrix:
 1. Convert all text to lowercase:
    * Document 1: "i love programming"
    * Document 2: "programming is fun"
    * Document 3: "i love fun programming"

2. Identify all unique words across the documents and sort it:
  * fun , is , love , programming

3. Count the occurrences of each word in each document:
    Document 1:
        "fun": 0
        "is": 0
        "love": 1
        "programming": 1
    Document 2:
        "fun": 1
        "is": 1
        "love": 0
        "programming": 1
    Document 3:
        "fun": 1
        "is": 0
        "love": 1
        "programming": 1
4. Form a matrix using the counts, where each row represents a document and each column represents a unique word:

Document 	 fun 	is 	love 	programming
Document 1 	0 	  0   	1   	1
Document 2 	1 	  1   	0   	1
Document 3 	1   	0 	  1   	1

* **To implement this BoW representation, sklearn offers a class** to work with called **Countvectorizer**
* It is available in the **feature_extraction.text module**
*  It is imported using the statement **from sklearn.feature_extraction.text import CountVectorizer**

* **`CountVectorizer`**:
- This is a tool from `sklearn.feature_extraction.text` used to convert text documents into a matrix of token counts.
- It creates a Bag of Words (BoW) representation of the text, where:
 - Each row represents a document.
 - Each column corresponds to a unique word (token) in the entire corpus.
 - The values in the matrix are the counts of each word's occurrence in the respective document

* **`fit_transform()`**:
- The **`fit_transform()`** method performs both **`fit()` and `transform()` in a single operation**.
- The `fit()` method learns the vocabulary from the provided documents (i.e., identifies the unique words).
- The `transform()` method converts the documents into a sparse matrix, where:
 - The matrix rows correspond to documents.
 - The columns represent the words from the learned vocabulary.
 - The values in the matrix are the word frequencies.
```
from sklearn.feature_extraction.text import CountVectorizer

Document_1 = "I love programming"
Document_2 = "programming is fun"
Document_3 = "i love fun programming"
list_of_docs = [Document_1,Document_2,Document_3]

bow_vec = CountVectorizer()
doc_matrix = bow_vec.fit_transform(list_of_docs)

# Compressed Sparse Row format
 # It’s a way to store large matrices efficiently when most of the elements are zero.
 # Instead of storing every element, including the zeros, CSR compresses the data by only storing non-zero values and their positions.
# Converting CSR to a numpy array
doc_matrix.toarray()

# returns the list of unique words (tokens) extracted from the documents.
bow_vec.get_feature_names_out()

# returns the list of unique words (tokens) extracted from the documents.
bow_vec.get_feature_names_out()
```
* The **max_features** parameter in CountVectorizer limits the number of words (or tokens) used to create the vocabulary.
* This helps when dealing with large datasets by keeping only the most important or frequent words.
```
# Initializing CountVectorizer with top 1000 words
bow_vec = CountVectorizer(max_features = 1000)

# Applying TfidfVectorizer on data
data_features_BOW = bow_vec.fit_transform(data['final_cleaned_text'])

# Convert the data features to array
data_features_BOW = data_features_BOW.toarray()

# Shape of the feature vector
data_features_BOW.shape

# Getting the 1000 words considered by the BoW model
words = bow_vec.get_feature_names_out()

# Creating a DataFrame from the data features
df_BOW = pd.DataFrame(data_features_BOW, columns=bow_vec.get_feature_names_out())
df_BOW.head()
```
* Note: **N-gram models** help understand language better by looking at the order or sequence of words. This means they pay attention to how words appear together in a sentence, which helps capture the meaning and flow of language better than the **bag-of-words (BOW) model, which treats each word separately and ignores their order**. The other points are incorrect because n-gram models don’t affect the size of the vocabulary. The vocabulary remains the same even though the model creates n-grams from the existing corpus. Removing stopwords (like "the" or "is") is optional for both n-gram and BOW models because it doesn’t affect their core functionalities.
* The **"Bag of Words" model represents words** in a document **based on their frequency**, providing a quantitative measure of each word's importance.
* To identify the emotional tone expressed in a piece of text, such as positive, negative, or neutral. **Sentiment analysis aims to understand and categorize the sentiment or emotion conveyed in textual content**, helping to gauge the author's attitude or opinion towards a particular subject.
