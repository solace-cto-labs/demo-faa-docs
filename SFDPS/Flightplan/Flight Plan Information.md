### Flight Plan Information

| Field | Value |
|---|---|
| **Message Name** | Flight Plan Information: FH, FH_FIXM |
| **Message Description** | The Flight Plan Message is sent to transfer active and proposed flight plan data. It is generally sent when an ERAM at an ARTCC first creates a new flight record for a flight. Multiple ARTCCs send copies of the same flight plan. A single ARTCC may have multiple flight plans for one flight, although only one should ever be active. |
| **Message Property Descriptions** | Refer to Table 5-1, below |
| **Permissible Property Values** | Refer to Table 5-1, below |
| **Message ID (if applicable)** | N/A |
| **Filter Criteria** | Refer to Table 5-1, below |
| **Applicable Topic/Queue** | FDPSDATA.IN |
| **Delivery Mode** | Nonpersistent |
| **Message Body Type** | Text |
| **Estimated Frequency** | 26.3/sec (Avg), 61/sec (Peak) |
| **Minimum/Maximum Size of message in Simple XML Format (FH) (bytes)** | 3472/5617 |
| **Minimum/Maximum Size of Message in FIXM Format (FH_FIXM) (bytes)** | 2524/13858 |