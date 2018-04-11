This project is prepared for the “Classifying Heart Sounds Challenge” (http://www.peterjbentley.com/heartchallenge/)

The goal of this challenge is to produce methods for heart beat classification. The main components of normal heart sound signals are S1 corresponding to systolic period, and followed by S2 corresponding to diastolic period. The aim of this challenge is to find a method that could locate S1 and S2, and futher differentiate these two classes.

1 Procedures

(1) Using 3-layer-wavelet to decrease noise (it is hard to extract information for more than 3-layer).

(2) Calculate Shannon energy of each example (but calculating information entropy does not work).

(3) Calculate derivative, find local maximum.

(4) Close peaks are grouped into one sub-group, and pick the highest peak.

(5) Calculate distances between peaks, delete outliers. Try different threshold values to make sure that all labeled peaks are picked, while false peaks are few.

(6) Feature engineering. According to 3 online reports, the positions of predictable peaks have some rules, the interval of S1 to S2 is shorter than S2 to next S1, and Shannon enrgy of S1 is higher than S2. Therefore most features are based on position and energy.

(7) Add features and generate labels.

(8) Building models. There are two ways:

a Predict classes of peaks directly (S1, S2, false peak).
Using SVM, decision tree, logistic regression and random forest, precision is around 75-80%, error of test set is around 170000.

b Predict pattern of peaks.
If one peak is same as previous one, label 0; if different to previous one, label 1, then change back to peak classes.
Here the second method decreases error to around 40000, much lower than online reports (around 70000) and first method.

2 Result discussion

Computing the error between labeled peaks and picked peaks, and find that false peaks are only around 3%, which means that the picking strategy is effective.

Train samples are splited to 70% train set and 30% validation set. The precision of SVM, decision tree, logistic regression and random forest are all above 95%, which means that the pattern of the data is quite strong, and it should be very effective to predict pattern in test set.

Here all the test samples are set to start with S1, while it is not always true, so the error of test set is still around 40000. It could be improved to use first method to predict classes of first peaks. And it should be noticed that all machine learning models used in this project are based on the simplest one. It could perform better with other parameters. Therefore the error of test set could be further decreased.
