 Event is missing indexed fields

Index event fields make the field more quickly accessible to off-chain tools that parse events. However, note that each index field costs extra gas during emission, so it’s not necessarily best to index the maximum allowed per event (three fields). Each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of the fields should be indexed.


https://github.com/ProjectOpenSea/seaport/blob/171f2cd7faf13b2bf0455851499f1981274977f7/contracts/interfaces/ConduitControllerInterface.sol#L29
https://github.com/ProjectOpenSea/seaport/blob/171f2cd7faf13b2bf0455851499f1981274977f7/contracts/interfaces/ConsiderationEventsAndErrors.sol#L31 (indexing the parameter recipient )
https://github.com/ProjectOpenSea/seaport/blob/171f2cd7faf13b2bf0455851499f1981274977f7/contracts/interfaces/ConduitInterface.sol#L47