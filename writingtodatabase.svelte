
<script>
//!removed this from the fireb.js file and attempt to add it to the userprofileform.svelte instead

// importing firebase database requirments
import {
    getFirestore,
    collection,
    getDocs,
    addDoc
  }from 'firebase/firestore'


// ** connecting to Firebase database *** \\
//Initialise Services
const userdatabase = getFirestore()

// 'collecting' from firestore UsersDetails and then passing the data into the variable userdatabase
const collect_Users_Details = collection(userdatabase,'UsersDetail')
                                                                                // const collect_Skills = collection(userdatabase,'UserKills')
                                                                                // const collect_Experience = collection(userdatabase,'UserExperience')
                                                                                // const colllect_Portfolio = collection(userdatabase,'UserPortfolio')

//getting collection data (firebase) by using the firebase function 'GetDocs'
//this is returning all the data in our firebase database (think Loop) 
getDocs(collect_Users_Details)
.then((snapshot)=>
  {
    //users array
    let users =[]
    // running through the DATAbase storing it into the array 
    snapshot.docs.forEach((data) => {
        users.push({...data.data(), id: data.id})
    })
    //displaying the actual DATA from our database in a console log (not on screen)
    console.log(users)
  })

  //NewUserProfile(with a form) called add
    
  const addprofile = document.querySelector('.addbasic')
    addprofile.addEventListener('Submit',(e)=> {
      e.preventDefault()
    
      //using the form addbasic in the userprofileform.svelte will take the user input and save the data into UsersDetail collection
      addDoc(collect_Users_Details,
      {
        Name: addprofile.name.value,
        Surname: addprofile.surname.value,
      })
      .then(() => goto("/"))

    })

  //User Unsubscribes using a form delete
  //const unsubscribe = document.querySelector('.delete')
  unsubscribe.addEventListener('Submit',(e)=> {
    //e.preventDefault()


 const addprofile = document.querySelector('.addbasic')
      addprofile.addEventListener('Submit',(e)=> {
      e.preventDefault()

// using the form addbasic, taking the user input and save the data into UsersDetail collection in firestore database
  addDoc(collect_Users_Details,
  {
      Name: addprofile.name.value,
      Surname: addprofile.surname.value,
  })
      .then(() => goto("/"))

  
  
  //pushing data manually to database , keeping the code here as a template/reference 
      try {
      const docRef = await addDoc(collection(userdatabase, "UsersDetail"), {
          Named: "Alan",
          Surname: "Mathison",
          Current: "Student"
  });


</script>


    <label for="name">Name:</label>
    <input type="text" name="name" required>
    <br>
    <br>
    <label for="surname">Surname:</label>
    <input type="text" name="surname" required>
        
    <a href="/index"><button type="submit" class="btn btn-primary">Submit</button></a>