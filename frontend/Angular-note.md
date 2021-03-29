## To use inline image in Angular
[style.background-image]="'url('+games[4].thumb+'})'"

## Logout
```typescript
export class LoginService {

  // inject Router from angular/router

  loggedIn(){
    return !!sessionStorage.getItem('currentUser')
  }

  logoutUser(){
    sessionStorage.removeItem("currentUser")
    this.router.navigate([""]);
  }

}        

```

```html
<!-- Navebar template -->
<span class="btn text-light" routerLink="/login" *ngIf="!loginService.loggedIn()" >Login</span>

<span class="btn text-light" (click)="logout()" *ngIf="loginService.loggedIn()">Logout</span>

```

```typescript
// Navbar component, inject LoginService
logout(){
    this.loginService.logoutUser()
 }
```
