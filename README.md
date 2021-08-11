# DafriBank Deposit and Withdrawal API
A library for integrate DafriBank deposit and withdrawal API.

# Deposit API

## Technical Procedure of Deposit
### Request Methods 
All payment requests must be sent using the HTTP POST method and the request data can be in the form of standard HTTP URL encoded parameters, or it can be sent as a POST method.
#### Request Submit Form For Payment Process:
```
<form action ="https://www.dafribank.com/charges" method="post" >
    <input type="hidden" name="order_id" value="10005">
    <input type="hidden" name="order_amount" value="10">
    <input type="hidden" name="currency_code" value="USD">
    <input type="hidden" name="merchant_key" value="XXXXXXXXXX"> // Merchant Key provided by DafriBank support team
    <input type="hidden" name="return_url" value="https://www.dafribank.com/success">
    <input type="submit" name="submit" value="submit">
</form>
```
**Sandbox Request URL:** https://www.sandbox.dafribank.com/charges

**Live Request URL:** https://www.dafribank.com/charges

| Field | Format |
| ------------- | ------------- |
| order_id | Text |
| merchant_key | Varchar |
| order_amount | Decimal |
| return_url | Text (URL format) |
| currency_code | Currency codes (ISO 4217) |

### Description:
**1. order_id -** The merchant side will provide the order Id. The need of the Order_Id is to save the order details for future records. Furthermore, every order Id will be unique for the differentiation and security purpose.

**2. order_amount -** It is the total of the entire order payment.

**3. merchant_key -** A merchant key is a key which is generated from the DafriBank admin panel at the time of approval of payment API integration. Thus, this key is provided by the DafriBank support team.

**4. return_url -** Return URL must be a get method containing the order number and the status of the payment confirmation.

**5. currency_code -** Currency field should have validation of three characters with the valid currency format of Currency codes (ISO 4217).

### Response for Payment Process:
**1. return_url -** The Merchant will provide the base url, and DafriBank will convert this into the transaction_id by decoding the given url. Decoding means converting it through Base 64 Decode and converting it into the link.
For example: Before decoding,10005 is the format of transaction id, and after decoding final URL will look like this - BASE_URL/Decoded_Value

**2. transaction_id -** Every transaction ID will be unique. After the entire process, we will provide a transaction id with the return url.

## Request For Getting Order Details:
All payment requests must be sent using the HTTP POST method and the request data can be in the form of standard HTTP URL encoded parameters, or it can be sent as a POST method.
#### Request Submit Form For Getting Order Details:
```
curl https://www.dafribank.com/api-transaction-detail \
-d transaction_id=2000 \
Method :--- Post
Params: transaction_id
```
**Sandbox Request URL :** https://www.sandbox.dafribank.com/api-transaction-detail

**Live Request URL :** https://www.dafribank.com/api-transaction-detail

| Field | Format |
| ------ | ----- |
| transaction_id | Text |

### Description:
**1. transaction_id -** Every transaction ID will be unique. After the entire process, we will provide a transaction id.
### Response for Getting Order Details:
**Response:** Response will be generated in json format like below :

```
{
"transaction_id": 1010, 
"order_id": 321, 
"status": "Success",
"date_time": "28-07-2021 14:57:18"
}
```

**1. transaction_id -** Every transaction ID will be unique. After the entire process, DafriBank will provide a transaction id to the merchant.

**2. order_id -** order ID will be unique which provided by merchnat end for deposit request.

**3. status -** As depicted by the name, status means it will show the status of the current response. It can be a success or failure as per the transaction response.

**4. date_time -** In this, merchants will get the exact date and time of the completion of the transaction.


# Withdrawal API

## Technical Procedure of Withdrawal
### Request Methods
All payment requests must be sent using the HTTP POST method and the request data can be in the form of standard HTTP URL encoded parameters, or it can be sent as a POST method.
#### Request Submit Form For Payment Process:

```
<form action ="https://www.dafribank.com/merchat-withdrawal" method="post" >
    <input type="hidden" name="merchant_key" value="XXXXXXXXXX"> // Merchant Key provided by DafriBank support team
    <input type="text" name="user_email">
    <input type="text" name="amount">
    <input type="text" name="remark">
    <input type="hidden" name="return_url" value="https://www.dafribank.com/success">
    <input type="submit" name="submit" value="submit">
</form>
```
**Live Request URL :** https://www.dafribank.com/merchat-withdrawal

**Sandbox Request URL :** https://www.sandbox.dafribank.com/merchat-withdrawal

| Field | Format |
| ----  | ------ |
| user_email | Email |
| merchant_key | Varchar |
| amount | Decimal |
| return_url | Text (URL format) |
| remark | Text | 
### Description:
**1. amount -** It is the total of the entire order payment.

**2. merchant_key -** A merchant key is a key which is generated from the DafriBank admin panel at the time of approval of payment API integration. Thus, this key is provided by the DafriBank support team.

**3. return_url -** Return URL must be a get method containing the order number and the status of the payment confirmation.

**4. user_email -** When processing the transaction, the user email should match an email they have registered on the DafriBank portal.

**5. remarks -** Users can also give remarks whatever they want to.

#### Response for Withdrawal:
**return_url -** The Merchant will provide the base url, and DafriBank will convert this into the transaction_id by decoding the given url. Decoding means converting it through Base 64 Decode and converting it into the link.

**1. For example:** Before decoding,10005 is the format of transaction id, and after decoding final URL will look like this - **BASE_URL/Decoded_Value**

**2. transaction_id:** Every transaction ID will be unique. After the entire process, we will provide a transaction id with the return url.

**Note -** Transaction_id will be given to the merchant just for reference to show the message of withdrawal request that has been sent successfully to the merchant. When the user initiates a withdrawal request, the merchant can approve, edit, or decline on the DafriBank portal.
