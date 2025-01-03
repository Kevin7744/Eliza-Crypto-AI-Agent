# Eliza-Crypto-AI-Agent

## Some Random Notes

- **Actions**
- **Providers**
- **Evaluators**

---

### Pizza Ordering Agent

#### Limitations

- Payments are challenging:
  - **Solution:** Have a portal where the user can enter their payment information.
  - **Alternative (less secure):** Collect payment information through direct messages (DMs).

**Question:** How do we connect the user's private info to the current conversation?

---

#### Example State

- **Cold** ↔ **Warm** ↔ **Hot**

---

#### Order Flow

1. **Agent** - Waiting for someone to order pizza.
2. **User** - "Yo, let me get a small cheese pizza."
3. **Agent** - Checks if it knows the user:
   - **If the agent knows the user:**
     - Checks if the user has a payment method on file:
       - **If payment method exists:**
         - Agent places the order.
       - **If no payment method exists:**
         - Agent asks the user for their payment method.
         - **If the user provides a payment method:**
           - Agent places the order.
           - Agent sends a confirmation message to the user.
         - **If the user does not provide a payment method:**
           - Agent asks the user again.
   - **If the agent does not know the user:**
     - The agent asks the user for their name.
     - The agent asks for a payment method.
     - The agent places the order.
     - The agent sends a confirmation message to the user.

![Diagram](https://github.com/user-attachments/assets/08b4ed04-73d3-417f-9c3d-121d04f57eea)

---

#### Caveat

- **We can't ask for private information in a public chat, so a private chat is required.**
  - **In DMs:** Collect important private information directly.
  - **In Public Messages:** Notify the user to DM the agent, but start the order process.

---

#### State Handling

We are not using finite states like `Waiting`, `CHECK_USER`, `GET_USER_NAME`, `GET_NEW_PAYMENT`, `PLACE_ORDER`, `SEND_CONFIRMATION`. Instead, we are implementing a **state object** with the following transitions:

- **State Transitions:**
  - **CHECK_USER:** `KnownUser` ↔ `UnknownUser`
  - **CHECK_PAYMENT:** `PaymentOnFile` ↔ `NoPaymentFile`
  - **CHECK_ADDRESS:** `AddressOnFile` ↔ `NoAddressFile`
  - **CURRENT_ORDER:** `Order`
  - **CONFIRMED:** `Confirmed` ↔ `NotConfirmed`

- **End State Transition Conditions:**
  - `KnownUser`, `PaymentOnFile`, `AddressOnFile`, `Confirmed`

- **If `currentState == END_STATE`:**
  - Place the order and check if it's confirmed on Domino's.
  - **If not confirmed:** Throw an error and prompt the user to update their state.
  - **If confirmed:** Send a confirmation message and clear the state.

- **State Caching:**  
  Cache the state per user using the cache key:  
  `user's_twitter_handle + pizza_order`

---

#### Steps to Implement Pizza Ordering

1. **Create a New Plugin**
     rename a plugin, files > packege.json
     delete files on src
     
3. **Create a New Provider** for Pizza State
4. **Define Actions:**
   - Start Order Action
   - Continue Order Action
   - End Order Action

---

#### Types

- **Pizza Order**
- **Pizza Order Step**
