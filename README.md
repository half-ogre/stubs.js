stubs.js
========
_A stubbing object for JavaScript to make unit testing and TDD less painful._

How to use stubs.js
-----------------------
Let's say you want to unit test the following code: 

    function usernameIsValid() {
      var username = document.getElementById("username").value;
      return /[a-z][a-z0-9-_]{2,16}/i.test(username);
    }

With stubs.js, your unit test might look like:

    test("username validation will fail if the username is empty", function() {
      // arrange
      Stubs.add("document.getElementById", function(id) {
        return { value: "" };
      });

      // act
      var isValid = usernameIsValid();

      // assert
      equals(isValid, false);
    });

You can then remove all stubs, restoring the original values, with `Stubs.removeAll()` (your unit test framework's tear down method might be a good place for this). For further examples of how to use stubs.js, see [its spec](http://github.com/anglicangeek/stubs.js/blob/master/spec/spec.html).
