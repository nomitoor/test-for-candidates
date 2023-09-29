Write a Symfony REST application to calculate the price of a product and process a payment
You need to write two endpoints:

POST: to calculate the price
http://127.0.0.1:80/calculate-price
Example json body of the request:

{
  "product": 1,
  "taxNumber": "DE123456789",
  "couponCode": "D15"
}
POST: to make a purchase
http://127.0.0.1:80/purchase
Example json body of the request:

{
  "product": 1,
  "taxNumber": "IT12345678900",
  "couponCode": "D15",
  "paymentProcessor": "paypal"
}
On successful completion of the request, return an HTTP response with a code of 200.

On invalid input data or payment errors, return an HTTP response with a code of 400 and a json object with errors.

Products
Iphone (100 euros)
Headphones (20 euros)
Case (10 euros)
Coupons
If a coupon is available, the buyer can apply it to the purchase.

A coupon can be of two types:

A fixed amount of discount
A percentage of the purchase amount
Tax calculation
When purchasing a product, the recipient must pay tax on top of the product price, based on the country of the tax number:

Germany - 19%
Italy - 22%
France - 20%
Greece - 24%
As a result, the price for an Iphone buyer from Greece is 124 euros (product price 100 euros + tax 24%).

If the buyer has a coupon for a 6% discount on the purchase, the price will be 116.56 euros (product price 100 euros - 6% discount + tax 24%).

Tax number format
DEXXXXXXXXX - for residents of Germany,

ITXXXXXXXXXXX - for residents of Italy,

GRXXXXXXXXX - for residents of Greece,

FRYYXXXXXXXXX - for residents of France

where:

The first two characters are the country code.
X is any digit from 0 to 9.
Y is any letter.
Please note that the length of the tax number varies for different countries.

Tax number formats may change, but this happens rarely. (This depends on the legislation.)

Details
When completing the task, you need to:

Implement validation of all fields (including the correctness of the tax number according to the format) in the request body, using Symfony validator.
Calculate the final purchase price, including the coupon (if specified) and tax.
Use PaypalPaymentProcessor::pay() or StripePaymentProcessor::processPayment() to process the payment.
These classes are provided in this project. You should use them. In the payment methods, they accept the price in different units (in cents or dollars).

OR copy them to your project. For simplicity, imagine that these two classes are included in two different third-party SDKs, and you do not have the ability to modify these classes or any logic within them.
OR add systemeio/test-for-candidates as a dependency via Composer.
Attach examples of HTTP requests to the two endpoints in README.md: path and request body (for manual testing) in the curl command format.
You do not need to write CRUD for entities.

When writing the test, use git. After completion, send a link to the repository.

It is necessary to consider the possibility of adding new PaymentProcessors.

Extra points
Use of containerization for php, postgres/mysql
Presence of PHPUnit tests
Compliance of the code with SOLID principles (without fanaticism)
Commit-based implementation stage design is welcome
Demonstrated ability to NOT! use approaches like onion-based/DDD/CQS/hexagonal architecture when completing the task: we value its correctness and completeness much more; such complex concepts are likely not relevant in our task
We do not limit you on the deadline for completing the task
