# back-end
Techincal Blog: https://catnip-kiwi-923.notion.site/AI-JANSORI-2ee6f08073534679a9a7073e9cbcba29

used language: Python

Framework: Django

Server distribute: Using 'ngrok'
##
###NUGU Server

### Basic features

There is a health function that conveys the current state of nugu and a test function to check the connection to the backend.

### \views\base_veiws.py

### **answer.weather : 오늘 밖에 어때?**

It is a function that transmits specific weather information to a user. Data is stored in a dictionary form in the global variable 'weather_msg' by executing a function that receives current weather data and fine dust index. The variables that must basically contain content to send a response to someone are 'wmessage1' and 'weather_yn', and messages and variable values suitable for each weather anomaly are stored while circling the for sentence.

### .\views\weather_views.py

def odd_weather(request) -> Deliver answers based on today's weather information 

def give_temp(request) -> Inform the highest and lowest temperature today

def give_rain_probability(request) -> Inform the today's rainfall probability

def give_dust(request) -> Inform the concentration of fine dust and the fine dust index

### **answer.weather : 오늘 {{DESTINATION}}가려구**

It is a function that transmits a real-time congestion degree to a user about a destination. Exception processing is performed in functions that receive requests from NUGU and deliver messages. If the user wants to go to 50 places and the surrounding stations are not included, the message "It's a place that can't be retrieved from real-time data" is delivered.

### .\views\congest_views.py

def answer_congest(reqeust) -> Communicate congestion response according to destination (Generate main message)

def get_congest(request) -> Get real-time congestion of destinations with real-time public data in Seoul

def special_date(request) -> If you ask about the degree of congestion on a special day, it provides a warning about places that may be crowded on that day regardless of destination.

### **answer.athome : 나 심심해**

It generates a different message depending on whether the user enters exercise, cleaning, or eating. In the case of meals, the number of meals is also delivered, and the corresponding message is delivered. In the case of exercise, it was forced to display recommended videos on TV after three days. In the case of cleaning, a different message is formed according to the cleaning period set by the initial user.

### .\views\athome_views.py

def answer_athome(request) ->  Forward a message that matches the value entered by the user (create a main message)

def what_user_did() -> Check the exercise, meal, clean

def msg_for_ex() -> Make a msg for exercise

def msg_for_clean() -> Make a msg for cleaning

##
### Application Server
![Untitled](https://user-images.githubusercontent.com/100753236/208034196-8774830c-fdde-4c69-a12d-19f40e8e1538.png)

### Sign up and login
Allows users to fill out a membership form and log in through it.

### views.py
@api_view(['GET', 'POST'])

def userAPI(request)

-> If you send a get request, all user information is given. This is for administrators and cannot be used by the general user. When you send a post request, the information entered by the user is stored in the database.

### models.py
class User(models.Model):name, user.id, pw, location, objects()

-> It is a user object that receives name, ID, password, and location information.

### serializers.py
class UserSerializer(serializers.ModelSerializer):
  ...
  fields = ['name', 'user_id', 'pw', 'location']

-> It plays a role in changing the data type received by post to a data type that can be understood by Django.

### Set the goal
Allows users to set a goal.

### views.py
@api_view(['GET', 'POST'])

def goalsAPI(request)

-> 

### models.py
class Goal(models.Model):goal_id, meal, exercise, clean, objects()

-> It is a user object that receives aim number of meals a day, cleaning cycle, exercise cycle

### serializers.py
class GoalSerializer(serializers.ModelSerializer):
  ...
  fields = ['goal_id', 'meal', 'exercise', 'clean']
