# vue-swapi-app

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


### Questions
### 1. What is a closure? Where in the code is there a closure?

A closure in programming refers to the combination of a function and the lexical environment in which that function was declared. In JavaScript, inner functions have access to the scope of outer functions, allowing them to “remember” the variables of that outer function even after the outer function has completed its execution.

In my code, there is a closure in the sortData function. This inner function accesses the variable this.sortBy, which belongs to the outer function scope of the methods. Here is the relevant snippet:

```
sortData() {
    this.planets.sort((a, b) => {
      return a[this.sortBy].localeCompare(b[this.sortBy]);
    });
},
```

The comparison function `(a, b) => a[this.sortBy].localeCompare(b[this.sortBy])` forms a closure since it uses the variable this.sortBy from the outer function scope.

### 2. What are the possible side effects of any function? Could you point out any of these cases in your code? Expected? Can they be avoided?

In my code, there are some possible side effects associated with the `fetchData` function. Common side effects of this feature include:

State Modification `(this.planets)`: The function assigns the API response to the variable this.planets, which modifies the state of the component.

Call Another Function `(this.sortData)`: Calls the sortData function, which also modifies the state by sorting the `this.planets` array based on the selected property `(this.sortBy)`.

These side effects are expected in this context because the function is designed to get data and update the state of the application. To manage them:

**Error Handling:** Error handling has been implemented to anticipate and handle potential problems during data collection.

**Transparent communication:** The code is documented and clearly communicates when and why certain side effects occur.

**Separation of Responsibilities:** The fetchData and sortData functions have specific responsibilities, making the code easier to understand and maintain.

**Immutability:** You can consider using immutable programming practices to reduce side effects when working with state. Instead of directly modifying this.planets, we could create a new ordered copy or apply immutability techniques as needed. This can make the code more predictable and easier to reason about in larger environments.
