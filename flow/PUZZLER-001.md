# Exercise 1: Simple Timer with Navigation
## Description:

Create a Jetpack Compose app with 2 screens:

**Home Screen**: Displays a button labeled "Start Timer". Clicking the button starts a timer in the ViewModel using a Flow, hides the "Start Timer" button and displays a circular progress indicator.
**Finish Screen**: Displays a message "Time's Up!" and a button labeled "Back". Clicking the button the app navigates to the **Home** screen.

When the timer reaches 5 seconds, the app should automatically navigate from **Home** Screen to **Finish** Screen.

## Focus:
* Understanding how to use Flow in a ViewModel to manage state.
* Observing Flow values in composables to trigger navigation.


---

# Implementation

## Add required dependencies
add the following in the `dependencies` section of `app/build.gradle.kts`

```gradle
implementation("androidx.navigation:navigation-compose:2.7.7")

val lifecycleVersion = "2.7.0"
implementation("androidx.lifecycle:lifecycle-viewmodel-ktx:$lifecycleVersion")
implementation("androidx.lifecycle:lifecycle-viewmodel-compose:$lifecycleVersion")
```
## Add Navigation

Create a navigation composable and Routes object

```kotlin
@Composable
fun Navigation() {
    val controller = rememberNavController()
    NavHost(navController = controller, startDestination = Routes.HOME) {

        composable(Routes.HOME) {
            HomeScreen(controller, HomeViewModel())
        }

        composable(Routes.FINISH) {
            FinishScreen(controller)
        }
    }
}
```

```kotlin
object Routes {
    const val HOME = "home"
    const val FINISH = "finish"
}
```

## Add the navigation composable in the main activity

`MainActivity.kt`

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            FlowTutorialTheme {
                Navigation()
            }
        }
    }
}
```

## Create TimerState class

`data/domain/TimerState.kt`

```kotlin
sealed class TimerState {
    data object Initial : TimerState()
    data object Pending : TimerState()
    data object Complete: TimerState()
}
```

## Create ViewModel for the Home screen

`/ui/viewmodel/HomeViewModel.kt`

```kotlin
class HomeViewModel : ViewModel() {
    private val _timerState = MutableStateFlow<TimerState>(TimerState.Initial)
    val timerState: Flow<TimerState> = _timerState

    fun startTimer(timeMillis: Long) {
        viewModelScope.launch {
            _timerState.emit(TimerState.Pending)
            delay(timeMillis = timeMillis)
            _timerState.emit(TimerState.Complete)
        }
    }
}
```

## Add the Home Screen

```kotlin
@Composable
fun HomeScreen(controller: NavHostController, vm: HomeViewModel) {
    val timerState = vm.timerState.collectAsState(initial = TimerState.Initial)
    Column(
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally,
        modifier = Modifier
            .fillMaxSize()
            .padding(20.dp)
    ) {
        when(timerState.value) {
            is TimerState.Initial -> {
                Button(onClick = {
                    vm.startTimer(5000)
                }) {
                    Text("Start Timer")
                }
            }
            is TimerState.Pending -> {
                CircularProgressIndicator(
                    modifier = Modifier.width(64.dp),
                    color = MaterialTheme.colorScheme.primary,
                    trackColor = MaterialTheme.colorScheme.surfaceVariant,
                )
            }
            is TimerState.Complete -> controller.navigate(Routes.FINISH)
        }
    }
}
```

## Add the Finish Screen

```kotlin
fun FinishScreen(controller: NavHostController) {
    Column(
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally,
        modifier = Modifier
            .fillMaxSize()
            .padding(20.dp)
    ) {
        Text(text = "Time's Up!", modifier = Modifier.padding(bottom = 30.dp))
        Button(onClick = {
            controller.navigate(Routes.HOME)
        }) {
            Text("Back")
        }
    }
}
```





