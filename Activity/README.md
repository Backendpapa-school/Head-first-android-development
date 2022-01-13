# Activity Lifecycle
In understanding how Activity works, we will be developing a Stopwatch application.The Stopwatch application possesses four(4) views
1. View that display the elapsed time
2. The pause button to pause the watch
3. The start button to start the watch
4. The reset button to set the watch back to 0

### Create new project
Create a new project in Android studio and naming the application **Stopwatch**, set the minumum SDK to API 21. we are developing as usual with kotlin and created withan empty activity.

### String resource for the text label
we added the string labels for the three button into the strings.xml

```
<resources>
    <string name="app_name">Stopwatch</string>
    <string name="start">Start</string>
    <string name="pause">Pause</string>
    <string name="reset">Reset</string>
</resources>
```