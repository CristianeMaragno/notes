React embraces the fact that rendering logic is inherently coupled with other UI logic. Instead of artificially separating _technologies_ by putting markup and logic in separate files, React [separates _concerns_](https://en.wikipedia.org/wiki/Separation_of_concerns) with loosely coupled units called “components” that contain both.

Unlike browser DOM elements, React elements are plain objects, and are cheap to create. React DOM takes care of updating the DOM to match the React elements.
One might confuse elements with a more widely known concept of “components”, but elements are what components are “made of”.

**Environment**
- Node
- Npm or equivalent package manager
- Has automatic refresh

**Create application**
npx create-react-app .
Execute: npm run
Build file to be used in deploy, created a dist folder: npm build

**Structure**
- The src folder contains everything used in your application

Small example
```
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<h1>Hello, world!</h1>);
```

**Concepts**
JSX: syntax extension to describe what the UI should look like. 
- ```const element = <h1>Hello, world! {message}</h1>;```. 
- React doesn’t require using JSX, but most people find it helpful
- You can put js inside the curly braces and use parenthesis to avoid automatic semicolon insertion when indenting
- JSX prevents injection attacks bacause everything is converted to a string before being rendered(DOM escaping)
- Babel compiles JSX down to React.createElement() calls
- You have to be careful about the meaning of this in JSX callbacks. In JavaScript, class methods are not bound by default. If you forget to bind this.handleClick and pass it to onClick, this will be undefined when the function is actually called.

Components: Let you split the UI into independent, reusable pieces.
- Components are like JavaScript functions. They accept arbitrary inputs (called “props”) and return React elements 
- Always start component names with a capital letter. React treats components starting with lowercase letters as DOM tags. For example, <div /> represents an HTML div tag, but <Welcome /> represents a component and requires Welcome to be in scope.
- Props are Read-Only
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
const element = <Welcome name="Sara" />;
root.render(element);
```

Composition: Give you all the flexibility you need to customize a component’s look and behavior in an explicit and safe way, used instead of inheritance.
- For especialization of behaviour
```
function Dialog(props) {
  return (
    <FancyBorder color="blue">
		  <h1 className="Dialog-title">
			{props.title}
		  </h1>
		  <p className="Dialog-message">
			{props.message}
		  </p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog title="Welcome" message="Thank you for visiting our spacecraft!" />
  );
}
```
- Some components don’t know their children ahead of time
```
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}

function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```
- Using props passing components
```
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />      }
      right={
        <Chat />      } />
  );
}
```

Conditional rendering: You can create a stateful component that uses logical operators to create the elements or use embed expressions in JSX.
```
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;

    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById('root')); 
root.render(<LoginControl />);
```

```
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}
```
Obs: returning a falsy expression will still cause the element after && to be skipped but will return the falsy expression. In the example below, ```<div> 0</div>```will be returned by the render method.

Forms: In HTML, form elements such as```<input>, <textarea>, and <select>``` typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, and only updated with setState().
```
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```

Handling events
- Pass parameters, like in a loop
```
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

- If you need to pass the this to handler you can
```
onClick={this.handleClick}
onClick={() => this.handleClick()}
```