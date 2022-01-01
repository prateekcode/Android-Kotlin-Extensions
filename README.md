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
   
## Extension for ACTIVITIES & FRAGMENTS   
   
   1. To replace child fragment with Animation
      ```kotlin
      fun Fragment.replaceChildFragmentWithAnimation(
             fragment: Fragment, @IdRes frameId: Int,
             addBackStack: String? = null
         ) {
             val fragTransaction = childFragmentManager.beginTransaction()
             fragTransaction.setCustomAnimations(android.R.animator.fade_in, android.R.animator.fade_out)
             fragTransaction.apply {
                 if (addBackStack != null) {
                     addToBackStack(addBackStack)
                 }
                 replace(frameId, fragment)
                 commitAllowingStateLoss()
             }
         }
   
   2. To replace child fragment
      ```kotlin
      fun Fragment.replaceChildFragment(
             fragment: Fragment, @IdRes frameId: Int,
             addBackStack: String? = null
         ) {
             val fragTransaction = childFragmentManager.beginTransaction()
             fragTransaction.apply {
                 if (addBackStack != null) {
                     addToBackStack(addBackStack)
                 }
                 replace(frameId, fragment)
                 commitAllowingStateLoss()
             }
         }


## Extension for LOGGER
   ```kotlin
   fun showLog(message: String?, tag: String = "TAG-NAME") {
    message?.let {
        if (BuildConfig.DEBUG) {
            printFullLog(it, tag)
        }
      }
   }
   
   private fun printFullLog(message: String, tag: String) {
    if (message.length > 3000) {
        Log.e(tag, message.substring(0, 3000))
        printFullLog(message.substring(3000), tag)
    } else {
        Log.e(tag, message)
      }
   }
