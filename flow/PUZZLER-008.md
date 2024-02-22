# Puzzler 008: Real-time Sensor Data

**Description:**

This exercise challenges you to create a screen that displays real-time sensor data, specifically accelerometer readings in this case. Utilize a Flow in the ViewModel to continuously access sensor data and update the UI dynamically.

**Problem Specification:**

* Implement a screen that displays the current X, Y, and Z values of the accelerometer in real-time.
* Use the appropriate Jetpack Compose APIs to access sensor data.
* Create a Flow in the ViewModel that emits new sensor readings at regular intervals.
* Update the UI on the screen whenever a new reading is received from the Flow.
* Consider handling potential errors or sensor unavailability.

**Focus:**

* Understanding how to use Flows for continuous data streams like sensor readings.
* Consuming sensor data and updating UI components dynamically.
* Handling potential errors or exceptions during sensor access.

**Implementation:**

1. **ViewModel:**
    * Use the `SensorManager` class to access the accelerometer sensor.
    * Register a listener for sensor data changes.
    * Create a Flow that emits new accelerometer readings received from the listener.
    * Unregister the listener when the ViewModel is cleared to avoid memory leaks.
2. **Screen:**
    * Observe the Flow emitted by the ViewModel using `viewModel.sensorData.collectAsState()`.
    * Extract the X, Y, and Z values from the latest sensor reading.
    * Update the UI components (e.g., Text views) to display the current sensor values.

**Additional Notes:**

* Consider using libraries like `androidx.core:core-ktx` for simplified sensor access.
* Implement proper error handling and display user-friendly messages if sensor data is unavailable.
* You can customize the update frequency and UI elements based on your preferences.

**Challenge:**

* Implement a visualization component (e.g., graph) to display the sensor data over time.
* Allow users to toggle between different sensor types (e.g., gyroscope, magnetometer).

