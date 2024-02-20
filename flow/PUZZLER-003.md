# Puzzler 003: Network Request with Loading State

## Description

This exercise challenges you to implement a screen that fetches data from an API using a Flow in the ViewModel. While fetching data, display a loading indicator. Upon successful retrieval, show the fetched data. If an error occurs, display an appropriate error message.

## Problem Specification:

* Create a screen with a button labeled "Fetch Data".
* Clicking the button triggers a network request using a Flow in the ViewModel.
* While fetching data, display a progress indicator or loading animation.
* If the data is fetched successfully, update the UI to display the retrieved information.
* If an error occurs during the network request, display an error message to the user.
* Use appropriate error handling mechanisms to catch potential exceptions.

## Focus:

* Understanding how to use Flows for asynchronous operations like network requests.
* Managing different emission states (loading, success, error) in the UI based on Flow values.
* Implementing error handling for network requests.

## Implementation:

1. **ViewModel:**
    * Define a Flow that fetches data from the API upon receiving a trigger (e.g., button click).
    * Use appropriate libraries or methods for making the network request.
    * Emit different states from the Flow based on the request outcome:
        * Loading state while fetching data.
        * Success state containing the fetched data.
        * Error state with an exception object.
2. **Screen:**
    * Observe the Flow emitted by the ViewModel using `viewModel.dataState.collectAsState()`.
    * Based on the observed state:
        * If loading, display a progress indicator.
        * If success, update the UI to display the fetched data.
        * If error, display an error message to the user.

**Additional Notes:**

* You can use libraries like [Retrofit](https://square.github.io/retrofit/) or [Volley](https://google.github.io/volley/) for making network requests.
* Consider using sealed classes or data classes to represent different emission states in the Flow.
* Implement proper error handling and display user-friendly error messages.

**Challenge:**

* Implement a retry mechanism for failed network requests.
* Display additional information like loading progress percentage or remaining time.

# Implementation (Simulate Network Delay)

## Add Data state class

```kotlin
sealed class DataState {
    data object Initial : DataState()
    data object Loading : DataState()
    data class Success(val data: String) : DataState()
    data class Error(val error: String) : DataState()
}
```

## Add Repository

```kotlin
interface DataRepository {
    suspend fun getData(): String
}

class HttpBinRepository: DataRepository {
    override suspend fun getData(): String {
        delay(5000) // Simulate network delay
        return "Fetched data!"
    }

}
```

## Add View Model

```kotlin
class NetworkRequestViewModel(
    private val repository: DataRepository
) : ViewModel() {
    private val _dataState = MutableStateFlow<DataState>(DataState.Initial)
    val dataState: Flow<DataState> = _dataState

    fun fetch() {
        viewModelScope.launch {
            try {
                _dataState.emit(DataState.Loading)
                val data = repository.getData()
                _dataState.emit(DataState.Success(data))
            } catch (e: Exception) {
                _dataState.emit(DataState.Error(e.message ?: "An error occurred"))
            }
        }
    }

    fun reset() {
        viewModelScope.launch {
            _dataState.emit(DataState.Initial)
        }
    }
}
```

## Add Screen

```kotlin
@Composable
fun NetworkRequestScreen(controller: NavHostController, vm: NetworkRequestViewModel) {
    val dataState = vm.dataState.collectAsState(initial = DataState.Initial)
    Column(
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally,
        modifier = Modifier
            .fillMaxSize()
            .padding(20.dp)
    ) {

        when(dataState.value) {
            DataState.Initial -> {
                Button(onClick = {
                    vm.fetch()
                }) {
                    Text("Fetch Data")
                }
            }
            DataState.Loading -> {
                CircularProgressIndicator(modifier = Modifier.padding(16.dp))
            }
            is DataState.Success -> {
                Text("Data: ${(dataState.value as DataState.Success).data}")
                Button(onClick = { vm.reset() }) {
                    Text("Reset")
                }
            }
            is DataState.Error -> {
                Text("Error: ${(dataState.value as DataState.Error).error}")
            }
        }
    }
}
```

# Implementation (Actual Network Request)

## Add required dependencies

`app/build.gradle.kts`

```kotlin
implementation("com.squareup.retrofit2:retrofit:2.9.0")
implementation("com.squareup.retrofit2:converter-gson:2.9.0")
```

## Add network permission

`app/src/main/AndroidManifest.xml`

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
     xmlns:tools="http://schemas.android.com/tools">

     <uses-permission android:name="android.permission.INTERNET"/>

     <application>
      ...
     </application>
```

## Add API client

`data/network/ApiClient.kt`

```kotlin
object ApiClient {
    private const val BASE_URL = "https://httpbin.org/"

    private val client = OkHttpClient.Builder().build()

    private val retrofit = Retrofit.Builder()
        .baseUrl(BASE_URL)
        .client(client)
        .addConverterFactory(GsonConverterFactory.create())
        .build()

    val apiService: ApiService by lazy {
        retrofit.create(ApiService::class.java)
    }
}
```

## Add API service

`data/service/ApiService.kt`

```kotlin
interface ApiService {

    @GET("uuid")
    suspend fun getUuid(): UuidResponse
}
```

## Add Response class

`data/domain/UuidResponse.kt`

```kotlin
data class UuidResponse(val uuid: String)
```

## Now modify the Repository

`data/repository/DataRepository.kt`

```kotlin
class HttpBinRepository: DataRepository {
    override suspend fun getData(): String {
        val response = ApiClient.apiService.getUuid()
        return response.uuid
    }

}
```




