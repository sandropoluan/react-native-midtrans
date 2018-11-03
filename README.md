# Usage
Lets require `react-native-midtrans` module

```
import PaymentMidtrans from 'react-native-midtrans'
```

Checkout Payment
```
PaymentMidtrans.checkOut(
	optionConect,
	transRequest,
	itemDetails,
	creditCardOptions,
  userDetail,
  optionColorTheme,
  optionFont,
	callback(res)
);
```


**Props of Payment CheckOut**
* 	**optionConect** (Object)
	1. clientKey (String) clientKey from [MAP](https://account.midtrans.com) (Merchant Admin 	Portal)
	2. urlMerchan (String) url Backend

	```
	Example:
	const optionConect = {
			clientKey: "VT-CLIENT-AAAAAAAAAAAAA",
			urlMerchant : "http://example.com/payment"
	}
	```

	*Note: in merchant Server (backend) must be have route with name* **charge** *for handle request to Veritrans server with Order Information.*
	*for detail can visit [here](http://mobile-docs.midtrans.com/#merchant-server-implementation)*

* 	**transRequest** (Object)
	1. 	transactionId (String) id of transaction
	2. 	totalAmount (Number) total amount be paied on checkOut

	```
	Example:
	const transRequest = {
			transactionId : "001",
			totalAmount : 6000
	}
	```

* 	**itemDetails** (Arrray), holds infromation about ilist of tem purchased by user transaction *required for Mandiri Bill and BCA KlikPay, Optional for another payment*
	1. id (String) id of item
	2. price (Number) price of item
	3. qty (Number) qty of item
	4. name (String) name of item

```
Example:
var itemDetails = [
              {id:"001", price:1000, qty:4, name:"cimory"},
              {id:"002", price:2000, qty:2, name:"cofimix"}
            ];
```

*Note: Sum of price must be equals with totalAmount in transRequest*

* **creditCardOptions** (Object)
    1. saveCard = save card to Snap (true or false)
    2. saveToken = save card token as 'one click' token (true or false)
    3. paymentMode = mode payment use credit Card ("Normal", "Two Click", "One Click")
    4. secure = using 3D secure (true, false)

```
var creditCardOptions = {
    saveCard:false,
    saveToken:false,
    paymentMode:"Normal",
    secure:false
    };
```

* **userDetail** (Object)
    1. fullName = Full Name member (customer)
    2. email = Email customer
    3. phoneNumber = Phone Number Customer
    4. userId = User Id Customer
    5. address = Address Customer
    6. city = City Customer
    7. country = Country Customer
    8. zipCode = ZipCode Customer

```
var userDetail = {
  fullName:"Ahmad", email:"ah@mad.com", phoneNumber:"0850000000", userId:"U01", address:"kudus", city:"kudus", country:"IDN", zipCode:"59382"
};
```
*Note: value of country use ISO 3166-1 alpha-3, visit [wikipedia](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) to learn about ISO 3166-1 alpha-3

* **optionColorTheme** (Object)
    1. primary = For top panels showing amount
    2. primaryDark = For bordered button, link button
    3. secondary =  For text field.

```
var optionColorTheme = {
  primary:'#c51f1f',
  primaryDark:'#1a4794',
  secondary:'#1fce38'
}
```

* **optionFont** (Object)
    1. defaultText = for default Text
    2. semiBoldText = for semi bold text
    3. boldText =  for bold text

```
var font = {
  defaultText:"open_sans_regular.ttf", semiBoldText:"open_sans_semibold.ttf",
  boldText:"open_sans_bold.ttf"
}
```
*Note: open_sans_regular.ttf, open_sans_semibold.ttf, open_sans_bold.ttf is path of the custom font on the assets directory.

* 	**Callback** (function) to return result of payment transaction;

```
var callback = (res)=>{console.log(res)};
```

# Payment Result

`TransactionResult` is wrapper for UI flow finished transaction object. It contains:

> status : either `canceled`, `pending`, `success`, `failed` or `invalid` based on payment API.

* status *canceled* is value if transaction canceled. for example when selecting payment method users click back
* status: *pending* will be only use on asynchronous transaction like bank transfer or internet banking.
* status *success* / *failed*: For synchronous transaction you can immediately know the status of the transaction.
* status *invalid* : There are unknown error happened.
