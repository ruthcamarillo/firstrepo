
import React, { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import "../Styles/login.css"

const Login = () => {
  const navigate = useNavigate();

  const [account, setAccount] = useState({
    login_id: '',
    email: ''
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setAccount((prevAccount) => ({ ...prevAccount, [name]: value }));
  };

  const handleLogin = (e) => {
    e.preventDefault();
    const { login_id, email } = account;

    fetch(`http://localhost:8080/accounts?loginId=${login_id}&email=${email}`)
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        if (data && data.length > 0) {
          const account = data.find((acc) => acc.login_id === login_id && acc.email === email);
          if (account) {
            const accountType = account.accountType;
            if (accountType && accountType.id === "A") {
              navigate("/admin");
              console.log("Is admin");
            } else if (accountType && accountType.id === "V") {
              navigate("/dashboard", { state: { user: account } });
              console.log("Is reg user");
            } else {
              console.error("Unknown account type:", accountType && accountType.id);
            }
          } else {
            console.error("Account not found");
          }
        } else {
          console.error("Account not found");
        }
      })
      .catch((error) => {
        console.error("Error occurred during login:", error);
      });
  };

  return (
    <div className="login-screen">
      <div className="login-container">
        <form>
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
            <button type="submit" onClick={handleLogin}>
              Login
            </button>
          </div>
        </form>
      </div>
    </div>
  );
};

export default Login;
