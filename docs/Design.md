#  High level

    Description:Use C/S model to develop an instant online game for go,neglecting loading
    balance and security.

        __________________________________________________________________________________________________________________
       /server:c++                                                                                                        \
       |                _ _ _ _ _ _ _ _ _        _____________           _ _ _ _ _ _ _       _ _ _ _ _ _ _                 |
       |               /**Business Layer**\     /**Msg agent**\         /  **Json**   \     /**Http Layer**\               |
       |   _ _ _       |-------------------|    |-------------|         |--------------|    |--------------|               |
       | /**DB**\      |  Login/Register   |-- >|   generate  |-------->|  Encode      |    |  Accept      |<---+          |
       | |-------|     |-------------------|    |             |         |              |--->|--------------|    |          |
       | |       |--- >|   Room Manager    |    |-------------|         |--------------|    |  Send        |--+ |          |
       | | Mysql |     |-------------------|< --|   dispatch  |<--------|              |    |--------------|  | |          |
       | \ _ _ _ /< ---|    Chat           |    |             |         |  Decode      |<---|  Recv        |<-|-|-+        |
       |               |-------------------|    |             |         \ _ _ _ _ _ _ _/    \_ _ _ _ _ _ _ /  | | |        |
       |               |    SmartGo Pro    |    |             |                                               | | |        |
       |               \ _ _ _ _ _ _ _ _ _ /    \_____________/                                               | | |        |
        \_____________________________________________________________________________________________________|_|_|________/
                                                                                                              | | |
                                                                                                              | | |TCP/IP
                                                                                                              | | |Connection:**Keep_alive**
        ______________________________________________________________________________________________________|_|_|_________
       / client:java                                                                                          | | |        \
       |                                                                                                      | | |        |
       |                 _ _ _ _ _ _ _           _____________           _ _ _ _ _ _     _ _ _ _ _ _ _ _      | | |        |
       |                /  **GUI**    \         /**Msg agent**\         / **Json**  \   /**Http Layer**  \    | | |        | 
       |               |--------------|         |-------------|        |------------|  |-----------------|    | | |        |
       |               |Login/Register|<--------|   dispatch  |<-------| Decode     |  |   Connect       |------+ |        |
       |               |--------------|         |             |        |            |  |-----------------|    |   |        |
       |               | Game Lobby   |         |-------------|        |            |<-| Recv Thread     |<---+   |        |
       |               |--------------|         |             |        |------------|  |-----------------|        |        |
       |               | Chat room    |-------->|   generate  |------->| Encode     |->| Send Thread     |--------+        |
       |   _ _ _ _     |              |         |             |        \ _ _ _ _ _ _/  |-----------------|                 |
       |  /**DB** \ -->| SmartGo Pro  |         |             |                        |   Close         |                 |
       |  |-------|<---|--------------|         |             |                        \  _ _ _ _ _ _ _ _/                 |
       |  |SQLite |    |   Logout     |         \_____________/                                                            |
       |  |_ _ _ _|    \_ _ _ _ _ _ _ /                                                                                    |
       \___________________________________________________________________________________________________________________/
