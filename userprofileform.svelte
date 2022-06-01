<script>

import {goto} from '$app/navigation';
import {userdatabase} from 'fireb.js';

import { collection, addDoc, getDoc } from "firebase/firestore"; 

let users = []

userdatabase.collection('UsersDetail').onSnapshot(data = >
{
  users =data.docs
})

//add data
try {
  const docRef = await addDoc(collection(userdatabase, "UsersDetail"), {
    first: "James",
    last: "Dean",
    born: 1880
  });
  console.log("Document written with ID: ", docRef.id);
} catch (e) {
  console.error("Error adding document: ", e);
}

//retrieve data

const docRef = doc(userdatabase, "cities", "SF");
const docSnap = await getDoc(docRef);

if (docSnap.exists()) {
  console.log("Document data:", docSnap.data());
} else {
  // doc.data() will be undefined in this case
  console.log("No such document!");
}


</script>

<!-- ############################################## -->

<div id="users">
  USER
  {#each users as user}
    <div> users </div>
  {/each}
</div>


<!-- ############################################## -->

<form>
  <div class="form-row">
    <div class="form-group col-md-6">
      <label for="firstname">First Name</label>
      <input type="firstname" class="form-control" id="fname" placeholder="First Name">
    </div>
    <div class="form-group col-md-6">
      <label for="lastname">Last Name</label>
      <input type="lastname" class="form-control" id="lname" placeholder="Last Name">
    </div>
  </div>
  
  <button type="submit" class="btn btn-primary">Save Data</button>
</form>

