# Review-Text-Data-Mining

Reviews have been a useful tool in education field. 
 Instructors could use student peer reviews to improve students' performance. 
 Researches show connection between different features in peer reviews to the achievement of students. 
 Here we try to discover the features in product reviews especially text book reviews, and find the connection between product review and self reported performance change.

## Introduction

### Features in peer reviews
Peer assessment is a widely used practice that holds considerable benefit for student learning. 
 It allows students to receive feedback from multiple sources and learn by seeing how their peers approach the same work.  
 It also trains students to in how to provide useful suggestions for performance improvement.
 Previous work by Nelson et. al.[1] has catalogued the features of as various types, shown in Fig. 1.
 
![Features of review texts](https://github.com/canhsiao/Review-Text-Data-Mining/blob/master/reviewfeatures.png)
 
 - Praise points out good aspects of the work and can be used to both increase motivation and help students to identify their strengths. 
 This makes students more receptive to criticism, since pointing both the positive and negative aspects of the work gives the impression of fairness and objectivity. 
 
 - Problem is used to identify a shortcoming of the work. 
 If the problem is not explicitly stated, the writer may not know what the problem actually is and so, including a problem in the feedback is expected to help students to identify the weaknesses and address them. 
 
 - Solution is defined as a comment that suggests a method to deal with a problem. 
 Including solutions as a part of formative feedback helps students to act on the feedback. 
 
 - Mitigation softens the review by making the criticisms sound less harsh. 
 Mitigated suggestions improve the author’s perception of the reviewer’s likability and personal integrity, and thus increases the chance that the author will act on the feedback. 
 
 - Localization refers to pinpointing the source or location of the problem and/or solution. 
 This draws the author’s attention to the problem and makes it easier to act on the feedback. 
 Neutrality means that the feedback is matter-of-fact, without language that would indicate personal preference such as approval or antagonism. 
 
 - Summary indicates that the review summarizes some part of the work. 
 Summarizing a work can serve as a quality control on the review, because it can show whether the reviewer understands the work.

### Features in book reviews
Book review, as a product review, naturally could extract similar features as peer reviews. We plan to explore the feature distribution, and find the relationship between book reviews to self reported performance change. 
In this way, we want to help identify what features in a book, or methods of using the book, would help achieve a better performance. And contribute to learning strategies. 

### Book reviews database
In this project, we use the reviews obtained from the [review database](http://jmcauley.ucsd.edu/data/amazon/) provided by Dr. Julian McAuley at UCSD. The books review section is used.

It has JSON format with the following example:

    "reviewerID": "A2SUAM1J3GNN3B",
    "asin": "0000013714",
    "reviewerName": "J. McDonald",
    "helpful": [2, 3],
    "reviewText": "I bought this for my husband who plays the piano.  He is having a wonderful time playing these old hymns.  The music  is at times hard to read because we think the book was published for singing from more than playing from.  Great purchase though!",
    "overall": 5.0,
    "summary": "Heavenly Highway Hymns",
    "unixReviewTime": 1252800000,
    "reviewTime": "09 13, 2009"

### Feature detection models
We have developed neural network models that detect the features in the review texts[2], and applied the models on the book review databse. We used CNN + doc2vec, which has a good performance accross different features. It can be seen from Fig. 2.

![Performance of different models](https://github.com/canhsiao/Review-Text-Data-Mining/blob/master/image.png)


## Preliminary results of feature detection
We use the model trained on prelabeled review text data, apply it to the book review texts obtained from the data base. 
And obtained some preliminary results from the distribution. 

### Data cleaning
We performed preliminary language data cleaning on duplicated reviews and the review texts themselfs. And we obtained some interesting observations.

- Rate of features detected in all books and text books:

| Type  | All Books |  Text Books   |
| ------------- | ------------- | ------------- |
| Praise  | 0.72  | 0.90 |
| Problem  | 0.17  |  0.21  |
| Solution  | 0.07  |  0.10  |
| Mitigation  | 0.07 | 0.40  |
| Localization  | 0.02 | 0.41  |
| Summary  | 0.12  | 0.07  |

From the table we can see users tend to have more praise, point out more problems, and offer more solutions for text books. 
This could be expectable, since these features indicate more understanding from user. And readers are expected to spend more effort on understanding text books.

While we also notice some not very obvious characters. 
Reader reviews have much higher rates for mitigation and localization for text books. 
Higher mitigation rate in text books indicates that means when readers review text books, they tend to tone down the critics.
But when reviewing other books, most reviews tend to give critics directly without mitigation.
Readers give fewer summary reviews to text books. This may imply readers assume other readers to 


## Future work

### Data mining of reader performance change/ knowledge gain
We are trying to connect the features of books between the effects of books, and the latter is characterized by readers' performance change or knowledge gain after reading the book.
Preliminary data mining of simple rule-based nlp methods tend to give very small positive rate, so these results are not presented. 
A few examples of current rules for positive performance change resulted from the books are by detecting these phrases for example.
- got better grade
- enhanced performance
etc

Currently, more tuning on the semantic rules are being conducted to try to obtain better model. 
A potentially effective method is to train another neural network model for this purpose. 

More information between the feature of reviews and how the effects of books could be obtained upon further investigation.
After we have a better understanding of the relationship between review features and text book effects, we can have better recommendation system, by rating textbooks based on small amount of reviews.

### More directions to explore
The metadata of the books contain much more information, such as ratings, fields of book, other related books. 
More applications beyond book rating/recomending system could be obtained from these information.



[1]: Melissa M. Nelson and Christian D. Schunn. 2009. The nature of feedback: how different types of peer feedback affect writing performance. Instr. Sci. 37, 4 (July 2009), 375–401.

[2]: Zhongcan Xiao, Chandrasekar Rajasekar, Vishal Ramaswamy Chittoor Venkatasubramanian, Abhilash Arivanan, Ferry Pramudianto, Ed Gehringer. Application of Neural Network Models to Labeling Educational Peer Reviews. Educational Data Mining in Computer Science workshop, Buffalo, NY, July 2018

