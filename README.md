# **Key Components of the JavaScript Code**

---

## **1. `script src="operations.js"`**

**What this does:**  
This script includes the glue code generated by Emscripten, responsible for loading and managing the WebAssembly module (`operations.wasm`). It defines a `Module` object that handles interaction between the WebAssembly code and the JavaScript environment. Specifically, the `operations.js` file:
- Loads the `.wasm` file into the browser.
- Defines how the WebAssembly functions (exported from C++) can be called from JavaScript.

**Note:** Without this file, your WebAssembly functions (e.g., `add`, `subtract`) won't be available in the JavaScript environment.

---

## **2. `Module.onRuntimeInitialized`**

**What this does:**  
`Module.onRuntimeInitialized` is an event handler called once the WebAssembly module is fully loaded and ready to use. The WebAssembly runtime requires time to load the `.wasm` file, ensuring functions like `add`, `subtract`, `multiply`, and `divide` are initialized only when the WebAssembly environment is fully ready.

**The `Module.cwrap()` function:**  
`Module.cwrap` is an Emscripten-provided function that wraps WebAssembly (C/C++) functions to make them callable from JavaScript.

- **Parameters:**
  - The first parameter (`'add'`) is the name of the WebAssembly function to wrap.
  - The second parameter (`'number'`) is the return type of the function.
  - The third parameter (`['number', 'number']`) is an array of argument types for the function.

**Result:** This allows calling the WebAssembly function `add` (written in C++) from JavaScript as if it were a normal JavaScript function. The same logic applies to `subtract`, `multiply`, and `divide`.

**Why is this necessary?**  
WebAssembly functions are not natively callable from JavaScript. `cwrap()` wraps these functions, enabling JavaScript to communicate with them. These wrapped functions are stored in variables, making them accessible throughout the script.

---

## **3. The `performCalculation` Function**

**What this does:**  
- Handles the calculation based on user input.
- Retrieves values entered by the user (`num1` and `num2`) and the chosen operation (addition, subtraction, etc.).
- Calls the corresponding WebAssembly function (`add`, `subtract`, `multiply`, or `divide`) with the user input.
- Displays the result in an alert box.

**How WebAssembly functions are used:**
- Triggered when the user clicks the "Calculate" button.
- If "add" is selected, the `add` function (wrapped via `cwrap()` from the WebAssembly module) is called with the input numbers, and the result is displayed in an alert box.

**Why WebAssembly?:** The actual arithmetic operations are done by the C++ code compiled to WebAssembly, which can be faster and more efficient for larger or more complex operations.

---

## **Summary of Key JavaScript-WASM Interactions**

- **Loading WebAssembly:** The `operations.js` file loads the WebAssembly module and provides the necessary glue code to interact with the WebAssembly functions from JavaScript.
- **`Module` Object:** Created by Emscripten, it provides access to the WebAssembly runtime and functions.
- **`cwrap()`:** Wraps WebAssembly (C++) functions so they can be called like normal JavaScript functions. In this example, `add`, `subtract`, `multiply`, and `divide` are WebAssembly functions wrapped with `cwrap()`.
- **`onRuntimeInitialized`:** Ensures that the WebAssembly module is fully loaded and ready before calling any functions.

---

## **Conclusion**

The `operations.js` and `operations.wasm` files generated by Emscripten are crucial as they load the WebAssembly module and allow JavaScript to invoke the WebAssembly functions. JavaScript wraps these functions using `cwrap` and handles user input, but the actual calculations are performed in WebAssembly, compiled from C++.

**Note:** While this approach might seem excessive for simple arithmetic, it is highly effective for performance-critical or complex operations that benefit from WebAssembly's speed and efficiency.

---

## **EXTRAS:**

- Extension for interacting with markdown files:  `Markdown All in One`
- Link for learning markdown:  `https://www.markdowntutorial.com/`
- Link for learning Emscripten:  `https://emscripten.org/docs/getting_started`
- Starting the Web app: Type the command `emrun --no_browser --port 8080 .`
- Dont forget the `Full Stop (.)` at the end of the command to run the web app

---

## Happy Coding!
