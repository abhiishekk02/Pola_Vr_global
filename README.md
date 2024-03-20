<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Product Details</title>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC"
      crossorigin="anonymous"
    />
  </head>
  <body>
    <div class="container itemDetails">
      <div class="row mt-4">
        <div class="col-md-6">
          <div class="product-image mt-4">
            <img id="productImage" src="" alt="Product Image" />
          </div>
        </div>
        <div class="col-md-6">
          <div class="product-details mt-4">
            <h1 id="productName"></h1>
            <p id="productPrice"></p>
            <p id="productRating"></p>
          </div>
        </div>
        <div class="btn1"></div>
      </div>
    </div>

    <!-- Include any JavaScript files needed for functionality -->
    <script>
      const addToCart = async (id) => {
        try {
          const addCartValue = await fetch(
            `http://localhost:8080/data/addToCart/${id}`,
            {
              method: "PUT",
              ContentType: "application/json",
            }
          );
          if (addCartValue.ok) {
            const addCartButton = document.getElementById(`btn_${id}`);
            addCartButton.classList.add("btn-danger");
            addCartButton.innerHTML = "Remove from cart";
            addCartButton.onclick = () => removeFromCart(id);
          }
        } catch (error) {
          console.log(error);
        }
      };

      const removeFromCart = async (id) => {
        try {
          const removeCartValue = await fetch(
            `http://localhost:8080/data/removeFromCart/${id}`,
            {
              method: "PUT",
              ContentType: "application/json",
            }
          );
          if (removeCartValue.ok) {
            const removeCartButton = document.getElementById(`btn_${id}`);
            removeCartButton.classList.remove("btn-danger");
            removeCartButton.classList.add("btn-primary");

            removeCartButton.innerHTML = "Add to cart";
            removeCartButton.onclick = () => addToCart(id);
          }
        } catch (error) {
          console.log(error);
        }
      };
      const updateProductDetails = async () => {
        try {
          const urlParams = new URLSearchParams(window.location.search);
          const productId = urlParams.get("id");

          const response = await fetch(
            `http://localhost:8080/data/getProductByID/${productId}`
          );

          if (response.ok) {
            const data = await response.json();
            console.log(data);
            console.log(data[0]);

            document.getElementById("productName").innerText = data[0].name;
            document.getElementById("productImage").src = data[0].imageLink;
            document.getElementById(
              "productPrice"
            ).innerText = `Price: $${data[0].price}`;
            document.getElementById(
              "productRating"
            ).innerText = `Rating ${data[0].rating}`;

            const btn1 = document.getElementsByClassName("btn1")[0];
            btn1.innerHTML = `
        <div class="col-md-6 h-100 mt-2 product-btn">
          ${
            data[0].cart
              ? `<button
                  id="btn_${data[0].id}"
                  onClick="removeFromCart(${data[0].id})"
                  class="btn btn-danger"
                >
                  Remove from cart
                </button>`
              : `<button
                  id="btn${data[0].id}"
                  onClick="addToCart(${data[0].id})"
                  class="btn btn-primary"
                >
                  Add to cart
                </button>`
          }
        </div>`;
          } else {
            console.error("Failed to fetch product details");
          }
        } catch (error) {
          console.error("Failed to update product details", error);
        }
      };

      updateProductDetails();
    </script>
  </body>
</html>




# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
