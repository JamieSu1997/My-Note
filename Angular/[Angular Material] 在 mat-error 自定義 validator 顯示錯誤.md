## [Angular Material] - 在 mat-error 自定義 validator 顯示錯誤

#### 問題:

使用了 validator(自定義的驗證器) ，檢查表單中兩個欄位的輸入值是否相等，validator 在一般的表單上會正確的顯示錯誤，但使用在 `mat-form-field` 中 `mat-error` 卻無法正確顯示錯誤。

![123](C:\Users\jamiesu\Documents\我的文件\Notes\123.png)

#### 原因 :  

在 `mat-form-flied` 內的 `mat-error` 只會出現在 **FormControl** 判斷為 " **無效** " 的狀態。

所以當  validator (自定義的驗證器) 沒有通過，但  **FormControl**  的狀態並不是 " **無效** "，就會造成驗證沒過應該要顯示的  `mat-error` 顯示不出來。



#### 解決方法:

使用 Angular Material 提供 `errorStateMatcher` directive，自定義  `mat-input` 的 **FormControl** 有效與無效狀態。  

---------------------

#### 補充:

遇到這個問題的時候，百思不得其解，明明 validator 的驗證邏輯沒有錯，`*ngIF` 大小寫也沒寫錯 ( 笑，怎麼用了 `mat-error` 就是無法正確顯示，在查了很久看了很多篇文章後，發現 Angular material 官網有以下這樣一段話:

> *The `<mat-form-field>` allows you to [associate error messages](https://material.angular.io/components/form-field/overview#error-messages) with your `matInput`. By default, these error messages are shown when the control is invalid and either the user has interacted with (touched) the element or the parent form has been submitted.*

什麼意思呢 ?  `<mat-form-field>` 可以讓你連結 `matInput`和錯誤訊息，但是只有在表單控制元件的狀態為無效、使用者為輸入狀態、整個表單已經送出過，這三種狀態下錯誤訊息才會被顯示。

也就是說寫在 `mat-error` 的錯誤訊息無法顯示的原因，有可能是不在這三種狀態下所以沒有顯示，雖然 validator 有回傳錯誤。

經過了幾次嘗試後，發現控制 `confirmPassword`  控制元件 (FromControl) 的狀態一直是"有效"，而 validator 驗證完的錯誤結果是回傳給 `confirmPassword` 的爸爸 `passwordForm` ，`passwordForm` 控制元件 (FromGroup)的狀態是 "無效"，但是顯示錯誤的條件是 **`confirmPassword` 的狀態要是"無效"** ，這就是問題的所在。![未命名](C:\Users\jamiesu\Documents\我的文件\Notes\未命名.png)



#### 參考:

[Display custom validator error with mat-error](https://stackoverflow.com/questions/47884655/display-custom-validator-error-with-mat-error)

[MatError & Cross-Field Validators In Angular Material 7](https://itnext.io/materror-cross-field-validators-in-angular-material-7-97053b2ed0cf)

-------------------------



#### 出現問題: 

[StackBlitz Code](https://stackblitz.com/edit/mat-error-validator-errorp?file=src/app/app.component.html)

* app.component.html

```html
<h2 class="mat-title">Password Validator</h2>
<form class="example-form" [formGroup]='passwordForm' appConfirmPassword>
    
  <mat-form-field>
    <input matInput placeholder="Password" formControlName='password'>
  </mat-form-field>
    
  <mat-form-field>
    <input matInput placeholder="ConfirmPassword" formControlName='confirmPassword'>
    <mat-error *ngIf="passwordForm.errors?.confirmFault">
      Passwords do not match!
    </mat-error>
  </mat-form-field>

</form>
```

* app.component.ts

```typescript
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { confirmPasswordValidator } from './confirm-password.directive';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.css' ]
})
export class AppComponent  {
  passwordForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.initForm();
  }

  initForm() {
    this.passwordForm = this.fb.group({
      password: ['', Validators.required],
      confirmPassword: ['',Validators.required]
    }, {
      validator: confirmPasswordValidator
    })
  }
  get password(){ return this.passwordForm.get('password'); }
  get confirmPassword(){ return this.passwordForm.get('confirmPassword');}
}
```

* confirm-password.directive.ts

```typescript
import { Directive } from '@angular/core';
import { AbstractControl, FormGroup, NG_VALIDATORS, ValidationErrors, Validator, ValidatorFn } from '@angular/forms';

@Directive({
  selector: '[appConfirmPassword]',
  providers: [{ provide: NG_VALIDATORS, useExisting: ConfirmPasswordDirective, multi: true }]
})

export class ConfirmPasswordDirective implements Validator{
  
  validate(control: AbstractControl): ValidationErrors {
    return confirmPasswordValidator(control);
  }
}

export const confirmPasswordValidator: ValidatorFn = (control: FormGroup): ValidationErrors | null => {

  const password = control.get('password');
  const confirmPassword = control.get('confirmPassword');

  return password.dirty && confirmPassword.dirty && password.value !== 		   confirmPassword.value ? {confirmFault: true} : null;
}
```



#### 解決方法:

[StackBlitz Code](https://stackblitz.com/edit/mat-error-validator-error?file=src%2Fapp%2Fapp.component.html)

* ErrorStateMatcher

```typescript
class PasswordErrorStateMatcher implements ErrorStateMatcher {
  isErrorState(control: FormControl | null, form: FormGroupDirective | NgForm | null): boolean {
    return control.touched && form.invalid;
  }
}
```

* app.component.ts 

```typescript
errorMatcher = new PasswordErrorStateMatcher();
```

* 在 `mat-form-field` 的 `input` 中，新增 `errorStateMatcher`。

```html
<mat-form-field>
    <input matInput placeholder="ConfirmPassword" formControlName='confirmPassword'  [errorStateMatcher]='errorMatcher'>
    <mat-error *ngIf="passwordForm.errors?.confirmFault">
      Passwords do not match!
    </mat-error>
  </mat-form-field>
```
