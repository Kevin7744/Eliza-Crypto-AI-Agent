# Eliza-Crypto-AI-Agent.
## Some random notes 
- actions
- providers, 
- evaluators
  
### Pizza ordering agent

Limitations:
- Payments are scary
  sol : have a portal where the user can put their payment
  sol : {way worse} just get the info in dms
-> ? How do connect the user's private info to the current conversation>

Example state: 
Cold
<->
warm
<->
hot

Order flow
agent - is waiting fpr someone to order pizza
user - "yo lemme get a small cheese pizza"
agent - checks if it knows the user
      - IF the agent know the user
        - the checks if the user has a payment metod file
          - if the user has a payment method file
            - agent places the order
          - if the user does not have a payment method on file
            - agent asks the user for their payment method
            - if the user provides a payment method
              - agent places the order
              - agent sends confirmation message to the user
            - if the user does not provide their payment method
              - ask the user again
      - If agent does not know the user
        - The agent asks the user for their name
        - The agent asks for the payment method
        - agent places order
        - agent send confirmation message to user 

![diagram](https://github.com/user-attachments/assets/08b4ed04-73d3-417f-9c3d-121d04f57eea)

Caveat -- We can't ask this on a public cha, so we need a private chat with the user

First, check if we are in dms or public messages -- if we're in DMs, we can get important private info
-- If we're in public messages, we need to tell the user to DM use [but we can start the order]

Were are not gonna do finite states
Waiting, CHECK_USER< GET_USER_NAME, GET_NEW_PAYMENT, PLACE_ORDER, SEND_CONFIRMATION

Were are gonna do a state object with end state transition conditions:
-  CHECK_USER: KnownUser, UnknownUser
-  CHECK_PAYMENT: PaymentOnFIle, NoPaymentFile
-  CHECK_ADDRESS: AddressOnFile, NoAddressFile
-  Current order: Order
-  CONFIRMED": Confirmed, NotConfirmed

END STATE traditions conditions:
KnownUser, PaymentOnFIle, AddressOnFile, Confirmed

IF currentState == END_STATE
  // go order a pizza and checks if its confirmed on dominos
  // if not, throw an error and let user update their state
  // if it is, send a confirmation message
  // clear the state

State should be cached per user with the cache key being the user's twitter handle + pizza-order

Ordering a pizza
- Create a new plugin
- Create a new provider for pizza state
- Create a start order action
- Create a continue order action
- Create an end order action

Types
- Pizza order
- Pizza order step

