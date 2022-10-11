---
title: Mocha-chai-testing-setup
date: 02/10/2022
tags: mocha unit-testing chai jest javascript quality-assurance
---

# **Mocha-chai-testing-setup** 202210021920 
> **49283e**

A simple setup for unit testing javascript[1].

- Anatomy of unit testing:
  ```javascript
  describe("pow", function() {

  it("2 raised to power 3 is 8", function() {
    assert.equal(pow(2, 3), 8);
  });

  it("3 raised to power 4 is 81", function() {
    assert.equal(pow(3, 4), 81);
  });
  });
  ```
- Testing more cases with loops
  ```javascript
    describe("pow", function() {

  function makeTest(x) {
    let expected = x * x * x;
    it(`${x} in the power 3 is ${expected}`, function() {
      assert.equal(pow(x, 3), expected);
    });
  }

  for (let x = 1; x <= 5; x++) {
    makeTest(x);
  }
  });
  ```


[1]: <index-test.html>


