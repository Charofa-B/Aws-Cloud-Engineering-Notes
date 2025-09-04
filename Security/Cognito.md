# Cognito

* `Authentication`, `authorization`, and `user management` for `web` and `mobile` `applications`
* [Federated identities]() for `sign in` with `social identity providers` (Amazon, Facebook, Google) or with `SAML`
* Enable the creation of `unique identities` and `permissions assignment` for users

## Key Components
### User Pool 
* User directory.
* Stores and manages users and Handles
    * **Authentication** → sign-up, sign-in, MFA.
    * **Password policies** → `resets`, `complexity rules`.
    * **Account recovery** → `forgot` password, account `confirmation`.
    * **User attributes** → standard `(name, email, phone)` + custom `attributes`.
    * **Token issuance** → after successful login, it `issues JWT tokens`
* Users can `sign into a web or mobile application` `through` `Cognito`. 
* Users Can `also federate through a third-party IdP`. 
* All `members of the user pool have a directory profile` that can be accessed through an SDK.

### Identity Pools 
* Enable the `creation of unique identities and permissions` assignment for `users`. 
* Provides `temporary AWS credentials (via STS)` to users so they can access AWS `services directly`
* Identity pools can `communicate with Amazon Cognito` user pools `social sign-in with Facebook, Google, and Login with Amazon and OIDC providers`.
* Identity pools use `STS behind the scenes`.

## Auth Across Phone And Web Apps
1. Successful `user pool sign-in`, web or mobile app will `receive user pool tokens from Cognito`.
2. Use `tokens` to control `access to server-side resources`. 
    * You can also `create user pool groups` to `manage permissions` and to represent `different types of users`.

## Cognito User Pools Features
* **Sign-up**
    * Let users enter their `information` in your `app` and create a `user profile that’s native to your user pool`. 
    * `Redirect users to a third-party IdP` that they can `authorize to pass their information` to `Cognito`. 
    * Create `users based on a data source` or `schema`.
* **Sign-in**
    * Use as a `standalone` `user directory` and `IdP` to your `app`.
* **Federate third-party identities**
    * `Manage` the `overhead of handling the tokens` returned from `social sign-in and from OIDC and SAML IdPs`.
* **Hosted UI for sign-up and sign-in**	
    * `Hosts` web `pages` for sign-up, sign-in, multi-factor authentication (MFA), and password reset.
* **Support for JWTs**	
    * Use [JWT]() tokens to access server-side resources or exchange them for temporary AWS credentials to access other AWS services.