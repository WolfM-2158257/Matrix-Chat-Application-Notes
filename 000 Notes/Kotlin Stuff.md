## Scope functions
- `.let{}`
```kotlin
question3.et{
	print(it.questionText)
	println(it.answer)
	println(it.difficulty)
}
// sames as (`it` replaces `question3`)
print(question3.questionText)
println(question3.answer)
println(question3.difficulty)
```
- `.apply{}`
```kotlin
val quiz = Quiz();
quiz.printQuiz();
// instead you can use
Quiz().apply {
	printQuiz();
}
```