**seaport/contracts/lib/ConsiderationDecoder.sol**
- L5/10 - Two structs are imported that are never used, these imports should be deleted.


**seaport/contracts/lib/ConsiderationEncoder.sol**
- L9/10/11/12/14 - Multiple structs are imported that are never used, these imports should be removed.


**seaport/contracts/lib/BasicOrderFulfiller.sol**
- L4 - ConduitInterface is imported but never used, so it should be removed.


**seaport/contracts/lib/OrderValidator.sol**
- L15/16 - Two structs are imported that are never used, these imports should be deleted.

- L26/31 - Se importa ContractOffererInterface y el helper getFreeMemoryPointer pero nunca son utilizados, por lo tanto deberian ser eliminados.


**seaport/contracts/lib/CriteriaResolution.sol**
- L8 - ConsiderationItem is imported but never used, so it should be removed.


**seaport/contracts/interfaces/ConsiderationEventsAndErrors.sol**
**seaport/contracts/interfaces/TransferHelperErrors.sol**
**seaport/contracts/interfaces/TokenTransferrerErrors.sol**
**seaport/contracts/interfaces/CriteriaResolutionErrors.sol**
**seaport/contracts/interfaces/FulfillmentApplicationErrors.sol**
**seaport/contracts/interfaces/SignatureVerificationErrors.sol**
**seaport/contracts/interfaces/ZoneInteractionErrors.sol**
**seaport/contracts/interfaces/AmountDerivationErrors.sol**
**seaport/contracts/interfaces/ReentrancyErrors.sol**
- There are several contracts that are interfaces, but they have a name without the word Interface or the I in front of the name, this is a convention and is beneficial for the understanding of contracts.


**seaport/contracts/conduit/lib/ConduitConstants.sol**
- L5/8/9/10/16/17/18 - Multiple constants were created, but they are not all capitalized, but a mixture of camemel case with underscore case is used, this
does not meet the standards when programming, a correct name for a constant could be: CHANNEL_CLOSED_ERROR_PTR

