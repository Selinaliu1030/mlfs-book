# ID2223 Lab1
Chih-Yun Liu (cyliu4@kth.se)
Hanaè Ben Makhlouf (???@kth.se)

## How to Run
make aq-features id=x
make aq-train id=x
make aq-reference id=x

(x=1 for Drottinggatan; x=2 for Ramshogsvagen; x=3 for Larod)

## Implementation
### Add New Feature (GradeC):
We selected lag_1, lag_2, and lag_3 as new features, which means the pm25 data from 1 day, 2 days, and 3 days before, into the model. And these new feature help significantly on the accuracy. First, the importance of lag features is high for the model(See Figure1). Also, as we can see in the comparison plot with and without lag features, the plot with lag features align more to the ground truth in both training and inferencing(See Figure 2 and 3).

![Fg1](./img/feature_2.png)

Without New Features (Training)
![Fg2](./img/p3.png)
With New Features (Training)
![Fg3](./img/p3_2.png)

Without New Features (Inference)
![Fg3](./img/cmp.png)

With New Features (Inference)
![Fg3](./docs/air-quality/assets/img/pm25_hindcast_1day_1.png)

### Multi-Sensors (GradeA)
For the notebooks to run multi-sensors, we do the following modifications.
1. Select Sensors
Our designated area is "Helsingborg and Landskorna", and the 3 sensors we chose are Drottinggatan, Ramshogsvagen, Larod.
<br>


2. .env
We give each sensors an id, and put all the information including url, country, city, street, and csv file path onto .env file with the name always ends with "_id".
<br>

3. Notebook
We modify the notebooks for to take sensor id as input through command line. First, we parse the input from the command line and got the attribute "id". Then, we get the station information through .env, with name ends with "_id". And the rest process are remain the same, but the feature group's name, feature view's name, and model name are also ends with "_id" so that each of the sensors can have independent traiing feature and model, thus provide independent prediction result. 
<br>

4. Make File
We modify the make file for us to run the notebook by command line and take id as input. We add "-- --id 1" at the end of the previous command, which means pass value 1 as argument id to the notebook.
<br>

5. .yml file
In section: execute python workflows from bash script, instead of running only "make aq-inference", we modify the command to "make aq-inference id=1 make aq-inference id=2 make aq-inference id=3", so that it can run 3 sensors each time we start a github action.


