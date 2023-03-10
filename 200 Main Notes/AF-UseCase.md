Top:: [[Application Flow]]
---
# UseCase
A use-case is a wrapper-class that overwrites the default invoke function to handle user input data to model data.
## Example
### Repository
```kt
class TestRepository {
	fun makeLoginRequest(username: String, password: String){
		// Do stuff here
	}
}
```
### UseCase
Usecase is responsible for validating the data and correct error handling
```kt
class LoginUseCase(
	username: String,
	password: String,
	repository: TestRepository = Singleton.getTestRepositoryInstance() 
	// pseudo code, could be resolved with dependency injection, custom singleton or Dagger-Hilt plugin
){
	// overwrite invoke function of a class
	operator fun invoke() : Result<String>{
		if(username.length() == 0) return Result.Error("Username must be of length greater than 0");
		if(password.length() == 0) return Result.Error("Password must be of length greater than 0");
		  // also pseudo code, just handle the login
		try{
			return Result.Success(repository.makeLoginRequest(username, password));
		}
		catch(e: LoginException){
			return Result.Error(e);
		}
		
	}
}
```

> [!note]
> Since we are overwriting the invoke operator 'LoginUseCase()'. We can execute the code within the function on class creation (See ViewModel [[#ViewModel]])
### ViewModel
ViewModel is responsible for updating the view data, making an easy interface between UseCases and view. 
```kt
class LoginViewModel : ViewModel(
	// viewmodel garbage here (context, etc...),
	// repository if needed, depends on implementation
){
	private val _isLoggedIn = MutableStateFlow(false);
	val isLoggedIn(): StateFlow(Boolean) = _isLoggedIn;

	fun login(username: String, password: String){
		when(LoginUseCase(username, password)){
			is Result.Error -> //TODO: handle error
			is Result.Success -> //TODO: handle login
		}
	}
}
```

### View
Just responsible for showing the data
```kt
@Composable
fun DiceRollScreen(
	viewModel: DiceRollViewModel = viewModel()
) {    
	val isLoggedIn by viewModel.isLoggedIn.collectAsStateWithLifecycle()    
	// Update UI elements
}
```