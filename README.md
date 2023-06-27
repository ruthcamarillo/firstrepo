# firstrepo
Practice creating first repo

import React, { useState } from 'react';

const NewUser = () => {
    const [account, setAccount] = useState({
        login_id: '',
        first_name: '',
        last_name: '',
        email: '',
        phone: '',
        address1: '',
        address2: '',
        city: '',
        st: '',
        zip: '',
        is_18: false,
        // points: 0,
        last_login_timestamp: new Date().toISOString()
      });
    
      const handleChange = (e) => {
        const { name, value } = e.target;
        setAccount((prevAccount) => ({ ...prevAccount, [name]: value }));
      };

      const handleSubmit = (e) => {
        e.preventDefault();
        // Call your create account API endpoint here, passing the account data
        fetch('http://localhost:8080/addUser', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(account)
        })
          .then((response) => response.json())
          .then((data) => {
            console.log('Account created successfully:', data);
            // Perform any additional actions after successful account creation
          })
          .catch((error) => {
            console.error('Error creating account:', error);
            // Handle any error that occurs during account creation
          });
      };
      return (
        
        <form onSubmit={handleSubmit}>
        <div>
          <label htmlFor="login_id">Login ID:</label>
          <input
            type="text"
            id="login_id"
            name="login_id"
            value={account.login_id}
            onChange={handleChange}
            required
          />
        </div>
  
        <div>
          <label htmlFor="first_name">First Name:</label>
          <input
            type="text"
            id="first_name"
            name="first_name"
            value={account.first_name}
            onChange={handleChange}
            required
          />
        </div>
  
        <div>
          <label htmlFor="last_name">Last Name:</label>
          <input
            type="text"
            id="last_name"
            name="last_name"
            value={account.last_name}
            onChange={handleChange}
            required
          />
        </div>
  
        <div>
          <label htmlFor="email">Email:</label>
          <input
            type="email"
            id="email"
            name="email"
            value={account.email}
            onChange={handleChange}
            required
          />
        </div>
  
        <div>
          <label htmlFor="phone">Phone:</label>
          <input
            type="text"
            id="phone"
            name="phone"
            value={account.phone}
            onChange={handleChange}
          />
        </div>
  
        <div>
          <label htmlFor="address1">Address 1:</label>
          <input
            type="text"
            id="address1"
            name="address1"
            value={account.address1}
            onChange={handleChange}
            required
          />
        </div>
  
        <div>
          <label htmlFor="address2">Address 2:</label>
          <input
            type="text"
            id="address2"
            name="address2"
            value={account.address2}
            onChange={handleChange}
          />
        </div>
  
        <div>
          <label htmlFor="city">City:</label>
          <input
            type="text"
            id="city"
            name="city"
            value={account.city}
            onChange={handleChange}
            required
          />
        </div>
  
        <div>
        <label htmlFor="st">State:</label>
        <input
          type="text"
          id="st"
          name="st"
          value={account.st}
          onChange={handleChange}
          required
        />
      </div>

      <div>
        <label htmlFor="zip">ZIP Code:</label>
        <input
          type="text"
          id="zip"
          name="zip"
          value={account.zip}
          onChange={handleChange}
          required
        />
      </div>

      <div>
        <label htmlFor="is_18">Is 18 or older?</label>
        <input
          type="checkbox"
          id="is_18"
          name="is_18"
          checked={account.is_18}
          onChange={(e) => setAccount((prevAccount) => ({ ...prevAccount, is_18: e.target.checked }))}
        />
      </div>

      {/* <div>
        <label htmlFor="points">Points:</label>
        <input
          type="number"
          id="points"
          name="points"
          value={account.points}
          onChange={handleChange}
          required
        />
      </div> */}

      <div>
        <button type="submit">Create Account</button>
      </div>
    </form>
  );
};
      

export default NewUser
