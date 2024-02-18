# Puzzler 002: Download Progress

## Description

This exercise simulates downloading a file and displaying its progress in real-time using Jetpack Compose and Flows.

## Problem Specification

* Implement a composable screen with the following elements:
    * A progress bar that visualizes the download progress (0-100%).
    * A text displaying the current download percentage.
* Simulate downloading a file using a Flow that emits progress updates over time.
* Update the progress bar and text dynamically based on the emitted values from the Flow.
* Handle potential errors during the download process and display an appropriate message to the user.

## Focus:

* Transforming Flow values to update UI elements (progress bar and text).
* Handling different emission states (progress updates, completion, error).

## Implementation:

1. **ViewModel:**
    * Define a `downloadProgress` Flow that emits integer values between 0 and 100 representing the download progress.
    * Implement a coroutine that simulates the download process with a delay and emits progress updates at regular intervals.
    * Handle potential exceptions during the download and emit an error message through the Flow.
2. **Screen:**
    * Observe the `downloadProgress` Flow from the ViewModel.
    * Use a `ProgressIndicator` composable to visualize the progress based on the received values.
    * Update a text composable to display the current download percentage alongside the progress bar.
    * Handle error messages emitted by the Flow and display them to the user using appropriate UI elements.

## Additional Notes

* You can customize the download simulation logic and error handling as needed.
* Consider using libraries like `coil` for handling image downloads in real-world scenarios.
* Explore different UI components and animations to enhance the user experience.

This exercise demonstrates how to utilize Flows to manage asynchronous operations like downloads and update UI elements accordingly.

---

## Implementation



