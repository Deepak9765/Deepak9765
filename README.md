Parse.initialize("YOUR-APP-ID", "YOUR-JS-KEY");
  Parse.serverURL = 'https://parseapi.back4app.com/';
  <h4 text-center margin-top>Insert your credentials</h4>

  <ion-item>
    <ion-label stacked>Username</ion-label>
    <ion-input [(ngModel)]="username"></ion-input>
  </ion-item>

  <ion-item>
    <ion-label stacked>Password</ion-label>
    <ion-input type="password" [(ngModel)]="password"></ion-input>
  </ion-item>

  <div text-center margin-top>
    <button ion-button margin-right (click)="signUp()">
      SIGN UP
    </button>

    <button ion-button color="secondary" (click)="signIn()">
      SIGN IN
    </button>
  </div>
   signUp() {
    Parse.User.signUp(this.username, this.password).then((resp) => {
      console.log('Logged in successfully', resp);

      // Clears up the form
      this.username = '';
      this.password = '';

      this.toastCtrl.create({
        message: 'Account created successfully',
        duration: 2000
      }).present();
    }, err => {
      console.log('Error signing in', err);

      this.toastCtrl.create({
        message: err.message,
        duration: 2000
      }).present();
    });
  }
   signIn() {
    Parse.User.logIn(this.username, this.password).then((resp) => {
      console.log('Logged in successfully', resp);

      // If you app has Tabs, set root to TabsPage
      this.navCtrl.setRoot('HomePage')
    }, err => {
      console.log('Error logging in', err);

      this.toastCtrl.create({
        message: err.message,
        duration: 2000
      }).present();
    });
  }
