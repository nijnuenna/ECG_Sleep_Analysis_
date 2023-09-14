# ECG_Sleep_Analysis_remake

* This project was created by referring to the paper 'Sleepiness Detection depending on Heart Rate Estimation Methods written by Minhae Kim, Seunghyeok Hong'.
## Set up
___
The following Python 3 libraries are required to execute code. Be sure to install it before running the code.
  * Keras
  * matplotlib
  * numpy
  * imageio
  * configargparse
  * scikit-learn
  * pandas
  * PyTorch
  * scipy
  * pickle
  * random

You can install dependencies using pip:


`pip install keras matplotlib numpy imageio configargparse scikit-learn pandas torch scipy`

## Data Introduction
___
### Data acquisition method :
Seven participants (male aged 25-32) in this study agreed to control their intake of chemicals that affect sleepiness. Before the experiment, participants were asked not to drink caffeine-containing drinks and alcohol for 5 to 24 hours. In addition, to avoid suppression of sleepiness due to hunger, all participants began the experiment 40–70 minutes after eating. To measure physiological signals under everyday conditions, volunteers were recruited without considering post-wake-up time, circadian rhythm changes, or physiological activities, and most participants said they did not perform much physical activity such as labor or exercise the day before the experiment. Before participating in the study, all participants agreed to the research plan (Seoul National University IRB No. C-1509-074-704), and before conducting the sleepiness detection experiment, participants drove for five minutes to familiarize themselves with the simulator and work.

___

<p align="center">
 
  ![캡처](https://github.com/nijnuenna/ECG_Sleep_Analysis_/assets/139520513/5548f22d-5fb0-47d3-8b6f-78e5bcbfc24c)

</p>


Among the six datasets provided, sync_data_bio and data_event were mainly used.


`sync_data_bio` : This is an ecg signal, and it is a frame form that contains various data such as electrocardiogram data, central blood pressure meter, respiration, etc.

`data_event` : It is in the form of a data frame that contains the time when the vehicle was randomly shaken, the reaction time and the area where the vehicle was shaken.

___
### Data visualization
* drowsiness = a state of drowsiness
* alertness = a state of being awakened


`sync_data_bio` : 
* The row shows the electrocardiogram data of drowsiness and alertness for the reaction time when the subject moves from side to side in a four-hour experiment.
  

* Column is the ECG data divided by Hz for 5 minutes.


* In this graph, the x-axis represents the number of samples and the y-axis represents the amplitude of the ECG signal


<p align="center">
  <img width="755" alt="image (2)" src="https://github.com/nijnuenna/ECG_Sleep_Analysis_/assets/139520513/6eff3073-8c7e-459a-b194-f4ce87a71f63">

</p>


<p align="center">
  <img width="755" alt="image (3)" src="https://github.com/nijnuenna/ECG_Sleep_Analysis_/assets/139520513/48669b21-41a1-4076-9759-cc6c6dcc7ed0">

</p>


`data_event` : 
* This is the data frame of data_event


* Response – Forced move = Reaction Time (RT)

* The RT value was judged as important data, and a scatterplot of the deviated area according to the reaction time was drawn.
* You can see that the blue dots in the range with a smaller reaction time are located more on the side with smaller values than the red dots in the range with a larger reaction time.


<p align="center">
  <img width="650" alt="image" src="https://github.com/nijnuenna/ECG_Sleep_Analysis_/assets/139520513/7833d46a-f89a-478c-ae29-2f90970f30fb">

</p>


___
### Data preprocessing


We proceeded with a total of three data preprocessing.

* Normalization : Since the ECG varies from person to person and the range varies, it was conducted to improve the accuracy of the analysis by unifying the range of people through data normalization.

* z-score processing : Through Z-SCORE processing, not only abnormalities but also noise were removed.


* Fourier transform : This transformation enables analysis in the frequency domain, which allows the distinction between noise and the desired signal.


___
### Modeling


We proceeded with modeling using 1D CNN.


* The features of this model consist of 6 conv1d layers and 2 dense layers
 We included leaky relu activation function and batch normalization, maxpooling, and dropout layer.
The rate of dropout is 0.2.


* In the modeling process, Hertz was extracted at equal intervals and used for model learning.


* By keeping the data intervals constant, the model can accommodate a wider range of data through batch normalization.


* It's the best result of 100hz.
On the left is a visualization of the degree of loss, and on the right is a visualization of the verification accuracy.
If you look closely, you can see that the maximum value of the accuracy of the verification data was 88.63%.


<p align="left">
  <img width="650" alt="image (5)" src="https://github.com/nijnuenna/ECG_Sleep_Analysis_/assets/139520513/ed85d578-a6fd-4ccc-882f-23828a7ea460">

</p>


<p align="right">
  <img width="650" alt="image (6)" src="https://github.com/nijnuenna/ECG_Sleep_Analysis_/assets/139520513/050fe8ba-8496-4755-90dd-d6fc6a2271b8">

</p>


___
### Final Conclusions and Accuracy


* This led us to conclude that data extraction over frequency intervals significantly affects the performance of the sleepiness detection model.






