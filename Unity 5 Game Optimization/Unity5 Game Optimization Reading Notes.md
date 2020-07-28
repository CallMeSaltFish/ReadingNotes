# Unity5 Game Optimization Reading Notes

## Chapter 1. Detecting Performance Issues（检测性能问题）

主要就是讲设备跟profiler组件的联调，以及设备的连接，profiler相关界面的介绍

The CPU Area will be most useful during **Chapter 2**, Scripting Strategies.

The GPU Area will be beneficial during **Chapter 6**, Dynamic Graphics.

The Rendering Area will be useful in **Chapter 3**, The Benefits of Batching.

The Audio Area will come in handy as we explore art assets in **Chapter 4**, Kickstart Your Art.

The Physics 3D/2D Area in **Chapter 5**, Faster Physics.



**System.Diagnostics  StopWatch**

we can easily acquire a measure of how much time has passed since the Stopwatch was started.Unfortunately, this class is not very accurate—it is accurate only to milliseconds, or tenths of a millisecond at best.However, if precision is important, then one effective way to increase it is by **running the same test multiple times**.

```c#
using UnityEngine;
using System;
using System.Diagnostics;
using System.Collections;
public class CustomTimer : IDisposable {
	private string m_timerName;
	private int m_numTests;
	private Stopwatch m_watch;
	// give the timer a name, and a count of the number of tests we're running
    public CustomTimer(string timerName, int numTests) {
        m_timerName = timerName;
        m_numTests = numTests;
        if (m_numTests <= 0)
        	m_numTests = 1;
        m_watch = Stopwatch.StartNew();
    }
	// called when the 'using' block ends
    public void Dispose() {
        m_watch.Stop();
        float ms = m_watch.ElapsedMilliseconds;
        UnityEngine.Debug.Log(string.Format("{0} finished: {1:0.00}ms total,
        {2:0.000000}ms per test for {3} tests", m_timerName, ms, ms / m_numTests,
        m_numTests));
        }
    }

	//The following is an example of the CustomTimer class usage:

    int numTests = 1000;
    using (new CustomTimer("My Test", numTests)) {
        for(int i = 0; i < numTests; ++i) {
        	TestFunction();
    	}
	} // the timer's Dispose() method is automatically called here
```

When the **using** block ends, it will automatically
invoke the object’s Dispose() method to handle any cleanup operations.

Another concern to worry about is application warm up. Unity has a significant startup cost when a Scene begins, given the number of calls to various GameObjects’ Awake() and Start() methods, as well as initialization of other components such as the Physics and Rendering systems.

```c#
if (Input.GetKeyDown(KeyCode.Space)) {
        int numTests = 1000;
        using (new CustomTimer("Controlled Test", numTests)) {
        for(int i = 0; i < numTests; ++i) {
            TestFunction();
        }
    }
}
```

Unity’s console logging mechanism is prohibitively expensive.

## Chapter 2. Scripting Strategies

### Cache Component references

**A common mistake when scripting in Unity is to overuse the GetComponent() method.**

### Obtaining Components using the fastest method

### Removing empty callback declarations

### Avoiding the Find() and SendMessage() methods at runtime

#### Static classes

#### Singleton Components

The disadvantage of the **static class** approach is that they must inherit from the lowest form of class—Object.（**cannot** inherit from **MonoBehaviour**）

P110--> a SingletonAsComponent class

122