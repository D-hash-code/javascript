## Authentication Structure from PedroTech

[Github](https://github.com/machadop1407/react-firebase-authentication/blob/main/src/App.js)

Basically you have a register, login and logout function defined on the app level. There are two input forms for each
register and login (corresponding to email and password). There is a button for register, login and logout.

Register and Login have their own react state variables. On change of the input form these states are updated. E.g.

```javascript
<input
    placeholder="Email..."
    onChange={(event) => {
        setRegisterEmail(event.target.value);
    }}
/>
```

And then we call the register/login functions when we hit the corresponding buttons.

```javascript
<button onClick={register}>Create User</button>
```

The login and register functions are similar in design. They call on the firebase provided functions. And differ in the obvious way.

```javascript
  const login = async () => {
    try {
        const user = await signInWithEmailAndPassword(
            auth,
            loginEmail,
            loginPassword
        );
        console.log(user);
    } catch (error) {
        console.log(error.message);
    }
};
```
## User State

We add another react state for the user, which updates using the onAuthStateChange hook provided by firebase.

```javascript
const [user, setUser] = useState({});

onAuthStateChanged(auth, (currentUser) => {
    setUser(currentUser);
})
```
This allows us to pass around the user as needed around the app using the react state variable of user.

Once we set this up we can handle logout 

## logout

The logout function is much simpler. Just uses signOut function from firebase

```javascript
const logout = async () => {
    await signOut(auth);
};
```

