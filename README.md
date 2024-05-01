# About the company
Bellabeat is a company specialized in high-tech health-focused products for women. Since its foundation in 2013, Bellabeat had a rapid success in the industry that will only grow over time. Urška Sršen, the co-founder of Bellabeat, used her background as an artist to develop beautifully designed technology that informs and inspires women around
the world. Collecting data on activity, sleep, stress, and reproductive health has allowed Bellabeat to empower women with knowledge about their own health and habits.

# About the project
This project is lead by Volkan Yiğit Oker for Bellabeat.
The project is aiming to answer the following questions:

 * What are some trends in smart device usage?
 * How could these trends apply to Bellabeat customers?
 * How could these trends help influence Bellabeat marketing strategy?
 
**With the usage of public dataset: FitBit Fitness Tracker Data**

Dataset license | CC0: Public Domain

Dataset Usability | %100 via [Kaggle](https://www.kaggle.com/datasets/arashnic/fitbit)

# Coding and Thought Process

## My method for sampling

I did not want to miss out on any potential chance to find something interesting so I've decided to do my analysis based on 3 samplings:

 * daily sampling: I'll use the values in daily data set 
 * sleep sampling: I'll use the values in sleep data set 
 * full sampling: I'll use the daily values of members who also provided sleep values and compare the results
 
## Lost Calories vs Total Steps
I'd like to start with the most obvious assumption we can make and test if it is correct!
**Does more steps taken means more calories have been lost?**
```{r}
ggplot(data = daily) + geom_point(mapping = aes(x= TotalSteps, y = Calories)) + geom_smooth(mapping = aes(x= TotalSteps, y = Calories)) + labs(title = "Calories vs Total Steps")
```
![](https://www.kaggleusercontent.com/kf/160312748/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Wh3dWtFjBeazDjrPCcjQrA.EEeCvoYRIF23ZNLR6HjshSQLHVpreZfBqaRS9TP6jFWVxBpTQgDoHiEgb1TA3fYcbRQ3aSh3f5uIdHr5-iS3xSU3ru7fphIlODatb3OYIH8rHWyA4lhQOuLz5AA8f5jOKh-_34iV74glDu9uXqQtJb3c_HND6qMeNzS2ydy0IUtBT3HaBAFjgNoEERwZxapSzHOfV7zMjRx6EOKVhZQnloBnsgvFkTyCn65Jy7vDsaGLGxPPIn3jMi1Vf4WbMoZWxbRMQO9aB4-6Nf48RqjMz087iNL6R5CP-IAFMyPnaBgQI38lZhexZxzky29zg3waSVSltgcDo70R4CiQekZjbOhRwyWd5mNb3VC6vPJOTXKdR6PZre65KK8NKfizJ0KFjOomPNLSGXZLHlpZOnnUt0sqn0mnPqmMW9mRF0fs7y-Cu1GuDHt2R8hnwS2HbzV2i9_dTRRwTSsicyl3KEiFc-RsEGDjdg3dnIEYbh2oKMAwMcVghkTEkp_KF30CLlxn_Y7vn_PRDMFWGQcoiiO97Ty91-jmi9TfssMg2vn8YEANPGCIP25m7aHRhvFIzoByEiEoXIzL0Uk8OFlPVD-XJOKBpk5JbHPeQjrJzH7DaLi9YZdLanDDePOF9dgCBbLrldxOOozIXzk-vMhYLem6MHyBBW1x0JrN5BWou9f93Fw.nYyBc5j5siFDuqGIB2DV0g/__results___files/__results___13_1.png)

Well the answer shortly is: **yes**, if we dive deeper to the analysis we can safely say that the more steps we take the more calories we lose. **However** as it can be seen in the graph same amount of steps doesn't always mean same amount of calories! While we can strongly agree that steps strongly affects the calories lost, it is not the only reason.

**What is it then?**
Great question.

## Lost Calories vs Active Movement

Red color: Very active minutes

Green color: lightly active minutes

```{r}
ggplot(data = daily) + geom_point(mapping = aes(x= VeryActiveMinutes, y = Calories, alpha=Calories), color="red") + geom_point(mapping = aes(x=LightlyActiveMinutes, y = Calories, alpha=Calories), color = "darkgreen") + labs(title = "Calories vs Active Minutes", x = "Active Minutes")
```
![](https://www.kaggleusercontent.com/kf/160312748/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Wh3dWtFjBeazDjrPCcjQrA.EEeCvoYRIF23ZNLR6HjshSQLHVpreZfBqaRS9TP6jFWVxBpTQgDoHiEgb1TA3fYcbRQ3aSh3f5uIdHr5-iS3xSU3ru7fphIlODatb3OYIH8rHWyA4lhQOuLz5AA8f5jOKh-_34iV74glDu9uXqQtJb3c_HND6qMeNzS2ydy0IUtBT3HaBAFjgNoEERwZxapSzHOfV7zMjRx6EOKVhZQnloBnsgvFkTyCn65Jy7vDsaGLGxPPIn3jMi1Vf4WbMoZWxbRMQO9aB4-6Nf48RqjMz087iNL6R5CP-IAFMyPnaBgQI38lZhexZxzky29zg3waSVSltgcDo70R4CiQekZjbOhRwyWd5mNb3VC6vPJOTXKdR6PZre65KK8NKfizJ0KFjOomPNLSGXZLHlpZOnnUt0sqn0mnPqmMW9mRF0fs7y-Cu1GuDHt2R8hnwS2HbzV2i9_dTRRwTSsicyl3KEiFc-RsEGDjdg3dnIEYbh2oKMAwMcVghkTEkp_KF30CLlxn_Y7vn_PRDMFWGQcoiiO97Ty91-jmi9TfssMg2vn8YEANPGCIP25m7aHRhvFIzoByEiEoXIzL0Uk8OFlPVD-XJOKBpk5JbHPeQjrJzH7DaLi9YZdLanDDePOF9dgCBbLrldxOOozIXzk-vMhYLem6MHyBBW1x0JrN5BWou9f93Fw.nYyBc5j5siFDuqGIB2DV0g/__results___files/__results___15_0.png)

In the above graph we can clearly see that even the same type of movement provides different results. **However** Very active movement generally results in more calories lost in comparison to lightly active minutes!

## Time Spent In Bed vs Time Asleep
You'd assume they mean the same thing, right?

```{r}
ggplot(data = sleep) + geom_point(mapping = aes(x=TotalTimeInBed, y = TotalMinutesAsleep)) + labs(title = "Total time in bed vs in asleep")
```
![](https://www.kaggleusercontent.com/kf/160312748/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Wh3dWtFjBeazDjrPCcjQrA.EEeCvoYRIF23ZNLR6HjshSQLHVpreZfBqaRS9TP6jFWVxBpTQgDoHiEgb1TA3fYcbRQ3aSh3f5uIdHr5-iS3xSU3ru7fphIlODatb3OYIH8rHWyA4lhQOuLz5AA8f5jOKh-_34iV74glDu9uXqQtJb3c_HND6qMeNzS2ydy0IUtBT3HaBAFjgNoEERwZxapSzHOfV7zMjRx6EOKVhZQnloBnsgvFkTyCn65Jy7vDsaGLGxPPIn3jMi1Vf4WbMoZWxbRMQO9aB4-6Nf48RqjMz087iNL6R5CP-IAFMyPnaBgQI38lZhexZxzky29zg3waSVSltgcDo70R4CiQekZjbOhRwyWd5mNb3VC6vPJOTXKdR6PZre65KK8NKfizJ0KFjOomPNLSGXZLHlpZOnnUt0sqn0mnPqmMW9mRF0fs7y-Cu1GuDHt2R8hnwS2HbzV2i9_dTRRwTSsicyl3KEiFc-RsEGDjdg3dnIEYbh2oKMAwMcVghkTEkp_KF30CLlxn_Y7vn_PRDMFWGQcoiiO97Ty91-jmi9TfssMg2vn8YEANPGCIP25m7aHRhvFIzoByEiEoXIzL0Uk8OFlPVD-XJOKBpk5JbHPeQjrJzH7DaLi9YZdLanDDePOF9dgCBbLrldxOOozIXzk-vMhYLem6MHyBBW1x0JrN5BWou9f93Fw.nYyBc5j5siFDuqGIB2DV0g/__results___files/__results___17_0.png)

While you are not entirely off the graph shows us that people may stay in bed longer than what they actually sleep for! What shocked me the most is that some people spending 200 minutes in addition to how long they sleep for!

## More stuff regarding to calories
After filtering the data in R I decided to visit my platform of choice: Excel
I could have done the same process in Tableau but I did not want to complete my first study without using a bit of Excel.
![](https://i.hizliresim.com/pdk5ea8.png)

What shocked me the most is having a more active average movement span does not mean that you are going to lose more calories! I can go in depth to this but let's save that to another project!

# Conclusion
With the analysis we have completed, here are my insights:

 * Your sleep matters:
   People can spend much more time in bed than what they actually have to spend! While the reason can be as simple as    scrolling at social media, it is not our main concern. We can let the users set a sleep alarm that will notify 
   them gently that they have surpassed the amount they wish to spend awake in bed, reminding them to sleep.
 * Lose weight personally:
   In our insights we provided that calorie loss is not dependent on a single factor, we can provide a new service
   That will assign personal coaches to our users who will provide the users with their optimal amount of movement
   type and time. We can even use an AI which will rise the fixed cost but will not have additional costs in the    
   future lowering our total cost for the service!

I'd strongly recommend you to consider the above projects I mentioned. Will be waiting for a response about the project as well as if you need me on another project.
