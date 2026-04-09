## Steps to build a real-time database
1. Create a new project on firebase  

2. Create a web App and configure the SDK

<img src="../Images/create-web-app.png" width="400">  


3. Build a real-time database.  

<img src="../Images/realtime-database.png" width="400">

4. Change the read and write rule so we can push the data

<img src="../Images/rule.png" width="400">

5. Create a reference, which is a **specific location** in the database where we can push the data.

6. Get the data by `onValue`. It listens to the **database reference changes**. (like addEventListener). Whenever it is happening, the code is running. 
    * snapshot is an object, and it is always `true` no matter it contains any data
    * To check if it contains anything, used `snapshot.exists()`

7. Remove all the data by `remove`

```js
import { initializeApp } from "https://www.gstatic.com/firebasejs/12.10.0/firebase-app.js"
import { getDataBase, ref, push, obValue, remove } from "https://www.gstatic.com/firebasejs/12.10.0/firebase-database.js"

const firebaseConfig = {
    databaseURL: "https://leads-tracker-app-602c5-default-rtdb.firebaseio.com/"
}

const app = initializeApp(firebaseConfig)
const database = getDataBase(app)
// birthday is the location name
const referenceInDB = ref(database, "birthdays")

submitButton.addEventListener("click", function() {
    push(referenceInDB, birthdayInputField.value)
    birthdayInputField.value = ""
})

deleteAllButtonEl.addEventListener("dblclick", function() {
    remove(referenceInDB)
    ulEl.innerHTML = ""
})


// snapshot.val will return an object that contains only the value
onValue(referenceInDB, function(snapshot) {
    // This is to avoid the error caused by remove, because we can't change undefined to an array
    if (snapshot.exists()) {
        console.log(Object.values(snapshot.val()))
    }
})
>>> {-Nw11oXz5yNwCakK46p-: 'Macbook Pro', -Nw11pznveNmjjnQ5FAB: 'iPhone', -Nw12tgVAbUMXOD2_ZyS: 'Playstation 4'}

```
<img src="../Images/reference.png" width="400">
