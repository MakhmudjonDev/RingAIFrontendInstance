<template>
  <div class="container">
    <div class="gray-box">
      <!-- Content inside the gray box -->

      <!-- Input field and submit button for adding new numbers -->
      <div class="addnum">
        <input class="input-field" type="text" v-model="newNumber" placeholder="Yangi raqam qo'shing">
        <button class="add-button" @click="addNumber">Qo'shish</button>
      </div>

      <h2>Raqamlar royhati</h2>
      <ul>
        <li v-for="(item, index) in numberList" :key="index">
          <div class="number-item">
            <div class="checkbox-container">
              <input type="checkbox" :id="'checkbox-' + index" />
              <label class="checkbox-label" :for="'checkbox-' + index">{{ item.phoneNumber }}</label>
            </div>
            <div class="button-container">
              <button class="button red-button" @click="deleteNumber(index)">O'chirish</button>
              <button class="add-button" @click="callNumber(item.phoneNumber)">Qo'ng'iroq</button>
            </div>
          </div>
        </li>
      </ul>

      <!-- Buttons below the gray box -->
      <div class="buttons">
        <button class="button gray-button" @click="showGrayAlert">Belgilanqanlariga qilish</button>
        <button class="button red-button" @click="showRedAlert">Hammasiga qilish</button>
      </div>
    </div>
  </div>
</template>


<script>
// import axios from 'axios';

export default {
  data() {
    return {
      numberList: [],
      newNumber: '',
      customerPKs: {}
    };
  },
  methods: {
    addNumber() {
      if (this.newNumber.trim() !== '') {
        const xhr = new XMLHttpRequest();
        xhr.open('POST', 'http://176.98.237.4/apiproject/api/v1/customer/');
        xhr.setRequestHeader('Content-Type', 'application/json');
        xhr.setRequestHeader('Authorization', 'Token 471619b0d8d6d5e58d9178e46775c2b90d8f1289');
        xhr.onload = () => {
          if (xhr.status === 201) {
            const response = JSON.parse(xhr.responseText);
            const customerPK = response.pk;
            this.numberList.push({
              phoneNumber: this.newNumber.trim(),
              pk: customerPK
            });
            this.newNumber = '';
          } else {
            console.error('Error adding number:', xhr.responseText);
          }
        };
        xhr.onerror = () => {
          console.error('Error adding number:', xhr.responseText);
        };
        xhr.send(JSON.stringify({
          fullName: 'Java',
          phoneNumber: this.newNumber.trim(),
          info: 'test'
        }));
      }
    },
    deleteNumber(index) {
      this.numberList.splice(index, 1);
    },
    callNumber(number) {
      const customer = this.numberList.find(item => item.phoneNumber === number);
      if (customer) {
        const xhr = new XMLHttpRequest();
        xhr.open('GET', `http://176.98.237.4/apiproject/api/v1/call/${customer.pk}/`);
        xhr.onload = () => {
          console.log('Status:', xhr.status);
          if (xhr.status === 200) {
            console.log("Call initiated successfully:", xhr.responseText);
            alert("Call initiated successfully!");
          } else if (xhr.status == 202){
            console.error("it is something else. Trying initiating call:", xhr.responseText);
            alert("Process started. Call is being initiated");
          } 
          else {
            console.error("it is something else. Trying initiating call:", xhr.responseText);
            alert("Trying to initiate call.");
          }
        };
        xhr.onerror = () => {
          console.error("Error initiating call:", xhr.responseText);
          alert("Failed to initiate call. Please try again later.");
        };
        xhr.send();
      }
    },
    showGrayAlert() {
      alert('Belgilangan raqamlarga qongiroq qilindi!');
    },
    showRedAlert() {
      alert('Hamma raqamlarga qongiroq qilindi!');
    },
    getCustomerId() {
      return 123; // Replace with actual customer ID retrieval logic
    }
  }
};
</script>
  
  <style>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 50vh; /* Minimum height of 50% of the viewport height */
  }
  
  .gray-box {
    background-color: #f2f2f2;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
    width: 70%; /* Adjust the width as needed */
    max-width: 600px; /* Maximum width for better readability */
    font-size: 1em; /* Font size for numbers */
  }
  .gray-box ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}
  
  .checkbox-container {
    display: flex;
    align-items: center;
  }
  
  .checkbox-label {
    margin-left: 10px;
  }
  
  .addnum {
    margin-top: 20px;
    display: flex;
    align-items: center;
  }
  
  .input-field {
    padding: 8px;
    font-size: 1em;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  
  .add-button {
    padding: 8px 15px;
    font-size: 1em;
    border: none;
    border-radius: 5px;
    background-color: #4CAF50;
    color: white;
    cursor: pointer;
  }
  
  .add-button:hover {
    background-color: #45a049;
  }
  
  .buttons {
    margin-top: 20px;
    display: flex;
    float: right;

  }
  
  .button {
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .gray-button {
    background-color: #ccc;
  }
  
  .red-button {
    background-color: #ff6347;
    color: #fff;
  }
  .number-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.button-container {
  display: flex;
}

.delete-button,
.call-button {
  margin-left: 10px;
}
  </style>
  