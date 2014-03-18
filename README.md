simple-state-machine
====================

A generic API for creating and using state machines.

```javascript
var SimpleStateMachine = require('simple-state-machine');

var machine = new SimpleStateMachine();

machine.addTransition('state-1', 'state-2', function(object) {
  // Check if object satisfies rtansition condition
  if (object === "@") {
    return true;
  }
  else {
    return false;
  }
}
, function() {
    console.log('State machine arrived to state \"state-2\".');
});

machine.currentStateNames['state-1'];

machine.push('@');
// will output "State machine arrived to state \"state-2\"."
```

## API

`machine.addTransition(stateFrom, stateTo, transitionCallback[, arrivalCallback])`

Add transition to a state machine.
`stateFrom` - String - name of state transition starts from.
`stateTo` - String - name of state transition goes to.
`transitionCallback` - Function - a function that will be called on attempt to transit, it will be passed one parameter being an object that is pushed to sate machine.
`arrivalCallback` - Function - (optional) a function that will be called when state machine arrives to stateTo on successful transition.

`machine.push(object)`

Push object through state machine. 
`object` - Any Type - this object will be sent to transition callbacks for all transition that go out of current state of a state machine. If transition callback after doing some logic with the objwct ereturn true machine transits to the according state.

`machine.currentStateNames[]`

Array of state names that the machine is currently in. Should be used once to set initial state.
