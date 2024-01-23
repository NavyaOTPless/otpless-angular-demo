[![OTPless](https://d1j61bbz9a40n6.cloudfront.net/website/home/v4/logo/white_logo.svg)](https://otpless.com/platforms/angular)

# Angular Demo

## Steps to add OTPless SDK to your Angular App

1. **Add OTPLESS Sign in**

> Add the following code to your sign up/ sign in page where you want to embed your sign in functionality.

```component.html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f0f0f0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
  
  
    .modal-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      backdrop-filter: blur(8px);
      display: none;
      justify-content: center;
      align-items: center;
    }
  
  
    .modal {
      background-color: white;
      height: fit-content;
      width: fit-content;
      border-radius: 10px;
      backdrop-filter: blur(2px);
    }
  
  
    button {
      padding: 10px 20px;
      border: none;
      background-color: #007bff;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
  
  
  
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <div class="modal-container" id="modalContainer" (click)="closeModal($event)">
    <div class="modal">
      <div id="otpless-login-page"></div>
    </div>
  </div>
  <button id="openModalBtn" (click)="openModal()">Open Modal</button>
  
</body>
</html>
```

2. **Retrieve User's Information**

> Implement the following function to retrive the **user data** upon successful authentication of the user.

```component.ts
export class AppComponent {
  title = 'LoginpageWithButton';

  constructor(@Inject(PLATFORM_ID) private platformId: Object) {
    if (isPlatformBrowser(this.platformId)) {
      const script = document.createElement('script');
      script.src = 'https://otpless.com/auth.js';
      script.id = 'otplessScriptId'
      document.body.appendChild(script);
  
  
      const otpless = (otplessUser: any) => {
        alert(JSON.stringify(otplessUser))
        // Additional code to handle otplessUser
      };
      (window as any).otpless = otpless;
    }
  
  
    openModal (){
      (window as any).otplessInit()
      const modalContainer = document.getElementById('modalContainer');
      const modal = document.getElementById('otpless-login-page');
      (modalContainer as any).style.display = 'flex';
      (modal as any).style.display = (modal as any).style.display === 'block' ? 'none' : 'block';
    };
  
  
    closeModal(e:Event){
      const modalContainer = document.getElementById('modalContainer');
      if (e.target === modalContainer) {
        (modalContainer as any).style.display = 'none';
      }
    };
    ngOnDestroy(): void {
      const otplessId = document.getElementById('otplessScriptId')
      if (otplessId) {
        document.body.removeChild(otplessId);
      }
    }
  }
}

  



```




### Usage

> **Prequisite** [NodeJS](https://nodejs.org/en)

- Install Packages

    ```bash
    npm install
    ```

- Add `cid` to the script by replacing [YOUR_CID_HERE](./src/app.component.ts#L14) with your cid from [OTPless docs](https://otpless.com/platforms/angular#angular_STEP_1)

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
