<template>
    <div id="main">
        <div id="input">
            <!-- div for email input -->
            <div id="email">   
             <b><label for="email">Email: </label></b>
                <input ref="emailBox" type="text" class="emailBox" name="emailBox">
            </div>
           <!-- div for message input -->
            <div id="messageInput">
                <b><label for="message">Message: </label></b>
                <textarea ref="message" name="paragraph_text" cols="30" rows="4"></textarea>
               
            </div>
            <!-- div for submit Container -->
            <div id="submitContainer">
                <input @click="saveMessage()" id="submit" type="submit" value="Add">
            </div>
            <br>
            <p class="success" ref="successMsg"></p>
        </div>
    </div>


</template>

<script>
import firebase from 'firebase/app'
import {db} from '../components/firebase'

export default {
  name: "messagesInput",
  props: {

  },
  data() {
      return {
          name: "messagesInput"
      }

  },
  methods: {
      saveMessage() {
          const email = this.$refs.emailBox.value
          const message = this.$refs.message.value
           
          console.log( email, message)
            // Add a new document in collection "message", within Firebase.
            db.collection("messages").doc(email).update({ messages: firebase.firestore.FieldValue.arrayUnion(message), })
            .then(function() {
                console.log("Document successfully written!");
                
            })
            .catch(function(error) {
                console.error("Error writing document: ", error);
            });
            // Alerts user that the message was successfully sent.
            this.$refs.successMsg.innerHTML = "Message successfully delivered!";
      }
  }
} 

</script>


<style scoped lang="scss">
#main {
    height: 100vh;
    width: 100vw;
    display: flex;
    flex-direction: row;
    background-color: #9c88ff;
    justify-content: space-evenly;
}

#input {
    height: 50%;
    width: 100%;
    display: flex;
    flex-direction: column;
    margin-top: 10px;
}



#email {
    display: flex;
    flex-direction: row;
    justify-content: center;
    height: 7.5%;
    margin-top: 17px;
    color: black;
    width: 100%;   
}

.emailBox {
    
}

#submitContainer {
    height: 20%;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

#submit {
  color: black;
  text-align: center;
  text-decoration: none;
  font-size: 16px;
  border-radius: 7px; 
  margin-top: 10%;
  width: 50px;
  height: 35px;
  border: solid 2px black;
}

#messageInput {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    height: 30%;
    margin-top: 10px;
    color: black;
    width: 100%;  
}

.messageBox {
    display: flex;
    justify-content: center;
    height: 50%;
    border: solid 2px pink;
}

.success {
    color: limegreen;
}
</style>