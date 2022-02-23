import React, { useEffect } from "react";
import ReactDOM from "react-dom";

import "./styles.css";

/*
  Instructions:
    part1:
    You're given the UI for a basic form. Your task is to 
    hook it all up using refs. 

    The `Focus X Input` buttons should focus that specific input
    field.

    The `Submit` button should log `name`, `email`, and `password`
    to the console.

    The `Reset` button should result all of the input fields to 
    empty strings.

    part2: 
    Develop a search tag with debounce functionality.
    Debouncing means that a function will not be called again until
    a certain amount of time has passed. So here the setsearch method
    is called repeatedly for every key stroke, instead it should
    be delayed by the time peroid mentioned in the debounce method (add some 
    console log to validate this no need to use any api mock). 
    It should avoid memory leaks and the solution provided should be scalable.
    
    For api integration create an account in https://developers.giphy.com/dashboard/
    Once you have got your API token refer the search api docs page

    eg: api endpoint
    https://api.giphy.com/v1/gifs/search?api_key=< your api token >&q=<search value>

    Display the result images below in a 4x4 grid box, you can choose any size of your preference

    NOTE: 
    do not use any external library like lodash

*/

function ReactForm() {
  const [formData, setFormData] = React.useState({
    name: "",
    email: "",
    password: ""
  });

  let inpName = React.createRef();
  let inpEmail = React.createRef();
  let inpPassword = React.createRef();

  const handleSubmit = (e) => {
    setFormData({
      name: inpName.current.value,
      email: inpEmail.current.value,
      password: inpPassword.current.value
    });
    console.log(formData, "Step 1 Success");
  };
  const handleonChange = (e) => {
    console.log(inpName, e);
    setFormData({
      name: inpName.current.value,
      email: inpEmail.current.value,
      password: inpPassword.current.value
    });
  };

  const handleReset = () => {
    setFormData({
      name: "",
      email: "",
      password: ""
    });
  };

  const handleSearch = (value) => {
    console.log(value, "Debounce check step 2 success");
  };

  const debounce = (callback, delay) => {
    // add your debounce logic here
    let timeout = null;
    return function () {
      let context = this;
      let args = arguments;
      clearTimeout(timeout);
      timeout = setTimeout(() => {
        timeout = null;
        callback.apply(context, args);
      }, delay);
    };
  };
  const focusonHandle = () => {
    const key = 
    switch (key) {
      case "name":
        inpName.current.focus();
        break;
      case "email":
        inpEmail.current.focus();
        break;
      case "password":
        inpPassword.current.focus();
        break;
      default:
        break;
    }
  };

  // do not modify this line
  const debouncedSearch = debounce(handleSearch, 1000);
  return (
    <React.Fragment>
      <div>
        <p>part 1</p>
        <label>
          Name:
          <input
            placeholder="name"
            type="text"
            name={"name"}
            ref={inpName}
            onChange={handleonChange}
            value={formData.name}
          />
        </label>
        <label>
          Email:
          <input
            placeholder="email"
            type="text"
            ref={inpEmail}
            name={"email"}
            onChange={handleonChange}
            value={formData.email}
          />
        </label>
        <label>
          Password:
          <input
            placeholder="password"
            type="text"
            ref={inpPassword}
            name={"password"}
            onChange={handleonChange}
            value={formData.password}
          />
        </label>
        <hr />
        <button
          onCLick={focusonHandle}
        >
          Focus Name Input
        </button>
        <br />
        <button onCLick={focusonHandle}>Focus Email Input</button>
        <button onCLick={focusonHandle}>Focus Password Input</button>
        <hr />
        <button onClick={handleSubmit}>Submit</button>
        <button onClick={handleReset}>Reset</button>
      </div>
      <div>
        <hr />
        <p>part 2</p>
        <label>
          Search:
          <input
            placeholder="search with debounce"
            type="text"
            // do not modify this line
            onChange={(e) => debouncedSearch(e.target.value)}
          />
        </label>
      </div>
    </React.Fragment>
  );
}
const rootElement = document.getElementById("root");
ReactDOM.render(<ReactForm />, rootElement);
