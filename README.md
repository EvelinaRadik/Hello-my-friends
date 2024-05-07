Для начала создаем новый проект в Android Studio на языке Kotlin.

Создаем две активности: MainActivity и SecondActivity.

В MainActivity создаем 5 EditText для ввода данных пользователем и кнопку для перехода на вторую активность. 

xml
<EditText
    android:id="@+id/editText1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

<EditText
    android:id="@+id/editText2"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

<EditText
    android:id="@+id/editText3"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

<EditText
    android:id="@+id/editText4"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

<EditText
    android:id="@+id/editText5"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

<Button
    android:id="@+id/buttonSubmit"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Submit" />


В MainActivity создаем обработчик нажатия кнопки и сохраняем данные в JSON файл:

kotlin
val jsonObject = JSONObject()
jsonObject.put("param1", editText1.text.toString())
jsonObject.put("param2", editText2.text.toString())
jsonObject.put("param3", editText3.text.toString())
jsonObject.put("param4", editText4.text.toString())
jsonObject.put("param5", editText5.text.toString())

// Записываем JSON в файл
val file = File(filesDir, "data.json")
file.writeText(jsonObject.toString())

// Переход на вторую активность
val intent = Intent(this, SecondActivity::class.java)
startActivity(intent)


В SecondActivity читаем данные из JSON файла и выводим на экран:

kotlin
val file = File(filesDir, "data.json")
val data = file.readText()
val jsonObject = JSONObject(data)

// Выводим данные на экран
editText1.setText(jsonObject.getString("param1"))
editText2.setText(jsonObject.getString("param2"))
editText3.setText(jsonObject.getString("param3"))
editText4.setText(jsonObject.getString("param4"))
editText5.setText(jsonObject.getString("param5"))


Также добавим кнопку в SecondActivity для перехода обратно на MainActivity:

xml
<Button
    android:id="@+id/buttonBack"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Back" />


kotlin
buttonBack.setOnClickListener {
    val intent = Intent(this, MainActivity::class.java)
    startActivity(intent)
}


Не забудьте добавить разрешение для работы с файлами в манифесте:

xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />


Теперь у вас есть приложение на Kotlin, которое сохраняет данные в JSON файл, выводит их на экран во второй активности и переходит между активностями.
