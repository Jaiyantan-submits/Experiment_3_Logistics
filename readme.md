# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:

1. #### Deploy the Contract

    ```
    Deploy LuxurySupplyChain()
    ```

    - Deploy the LuxurySupplyChain contract to 
    create a system for tracking luxury products.
   
   - Initialize an empty mapping to store product details (productId, name, currentOwner, and verified status).

2. #### Register Products

    ```
    registerProduct(productId, name) if product not already registered
    ```

   -  Allow authorized entities (e.g., manufacturers) to register a new luxury product by providing a unique productId and product name.

   - Set the registrant as the initial owner and mark the product as verified.


3. #### Transfer Ownership

    ```
    transferOwnership(productId, newOwner) if caller == currentOwner
    ```

    - Enable the current owner of a product to transfer ownership to a new owner by specifying the productId and newOwner address.
   
   - Update the currentOwner field to reflect the new owner and emit an event to log the transfer.


4. #### Verify Product Details

    ```
    verifyProduct(productId) returns (name, currentOwner, verified)
    ```

    - Allow anyone to verify the details of a product by querying its productId.
    
    - Return the product's name, currentOwner, and verified status for transparency and authenticity checks.

5. #### Handle Edge Cases
    
    ```
    revert() if invalid conditions are met
    ````

   -  Prevent invalid actions, such as registering a product with a duplicate productId or transferring ownership without being the current owner.
   
   - Revert transactions with descriptive error messages to ensure proper contract behavior.

6. #### Emit Events for Transparency

    ```
    emit events for product registration and ownership transfers
    ```

    - Emit ProductRegistered when a new product is registered, logging the productId and name.
   
   - Emit OwnershipTransferred when ownership is transferred, logging the productId and newOwner.

# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LuxurySupplyChain {
    struct Product {
        string name;
        address currentOwner;
        bool verified;
    }

    mapping(uint256 => Product) public products;

    event ProductRegistered(uint256 productId, string name);
    event OwnershipTransferred(uint256 productId, address newOwner);

    function registerProduct(uint256 productId, string memory name) public {
        require(products[productId].currentOwner == address(0), "Product already registered");
        products[productId] = Product(name, msg.sender, true);
        emit ProductRegistered(productId, name);
    }

    function transferOwnership(uint256 productId, address newOwner) public {
        require(products[productId].currentOwner == msg.sender, "Not the owner");
        products[productId].currentOwner = newOwner;
        emit OwnershipTransferred(productId, newOwner);
    }

    function verifyProduct(uint256 productId) public view returns (string memory, address, bool) {
        Product memory p = products[productId];
        return (p.name, p.currentOwner, p.verified);
    }
}
```
# Expected Output:
1. The `LuxurySupplyChain` contract was successfully deployed with transaction hash `0x7f892c54ea804bc581c163057f77326c4e73c644c5a882ed5b036a93f7a7f862`.  

2. It resides at contract address `0xd2a5bC10698FD955D1Fe6cb468a17809A08fd005` and was included in block #13.

3. The deployment consumed 791,705 gas, with no errors during execution.

4. The contract is now live and ready for registering products, transferring ownership, and verification.


# Output:

![image](https://github.com/user-attachments/assets/3794ba00-94f4-409d-8490-87c6d2ca58de)

![image](https://github.com/user-attachments/assets/e1229a2a-db1e-4bdb-a16a-a18106fe3807)

![image](https://github.com/user-attachments/assets/5d3c9798-c34a-4821-812d-d7403b820b9e)

![image](https://github.com/user-attachments/assets/9e8172d4-9036-4434-bb1e-b4d17dcbb296)


# High-Level Overview:
Helps prevent counterfeit luxury goods.


Teaches real-world supply chain use cases.

# RESULT : 
The expected output is achieved.
