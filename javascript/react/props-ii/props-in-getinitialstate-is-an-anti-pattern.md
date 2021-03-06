---
author: tommarshall

levels:

  - basic

  - advanced

  - medium

type: normal

category: tip


links:

  - '[facebook.github.io](https://facebook.github.io/react/tips/props-in-getInitialState-as-anti-pattern.html){website}'

parent: custom-proptype-s-to-be-required

---

# Props in getInitialState is an Anti-Pattern

---
## Content

Passing down props from the parent to generate state in `getInitialState` can lead to duplication of *source of truth*, where the real data is located.

An example of a duplication of source of truth:
```javascript
var Duplication = React.createClass({
  getInitialState: function() {
    return {
      nameWithQualifier: 'Country ' +
        this.props.country
    };
  }
  render: function() {
    return <div>
      {this.state.nameWithQualifier}
    </div>;
  }
});
```
This is bad due to `getInitialState` being invoked when the component is first created, therefore the example allows a value to get out of sync.

Computing values on-the-fly ensures that values don't get out of sync later and cause maintenance issues.

```javascript
var OnTheFly = React.createClass({
  render: function() {
    return <div>{
      'Country: ' + this.props.country
    }</div>;
  }
});

ReactDOM.render(
  <OnTheFly country="England" />,
  document.getElementByID('foo')
);


```

