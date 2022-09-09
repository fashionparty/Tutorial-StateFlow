## StateFlow

Pełni podobną funkcję co `LiveData` ale nie posiada lifecycle awareness. Wysyła emisje nawet jeśli nic ich nie zbiera (hot flow). Notyfikuje swoich obserwatorów o zmianach.

```
// VM

private val _stateFlow = MutableStateFlow(value=0)
val stateFlow = _stateFlow.asStateFlow()

fun incrementCounter() {
  _stateFlow.value += 1
}



// Fragment

lifecycleScope.launch {
//repeatOnLifecycle zapewnia bezpieczne wykonanie korutyny bez względu na zmiany stanu fragmentu
  repeatOnLifecycle(LifecycleState.STARTED) {
    viewModel.stateFlow.collectLatest {
      binding.tv.text = it.toString()
     }  
   }
 }
 
 binding.button.setOnClickListener {
  viewModel.incrementCounter()
 }
```
