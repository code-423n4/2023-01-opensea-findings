[G-01] Cheap Contract Deployment Through Clones
01: https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L93-L94
There's a way to save a significant amount of gas on deployment using Clones: https://www.youtube.com/watch?v=3Mw-pMmJ7TA .
ConduitController                                                    vs                             ConduitControllerClone
"method": "createConduit",                                                                                                                             
          "min": 712826,                                                                                       "min": 323304,
          "max": 712970,                                                                                      "max": 367215,
          "avg": 712931,                                                                                       "avg": 319739,
          "calls": 51                                                                                               "call": 51