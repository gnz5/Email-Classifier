# Email-Classifier
A hierarchical Naive Bayes classifier for emails.

<b> Extracting and Processing the Raw Emails </b>

The email data was first extracted using the Unix tar command “tar xvzf data.tgz.” Next, a function named extract_body was made to return just the body of the email. This was done by skipping every line in the email prior to the line beginning with the string “Line:” since it appeared this string immediately preceded the body of every email. 

Feature Selection

For simplicity, a bag-of-words approach was used to select the features. Specifically, the 300 most frequently occurring words in each top-level email category were selected as features. These 300 words were identified by counting the occurrence of each word in a document. Then this number was divided by the total number of words to normalize the data and prevent very long emails from distorting the outcome. Next, the average frequency of each word among all documents was found and those with the highest average frequency were selected.

Feature Extraction

Once the feature words were chosen, they could be counted within the emails of interest. A single training example corresponding to a single email was a dictionary where each key was a feature word and its value is the number of times this word occurred in the document. Initially, the frequency of the word was used as the value, however the count seemed to achieve better results.

Selecting a Model

The model used was a hierarchy of Naïve Bayes classifiers. First the “root” classifier would predict the top-level category of the document. For example, it might predict alt, rec, talk, etc. Next, if for example it predicted rec, the email would then be passed along to the rec classifier which would either output rec.autos, rec.motorcycles, or rec.sports. It would continue to be passed down the “classifier tree” until it reached a leaf node.

Results

The results, while better than random chance, left significant room for improvement. However, this was to be expected given the simple method used for feature selection and lack of time spent tuning hyperparameters.  The accuracy of the root classifier was 53.57% and the f1 score of the overall model was 0.297. The macro-average f1 was computed using the metrics module from sklearn.

Ideas for Improvements

The feature words were not manually inspected to remove junk words and words that are likely outliers and would reduce the classifiers ability to generalize to unseen emails. Also, the model may have benefitted from increasing the number of feature words, however this would have dramatically increased computation time. In addition, different types of classifiers such as Decision Trees or Neural Networks may have been able to achieve better results. Finally, the model could have been improved by tuning the hyperparameters such as the kernel and gamma.

References

https://www.nltk.org/book/ch01.html
https://www.nltk.org/book/ch06.html
