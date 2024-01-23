[![OTPless](https://d1j61bbz9a40n6.cloudfront.net/website/home/v4/logo/white_logo.svg)](https://otpless.com/platforms/angular)

# Angular Demo

## Steps to add OTPless SDK to your Angular App

1. **Add OTPLESS Sign in**

> Add the following code to your sign up/ sign in page where you want to embed your sign in functionality.

```index.html

<script type="text/javascript" src="https://otpless.com/auth.js" cid="YOUR_CID_HERE"></script>
// Replace YOUR_CID_HERE with your cid
```

2. **Retrieve User's Information**

> Implement the following function to retrive the **user data** upon successful authentication of the user.

```component.ts
constructor() {
    //@ts-ignore
    window.otpless = (otplessUser) => {
     alert(JSON.stringify(otplessUser));
    };
   }

```




### Usage

> **Prequisite** [NodeJS](https://nodejs.org/en)

- Install Packages

    ```bash
    npm install
    ```

- Add `cid` to the script by replacing [YOUR_CID_HERE](./src/index.html#L14) with your cid from [OTPless docs](https://otpless.com/platforms/angular#angular_STEP_1)

- Run the demo

    ```bash
   ng serve

    ```

- Open [localhost:4200]((http://localhost:4200/)) in your browser
- Switch branches to check out available options to integrate *OTPless* in your project



> Received User Data Format

```js
// otpless user Format
{
    "token": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "timestamp": "YYYY-MM-DD HH:MM:SS",
    "timezone": "+XX:XX",
    "mobile": {
        "name": "User Name",
        "number": "User Mobile Number"
    },
    "email": {
        "name": "User Name ",
        "email": "User Email"
    }
}
```
