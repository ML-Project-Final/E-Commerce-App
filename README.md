# E-Commerce-App
## Introductory
In our ongoing project, we are diligently crafting a recommendation system designed to enhance user experience and boost the likelihood of successful product purchases.
Our primary objective is to optimize the presentation of personalized recommendations of products on our designated website, ensuring that users not only receive valuable suggestions but also find themselves more inclined to make informed and satisfying purchase decisions.
Through meticulous development, we aim to increase user engagement, providing individuals with ample opportunities to discover products tailored to their preferences, ultimately fostering a more enjoyable and fruitful shopping journey.
In pursuit of this goal, we leverage historical data from registered users to train our recommendation model, enhancing its accuracy and effectiveness. The system is designed to actively collect user data, continually refining and improving recommendations to maximize efficiency.
While ensuring essential functionality in the user interface, our primary focus lies in the intricate development of the recommendation engine, prioritizing its capacity to provide users with highly personalized and efficient suggestions.
By seamlessly integrating user preferences and behaviors, we aim to create an engaging and satisfying shopping experience, empowering users to discover and make informed choices effortlessly.

## Methodology
Our recommendation system consists of two models, each of them was created using different algorithms which are Item-Based Collaborative Filtering (IBCF) and Matrix Factorization (MF). Both of these models are similar in which they are used to predict the missing ratings of non-purchased products for each user. Once all missing ratings have been predicted, we select the top n non-purchased products with highest predicted ratings as recommendations.

### Item-Based Collaborative Filtering (IBCF):
Collaborative filtering is a technique in which the recommendation is generated based on the preferences of similar users. There are mainly two methods of collaborative filtering which are User-Based and Item-Based.

In this project, we selected the Item-Based method due to lesser impact of the cold start problem when comparing to the User-Based method
In order to create the model, we constructed an item-to-item similarity matrix based on the User-Rating sparse matrix.

Once the similarity matrix has been constructed, for each user-product pair, we can predict the missing rating using the sum of other products' ratings weighted by their similarities to the current product.

### Matrix Factorization (MF):
Matrix factorization is also one of a class of collaborative filtering in which the User-Rating sparse matrix is decomposed into two smaller matrices where the smaller matrices can be linked using the latent features.

The latent features k are used to represent the association between users preferences and products characteristics. These features are determined to find similarity and make a prediction based on both item and user entities.
In order to find the most optimal P and Q matrices, their values are first randomized, then we can minimize the loss of PQ using metrics such RMSE through an iterative approach such as gradient descent.

### Ensemble Voting (EN):
The ensemble voting simply aggregates the predicted ratings from both models using the predefined model weights. Models with higher corresponding weight will have a higher impact on the final predictions than the others.

## Application
Our application is built using React for frontend framework (web UI components), Django and Flask for backend (Django for interactions with our databases and Flask for ML services).
The followings are steps that each user performs once they entered our website:
1. User enters our website and lands on the authentication page. A user can choose to sign in if they already have an account or register if they do not.
2. If a user chooses to register, the system asks for their username and password. Once submitting, the system asks the user to give ratings to the randomly selected products from the database.
3. Once a user submits their ratings, Our system will immediately store their ratings in our database and the prediction for the user’s missing ratings will be initiated.
4. After a user has finished signing in or registering, they are greeted with the product exploration page. In this page, a search bar, recommended products, as well as products sorted by popularity are displayed. A user can choose to click on the product that they are interested in or search for specific products using the search bar.
5. Once a user clicks on a specific product, the product page will be shown which contains detailed information about the product as well as the “add to cart” button. If a user chooses to add a product to their cart, they can proceed to check out and give a rating to the product they purchased. Rating given by the user will be used to retrain our recommendation model for more accurate and personalized future recommendations.
