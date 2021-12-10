# Android-Kotlin-Extensions
Kotlin extension for common functions that save your time

## Extensions For CONTEXT & VIEW

1. Show <b>TOAST</b>
   ```kotlin
   fun Context.showToast(message: String?, length: Int = Toast.LENGTH_SHORT) {
      message?.let {
          Toast.makeText(this, it, length).show()
       }
    }

2. To show and hide visibility of any <b>VIEW</b>
   ```kotlin
   
   //To Show
   fun View.show() {
      visibility = View.VISIBLE
   }
   
   //To Hide
   fun View.hide() {
       visibility = View.GONE
   }
   
3. To get the String of EditText 
   ```kotlin
   fun EditText.getStringInput(): String {
      return text?.trim()?.toString() ?: ""
    }
   
4. To get the EditText on change
   ```kotlin
   fun EditText.onChange(textChanged: ((String) -> Unit)) {
      this.addTextChangedListener(object : TextWatcher {
          override fun afterTextChanged(s: Editable?) {
          }
          override fun beforeTextChanged(s: CharSequence?, start: Int, count: Int, after: Int) {}

          override fun onTextChanged(s: CharSequence?, start: Int, before: Int, count: Int) {
              textChanged.invoke(s.toString())
          }
      })
   }
   
5. To get the Editable from String
   ```kotlin
   fun String.toEditable(): Editable = Editable.Factory.getInstance().newEditable(this)
   
   
   
