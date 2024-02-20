## Puzzler 006: Shared Flow for Global Events

**Description:**

This exercise introduces the concept of using a Shared Flow to manage global events that can be observed by multiple screens in your Jetpack Compose application.

**Problem Specification:**

* Implement a shared Flow in the ViewModel that emits events indicating network connectivity changes (online/offline).
* Create two separate screens:
    * Screen 1 displays a text message indicating the current network status.
    * Screen 2 displays a button that is only enabled when the network is online.
* Both screens should observe the shared Flow from the ViewModel and update their UI accordingly.

**Focus:**

* Understanding how to use Shared Flow for communication between different screens.
* Observing Flow values from multiple composables.
* Updating UI based on shared state changes.

**Implementation:**

1. **ViewModel:**
    * Define a `SharedFlow<NetworkState>` to emit network connectivity events.
    * Use appropriate libraries or methods to monitor network changes.
    * Emit `NetworkState.Online` when online and `NetworkState.Offline` when offline.
2. **Screen 1:**
    * Observe the shared Flow using `viewModel.networkState.collectAsState()`.
    * Update the text message to display the current network status based on the observed state.
3. **Screen 2:**
    * Observe the shared Flow using `viewModel.networkState.collectAsState()`.
    * Enable the button only when the observed state is `NetworkState.Online`.

**Additional Notes:**

* You can use libraries like ConnectivityManager to detect network changes.
* Consider using different UI elements or functionalities based on network availability.

**Challenge:**

* Implement a mechanism to handle initial network state upon app launch.
* Display additional information like signal strength or estimated download speed.

