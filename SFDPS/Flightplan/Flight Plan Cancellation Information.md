### Flight Plan Cancellation Information: 

| Field | Value |
|---|---|
| **Message Name** | Cancellation Information: CL, CL_FIXM |
| **Message Description** | The Cancellation Message is sent when a flight plan record is canceled within a particular ARTCC's ERAM. This means that no more data is sent from that center for that flight plan. |
| **Message Property Descriptions** | Refer to Table 5-1, below |
| **Permissible Property Values** | Refer to Table 5-1, below |
| **Message ID (if applicable)** | NA |
| **Filter Criteria** | Refer to Table 5-1, below |
| **Applicable Topic/Queue** | FDPSDATA.IN |
| **Delivery Mode** | Nonpersistent |
| **Message Body Type** | Text |
| **Estimated Frequency** | .9/sec (Avg), 27/sec (Peak) |
| **Minimum/Maximum Size of Message in Simple XML format (CL) (bytes)** | 2488/2716 |
| **Minimum/Maximum Size of Message in FIXM Format (CL_FIXM) (bytes)** | 1140/2103 |