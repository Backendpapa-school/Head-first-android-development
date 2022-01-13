# Activity Lifecycle
In understanding how Activity works, we will be developing a Stopwatch application.The Stopwatch application possesses four(4) views
1. View that display the elapsed time
2. The pause button to pause the watch
3. The start button to start the watch
4. The reset button to set the watch back to 0

### Create new project
Created a new project in Android studio and naming the application **Stopwatch**, set the minumum SDK to API 21. we are developing as usual with kotlin and created withan empty activity.

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

### Layout
The layout will include three buttons and one view to display the timer. This view is called the chronometer.
```

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center_horizontal"
    tools:context=".MainActivity">

    <Chronometer
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="56sp"
        android:id="@+id/stopwatch"
        />
    <Button
        android:layout_height="wrap_content"
        android:layout_width="wrap_content"
        android:id="@id/start"
        android:text="@string/start"

        />

    <Button
        android:layout_height="wrap_content"
        android:layout_width="wrap_content"
        android:id="@+id/pause"
        android:text="@string/pause"

        />
    <Button
        android:layout_height="wrap_content"
        android:layout_width="wrap_content"
        android:id="@+id/reset"
        android:text="@string/reset"

        />

</LinearLayout>

```
we used a Linear Layout,set the orientation of the Layout to vertical. Our app design requires all app to be aligned in a centered and horizontal position. so we used the the **gravity** property and set it to center_horizontal.


### Activity or control code
Here we determine how the views behave, both the buttons and the chronometer
Here is a break down of it:
1. The start button needs to start if it not already.
2. The pause button should pause the timing
3. While the reset should return the time to 0

**Chromometer base property**
it is used to set the start time of the timer. it is set to 
``` 
SystemClock.elapsedRealtime()
```
it sets the base to zero.

**Start method**
Starts the chronometer

**Stop method**
Stops the chronometer

Read more: [Chronometer](https://developer.android.com/reference/android/widget/Chronometer)



Each buttons require an onclicklistener to listen to events.
There are 3 variables that will be set which are
1. **stopwatch:** This holds a reference to the chronometer
2. **running:** This is a boolean that keeps track of if the timer is running or not.
3. **Offset:** Keep track of the accurate time when the timer is paused, its important in restarting the timer


```
package com.backendpapa.stopwatch

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.os.SystemClock
import android.widget.Button
import android.widget.Chronometer

class MainActivity : AppCompatActivity() {

//    1
    lateinit var stopwatch:Chronometer;
    var running=false;
    var offset:Long=0;
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

//        2
        stopwatch=findViewById(R.id.stopwatch)

//        3
        val startButton=findViewById<Button>(R.id.start)
        startButton.setOnClickListener{
            if( !running){
                setBaseTime()
                stopwatch.start()
                running=true;
            }
//            5
            val pauseButton=findViewById<Button>(R.id.pause)
            pauseButton.setOnClickListener{
                if(running){
                    stopwatch.stop()
                    saveOffset()
                    running=false
                }
            }
//            7
            val resetButton=findViewById<Button>(R.id.reset)
            resetButton.setOnClickListener{
                offset=0;
                setBaseTime()

            }
        }
    }
// 4
    fun setBaseTime(){
        stopwatch.base=SystemClock.elapsedRealtime()-offset;
    }
//    6
    fun saveOffset(){
        offset=SystemClock.elapsedRealtime()-stopwatch.base
    }
}
```

![alt text](https://github.com/backendpapa/Head-first-android-development/blob/main/Activity/result1.png?raw=true)