**U.S. Department of Transportation Federal Aviation Administration**

# **Java Messaging Service Description Document System Wide Information Management (SWIM) Flight Data Publication Service (SFDPS)**

**_Prepared for:_ Federal Aviation Administration System Wide Information Management Program Office - Enterprise Programs 800 Independence Avenue, SW Washington, DC 20591**

**_Prepared by:_ Volpe NationalTransportation Systems Center Air Traffic Management Systems Division 55 Broadway Cambridge, MA 02142**

NAS-JMSDD-4309-001 Rev C July 10, 2018

### **Java Messaging Service Description Document SWIM Flight Data Publication Service**

#### **Approval Signatures**

|**Name**|**Organization**|**Signature**|**Date Signed**|
|---|---|---|---|
|Melissa Matthews|AJM-316|MELISSA ANN MATTHEWS<br>Digitally signed by MELISSA ANN<br>MATTHEWS<br>Date: 2018.07.17 12:34:20 -04'00'|July 17, 2018|

ii

NAS-JMSDD-4309-001 Rev C July 10, 2018

### **Java Messaging Service Description Document SWIM Flight Data Publication Service**

#### **Revision Record**

|**Revision**<br>**Letter**|**Description**|**Revision**<br>**Date**|**Entered**<br>**by**|
|---|---|---|---|
|1.0|Initial draft|July 10, 2014|Volpe Center|
|1.1|Initial version with edits|August 8, 2014|Volpe Center|
|1.2|Added new message types<br>Modified security section 4.1.<br>Added AIXM schema for<br>airspace messages.<br>Minor edits.|November 12, 2014|Volpe Center|
|2.0|Updated version numbers of<br>FIXM, SimpleXML, and of SFDPS<br>software. Changed version<br>number of document to 2.0.<br>Completed sections for<br>reconstitution messages.|February 13, 2015|Volpe Center|
|2.1|Included a paragraph<br>describing how SFDPS obtains<br>and uses data files to<br>determine whether a flight is<br>military/sensitive.|March 24, 2015|Volpe Center|
|2.2|Filled In Service Category<br>Information; Added<br>information on<br>FDPS_sourceSystem property|June 19, 2015|Volpe<br>Center/Noblis/Engility|
|2.3|Minor edits (added ‘potential’,<br>removed ‘binary encoded’<br>data, updated references)|July 01, 2015|Noblis/Engility|
|2.4|Updated frequency<br>information|October 7, 2015|Noblis/Engility|

iii

NAS-JMSDD-4309-001 Rev C July 10, 2018

|2.5|Added “coordFix_06a” to the|January 29, 2016<br>Volpe Center|
|---|---|---|
||data elements table of the HP<br>message. Deleted<br>“externalBeaconCode_04b”,<br>“coordFix_06a”,<br>“coordStatusTime_07d”,<br>“coordStatus_07d1”,<br>“coordTime_07d2” and<br>“delayTime_07e” from data<br>elements table of the NP<br>message.<br>Updated message frequency<br>estimates based on data<br>received on August 10<sup>th</sup>2015.<br>Updated message frequency<br>estimates based on data<br>received on August 10<sup>th</sup>2015.<br>Added tables for FIXM<br>formatted messages.<br>Added description of<br>BATCH_TH and<br>BATCH_TH_FIXM messages.||
|B|Formatting Changes<br>Modified ERFDP table in 5.5 to<br>remove TH.|April 07, 2016<br>Noblis/Engility|
||Updated Section 4.1.1 with<br>current POC.<br>Replaced eramGufi_316aFPId<br>and eramGufi_316aDT with<br>eramGufi_316a where<br>appropriate.<br>Added FDPS_OneMinFreq to<br>Flight Data Properties (Table 5-<br>1).<br>Added missing fields in 5.5.1.13<br>Marked currentBeaconCode as<br>required (Section 5.5.1.64).<br>Removed note about<br>eramGufi_316a not being used<br>in 5.5.1.4, 5.5.1.40, 5.5.1.64,<br>5.5.1.67, 5.5.1.70, 5.5.1.82.<br>Corrected HR_FIXM to<br>HR_AIXM (5.5.2.8) and<br>Airspace to Operational<br>(5.3.3.6).|October 28, 2016<br>December 13, 2016|

iv

NAS-JMSDD-4309-001 Rev C July 10, 2018

|Updated Section 2.3 based on<br>comments from AJW-17.<br>Updated Section 5.2.1 based<br>on comments from AJR-G<br>Administrative changes (re-<br>introduced changes for this<br>version with track changes on,<br>some of the tracking had<br>previously been lost).  Also<br>changed the version number to<br>reflect FAA standard.<br>Editorial changes|December 16, 2016<br>December 29, 2016<br>March 27, 2017||
|---|---|---|
|C<br>Updated to reflect changes<br>made in SFDPS Release 1.3.1 to<br>emit two versions of flight<br>messages for flights that are<br>not active, one containing<br>beacon code information and<br>one not; and the addition of a<br>JMS property to all flight<br>messages for NEMS to route<br>the messages to appropriately<br>authorized users.|December 22, 2017|Noblis|
|Updated some erroneous<br>information<br>1. FDPS1, FDPS2->ATL, SLC.<br>2. Corrected bad copy/paste in<br>‘Required’ column of 5.5.1.13.<br>3. Updated description for<br>FDPS_FlightOperator in Table<br>5-1|July 10, 2018|Noblis/Cavan<br>Solutions, AJW-17|

v

NAS-JMSDD-4309-001 Rev C July 10, 2018

### **Table of Contents**

|**_1._**<br>**_Scope ......................................................................................... 1_**|
|---|
|**1.1**<br>**Background .................................................................................... 1**|
|**_2._**<br>**_Applicable Documents ............................................................... 3_**|
|**2.1**<br>**Government Documents ................................................................. 3**|
|**2.2**<br>**Non-Government Documents and Other Publications ..................... 4**|
|**2.3**<br>**Security Policies ............................................................................. 4**|
|**_3._**<br>**_Definitions ................................................................................. 5_**|
|**3.1**<br>**Terms and Definitions .................................................................... 5**|
|**3.2**<br>**Acronyms ....................................................................................... 7**|
|**_4._**<br>**_Service Profile ......................................................................... 10_**|
|**4.1**<br>**Service Provider ........................................................................... 12**|
|4.1.1<br>Point of Contact ....................................................................................... 12|
|**4.2**<br>**Service Consumers ....................................................................... 12**|
|**4.3**<br>**Service Functionality .................................................................... 13**|
|**4.4**<br>**Security ........................................................................................ 13**|
|4.4.1<br>Roles ..................................................................................................... 14|
|4.4.2<br>Access Control Mechanisms ...................................................................... 14|
|**4.5**<br>**Quality of Services (QoS) ............................................................. 15**|
|**4.6**<br>**Service Policies ............................................................................ 15**|
|**4.7**<br>**Environmental Constraints ........................................................... 15**|
|**_5._**<br>**_Service Interfaces ................................................................... 16_**|
|**5.1**<br>**Interface ...................................................................................... 16**|
|**5.2**<br>**Operations .................................................................................... 16**|
|<br>5.2.1<br>Processing Considerations......................................................................... 16|
|**5.3**<br>**Messages ...................................................................................... 17**|
|<br>5.3.1<br>Flight Data Publication Service Messages .................................................... 19|
|5.3.1.1<br>Flight Plan Information: FH, FH_FIXM ................................................... 19|
|<br>5.3.1.2<br>Flight Amendment Information: AH, AHFIXM ....................................... 20|
|_<br>5.3.1.3<br>Converted Route Information: HX, HX_FIXM ......................................... 21|
|<br>5.3.1.4<br>Cancellation Information: CL, CL_FIXM ................................................. 21|
|<br>5.3.1.5<br>Departure Information: DH, DH_FIXM .................................................. 22|
|<br>5.3.1.6<br>Aircraft Identification Amendment Information: IH, IH_FIXM ................... 22|
|5.3.1.7<br>Hold Information: HH, HH_FIXM .......................................................... 23|
|5.3.1.8<br>Progress Report Information: PH, PH_FIXM ........................................... 24|
|<br>5.3.1.9<br>Flight Arrival Information: HV, HV_FIXM ............................................... 24|
|<br>5.3.1.10 Flight Plan Update Information: HU, HU_FIXM ....................................... 25|
|5.3.1.11 Expected Departure Time Information: ET, ET_FIXM .............................. 25|
|5.3.1.12 Position Update Information: HP, HP_FIXM ............................................ 26|

vi

NAS-JMSDD-4309-001 Rev C July 10, 2018

|5.3.1.13 <br>|Tentative Flight Plan Information: NP, NP_FIXM ..................................... 27<br>|
|---|---|
|5.3.1.14|Tentative Aircraft Identification Amendment Information: NI NIFIXM ..... 27|
|<br>5.3.1.15|, _<br> Tentative Flight Plan Removal: NL, NL_FIXM ......................................... 28|
|5.3.1.16 <br>|Tentative Flight Plan Amendment Information: NU, NU_FIXM .................. 29<br>|
|5.3.1.17|Batch Track Information: BATCH_TH, BATCH_TH_FIXM .......................... 29|
|5.3.1.18|Drop Track Information: RH, RH_FIXM ................................................. 30|
|5.3.1.19|Interim Altitude Information: LH, LH_FIXM ............................................ 30|
|5.3.1.20|ARTS Flow Control Track/Full Data Block Information: HZ, HZ_FIXM ........ 31|
|5.3.1.21|Beacon Code Reassignment: BA, BA_FIXM ............................................ 32|
|5.3.1.22|Beacon Code Restricted: RE, RE_FIXM .................................................. 32|
|5.3.1.23|FDB Fourth Line Information: HF, HF_FIXM ........................................... 33|
|5.3.1.24|<br> Point Out Information: HT, HT_FIXM .................................................... 34|
|5.3.1.25|Inbound Point Out Information: PT, PT_FIXM ......................................... 34|
|5.3.1.26|Handoff Status: OH, OH_FIXM ............................................................. 35|
|5.3.1.27|Flight Plan Reconstitution: DBRTFPI, DBRTFPI_FIXM ............................... 36|
|5.3.1.28|Flight Data Properties ......................................................................... 36|
|5.3.2<br>Air|space Data Publication Service Messages ................................................ 40|
|5.3.2.1|Sector Assignment Status: SH, SH_AIXM .............................................. 40|
|5.3.2.2|Route Status: HR, HR_AIXM ................................................................ 41|
|5.3.2.3|Special Activities Airspace (SAA): SU, SU_AIXM ..................................... 42|
|5.3.2.4|Altimeter Setting: HA ......................................................................... 42|
|5.3.2.5|Adapted Route Status Reconstitution:  DBRTRI, DBRTRI_AIXM ................ 43|
|5.3.2.6|Altimeter Status Reconstitution: DBRTAI ............................................... 44|
|5.3.2.7|Sector Assignment Reconstitution: DBRTSI, DBRTSI_AIXM ..................... 44|
|5.3.2.8|Airspace Data Properties ..................................................................... 45|
|5.3.3<br>Op|erational Data Publication Service Messages ........................................... 46|
|5.3.3.1|Traffic Count Adjustment: AK .............................................................. 46|
|5.3.3.2|Instrument Approach Count Adjustment: AC ......................................... 47|
|5.3.3.3|Sign In Sign Out: SY .......................................................................... 49|
|5.3.3.4|Beacon Code Utilization: UB ................................................................ 49|
|5.3.3.5|Geographic Beacon Code Utilization: UG ............................................... 50|
|5.3.3.6|Operational Data Properties................................................................. 50|
|5.3.4<br>Ge|neral Information Publication Service Message ........................................ 51|
|5.3.4.1|General Information: GH..................................................................... 51|
|5.3.4.2|Interim Altitude Status Information: HE ................................................ 52|
|5.3.4.3|Hold Status Information:  HO .............................................................. 52|
|5.3.4.4|ERAM Status Information:  HS ............................................................. 53|
|5.3.4.5|Unsuccessful Transmission Information:  UI .......................................... 53|
|5.3.4.6|General Information Data Properties .................................................... 54|
|**5.4**<br>**Exc**|**eptions Handling ..................................................................... 56**|
|**5.5**<br>**Dat**|**a ............................................................................................. 58**|
|5.5.1<br>Flig|ht Data Publication Service Data Elements and Diagrams ......................... 62|
|5.5.1.1|ERFDP Service: targetNamespace ........................................................ 63|
|5.5.1.2|SimpleXML Flight Plan, Flight Amendment, and Flight Update [FH, AH and|
|HU] - Da|ta Elements ........................................................................................ 63|
|5.5.1.3|Flight Plan, Flight Amendment, and Flight Update [FH, AH and HU]: Diagram<br>95|
|5.5.1.4|FIXM Flight Plan, Flight Amendment, and Flight Update [FH_FIXM, AH_FIXM|
|and HU_|<br>FIXM] - Data Elements ....................................................................... 100|
|5.5.1.5|Flight Amendment Information [AH] – Data Elements ........................... 134|
|5.5.1.6|Flight Amendment Information [AH] – Diagram ................................... 134|

vii

NAS-JMSDD-4309-001 Rev C July 10, 2018

|5.5.1.7|Flight Amendment Information in FIXM Format [AH_FIXM] – Data Elements<br>134|
|---|---|
|5.5.1.8|Converted Route Information [HX] - Data Elements ............................. 135|
|5.5.1.9<br>|Converted Route Information [HX]- Diagram ....................................... 137<br>|
|5.5.1.10 <br>|Converted Route Information FIXM format (HX_FIXM) – Data Elements .. 138<br>|
|5.5.1.11 <br>|Cancellation Information [CL] - Data Elements .................................... 142<br>|
|5.5.1.12|Cancellation Information [CL] – Diagram ............................................ 144|
|5.5.1.13|Cancellation Information in FIXM Format [CL_FIXM] – Data Elements ..... 144|
|5.5.1.14|Departure Information [DH] - Data Elements ...................................... 147|
|5.5.1.15|Departure Information [DH] - Diagram ............................................... 151|
|5.5.1.16|Departure Information Message in FIXM Format [DH_FIXM] – Data Elements<br>152|
|5.5.1.17|Aircraft Identification Amendment Information [IH] - Data Elements ...... 158|
|5.5.1.18|Aircraft Identification Amendment Information [IH] - Diagram ............... 160|
|5.5.1.19|Flight Identification Amendment Information Message in FIXM Format|
|[IH_FIXM|] – Data Elements............................................................................. 160|
|5.5.1.20|Hold Information [HH] – Data Elements .............................................. 164|
|5.5.1.21|Hold Information [HH] - Diagram ....................................................... 166|
|5.5.1.22|Hold Information Message in FIXM Format [HH_FIXM] – Data Elements .. 166|
|5.5.1.23|Progress Report Information [PH] – Data Elements .............................. 171|
|5.5.1.24|Progress Report Information [PH] - Diagram ....................................... 172|
|5.5.1.25|Progress Report Information Message in FIXM Format [PH_FIXM] – Data|
|Elements|172|
|5.5.1.26|Flight Arrival Information [HV] – Data Elements .................................. 176|
|5.5.1.27|Flight Arrival Information [HV] - Diagram ........................................... 179|
|5.5.1.28 <br>|Flight Arrival Information Message in FIXM Format [HV_FIXM] – Data<br>|
|Elements|179|
|5.5.1.29|Flight Plan Update Information [HU] – Data Elements ........................... 182|
|5.5.1.30|Flight Plan Update Information [HU] - Diagram .................................... 183|
|5.5.1.31 <br>Elements|Flight Plan Update Information Message in FIXM Format [HU_FIXM] – Data<br>183|
|5.5.1.32|Expected Departure Time Information [ET] – Data Elements ................. 183|
|5.5.1.33|Expected Departure Time Information [ET] - Diagram .......................... 185|
|5.5.1.34|Expected Departure Time Information Message in FIXM Format [ET_FIXM] –|
|Data Ele|ments ............................................................................................... 185|
|5.5.1.35|Position Update Information [HP] – Data Elements ............................... 189|
|5.5.1.36|Position Update Information [HP] - Diagram ........................................ 192|
|5.5.1.37|Position Update Information Message in FIXM Format [HP_FIXM] – Data|
|Elements|192|
|5.5.1.38|Tentative Flight Plan Information [NP] – Data Elements ........................ 197|
|5.5.1.39|Tentative Flight Plan Information [NP] - Diagram ................................. 205|
|5.5.1.40|Tentative Flight Plan Information in FIXM Format [NP_FIXM] – Data|
|Elements|<br>206|
|5.5.1.41|Tentative Aircraft Identification Amendment Information [NI] – Data|
|Elements|214|
|5.5.1.42|Tentative Aircraft Identification Amendment Information [NI] - Diagram . 217|
|5.5.1.43|Tentative Aircraft Identification Amendment Information Message in FIXM|
|Format [|NI_FIXM] – Data Elements .................................................................. 217|
|5.5.1.44|Tentative Flight Plan Removal [NL] – Data Elements ............................ 221|
|5.5.1.45|Tentative Flight Plan Removal [NL] - Diagram ..................................... 224|
|5.5.1.46|Tentative Flight Plan Removal Message in FIXM Format [NL_FIXM] ........ 224|
|5.5.1.47|Tentative Flight Plan Amendment Information [NU] – Data Elements ...... 230|
|5.5.1.48|Tentative Flight Plan Amendment Information [NU] - Diagram ............... 238|

viii

NAS-JMSDD-4309-001 Rev C July 10, 2018

|5.5.1.49 <br>|Tentative Flight Plan Amendment Information Message in FIXM Format<br>|
|---|---|
|[NUFIXM|] – Data Elements ............................................................................ 239|
|_<br>5.5.1.50|<br>Batch Track Information [BATCH_TH] – Data Elements ......................... 250|
|5.5.1.51|Batch Track Information [BATCH_TH] - Diagram .................................. 261|
|5.5.1.52 <br>|Batch Track Information Message in FIXM Format [BATCH_TH_FIXM] – Data<br>|
|Elements<br>|262<br>|
|5.5.1.53|Drop Track Information [RH] – Data Elements ..................................... 272|
|5.5.1.54|Drop Track Information [RH] - Diagram .............................................. 274|
|5.5.1.55 <br>|Drop Track Information Message in FIXM Format [RH_FIXM] – Data<br>|
|Elements|274|
|5.5.1.56|Interim Altitude Information [LH] – Data Elements ............................... 277|
|5.5.1.57|Interim Altitude Information [LH] - Diagram ........................................ 279|
|5.5.1.58|<br>Interim Altitude Information Message in FIXM Format [LH_FIXM] – Data|
|Elements|279|
|5.5.1.59|ARTS Flow Control Track/Full Data Block Information [HZ] – Data Elements<br>283|
|5.5.1.60 <br>|ARTS Flow Control Track/Full Data Block Information [HZ] - Diagram ..... 287<br>|
|5.5.1.61 <br>|ARTS Flow Control Track/Full Data Block Information [HZ_FIXM] – Data<br>|
|Elements|287|
|5.5.1.62|Beacon Code Reassignment [BA] – Data Elements ............................... 294|
|5.5.1.63|Beacon Code Reassignment [BA] - Diagram ........................................ 296|
|5.5.1.64|Beacon Code Reassignment Message in FIXM Format [BA_FIXM] – Data|
|Elements|296|
|5.5.1.65|Beacon Code Restricted [RE] – Data Elements ..................................... 300|
|5.5.1.66|Beacon Code Restricted [RE] - Diagram .............................................. 303|
|5.5.1.67 <br>|Beacon Code Restricted Message in FIXM Format [RE_FIXM] – Data<br>|
|Elements|303|
|5.5.1.68|FDB Fourth Line Information [HF] – Data Elements .............................. 307|
|5.5.1.69|FDB Fourth Line Information [HF] - Diagram ....................................... 309|
|5.5.1.70|FDB Forth Line Message in FIXM Format [HF_FIXM] – Data Elements ..... 309|
|5.5.1.71|Point Out Information [HT] – Data Elements ....................................... 313|
|5.5.1.72|Point Out Information [HT] - Diagram ................................................ 314|
|5.5.1.73|Point Out Information Message in FIXM Format [HT_FIXM] – Data Elements<br>314|
|5.5.1.74|Inbound Point Out Information [PT] – Data Elements ........................... 318|
|5.5.1.75|Inbound Point Out Information [PT] - Diagram .................................... 320|
|5.5.1.76|Inbound Point Out Information Message in FIXM [PT_FIXM] – Data Elements<br>320|
|5.5.1.77|Handoff Status [OH] – Data Elements ................................................. 325|
|5.5.1.78|Handoff Status [OH] – Diagram ......................................................... 328|
|5.5.1.79|Handoff Status Message in FIXM Format [OH_FIXM] – Data Elements..... 328|
|5.5.1.80|Flight Plan Reconstitution [DBRTFPI] – Data Elements .......................... 333|
|5.5.1.81|Flight Plan Reconstitution [DBRTFPI] – Diagram ................................... 363|
|5.5.1.82|Flight Plan Reconstitution Message in FIXM Format [DBRTFPI_FIXM] – Data|
|Elements|<br>365|
|5.5.2<br>Airs|pace Data Publication Service Data Elements and Diagrams .................. 405|
|5.5.2.1|ERADP Service: targetNamespace ...................................................... 405|
|5.5.2.2|<br>Sector Assignment Status [SH] – Data Elements .................................. 405|
|5.5.2.3|Sector Assignment Status [SH] - Diagram ........................................... 409|
|5.5.2.4|Sector Assignment Status Message in AIXM Format [SHAIXM] – Data|
|Elements|_<br>409|
|5.5.2.5|Route Status [HR] – Data Elements .................................................... 410|
|5.5.2.6|Route Status [HR] - Diagram ............................................................. 412|

ix

NAS-JMSDD-4309-001 Rev C July 10, 2018

|5.5.2.7|Route Status Message in AIXM Format [HR_AIXM] – Data Elements ....... 412<br>|
|---|---|
|5528|Route Status Message in AIXM Format [HRAIXM] – Diagram  413|
|...<br>5.5.2.9|_   ...............<br>Special Activities Airspace (SAA) [SU] – Data Elements ........................ 414|
|5.5.2.10 <br>|Special Activities Airspace (SAA) [SU] – Diagram ................................. 416<br>|
|5.5.2.11 <br>Elements<br>|Special Activities Airspace (SAA) in AIXM Format [SU_AIXM] – Data<br>416<br>|
|5.5.2.12 <br>|Altimeter Setting [HA] – Data Elements .............................................. 419<br>|
|5.5.2.13|Altimeter Setting [HA] – Diagram ...................................................... 421|
|5.5.2.14|Adapted Route Status Reconstitution [DBRTRI] – Data Elements ........... 421|
|5.5.2.15|Adapted Route Status Reconstitution [DBRTRI] – Diagram .................... 422|
|5.5.2.16|Adapted Route Status Reconstitution Message in AIXM Format|
|[DBRTRI|_AIXM] – Data Elements ..................................................................... 422|
|5.5.2.17|Altimeter Status Reconstitution [DBRTAI] – Data Elements ................... 423|
|5.5.2.18|Altimeter Status Reconstitution [DBRTAI] – Diagram ............................ 425|
|5.5.2.19|Sector Assignment Reconstitution [DBRTSI] – Data Elements ................ 425|
|5.5.2.20|Sector Assignment Reconstitution [DBRTSI] – Diagram ........................ 427|
|5.5.2.21 <br>|Sector Assignment Reconstitution Message in AIXM Format [DBRTSI_AIXM]<br>|
|– Data El|ements ............................................................................................ 427|
|5.5.3<br>Op|erational Data Publication Service Data Elements and Diagrams .............. 429|
|5.5.3.1|ERODP Service: targetNamespace ...................................................... 429|
|5.5.3.2|Traffic Count Adjustment [AK] – Data Elements ................................... 429|
|5.5.3.3|Traffic Count Adjustment [AK] - Diagram ............................................ 433|
|5.5.3.4|Instrument Approach Count Adjustment [AC] – Data Elements .............. 433|
|5.5.3.5|Instrument Approach Count Adjustment [AC] - Diagram ....................... 437|
|5.5.3.6<br>|Sign In Sign Out [SY] – Data Elements ............................................... 437<br>|
|5.5.3.7|Sign In Sign Out [SY] - Diagram ........................................................ 442|
|5.5.3.8|Beacon code Utilization [UB] – Data Elements ..................................... 443|
|5.5.3.9|Beacon code Utilization [UB] - Diagram .............................................. 444|
|5.5.3.10|Geographic Beacon Code Utilization [UG] – Data Elements .................... 445|
|5.5.3.11 <br>|Geographic Beacon Code Utilization [UG] - Diagram ............................. 446<br>|
|5.5.4<br>Ge|neral Information Publication Service Data Elements and Diagram ........... 447|
|5.5.4.1|ERGMP Service: targetNamespace ..................................................... 447|
|5.5.4.2|<br>General Information [GH] – Data Elements ......................................... 447|
|5.5.4.3|General Information [GH] - Diagram .................................................. 449|
|5.5.4.4|Interim Altitude Status Information [HE] – Data Elements .................... 449|
|5.5.4.5|Interim Altitude Status Information [HE] – Diagram ............................. 451|
|5.5.4.6|Hold Status Information [HO] – Data elements .................................... 451<br>|
|5.5.4.7|Hold Status Information [HO] – Diagram ............................................ 453|
|5.5.4.8|ERAM Status Information [HS] – Data Elements .................................. 453|
|5.5.4.9|ERAM Status Information [HS] – Diagram ........................................... 456|
|5.5.4.10|Unsuccessful Transmission Information [UI] – Data Elements ................ 456|
|5.5.4.11|Unsuccessful Transmission Informattion [UI] - Diagram ........................ 458|
|**_6._**<br>**_Service_**|**_Implementation ........................................................ 459_**|
|**6.1**<br>**Bind**|**ings ..................................................................................... 459**|
|6.1.1<br>Act|iveMQ .............................................................................................. 459|
|6.1.1.1|Data format .................................................................................... 459|
|6.1.1.2|Message protocol ............................................................................. 459|
|6.1.1.3|Transport protocol ............................................................................ 459|
|**6.2**<br>**End**|**Points .................................................................................. 459**|
|6.2.1<br>End|Point 1 ........................................................................................... 459|

x

NAS-JMSDD-4309-001 Rev C July 10, 2018

## **1. Scope**

This Java Messaging Service Description Document (JMSDD) describes the Java messaging services for the System-Wide Information Management (SWIM) Flight Data Publication Service (SFDPS). These Service Oriented Architecture (SOA) services are available to Federal Aviation Administration (FAA) users and non-FAA users as National Airspace System (NAS) services. This document was prepared in accordance with the FAA Standard Practice Preparation of Java Messaging Service Description Documents [FAA-STD-073 (Reference 13)].

SFDPS publishes four different categories of data, defined as four En Route Data Services. The four services are:

- En Route Flight Data Publication (ERFDP) – Includes any data specific to an individual flight.

- En Route Airspace Data Publication (ERADP) – Includes airspace data that is of general interest.

- En Route Operational Data Publication (ERODP) – Includes data sent by En Route Automation Modernization (ERAM) to support specific FAA monitoring functions.

- En Route General Message Publication (ERGMP) – The ability to send general, free-form text messages and other messages to one or more clients or classes of clients.

The description is divided into three core sections: Service Profile, Service Interfaces, and Service Implementation.

- The Service Profile section answers the question “What does the service do?” It does this in a manner that allows a service consumer to determine whether a particular service meets its needs.

- The Service Interfaces section answers the question “How does the service work?” It describes the interface and semantics of the service; that is, it details the content of requests, message formats, data types, and transport formats.

- The Service Implementation section answers the question “How does one access the service?” It specifies the communication protocol and network address.

### **1.1 Background**

This JMSDD applies to the current version (1.3.0) of Phase 1 of the SFDPS. SFDPS is the SWIM program developed to provide flight information services to a wide variety of consumers in a manner that complies with SWIM standards and requirements. The general purpose of Phase 1 is to make ERAM system data easily accessible to consumers. Phase 1 provides only a one-way data distribution; two-way communications between other systems and ERAM are deferred to the future.

SFDPS data consumers could be FAA facilities, FAA systems or programs, other government systems or programs, or non-government systems or programs. This data is derived completely from the Host Air Traffic Management (ATM) Data Distribution System (HADDS)

1

NAS-JMSDD-4309-001 Rev C July 10, 2018

Common Message Set (CMS) messages. The general behavior is that an incoming CMS message from HADDS triggers a data publication from SFDPS.

SFDPS publishes messages to the National Airspace (NAS) Enterprise Messaging Service (NEMS), which then delivers those messages to subscribers.

This document only deals with SFDPS JMS publication services. Request-Response web services are described in the Web Service Description Document (WSDD) (See Reference 8).

2

NAS-JMSDD-4309-001 Rev C July 10, 2018

## **2. Applicable Documents**

### **2.1 Government Documents**

1. Ken Howard, _FDPS Architecture Description_ , Volpe National Transportation System Center, Cambridge, MA, report no. VNTSC-TFM-12-6, March 2012

2. _SFDPS-SSS-4309-001, System/Subsystem Specification (SSS) Document for the En Route Flight Data Publication Service, Version 2.2_ , Volpe National Transportation System Center, Cambridge, MA, August 25, 2016

3. _Host Air Traffic Management (ATM) Data Distribution System (HADDS) Application Programming Interface (API) Document, Revision 1 For Common Message Set (CMS)_ , May 2008

4. _System/Subsystem Design Description (SSDD) For the En Route SWIM Flight Data Publication Service, Draft_ , Version 0.37, Volpe National Transportation System Center, Cambridge, MA, September 1, 2014

5. _Development Test (DT) Test Plan For the En Route Flight Data Publication Service (FDPS)_ Version 1.10, Volpe National Transportation System Center, Cambridge, MA, October 19, 2012

6. _Software Design Description (SDD) For the En Route System Wide Information Management (SWIM) Flight Data Publication Service (SFDPS),_ Version 2.0, Volpe National Transportation System Center, Cambridge, MA, January 29, 2016

7. _Web Service Requirements Document (WSRD) System Wide Information Management (SWIM) Flight Data Publication Service (SFDPS)_ , Version 2.3, Volpe National Transportation System Center, Cambridge, MA, November 9, 2015

8. _Web Service Description Document (WSDD) System Wide Information Management (SWIM) Flight Data Publication Service (SFDPS)_ , Version 2.5, Volpe National Transportation System Center, Cambridge, MA, March 02, 2016

9. FAA–STD–063, _XML Namespaces,_ May 1, 2009 http://www.tc.faa.gov/its/worldpac/standards/faa-std-063.pdf

10. FAA–STD–064, _Web Service Registration_ , May 1, 2009 http://www.tc.faa.gov/its/worldpac/standards/faa-std-064.pdf

11. FAA–STD–065, _Standard Practice Preparation of Web Service Description Documents_ , February 26, 2010 http://www.tc.faa.gov/its/worldpac/standards/faa-std-065.pdf

12. FAA–STD–066, _Web Service Taxonomies_ , February 26,2010 http://www.tc.faa.gov/its/worldpac/standards/faa-std-066.pdf

13. FAA-STD-073, Preparation of Java Messaging Service Description Documents, January 29,2014 http://www.tc.faa.gov/its/worldpac/standards/faa-std-073.pdf

14. _NAS Enterprise Messaging Service (NEMS) Asynchronous Messaging ICD_ , _Draft,_ Federal Aviation Administration, System Wide Information Management Program, July 20, 2012

15. SFDPSSchema_v1.3.8.xsd, Volpe National Transportation System Center, Cambridge, MA, June 10, 2016

3

NAS-JMSDD-4309-001 Rev C July 10, 2018

16. SS to FIXM 3.0 Mapping v6, Volpe National Transportation System Center, Cambridge, MA, January 22, 2016

17. FIXM Core v3.0 and FIXM US Extension v3.0 Schema Files, http://www.fixm.aero

18. AIXM 5.1 and AIXM SFDPS Extension Schema Files, http://www.aixm.aero

19. ATS Message Content to FIXM Logical Model Map_v2_0.pdf, http://www.fixm.aero

20. SWIM Flight Data Publication Service (SFDPS) Consumer Reference Manual, Version 2.1.3, Volpe National Transportation System Center, Cambridge, MA, July 7, 2016.

### **2.2 Non-Government Documents and Other Publications**

21. World Wide Web Consortium (W3C) XML Schema http://www.w3.org/XML/Schema

22. W3C Recommendation, "XML-Signature Syntax and Processing", 12 February 2002. http://www.w3.org/TR/2002/REC-xmldsig-core-20020212/

23. W3C Recommendation, D. Eastlake et al. XML Signature Syntax and Processing

24. Java 2 Platform, Enterprise Edition, v 1.3 API Specification http://docs.oracle.com/javaee/1.3/api/

25. XML Signature Syntax and Processing (Second Edition). 10 June 2008. http://www.w3.org/TR/2008/REC-xmldsig-core-20080610/

26. Organization for the Advancement Structured of Information Standards (OASIS) SOA Reference Model. http://docs.oasis-open.org/soa-rm/v1.0/soa-rm.pdf

### **2.3 Security Policies**

27. FAA Order 1370.103, Encryption Policy, dated 11/12/08

28. FAA Order 1370.104, Digital Signature Policy dated 10/31/2008

29. FAA Order 1370.112, FAA Application Security Policy dated 10/5/2010

30. FAA Order 1370.92A, Password and PIN Management Policy dated 8/6/2010

31. FAA Order 1370.95, Wide Area Network Connectivity Security dated 9/12/2006

32. FAA Order 1280.1B, Protecting Personally Identifiable Information dated 12/17/08 33. FAA Order 1370.113, Web Security Management Policy dated 5/16/12

4

NAS-JMSDD-4309-001 Rev C July 10, 2018

## **3. Definitions**

Many of the terms listed in this section are defined in FAA-STD-073, Preparation of Java Messaging Service Description Documents (see Reference 13).

### **3.1 Terms and Definitions**

|**Asynchronous**|An interaction in which the associated messages are chronologically<br>and procedurally decoupled. For example, in a request-response<br>interaction, the client agent can process the response at some<br>indeterminate point in the future when its existence is discovered.|
|---|---|
|**Authentication**|The process of verifying an identity claimed by or for a system<br>entity.|
|**Authorization**|The granting of rights or permission to a system entity (mainly but<br>not always a user or a group of users) to access a service.|
|**Binding**|An association between an interface, a concrete protocol, and a<br>data format. A binding specifies the protocol and data format to be<br>used in transmitting messages defined by the associated interface.|
|**Client**|A client is an external entity that interacts with a service. A client<br>makes a request of a service and receives a response from the<br>service. The client may also request a subscription and receive<br>messages when a service publishes information. A client may be a<br>software system, software application, or another service. A client<br>may be a NAS client or a non-NAS client.|
|**Data Element**|A unit of data for which the definition, identification,<br>representation, and permissible values are specified by means of a<br>set of attributes.|
|**Datatype**|A set of distinct values, characterized by properties of those<br>values, and by operations on those values.|
|**Effect**|A state or condition that results from interaction with a service.<br>Multiple states may result depending on the extent to which the<br>interaction completes successfully or generates a fault.|
|**End Point**|An association between a fully specified binding and a physical<br>point (i.e., a network address) at which a service may be accessed.|
|**Fault**|A message that is returned as a result of an error that prevents a<br>service from implementing a required function. A fault usually<br>contains information about the cause of the error.|
|**Format**|The arrangement of bits or characters within a group, such as a<br>data element, message, or language.|
|**Input**|Data entered into, or the process of entering data into, an<br>information processing system or any of its parts for storage or<br>processing.|
|**Java Message Service**|**(JMS)**<br>A Java-based application programming interface (API) that|

5

NAS-JMSDD-4309-001 Rev C July 10, 2018

provides a common way for Java programs to create, send, receive, and read an enterprise messaging system's messages. **JMS Client** An application or process that produces and/or receives messages. **Message** A basic unit of communication from one software agent to another sent in a single logical transmission. **Message Producer** A JMS client that creates and sends messages. **Namespace** A collection of names, identified by a Uniform Resource Identifier (URI) reference, that are used in Extensible Markup Language (XML) documents as element types and attribute names. The use of XML namespaces to identify uniquely metadata terms allows those terms to be used unambiguously across applications, promoting the possibility of shared semantics.

###### **NAS Enterprise Messaging Service (NEMS)**

A NAS-based implementation of message-oriented middleware (MOM) that is responsible for distributing messages among information consumers and providers, as well as providing administrative functionality that includes (but is not limited to) fault tolerance, load balancing, mediation and orchestration support.

**Operation** A set of messages related to a single service action. **Organization** A unique framework of authority within which a person or persons act, or are designated to act, towards some purpose. Any department, service, or other entity within an organization which needs to be identified for information exchange. **Output** Data transferred out of, or the process by which an information processing system or any of its parts transfers data out of, that system or part. **Permissible Values** The set of allowable instances of a data element. **Protocol** A formal set of conventions governing the format and control of interaction among communicating functional units. **Quality of Service (QoS)** A parameter that specifies and measures the value of a provided service. **Security** The protection of information and data so that unauthorized persons or systems cannot read or modify them and authorized persons or systems are not denied access to them. **Service** A mechanism to enable access to one or more capabilities, where the access is provided using a prescribed interface and is exercised consistent with constraints and policies as specified by the service description. **Service Consumer** An organization that seeks to satisfy a particular need through the use of capabilities offered by means of a service. **Service Description** The information needed in order to use, or consider using, a service.

6

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Service Interface**|The means by which the underlying capabilities of a service are<br>accessed.|
|---|---|
|**Service Provider**|An organization that offers the use of capabilities by means of a<br>service.|
|**Subscription**|For Phase 1 of SFDPS, the term “subscription” used in this<br>document or in the service names/artifacts, is a connection for<br>published data by an SFDPS consumer. Consumers can request<br>specific data sets by specifying values during on-ramping to NEMS.|
|**Topic**|A distribution mechanism for publishing messages that are<br>delivered to multiple subscribers.|
|**Uniform Resource I**|**dentifier (URI)**<br>A compact string of characters for identifying an abstract or<br>physical resource.|
|**User**|A human, his/her agent, a surrogate, or an entity that interacts<br>with information processing systems. A person, organization entity,<br>or automated process that accesses a system, whether authorized<br>to do so or not.|
|**Web Service**|A platform-independent, loosely coupled software component<br>designed to support interoperable machine-to-machine interaction<br>over a network. It has an interface described in a machine-<br>processable format. XML formatted messages are exchanged over<br>the Internet using standard transport and Web-based protocols.|

### **3.2 Acronyms**

|ADS/ADS-B|Automated Dependent Surveillance (-Broadcast)|
|---|---|
|AIXM|Airspace Information Exchange Model|
|API|Application Programming Interface|
|ARTCC|Air Route Traffic Control Center|
|ARTS|Automated Radar Terminal System|
|ATM|Air Traffic Management|
|ATS|Air Traffic Service|
|BARR|Block Aircraft Registration Request|
|CMS|Common Message Set|
|CTAS|Center-TRACON Automation System|
|DME|Distance Measuring Equipment|
|EDCT|Estimated Departure Clearance Time|
|EET|Estimated Elapsed Time|
|ERADP|En Route Airspace Data Publication|
|ERAM|En Route Automation Modernization|
|ERFDP|En Route Flight Data Publication|

7

NAS-JMSDD-4309-001 Rev C July 10, 2018

|ERGMP|En Route General Message Publication|
|---|---|
|ERODP|En Route Operational Data Publication|
|FDB|Full Data Block|
|FDPS|Flight Data Publication Service|
|FIR|Flight Information Region|
|FIXM|Flight Information Exchange Model|
|FMS|Flight Management System|
|GNSS|Global Navigation Satellite System|
|GPS|Global Positioning System|
|GUFI|Globally Unique Flight Identifier|
|HADDS|Host ATM Data Distribution System|
|ICAO|International Civil Aviation Organization|
|ICD|Interface Control Document|
|IFPA|Instrument Flight Procedure Automation|
|IFR|Instrument Flight Rules|
|IPOP|Intermediate Point of Presence|
|IRU|Inertial Reference Unit|
|JMS|Java Message Service|
|JMSDD|Java Messaging Service Description Document|
|LOCID|Location Identifier|
|MOM|Message-Oriented Middleware|
|NAS|National Airspace System|
|NEMS|NAS Enterprise Messaging System|
|PBN|Performance-Based Navigation|
|QoS|Quality of Service|
|RIF|Revised In Flight|
|RNAV|Area Navigation|
|RNP|Required Navigation Performance|
|RVSM|Reduced Vertical Separation Minimums|
|SAA|Special Activities Airspace|
|SOA|Service Oriented Architecture|
|SSDD|System/Subsystem Design Document|
|SSR|Secondary Surveillance Radar|
|SSS|System/Subsystem Specification|
|STARS|Standard Terminal Automation Replacement System|
|SFDPS|SWIM Flight Data Publication Service|

8

NAS-JMSDD-4309-001 Rev C July 10, 2018

SWIM System Wide Information Management TCP Transmission Control Protocol TFDM Terminal Flight Data Manager TFMS Traffic Flow Management System TRACON Terminal Radar Approach Control Facility UFPI Unique Flight Plan Identifier, same as the ERAM-GUFI. URI Uniform Resource Identifier VFR Visual Flight Rules VHF Very High Frequency VOR VHF Omni-directional Radar W3C World Wide Web Consortium WAAS Wide-Area Augmenation System WMSCR Weather Message Switching Center Replacement WSDD Web Service Description Document XML Extensible Markup Language

9

NAS-JMSDD-4309-001 Rev C July 10, 2018

## **4. Service Profile**

The SWIM Flight Data Publication Service makes CMS messages sent from ERAM available through one of four publication services depending on the type of the message. The messages supported by each service are defined in the schema document, SFDPS_v1.2.xsd (see reference 15).

###### **1. En Route Flight Data Publication Service**

**Name** EnrouteFlightDataPublication

**Namespace** us:gov:dot:faa:atm:enroute:services:flightdatapub **Description** This Java Messaging Service accepts subscriptions for flight and track data. It allows users to specify a range of selection criteria defined in Section 5.5.1. Flight messages meeting these criteria are routed to the consumer by NEMS.

**Version** 1.3.0 **Service Category** Flight Information Service **Lifecycle Stage** Production **Criticality Level** Essential

###### **2. En Route Airspace Data Publication Service**

**Name** EnrouteAirspaceDataPublication

**Namespace** us:gov:dot:faa:atm:enroute:services:airspacedatapub

**Description** This Java Messaging Service accepts subscriptions for sector and route data. It allows users to specify a range of selection criteria defined in Section 5.5.2. Airspace messages meeting these criteria are routed to the consumer by NEMS.

**Version** 1.3.0 **Service Category** Navigation Information Service **Lifecycle Stage** Production **Criticality Level** Essential

10

NAS-JMSDD-4309-001 Rev C July 10, 2018

###### **3. En Route Operational Data Publication Service**

**Name** EnrouteOperationalDataPublication

**Namespace** us:gov:dot:faa:atm:enroute:services:operationaldatapub **Description** This Java Messaging Service accepts subscriptions for operational message data. It allows users to specify a range of selection criteria defined in Section 5.5.3. Operational messages meeting these criteria are routed to the consumer by NEMS.

**Version** 1.3.0 **Service Category** Air Traffic Support Service **Lifecycle Stage** Production **Criticality Level** Essential

###### **4. En Route General Message Publication Service**

**Name** EnrouteGeneralMessagePublication

**Namespace** us:gov:dot:faa:atm:enroute:services:generalmessagepub

**Description** This Java Messaging Service accepts subscriptions for general message publication data. It allows users to specify a range of selection criteria defined in Section 5.5.4. General messages meeting these criteria are routed to the consumer by NEMS.

**Version** 1.3.0

**Service Category** Air Traffic Support Service **Lifecycle Stage** Production

**Criticality Level** Essential

11

NAS-JMSDD-4309-001 Rev C July 10, 2018

### **4.1 Service Provider**

**Name** Federal Aviation Administration (FAA) System Wide Information Management (SWIM) Program Office, Enterprise Programs

**Description** A program within the FAA Air Traffic Organization that is responsible for transforming technologies that provide more efficient operations and streamlined data communications capabilities.

**Web page** http://www.faa.gov/nextgen/swim/

#### **4.1.1 Point of Contact**

|**Name**|Melissa Matthews|
|---|---|
|**Organization**|Federal Aviation Administration|
|**Title**|SWIM Capabilities Lead|
|**Phone**|202-267-0764|
|**email**|Melissa.Matthews@faa.gov|

### **4.2 Service Consumers**

Potential consumers of SFDPS data and services include the following:

- **Traffic Flow Management System (TFMS)** – TFMS monitors all planned and current flights. It would subscribe for all flight plan data, position updates, and other flight data messages. It also needs current sector configurations and route status messages. It is a trusted FAA system, and would therefore get all messages.

- **Terminal Radar Approach Control Facility (TRACON)/Tower** – An FAA system such as the Standard Terminal Automation Replacement System (STARS) or the Terminal Flight Data Manager (TFDM) could subscribe to a subset of the en route data of particular interest to that system. For example, TFDM might want all flight plans for flights departing from or arriving at a certain airport, and track updates for flights approaching that airport. Being an FAA system, they would have access to all of the flight data.

- **Non-FAA Government Data Consumer** – This could be a military group or any other government agencythat isauthorized to get data for any flight, but might have very specific data requirements. That is, they might want only a small subset of the message types. Other agencies, such as NASA, might not be authorized to receive military/sensitive data.

- **Non-government Data Consumer** – This could be an airline or a company that shows flight progress and status. They might want only certain flights; for example,

12

NAS-JMSDD-4309-001 Rev C July 10, 2018

an airline might want position updates for only its own flights. Being non-government entities, they would not have authorization to get data for military/sensitive flights.

### **4.3 Service Functionality**

SFDPS is the SWIM program developed to provide ERAM en-route flight information services to a wide variety of consumers in manner that complies with SWIM standards and requirements. The consumers could be FAA facilities, FAA systems or programs, other government systems or programs, or non-government systems or programs.

A goal of SFDPS is to transform the data it receives from 20 different ERAM sources into a single stream of Extensible Markup Language (XML) formatted text. Each discrete message is further associated with:

- A unique flight identifier so that the consumer knows which flight a message belongs to rather than having to perform message matching.

- The state of the flight as it moves from Proposed to Active to Landed. Flights may also be cancelled.

- A means to know whether a message was sent from an Air Route Traffic Control Center (ARTCC) that is controlling a flight or not. This allows extraneous messages to be ignored.

The effect of these functions is to relieve consumers of the burdens of processing the raw messages themselves. A consumer is able to track flights easily, to know when flights are canceled or delayed, and to know if the flight is affected by a ground-delay program or some other traffic management initiative.

Furthermore, by tagging each message with JMS properties, a consumer can arrange for a filtered feed of messages. A military consumer can receive only messages that relate to military flights, an airline can receive only messages related to its operations, a company that displays live flight data can receive only flight plan messages for the predicted route and track messages for the actual route.

### **4.4 Security**

SFDPS complies with NEMS security requirements as a message producer. NEMS handles identification and authentication of SFDPS consumers. NEMS also performs authorization. When SFDPS is deployed, both operationally with NAS Operational NEMS and with Research and Development NEMS, it is provisioned in “trusted” and “untrusted” regions.

SFDPS obtains updated sensitive flight data tagging files from AJR-2 on a periodic basis or as directed by AJR-2 for time critical requirements.  Following the AJR-2 flight data sensitivity identification process, SFDPS uses the information in those files to mark, or tag, service messages as containing sensitive or non-sensitive flight data.  During the SWIM onboarding process, each client is authorized to receive either sensitive or non-sensitive flight data, and is configured accordingly when on-ramped to NEMS.  NEMS uses the client configuration and each message’s “Send To” tag (FDPS_Sensitive) to ensure messages with sensitive flight data are only sent to clients authorized to receive sensitive flight data.  Flight data tagged as sensitive is Sensitive Security Information (SSI) and must be protected in accordance with FAA Order 1600.75, Protecting Sensitive Unclassified Information (SUI).

The FAA has also placed a restriction on the sharing of beacon code information on flights not yet active to address safety concerns. To address this, SFDPS generates two versions of

13

NAS-JMSDD-4309-001 Rev C July 10, 2018

some messages for flights that are not yet active, one containing beacon code information and one not. All messages are marked with a property (FDPS_Restricted) indicating whether the message may be shared with all consumers (FDPS_Restricted=‘A’) because it contains no beacon code information or is for a post-departure flight, only consumers authorized to receive beacon code information for non-active flights (FDPS_Restricted=’R’, indicating beacon code data is retained in the message), or only consumers not authorized to receive beacon code information for non-active flights (FDPS_Restricted=’D’, indicating that any beacon code data has been removed from the message). Consumer subscriptions to NEMS are set up appropriately during the on-boarding process, based upon their authorizations, and NEMS uses this message property in conjuction with others and the consumer subscription information to route messages appropriately. Flight messages not containing any beacon code information are marked with FDPS_Restricted = ‘A’ indicating there is no restriction other than that imposed by the FDPS_Sensitive flag on message distribution. Flight messages containing primarily beacon code information (BA/BA_FIXM and

RE/RE_FIXM) are marked with FDPS_Restricted = ‘R’ if the flight is not yet active, indicating these messages cannot be shared with those users not authorized to receive beacon code information The FDPS_Restricted property is independent of the FDPS_Sensitive property.

#### **4.4.1 Roles**

|**Role**|**Description**|
|---|---|
|**NON-GOVERENMENT-**<br>**NON-FAA**|Access is restricted to non-sensitive data only.  SFDPS filters military<br>operations and privacy track data (BARR) sent in real time and marks the<br>filtered data as FDPS_sensitive = false.|
|**GOVERNMENT -NON-FAA**|Access to non-military/sensitive data is granted. Access to<br>military/sensitive data may be granted based upon need-to-know (e.g.,<br>US Department of Defense has access to all military/sensitve flight data,<br>whereas NASA does not have access). Data is marked<br>FDPS_sensitive=true for unfiltered data or FDPS_sensitive=false for<br>filtered data.|
|**FAA**|Unrestricted data access. Data is marked FDPS_sensitive= true.|

#### **4.4.2 Access Control Mechanisms**

|**Access Control**|**Description / Regulating Document**|
|---|---|
|**Identification &**<br>**Authentication**|NEMS provides credentials for the JMS-Producer(SFDPS) and JMS-<br>Consumer of SFDPS services.|
|**Authorization**|When a client registers to connect to a topic, a process called on-<br>ramping, NEMS assigns a role to the client. SFDPS attaches metadata to<br>each message it sends to NEMS and NEMS applies correct access control<br>rules based on this metadata.|

14

NAS-JMSDD-4309-001 Rev C July 10, 2018

### **4.5 Quality of Services (QoS)**

The SFDPS QoS requirements are as defined in sections 3.11.2, 3.11.3, 3.11.4, and 3.11.5 of the SFDPS SSS. See Reference [2].

### **4.6 Service Policies**

No specific service policies are applied to this service. However, through the consumer onramping process, NEMS designates a consumer as either a NAS or non-NAS consumer.

These headers are defined in more detail in Section 5.2.1.

### **4.7 Environmental Constraints**

One instance of SFPDS is deployed to publish into the Research and Development NEMS. This instance of SFPDS has a record type of pre-recorded, which consists of HADDS replay data that was recorded seven days prior to the current date.

The operational implementation of SFDPS is a NAS message producer deployed to publish into the NAS Operational NEMS. The record type is live.

15

NAS-JMSDD-4309-001 Rev C July 10, 2018

## **5. Service Interfaces**

This section provides detailed information about the types and content of messages that the SFDPS exchanges, message exchange models that the service deploys, and any conditions implied by these messages.

### **5.1 Interface**

SFDPS follows version 1.1 of the JMS specification.

SFPDS uses the Publish/Subscribe messaging model.

### **5.2 Operations**

None.

#### **5.2.1 Processing Considerations**

SFDPS publishes flight data in two formats, SimpleXML andFlight Information Exchange Model (FIXM), and it publishes airspace data in two formats, SimpleXML andAirspace Information Exchange Model(AIXM). It publishes operational and general messages only in SimpleXML format. All SimpleXML messages have a one-to-one correspondence between the corresponding CMS message and the SimpleXML output. FIXM and AIXM, as general purpose data exchange models, do not have a complete one-to-one correspondence between the CMS messages and the FIXM or AIXM versions.  A small number of fields can not be translated into FIXM and AIXM.  These are noted in the data description sections.

In addition to the message body, SFDPS attaches data to each message:

- JMS properties – These allow NEMS to filter the message and deliver it only to those consumers who want it.

- SFDPS properties – These are optional data fields derived from the messages that provide additional information about the message. They provide additional context for the message.

SFDPS processes each flight related message and assigns the following fields based on the contents of the current message and of previous messages for the flight:

- Globally Unique Flight Identifier (GUFI) – This is a unique identifier that identifies all of the messages that belong to one flight. A flight is defined as the operation of an aircraft from take-off to touch-down.

- Flight status – Indicates the current state of a flight, one of proposed, active, landed, cancelled, dropped.

- Flight plan sequence number – the number of flight plans received by a flight.

SFDPS maintains a database of received messages to aid in the processing of flight level data.

SFDPS also sets the following JMS properties based on its stored data:

16

NAS-JMSDD-4309-001 Rev C July 10, 2018

- Sensitive – Whether the message pertains to a flight that is military/sensitive or not.

- Authoritative – Whether the message was sent from an ARTCC that has control of the flight or not.

SFDPS batches the flight track messages before publishing them to NEMS to reduce bandwidth usage. The Sensitive and Authoritative JMS properties (among others, as specified in 5.3.1.28) also apply to these batched messages. A batched message contains individual track messages that are all military/sensitive or all not military/sensitive. Similarly, a batched message contains individual track messages that are all authoritative or all not authoritative. All filtering of published data is performed by NEMS as described in the NEMS Interface Control Document (ICD) [see Reference 14].

In prior releases of SFDPS, the FIXM feed contained only authoritative messages. With this release, a FIXM message could also be a non-authoritative message, so that the FIXM feed contains the same messages as the Simple XML feed.

### **5.3 Messages**

This section describes messages and data properties for the four En Route data publication services supported by SFDPS Java Messaging services. The tables below show crossreferences to the subsection which contains the message’s detailed description.

|**EN ROUTE FLIGHT DATA PUBLICA**|**TION [Section 5.3.1]**||
|---|---|---|
|**Message Name**|**Message Code**|**Subsection**|
|Flight Plan Information|FH/FH_FIXM|5.3.1.1|
|Flight Amendment Information|AH/AH_FIXM|5.3.1.2|
|Converted Route Information|HX/HX_FIXM|5.3.1.3|
|Cancellation Information|CL/CL_FIXM|5.3.1.4|
|Departure Information|DH/DH_FIXM|5.3.1.5|
|Aircraft Identification Amendment Information|IH/IH_FIXM|5.3.1.6|
|Hold Information|HH/HH_FIXM|5.3.1.7|
|Progress Report Information|PH/PH_FIXM|5.3.1.8|
|Flight Arrival Information|HV/HV_FIXM|5.3.1.9|
|Flight Plan Update Information|HU/HU_FIXM|5.3.1.10|
|Expected Departure Time Information<sup>1</sup>|ET/ET_FIXM|5.3.1.11|
|Position Update Information|HP/HP_FIXM|5.3.1.12|
|Tentative Flight Plan Information|NP/NP_FIXM|5.3.1.13|
|Tentative Aircraft Identification Amendment<br>Information|NI/NI_FIXM|5.3.1.14|

> 1 This message could be phased out once it becomes available from its primary source (for ET, this would be TFMS; for HZ, this would be ARTS/STARS).

17

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**EN ROUTE FLIGHT DATA PUBLIC**|**ATION [Section 5.3.1]**||
|---|---|---|
|**Message Name**|**Message Code**|**Subsection**|
|Tentative Flight Plan Removal|NL/NL_FIXM|5.3.1.15|
|Tentative Flight Plan Amendment Information|NU/NU_FIXM|5.3.1.16|
|Batch Track Information|BATCH_TH/<br>BATCH_TH_FIXM|5.3.1.17|
|Drop Track Information|RH/RH_FIXM|5.3.1.18|
|Interim Altitude Information|LH/LH_FIXM|5.3.1.19|
|Automated Radar Terminal System (ARTS) Flow<br>Control Track/Full Data Block Information<sup>1</sup>|HZ/HZ_FIXM|5.3.1.20|
|Beacon Code Reassignment|BA/BA_FIXM|5.3.1.21|
|Beacon Code Restricted|RE/RE_FIXM|5.3.1.22|
|FDB Fourth Line Information|HF/HF_FIXM|5.3.1.23|
|Point Out Information|HT/HT_FIXM|5.3.1.24|
|Inbound Point Out Information|PT/PT_FIXM|5.3.1.25|
|Handoff Status|OH/OH_FIXM|5.3.1.26|
|Flight Plan Reconstitution Message|DBRTFPI/<br>DBRTFPI_FIXM|5.3.1.27|
|Flight Data Properties|---|5.3.1.28|

|**EN ROUTE AIRSPACE DATA PU**|**BLICATION [Section 5.3.2**<br>|**]**<br>|
|---|---|---|
|**Message Name**|**Message Code**|**Sub-section**|
|Sector Assignment Status|SH/SH_AIXM|5.3.2.1|
|Route Status|HR/HR_AIXM|5.3.2.2|
|Special Activities Airspace (SAA)|SU/SU_AIXM|5.3.2.3|
|Altimeter Setting|HA|5.3.2.4|
|Adapted Route Status Reconsititution|DBRTRI/<br>DBRTRI_AIXM|5.3.2.5|
|Altimeter Status Reconstitution|DBRTAI|5.3.2.6|
|Sector Assignment Reconstitution|DBRTSI/<br>DBRTSI_AIXM|5.3.2.7|
|Airspace Data Properties|---|5.3.2.8|

18

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**EN ROUTE OPERATIONAL DATA P**<br>|**UBLICATION [Section 5.3.**<br>|**3]**<br>|
|---|---|---|
|**Message Name**|**Message Code**|**Sub-section**|
|Traffic Count Adjustment|AK|5.3.3.1|
|Instrument Approach Count Adjustment|AC|5.3.3.2|
|Sign In Sign Out|SY|5.3.3.3|
|Beacon code Utilization|UB|5.3.3.4|
|Geographic Beacon Code Utilization|UG|5.3.3.5|
|Operational Data Properties|---|5.3.3.6|

|**EN ROUTE GENERAL MESSAGE P**|**UBLICATION [Section 5.3.**|**4]**|
|---|---|---|
|**Message Name**|**Message Code**|**Sub-section**|
|General Information|GH|5.3.4.1|
|Interim Altitude Status Information|HE|5.3.4.2|
|Hold Status Information|HO|5.3.4.3|
|ERAM Status Information|HS|5.3.4.4|
|Unsuccessful Transmission Information|UI|5.3.4.5|
|General Message Properties|---|5.3.4.6|

#### **5.3.1 Flight Data Publication Service Messages**

Frequency estimates provided are based on data received from the operational SFDPS on August 10<sup>th</sup> , 2015.

##### **5.3.1.1 Flight Plan Information: FH, FH_FIXM**

||**Flight Plan Information: FH, FH_FIXM**|
|---|---|
|**Message Name**|Flight Plan Information: FH, FH_FIXM|
|**Message Description**|The Flight Plan Message is sent to transfer active and proposed flight<br>plan data. It is generally sent when an ERAM at an ARTCC first<br>creates a new flight record for a flight. Multiple ARTCCs send copies<br>of the same flight plan. A single ARTCC may have multiple flight<br>plans for one flight, although only one should ever be active.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|N/A|

19

NAS-JMSDD-4309-001 Rev C July 10, 2018

||**Flight Plan Information: FH, FH_FIXM**|
|---|---|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|26.3/sec (Avg), 61/sec (Peak)|
|**Minimum/Maximum Size of**<br>**message in Simple XML Format**<br>**(FH) (bytes)**|3472/5617|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(FH_FIXM) (bytes)**|2524/13858|

##### **5.3.1.2 Flight Amendment Information: AH, AH_FIXM**

|**Flig**|**ht Amendment Information: AH, AH_FIXM**|
|---|---|
|**Message Name**|Flight Amendment Information: AH, AH_FIXM|
|**Message Description**|The Flight Amendment Message is used to resend all data/fields in<br>the Flight Plan Information message when an amendment has been<br>made to one or more of those fields.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|3/sec (Avg), 108/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(AH) (bytes)**|3185/5610|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(AH_FIXM) (bytes)**|2571/13857|

20

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.3.1.3 Converted Route Information: HX, HX_FIXM**

|**Co**|**nverted Route Information: HX, HX_FIXM**|
|---|---|
|**Message Name**|Converted Route Information: HX, HX_FIXM|
|**Message Description**|The Converted Route Message is sent to provide the fixes along the<br>route and calculated time of arrival at each fix, as computed by<br>ERAM. It should be re-sent whenever an FH, AH, DH, or HU is sent.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|4.1/sec (Avg), 107/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(HX) (bytes)**|2812/10947|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(HX_FIXM) (bytes)**|1585/9558|

##### **5.3.1.4 Cancellation Information: CL, CL_FIXM**

||**Cancellation Information: CL, CL_FIXM**|
|---|---|
|**Message Name**|Cancellation Information: CL, CL_FIXM|
|**Message Description**|The Cancellation Message is sent when a flight plan record is<br>canceled within a particular ARTCC’s ERAM. This means that no<br>more data is sent from that center for that flight plan.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.9/sec (Avg), 27/sec (Peak)|

21

NAS-JMSDD-4309-001 Rev C July 10, 2018

||**Cancellation Information: CL, CL_FIXM**|
|---|---|
|**Minimum/Maximum Size of**|2488/2716|
|**Message in Simple XML format**<br>**(CL) (bytes)**||
|**Minimum/Maximum Size of**|1140/2103|
|**Message in FIXM Format**||
|**(CL_FIXM) (bytes)**||

##### **5.3.1.5 Departure Information: DH, DH_FIXM**

||**Departure Information: DH, DH_FIXM**|
|---|---|
|**Message Name**|Departure Information: DH, DH_FIXM|
|**Message Description**|Departure Message – Provides departure related data for a flight<br>plan. If the flight plan was proposed, the DH indicates the flight is<br>now active.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.3/sec (Avg), 6/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(DH) (bytes)**|2753/3963|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(DH_FIXM) (bytes)**|1448/2503|

##### **5.3.1.6 Aircraft Identification Amendment Information: IH, IH_FIXM**

|**Aircraft Ide**|**ntification Amendment Information: IH, IH_FIXM**|
|---|---|
|**Message Name**|Aircraft Identification Amendment Information: IH, IH_FIXM|
|**Message Description**|The Aircraft Identifier Amendment Message is sent to indicate a<br>change to the flight identification field (**flightId_02a**) or assignment<br>of computer identification (**computerId_02d**) for a flight.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|

22

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Aircraft Id**|**entification Amendment Information: IH, IH_FIXM**|
|---|---|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|9.5/hour (Avg), 2/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(IH) (bytes)**|2635/2817|
|**Minimum/Maximum Size of**<br>**message in FIXM Format**<br>**(IH_FIXM) (bytes)**|1263/1960|

##### **5.3.1.7 Hold Information: HH, HH_FIXM**

||**Hold Information: HH, HH_FIXM**|
|---|---|
|**Message Name**|Hold Information: HH, HH_FIXM|
|**Message Description**|The Hold Message indicates a hold of a definite duration, an<br>indefinite hold, or hold release for a specified flight.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.6/min (Avg), 3/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(HH) (bytes)**|2434/2710|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(HH_FIXM) (bytes)**|1090/2466|

23

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.3.1.8 Progress Report Information: PH, PH_FIXM**

|**Pr**|**ogress Report Information: PH, PH_FIXM**|
|---|---|
|**Message Name**|Progress Report Information: PH, PH_FIXM|
|**Message Description**|The Progress Report Message is sent from ERAM to update the<br>position for an active flight, or to release it from a prior hold status.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.46/hour (Avg), 1/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(PH) (bytes)**|2681/2721|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(PH_FIXM) (bytes)**|1000/1500|

##### **5.3.1.9 Flight Arrival Information: HV, HV_FIXM**

||**Flight Arrival Information: HV, HV_FIXM**|
|---|---|
|**Message Name**|Flight Arrival Information: HV, HV_FIXM|
|**Message Description**|The Flight Arrival Message provides arrival data from ERAM for any<br>arriving flight.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.3/sec (Avg), 7/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**|2537/2756|

24

NAS-JMSDD-4309-001 Rev C July 10, 2018

||**Flight Arrival Information: HV, HV_FIXM**|
|---|---|
|**(HV) (bytes)**||
|**Minimum/Maximum Size of**|1373/2158|
|**Message in FIXM Format**||
|**(HV_FIXM) (bytes)**||

##### **5.3.1.10 Flight Plan Update Information: HU, HU_FIXM**

|**Flig**|**ht Plan Update Information: HU, HU_FIXM**|
|---|---|
|**Message Name**|Flight Plan Update Information: HU, HU_FIXM|
|**Message Description**|The Flight Plan Update Message is sent to provide the latest flight<br>plan data on an active flight when a new ARTCC assumes control of<br>that flight.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.5/sec (Avg), 7/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(HU) (bytes)**|3234/5065|
|**Minimum/Maximum Size of**<br>**message in FIXM Format**<br>**(HU_FIXM) (bytes)**|2789/13857|

##### **5.3.1.11 Expected Departure Time Information: ET, ET_FIXM**

|**Expec**|**ted Departure Time Information: ET, ET_FIXM**|
|---|---|
|**Message Name**|Expected Departure Time Information: ET, ET_FIXM|
|**Message Description**|The Expected Departure Time Message provides Estimated<br>Departure Clearance Time (EDCT) information; that is, the assigned<br>departure time for a proposed flight plan inbound to a controlled<br>airport with a ground delay in effect, and is used to cancel a<br>previously issued EDCT. The original source of this data is TFMS.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|

25

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Expec**|**ted Departure Time Information: ET, ET_FIXM**|
|---|---|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|1.2/min (Avg), 21/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(ET) (bytes)**|2435/2658|
|**Minimum/Maximum Size of**<br>**message in FIXM Format**<br>**(ET_FIXM) (bytes)**|2157/2167|

##### **5.3.1.12 Position Update Information: HP, HP_FIXM**

|**Po**|**sition Update Information: HP, HP_FIXM**|
|---|---|
|**Message Name**|Position Update Information: HP, HP_FIXM|
|**Message Description**|The Position Update Message is sent to update the coordination<br>time on an active flight when the present position fix time is<br>updated.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|4.2/sec (Avg), 52/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(HP) (bytes)**|2588/2849|
|**Minimum/Maximum Size of**<br>**message in FIXM Format**<br>**(HP_FIXM) (bytes)**|1188/2147|

26

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.3.1.13 Tentative Flight Plan Information: NP, NP_FIXM**

|**Tent**|**ative Flight Plan Information: NP, NP_FIXM**|
|---|---|
|**Message Name**|Tentative Flight Plan Information: NP, NP_FIXM|
|**Message Description**|The Tentative Flight Plan Message is sent when a controller creates a<br>temporary, partial set of flight plan data and associates it with a<br>flight. It includes the source, flight identification, and may include<br>optional UFPI (ERAM-GUFI), aircraft data, type of aircraft, airborne<br>equipment qualifier, beacon code, speed, assigned altitude,<br>reported altitude, and interim altitude. Often, many of these fields<br>are missing. A tentative flight plan may be either canceled or merged<br>with a real flight plan (FH). In the latter case, the FH might have the<br>same Site Specific Plan Identifier (**sspId_167a**) and Computer ID<br>(**computerId_02d**) as the NP, or it may be different. An NP can be<br>issued only for an active flight.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.6/min (Avg), 3/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(NP) (bytes)**|2614/2818|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(NP_FIXM) (bytes)**|1058/1291|

##### **5.3.1.14 Tentative Aircraft Identification Amendment Information: NI, NI_FIXM**

|**Tentative Aircra**|**ft Identification Amendment Information: NI, NI_FIXM**|
|---|---|
|**Message Name**|Tentative Aircraft Identification Amendment Information: NI,<br>NI_FIXM|
|**Message Description**|The Tentative Aircraft Identifier Amendment Message is sent from<br>ERAM to indicate a change to the flight identification field<br>(**flightId_02a**) of a tentative flight plan.|
|**Message Property Descriptions**|Refer to Table 5-1, below|

27

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Tentative Aircra**|**ft Identification Amendment Information: NI, NI_FIXM**|
|---|---|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|23/day (Avg), 1/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(NI) (bytes)**|2612/2619|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(NI_FIXM) (bytes)**|1345/1348|

##### **5.3.1.15 Tentative Flight Plan Removal: NL, NL_FIXM**

|**Te**|**ntative Flight Plan Removal: NL, NL_FIXM**|
|---|---|
|**Message Name**|Tentative Flight Plan Removal: NL, NL_FIXM|
|**Message Description**|The Tentative Flight Plan Removal Message is sent to indicate the<br>removal of a tentative flight plan; may indicate that the tentative<br>flight plan has been merged with a normal flight plan.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.6/min (Avg), 2/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(NL) (bytes)**|2434/2761|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(NL_FIXM) (bytes)**|1308/1924|

28

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.3.1.16 Tentative Flight Plan Amendment Information: NU, NU_FIXM**

|**Tentative F**|**light Plan Amendment Information: NU, NU_FIXM**|
|---|---|
|**Message Name**|Tentative Flight Plan Amendment Information: NU, NU_FIXM|
|**Message Description**|The Tentative Flight Amendment Message is used to update<br>tentative flight plan data.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|7.4/hour (Avg), 2/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(NU) (bytes)**|2480/2763|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(NU_FIXM) (bytes)**|1375/2989|

##### **5.3.1.17 Batch Track Information: BATCH_TH, BATCH_TH_FIXM**

|**Batch Tr**|**ack Information: BATCH_TH, BATCH_TH_FIXM**|
|---|---|
|**Message Name**|Batch Track Information: BATCH_TH, BATCH_TH_FIXM|
|**Message Description**|The Batch Track Message includes multiple individual Track<br>Messages. The single Track message provides track data/target<br>information, such as aircraft track/target position, altitude, and<br>speed. It is normally sent every 12 seconds for an active flight.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency of Message**<br>**in Simple XML format**|114/sec|

29

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Batch Tr**<br>|**ack Information: BATCH_TH, BATCH_TH_FIXM**|
|---|---|
|**(BATCH_TH)**||
|**Estimated Frequency of Message**<br>**in FIXM Format**<br>**(BATCH_TH_FIXM)**|109/sec|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(BATCH_TH) (bytes)**|893/199,503|
|**Minimum/Maximum Size of**|2187/284,851|
|**Message in FIXM Format**||
|**(BATCH_TH_FIXM) (bytes)**||

##### **5.3.1.18 Drop Track Information: RH, RH_FIXM**

||**Drop Track Information: RH, RH_FIXM**|
|---|---|
|**Message Name**|Drop Track Information: RH, RH_FIXM|
|**Message Description**|The Drop Track Message indicates that an ARTCC has discontinued<br>tracking of a particular flight.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.4/sec (Avg), 6/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(RH) (bytes)**|2384/2602|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(RH_FIXM) (bytes)**|993/2097|

##### **5.3.1.19 Interim Altitude Information: LH, LH_FIXM**

||**Interim Altitude Information: LH, LH_FIXM**|
|---|---|
|**Message Name**|Interim Altitude Information: LH, LH_FIXM|
|**Message Description**|The Interim Altitude Message provides an ATM Intermediate Point<br>of Presence (IPOP) with interim altitude data for a flight.|

30

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**In**|**terim Altitude Information: LH, LH_FIXM**|
|---|---|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|1.7/sec (Avg), 19/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(LH) (bytes)**|2425/2643|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(LH_FIXM) (bytes)**|1050/2161|

##### **5.3.1.20 ARTS Flow Control Track/Full Data Block Information: HZ, HZ_FIXM**

|**Automated Radar Terminal**|**System (ARTS) Flow Control Track/Full Data Block  Information: HZ,**<br>**HZ_FIXM**|
|---|---|
|**Message Name**|ARTS Flow Control Track/Full Data Block Information: HZ, HZ_FIXM|
|**Message Description**|The ARTS TZ Flow Control Track/Full Data Block (FDB) Message<br>provides a position update from an ARTS; this is a data pass-through.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|3.3/sec (Avg), 36/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(HZ) (bytes)**|2597/2819|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(HZ_FIXM) (bytes)**|1631/2746|

31

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.3.1.21 Beacon Code Reassignment: BA, BA_FIXM**

|**B**|**eacon Code Reassignment: BA, BA_FIXM**|
|---|---|
|**Message Name**|Beacon Code Reassignment: BA, BA_FIXM|
|**Message Description**|The Beacon Code Reassignment Message provides an updated<br>beacon code for a flight plan when ERAM determines that an<br>automatic beacon code reassignment occurred because the<br>requested beacon code was already in use by another aircraft.<br>The FDPS_Restricted property on this type of message has a value of<br>‘R’ when the flightState element has a value of ‘Canceled’ or<br>‘Proposed’ (BA), or the flight/flightStatus/@fdpsFlightStatus<br>attribute has a value of ‘CANCELED or ‘PROPOSED (BA_FIXM),<br>indicating that for non-active flights, this type of message can only<br>be shared with users authorized to receive beacon code data. If the<br>flight associated with this type of message is active, the<br>FDPS_Restricted property has a value of ‘A’ and can be shared with<br>all consumers otherwise authorized to receive this message based<br>on the FDPS_Sensitive flag.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.1/sec (Avg), 5/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(BA) (bytes)**|2764/2933|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(BA_FIXM) (bytes)**|1408/2309|

##### **5.3.1.22 Beacon Code Restricted: RE, RE_FIXM**

||**Beacon Code Restricted: RE, RE_FIXM**|
|---|---|
|**Message Name**|Beacon Code Restricted: RE, RE_FIXM|
|**Message Description**|The Beacon Code Restricted Message provides an updated beacon<br>code for a flight when ERAM determines that a beacon code<br>reassignment occurred because the requested beacon code is<br>adapted as restricted.|

32

NAS-JMSDD-4309-001 Rev C July 10, 2018

||**Beacon Code Restricted: RE, RE_FIXM**|
|---|---|
||The FDPS_Restricted property on this type of message has a value of<br>‘R’ when the flightState element has a value of ‘Canceled’ or<br>‘Proposed’ (RE), or the flight/flightStatus/@fdpsFlightStatus<br>attribute has a value of ‘CANCELED or ‘PROPOSED (RE_FIXM),<br>indicating that for non-active flights, this type of message can only<br>be shared with users authorized to receive beacon code data. If the<br>flight associated with this type of message is active, the<br>FDPS_Restricted property has a value of ‘A’ and can be shared with<br>all consumers otherwise authorized to receive this message based<br>on the FDPS_Sensitive flag.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|5.3/hour (Avg), 2/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(RE) (bytes)**|2828/2985|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(RE_FIXM) (bytes)**|1473/2373|

##### **5.3.1.23 FDB Fourth Line Information: HF, HF_FIXM**

|**F**|**DB Fourth Line Information: HF, HF_FIXM**|
|---|---|
|**Message Name**|FDB Fourth Line Information: HF, HF_FIXM|
|**Message Description**|The FDB Fourth Line Message is used to send the displayable, user-<br>specified FDB fourth line data stored in ERAM; this can be heading,<br>speed, or free-form text.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|

33

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**F**|**DB Fourth Line Information: HF, HF_FIXM**|
|---|---|
|**Message Body Type**|Text|
|**Estimated Frequency**|.9/sec (Avg), 10/sec (Peak0|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(HF) (bytes)**|2383/2713|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(HF_FIXM) (bytes)**|994/2283|

##### **5.3.1.24 Point Out Information: HT, HT_FIXM**

||**Point Out Information: HT, HT_FIXM**|
|---|---|
|**Message Name**|Point Out Information: HT, HT_FIXM|
|**Message Description**|The Point Out Message provides inter-facility and intra-facility point<br>out information when these actions occur.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.3/sec (Avg), 10/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(HT) (bytes)**|2493/2796|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(HT_FIXM) (bytes)**|1366/2585|

##### **5.3.1.25 Inbound Point Out Information: PT, PT_FIXM**

|**Inb**|**ound Point Out Information: PT, PT_FIXM**|
|---|---|
|**Message Name**|Inbound Point Out Information: PT, PT_FIXM|
|**Message Description**|The Inbound Point Out Message is sent by ERAM upon receipt of an<br>inter-facility point out message from another center.|
|**Message Property Descriptions**|Refer to Table 5-1, below|

34

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Inb**|**ound Point Out Information: PT, PT_FIXM**|
|---|---|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|1.2/min (Avg), 2/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(PT) (bytes)**|2624/2835|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(PT_FIXM) (bytes)**|1368/2468|

##### **5.3.1.26 Handoff Status: OH, OH_FIXM**

|**H**|**andoff Status: OH, OH_FIXM**|
|---|---|
|**Message Name**|Handoff Status: OH, OH_FIXM|
|**Message Description**|The Handoff Status Message is sent when a handoff is<br>initiated, accepted, control is taken away (assert control), or<br>retracted, or when the failure of handoff is detected. It<br>includes field**handoffEventIndicator_336a**, a single letter<br>value, where the letter stands for:**I**= Initiation;**A**=<br>Acceptance;**R**= Retraction;**T**= Take Control (Assert Control);<br>**U**= Update;**F**= Failure|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|6.1/sec (Avg), 73/sec (Peak)|
|**Minimum/Maximum Size of Message**<br>**in Simple XML format (OH) (bytes)**|2687/3019|
|**Minimum/Maximum Size of Message**<br>**in FIXM Format (OH_FIXM) (bytes)**|1532/2764|

35

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.3.1.27 Flight Plan Reconstitution: DBRTFPI, DBRTFPI_FIXM**

|**Flight**|**Plan Reconstitution: DBRTFPI, DBRTFPI_FIXM**|
|---|---|
|**Message Name**|Flight Plan Reconstitution: DBRTFPI, DBRTFPI_FIXM|
|**Message Description**|The Flight Plan Reconstitution Message is sent when a client first<br>connects to a HADDS or when it reconnects to a HADDS after<br>communication between the client and HADDS is disrupted.|
|**Message Property Descriptions**|Refer to Table 5-1, below|
|**Permissible Property Values**|Refer to Table 5-1, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-1, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.6/min (Avg), 293/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(DBRTFPI) (bytes)**|2779/8039|
|**Minimum/Maximum Size of**<br>**Message in FIXM Format**<br>**(DBRTFPI_FIXM) (bytes)**|1066/12942|

##### **5.3.1.28 Flight Data Properties**

**Table 5-1: Flight Data Properties**

|**Property Name**|**Description**|**Permissible Values**|
|---|---|---|
|FDPS_SourceFacility|This property,<br>of type String,<br>indicates the<br>source, the<br>ARTCC, of the<br>CMS message<br>that caused this<br>message to be<br>published.|ZAB, ZAU, ZBW, ZDC, ZDV, ZFW, ZHU, ZID, ZJX, ZKC, ZLA, ZLC,<br>ZMA, ZME, ZMP, ZNY, ZOA, ZOB, ZSE, ZTL|

36

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Property Name**|**Description**|**Permissible Values**|
|---|---|---|
|FDPS_SourceSystem|This property,<br>of type String,<br>indicates the<br>specific<br>instance of<br>SFDPS that<br>published the<br>message. A<br>change in the<br>value of this<br>property<br>indicates that<br>the producer<br>has switched<br>from one site to<br>the other.|ATL, SLC|
|FDPS_MessageType|This property,<br>of type String,<br>indicates the<br>type of<br>message|FH, AH, HX, CL, DH, IH, HH, PH, HV, HU, ET, HP, NP, NI, NL,<br>NU, BATCH_TH, RH, LH, HZ, BA, RE, HF, HT, PT, OH,<br>FH_FIXM, AH_FIXM, HX_FIXM, CL_FIXM, DH_FIXM, IH_FIXM,<br>HH_FIXM, PH_FIXM, HV_FIXM, HU_FIXM, ET_FIXM,<br>HP_FIXM, NP_FIXM, NI_FIXM, NL_FIXM, NU_FIXM,<br>BATCH_TH_FIXM, RH_FIXM, LH_FIXM, HZ_FIXM, BA_FIXM,<br>RE_FIXM, HF_FIXM, HT_FIXM, PT_FIXM, OH_FIXM, DBRTFPI,<br>DBRTFPI_FIXM|
|FDPS_FlightOperator|This property,<br>of type String,<br>indicates the<br>operator of the<br>flight that<br>caused this<br>message to be<br>published.|While this property may contain any code or none, only<br>those listed below are available for routing due to<br>limitations of NEMS:<br>DAL,SWA,UAL,AAL,USA,ASQ,JBU,SKW,  TRS,<br>ASA,WJA,NKS,FFT,HAL,AAY,UPS,FDX<br>This property is not available as a JMS property for the<br>BATCH_TH and BATCH_TH_FIXM messages. However, for<br>the SimpleXML formatted messages, it is available as an<br>SFDPS property (propFlightOperator) of each individual<br>Track message within the BATCH_TH message. For the FIXM<br>formatted messages, it is specified as an attribute in each<br>individual Track message within the BATCH_TH_FIXM<br>message:<br>_flight/operator/operatingOrganization/organization/@nam_<br>_e_.|

37

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Property Name**|**Description**|**Permissible Values**|
|---|---|---|
|FDPS_Origin|This property,<br>of type String,<br>indicates the<br>originating<br>airport of the<br>flight to which<br>this message<br>applies.|While this property may contain any destination or none,<br>only those listed below are available for routing due to<br>limitations of NEMS:<br>KATL,KBOS,KBWI,KCLE,KCLT,KCVG,<br>KDCA,KDEN,KDFW,KDTW,KEWR,KFLL,<br>KHNL,KIAD,KIAH,KJFK,KLAS,KLAX,<br>KLGA,KMCO,KMDW,KMEM,KMIA,KMSP,<br>KORD,KPDX,KPHL,KPHX,KPIT,KSAN,KSEA,<br>KSFO,KSLC,KSTL,KTPA<br>This property is not available as a JMS property for the<br>BATCH_TH and BATCH_TH_FIXM messages. For the<br>SimpleXML formatted messages, it is specified as a property<br>(propOrigin) of each individual Track message within the<br>BATCH_TH message. For the FIXM formatted messages, it is<br>specified as an attribute in each individual Track message<br>within the BATCH_TH_FIXM message:<br>_flight/departure/@departurePoint_.|
|FDPS_DestId|This property,<br>of type String,<br>indicates the<br>destination<br>airport of the<br>flight to which<br>this message<br>applies.|While this property may contain any destination or none,<br>only those listed below are available for routing due to<br>limitations of NEMS:<br>KATL,KBOS,KBWI,KCLE,KCLT,KCVG,<br>KDCA,KDEN,KDFW,KDTW,KEWR,KFLL,<br>KHNL,KIAD,KIAH,KJFK,KLAS,KLAX,<br>KLGA,KMCO,KMDW,KMEM,KMIA,KMSP,<br>KORD,KPDX,KPHL,KPHX,KPIT,KSAN,KSEA,<br>KSFO,KSLC,KSTL,KTPA<br>This property is not available as a JMS property for the<br>BATCH_TH and BATCH_TH_FIXM messages. For the<br>SimpleXML formatted messages, it is specified as a property<br>(propDestination) of each individual Track message within<br>the BATCH_TH message. For the FIXM formatted messages,<br>it is specified as an attribute in each individual Track<br>message within the BATCH_TH_FIXM message:<br>_flight/arrival/@arrivalPoint_.|

38

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Property Name**|**Description**|**Permissible Values**|
|---|---|---|
|FDPS_Sensitive|This property,<br>of type<br>Boolean,<br>indicates<br>whether the<br>flight to which<br>this message<br>applies is<br>military/sensitiv<br>e or not.|TRUE – The flight is military/sensitive<br>FALSE – The flight is neither military nor sensitive|
|FDPS_Authoritative|This property,<br>of type<br>Boolean,<br>indicates<br>whether the<br>CMS message<br>that caused this<br>message to be<br>published was<br>sent from an<br>Source Facility<br>or ARTCC that<br>was the<br>authoritative or<br>controlling<br>Center of the<br>flight.|TRUE – The CMS message came from the controlling center<br>FALSE – The CMS message did not come from the<br>controlling center|
|FDPS_Recon|This property,<br>of type<br>Boolean,<br>indicates<br>whether this<br>message was<br>generated as<br>the result of a<br>data<br>reconstitution.|TRUE – The message was generated as the result of a data<br>reconstitution.<br>FALSE – The message was not generated as the result of a<br>data reconstitution.<br>Value is set only for reconsisitution messages, DBRTFPI,<br>DBRTPFI_FIXM.|
|FDPS_DataType|This property,<br>of type String,<br>indicates the<br>type of data<br>publication this<br>message is part<br>of.|FlightSimpleXML, FlightFIXM|

39

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Property Name**|**Description**|**Permissible Values**|
|---|---|---|
|FDPS_OneMinFreq|This property,<br>of type String,<br>indicates<br>whether a track<br>message was<br>sent at one-<br>minute<br>intervals or at<br>twelve-second<br>intervals.|TRUE – The track message was sent at a one-minute<br>interval.<br>FALSE- the track message was sent at a 12-second interval.|
|FDPS_Restricted|This property,<br>of type String,<br>indicates<br>whether a<br>message can be<br>shared with all<br>users, only<br>users<br>authorized to<br>receive beacon<br>code<br>information on<br>proposed and<br>canceled flights,<br>or only users<br>not authorized<br>to receive<br>beacon code<br>information on<br>proposed and<br>active flights.|1. A – the message can be received by All<br>consumers; it contains no beacon codes or is<br>post-departure<br>2. R – the message is Restricted to only<br>consumers authorized to receive the<br>message; it is a pre-departure message with<br>a beacon code<br>3. D – the beacon code has been removed<br>(Desensitized) and so the message can be<br>received by consumers not otherwise<br>authorized to receive it<br>Note: The FDPS_Sensitive property still applies, and a<br>message marked sensitive  (FDPS_Sensitive = ‘true’) will only<br>be shared with users authorized to receive sensitive data,<br>even if the value in the FDPS_Restricted property is ‘A’ or<br>‘D’.|

#### **5.3.2 Airspace Data Publication Service Messages**

##### **5.3.2.1 Sector Assignment Status: SH, SH_AIXM**

||**Sector Assignment Status: SH, SH_AIXM**|
|---|---|
|**Message Name**|Sector Assignment Status: SH, SH_AIXM|
|**Message Description**|The Sector Assignment Status Message is used to communicate<br>current sector and TRACON configurations. A sector or TRACON may<br>either be closed or open. If the sector or TRACON is open, it is<br>composed of one or more FAVs.|

40

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**S**|**ector Assignment Status: SH, SH_AIXM**|
|---|---|
|**Message Property Descriptions**|Refer to Table 5-2, below|
|**Permissible Property Values**|Refer to Table 5-2, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-2, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|1.2/min (Avg), 6/sec (Peak)|
|**Minimum/Maximum Size of the**<br>**Message in Simple XML Format**<br>**(SH) (bytes)**|8325/16677|
|**Minimum/Maximum Size of the**<br>**Message in AIXM Format**<br>**(SH_AIXM) (bytes)**|60760/115008|

##### **5.3.2.2 Route Status: HR, HR_AIXM**

||**Route Status: HR, HR_AIXM**|
|---|---|
|**Message Name**|Route Status: HR, HR_AIXM|
|**Message Description**|A Route Status message is used to communicate whether some<br>adapted departure and/or arrival routes are active or not. A route<br>status is indicated by the route name followed by either “ON” or<br>“OFF.”<br>ERAM generates an HR when an assignment at a center changes, or<br>when reconstituting data. A single HR contains only route<br>assignments for that one center, and can include one or more<br>routes.|
|**Message Property Descriptions**|Refer to Table 5-2, below|
|**Permissible Property Values**|Refer to Table 5-2, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-2, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|12/hour (Avg), 9/sec (Peak)|
|**Minimum/Maximum Size of**<br>**Message in Simple XML format**<br>**(HR) (bytes)**|1885/38401|

41

NAS-JMSDD-4309-001 Rev C July 10, 2018

||**Route Status: HR, HR_AIXM**|
|---|---|
|**Minimum/Maximum Size of**|4845/993377|
|**Message in AIXM format**||
|**(HR_AIXM) (bytes)**||

##### **5.3.2.3 Special Activities Airspace (SAA): SU, SU_AIXM**

|**Spe**|**cial Activities Airspace (SAA): SU, SU_AIXM**|
|---|---|
|**Message Name**|Special Activities Airspace (SAA): SU, SU_AIXM|
|**Message Description**|The SAA Information message provides the status and schedules for<br>the SAA.|
|**Message Property Descriptions**|Refer to Table 5-2, below|
|**Permissible Property Values**|Refer to Table 5-2, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-2, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|31/hour (Avg), 7/sec (Peak)|
|**Minimum/Maximum Size of the**<br>**Message in Simple XML Format**<br>**(SU) (bytes)**|1821/6063|
|**Minimum/Maximum Size of the**<br>**Message in AIXM Format**<br>**(SU_AIXM)  (bytes)**|2224/24225|

##### **5.3.2.4 Altimeter Setting: HA**

||**Altimeter Setting: HA**|
|---|---|
|**Message Name**|Altimeter Setting: HA|
|**Message Description**|An Altimeter-Setting message is used to communicate altimeter<br>reference data for a particular station, generally an airport. The<br>altimeter reference data includes the data reporting time (35a), the<br>reporting station (13.3), and the altimeter setting (34a).<br>ERAM generates an HA when an altimeter setting is processed.<br>ERAM receives most altimeter settings from the Weather Message<br>Switching Center Replacement (WMSCR), but occasionally a value<br>might be entered by a controller. Either source causes ERAM to<br>generate an HA message; there is no way to distinguish the source.|

42

NAS-JMSDD-4309-001 Rev C July 10, 2018

||**Altimeter Setting: HA**|
|---|---|
||ERAM at an ARTCC may receive altimeter data for many stations,<br>both internal and external to that ARTCC. As a result, SFDPS may<br>receive multiple copies of altimeter setting data for a particular<br>station. For example, SFDPS could receive HA messages from ZBW,<br>ZNY, ZDC, ZOB, ZTL, and ZLA for the airport DCA. In almost all cases,<br>these messages are copies of the same data; that is, they have the<br>same data reporting time and altimeter setting.|
|**Message Property Descriptions**|Refer to Table 5-2, below|
|**Permissible Property Values**|Refer to Table 5-2 , below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-2, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.9/sec (Avg), 578/sec (Peak)|
|**Minimum/Maximum Size of the**<br>**Message in Simple XML Format**<br>**(bytes)**|1835/1900|

##### **5.3.2.5 Adapted Route Status Reconstitution:  DBRTRI, DBRTRI_AIXM**

|**Adapted Ro**|**ute Status Reconstitution:  DBRTRI, DBRTRI_AIXM**|
|---|---|
|**Message Name**|Adapted Route Status Reconstitution: DBRTRI, DBRTRI_AIXM|
|**Message Description**|The Adapted Route Status Reconstitution message is sent when a<br>client first connects to a HADDS or when a client reconnects to a<br>HADDS due to a disruption in communication.|
|**Message Property Descriptions**|Refer to Table 5-2, below|
|**Permissible Property Values**|Refer to Table 5-2 , below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-2, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.1/sec (Avg), 2091/sec (Peak)|
|**Minimum/Maximum Size of the**<br>**Message in Simple XML Format**<br>**(DBRTRI) (bytes)**|1919/1922|
|**Minimum/Maximum Size of the**<br>**Message in AIXM Format**|4858/4860|

43

NAS-JMSDD-4309-001 Rev C July 10, 2018

**Adapted Route Status Reconstitution:  DBRTRI, DBRTRI_AIXM**

**(DBRTRI_AIXM) (bytes)**

##### **5.3.2.6 Altimeter Status Reconstitution: DBRTAI**

|**A**|**ltimeter Status Reconstitution:  DBRTAI**|
|---|---|
|**Message Name**|Altimeter Status Reconstitution: DBRTAI|
|**Message Description**|The Altimeter Status Reconstitution message is sent when a client<br>first connects to a HADDS or when a client reconnects to a HADDS<br>due to a disruption in communication.|
|**Message Property Descriptions**|Refer to Table 5-2, below|
|**Permissible Property Values**|Refer to Table 5-2 , below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-2, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|.6/min (Avg), 229/sec (Peak)|
|**Minimum/Maximum Size of the**<br>**Message in Simple XML Format**<br>**(bytes)**|1902/1969|

##### **5.3.2.7 Sector Assignment Reconstitution: DBRTSI, DBRTSI_AIXM**

|**Sector As**|**signment Reconstitution: DBRTSI, DBRTRSI_AIXM**|
|---|---|
|**Message Name**|Sector Assignment Reconstitution: DBRTSI, DBRTSI_AIXM|
|**Message Description**|The Sector Assignment Reconstitution message is sent when a client<br>first connects to a HADDS or when a client reconnects to a HADDS<br>due to a disruption in communication.|
|**Message Property Descriptions**|Refer to Table 5-2, below|
|**Permissible Property Values**|Refer to Table 5-2 , below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-2, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|

44

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Sector Ass**|**ignment Reconstitution: DBRTSI, DBRTRSI_AIXM**|
|---|---|
|**Message Body Type**|Text|
|**Estimated Frequency**|11.1/hour (Avg), 65/sec (Peak)|
|**Minimum/Maximum Size of the**|1912/5779 9|
|**Message in Simple XML Format**<br>**(DBRTSI) (bytes)**||
|**Minimum/Maximum Size of the**|2166/9145|
|**Message in AIXM Format**<br>**(DBRTSI_AIXM) (bytes)**||

##### **5.3.2.8 Airspace Data Properties**

**Table 5-2: Airspace Data Properties**

|**Property Name**|**Description**|**Permissible Values**|
|---|---|---|
|FDPS_SourceFacility|This property, of type String,<br>indicates the source, the ARTCC,<br>of the CMS message that caused<br>this message to be published.|ZAB, ZAU, ZBW, ZDC, ZDV, ZFW,<br>ZHU, ZID, ZJX, ZKC, ZLA, ZLC,<br>ZMA, ZME, ZMP, ZNY, ZOA, ZOB,<br>ZSE, ZTL|
|FDPS_SourceSystem|This property, of type String,<br>indicates the specific instance of<br>SFDPS that published the<br>message. A change in the value<br>of this property indicates that<br>the producer has switched from<br>one site to the other.|ATL, SLC|
|FDPS_MessageType|This property, of type String,<br>indicates the type of message|SH, HR, HA, SU, SH_AIXM,<br>HR_AIXM, SU_AIXM,  DBRTSI,<br>DBRTAI, DBRTRI, DBRTSI_AIXM,<br>DBRTRI_AIXM|
|FDPS_Recon|This property, of type Boolean,<br>indicates whether this message<br>was generated as the result of a<br>data reconstitution.|TRUE – The message was<br>generated as the result of a data<br>reconstitution.<br>FALSE – The message was not<br>generated as the result of a data<br>reconstitution.<br>Value is set only on<br>reconstitution messages, DBRTSI,<br>DBRTAI, DBRTRI, DBRTSI_AIXM,<br>DBRTRI_AIXM|
|FDPS_DataType|This property, of type String,<br>indicates the type of data<br>publication of which this|ERADP, AirspaceAIXM|

45

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Property Name**|**Description**|**Permissible Values**|
|---|---|---|
||message is a part.||
|FDPS_Sensitive|This property, of type Boolean,<br>indicates whether the flight to<br>which this message applies is<br>military/sensitive or not.|FALSE – The flight is neither<br>military nor sensitive.  Even<br>though Airspace messages do<br>not have flight data, this<br>property must exist in order to<br>simplify NEMS filtering rules that<br>allow all users to receive the<br>data.|
|FDPS_Authoritative|This property, of type Boolean,<br>indicates whether the CMS<br>message that caused this<br>message to be published was<br>sent from an Source Facility or<br>ARTCC that was the authoritative<br>or controlling Center of the<br>flight.|TRUE – The CMS message came<br>from the controlling center<br>FALSE – The CMS message did<br>not come from the controlling<br>center|
|FDPS_Restricted|This property, of type String,<br>indicates whether a message can<br>be shared with all users, only<br>users authorized to receive<br>beacon code information on<br>proposed and canceled flights, or<br>only users not authorized to<br>receive beacon code information<br>on proposed and active flights.|This property has a value of ‘A’<br>for all airspace data messages,<br>indicating there is no beacon<br>code information in these<br>messages. This is just to simplify<br>NEMS filitering rules.<br>Note: The FDPS_Sensitive<br>property still applies, and a<br>message marked sensitive<br>(FDPS_Sensitive = ‘true’) will only<br>be shared with users authorized<br>to receive sensitive data, even<br>though the value in the<br>FDPS_Restricted property is ‘A’|

#### **5.3.3 Operational Data Publication Service Messages**

##### **5.3.3.1 Traffic Count Adjustment: AK**

||**Traffic Count Adjustment: AK**|
|---|---|
|**Message Name**|Traffic Count Adjustment: AK|
|**Message Description**|The Traffic Count Adjustment message is used to adjust (increment<br>or decrement) one of the following traffic counts:|
||•<br>ACDD (Air Carrier Domestic Departures)|

46

NAS-JMSDD-4309-001 Rev C July 10, 2018

||**Traf**|**fic Count Adjustment: AK**|
|---|---|---|
||•<br>•<br>•<br>•<br>•<br>•<br>•<br>•<br>•<br>•<br>•<br>•<br>•<br>•<br>•<br>•|ATDD (Air Taxi Domestic Departures)<br>GADD (General Aviation Domestic Departures)<br>MIDD (Military Domestic Departures)<br>ACDO (Air Carrier Domestic Overs)<br>ATDO (Air Taxi Domestic Overs)<br>GADO (General Aviation Domestic Overs)<br>MIDO (Military Domestic Overs)<br>ACOD (Air Carrier Oceanic Departures)<br>ATOD (Air Taxi Oceanic Departures)<br>GAOD (General Aviation Oceanic Departures)<br>MIOD (Military Oceanic Departures)<br>ACOO (Air Carrier Oceanic Overs)<br>ATOO (Air Taxi Oceanic Overs)<br>GAOO (General Aviation Oceanic Overs)<br>MIOO (Military Oceanic Overs)<br>VFRC (Visual Flight Rules [VFR] Traffic Count)|
|**Message Property Descriptions**|Refer t|o Table 5-3, below|
|**Permissible Property Values**|Refer t|o Table 5-3, below|
|**Message ID (if applicable)**|NA||
|**Filter Criteria**|Refer t|o Table 5-3, below|
|**Applicable Topic/Queue**|FDPSD|ATA.IN|
|**Delivery Mode**|Nonpe|rsistent|
|**Message Body Type**|Text||
|**Estimated Frequency**|2/hour|(Avg), 2/sec (Peak)|
|**Minimum/Maximum Size (bytes)**|1957/2|595|

##### **5.3.3.2 Instrument Approach Count Adjustment: AC**

||**Instrument Approach Count Adjustment: AC**|
|---|---|
|**Message Name**|Instrument Approach Count Adjustment: AC|
|**Message Description**|The Instrument Approach Count message is used to adjust<br>(increment or decrement) one of the following instrument approach<br>counts:|
||•<br>AC (air carrier)|
||•<br>AT (air taxi)|
||•<br>GA (general aviation)|

47

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Ins**|**trument Approach Count Adjustment: AC**|
|---|---|
||•<br>MI (military)|
|**Message Property Descriptions**|Refer to Table 5-3, below|
|**Permissible Property Values**|Refer to Table 5-3, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-3, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|1/hour (Avg), 8/sec (Peak)|
|**Minimum/Maximum Size (bytes)**|1987/1989|

48

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.3.3.3 Sign In Sign Out: SY**

||**Sign In Sign Out: SY**|
|---|---|
|**Message Name**|Sign In Sign Out: SY|
|**Message Description**|The Sign In Sign Out Information (SY) message is sent to the ATM<br>IPOP each time a sign in or sign out occurs, or when a reconstitution<br>request is received.|
|**Message Property Descriptions**|Refer to Table 5-3, below|
|**Permissible Property Values**|Refer to Table 5-3, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-3, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|10/min (Avg), 7/sec (Peak)|
|**Minimum/Maximum Size (bytes)**|2114/2399|

##### **5.3.3.4 Beacon Code Utilization: UB**

||**Beacon Code Utilization: UB**|
|---|---|
|**Message Name**|Beacon Code Utilization: UB|
|**Message Description**|The Beacon Code Utilization Information message is used to provide<br>the peak number of beacon codes used, the total number of<br>adapted codes, and the number of code reassignments since start-<br>up or local midnight, for an adapted period of time.|
|**Message Property Descriptions**|Refer to Table 5-3, below|
|**Permissible Property Values**|Refer to Table 5-3, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-3, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|13/hour (Avg), 1/sec (Peak)|
|**Minimum/Maximum Size (bytes)**|2160/2160|

49

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.3.3.5 Geographic Beacon Code Utilization: UG**

|**G**|**eographic Beacon Code Utilization: UG**|
|---|---|
|**Message Name**|Geographic Beacon Code Utilization: UG|
|**Message Description**|The Geographic Beacon Code Utilization message provides the total<br>number of adapted beacon codes for each destination region as well<br>as the peak number of beacon codes used for each destination<br>region during the period.|
|**Message Property Descriptions**|Refer to Table 5-3, below|
|**Permissible Property Values**|Refer to Table 5-3, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-3, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|1/day (Avg)|
|**Minimum/Maximum Size (bytes)**|2541/4241|

##### **5.3.3.6 Operational Data Properties**

**Table 5-3: Operational Data Properties**

|**Property Name**|**Description**|**Permissible Values**|
|---|---|---|
|FDPS_SourceFacility|This property, of type String,<br>indicates the source, the<br>ARTCC, of the CMS message<br>that caused this message to be<br>published.|ZAB, ZAU, ZBW, ZDC, ZDV, ZFW,<br>ZHU, ZID, ZJX, ZKC, ZLA, ZLC,<br>ZMA, ZME, ZMP, ZNY, ZOA,<br>ZOB, ZSE, ZTL|
|FDPS_SourceSystem|This property, of type String,<br>indicates the specific instance<br>of SFDPS that published the<br>message. A change in the value<br>of this property indicates that<br>the producer has switched from<br>one site to the other.|ATL, SLC|
|FDPS_MessageType|This property, of type String,<br>indicates the type of message|AC, AK, SY, UB, UG|
|FDPS_DataType|This property, of type String,<br>indicates the type of data<br>publication this message ispart|ERODP|

50

NAS-JMSDD-4309-001 Rev C July 10, 2018

||of.||
|---|---|---|
|FDPS_Sensitive|This property, of type Boolean,<br>indicates whether the flight to<br>which this message applies is<br>military/sensitive or not.|FALSE – Even though<br>Operational data messages do<br>not have flight data, this<br>property must exist in order to<br>simplify NEMS filtering rules<br>that allow all users to receive<br>the data.|
|FDPS_Authoritative|This property, of type Boolean,<br>indicates whether the CMS<br>message that caused this<br>message to be published was<br>sent from an Source Facility or<br>ARTCC that was the<br>authoritative or controlling<br>Center of the flight.|TRUE – Even though<br>Operational data messages do<br>not have flight data, this<br>property must exist in order to<br>simplify NEMS filtering rules<br>that allow all users to receive<br>the data.|
|FDPS_Restricted|This property, of type String,<br>indicates whether a message<br>can be shared with all users,<br>only users authorized to receive<br>beacon code information on<br>proposed and canceled flights,<br>or only users not authorized to<br>receive beacon code<br>information on proposed and<br>active flights.|This property has a value of ‘A’<br>for all operational data<br>messages, indicating there are<br>no specific beacon codes in<br>these messages. This is just to<br>simplify NEMS filitering rules.|

#### **5.3.4 General Information Publication Service Message**

##### **5.3.4.1 General Information: GH**

||**General Information: GH**|
|---|---|
|**Message Name**|General Information: GH|
|**Message Description**|A general information message is used to communicate a free-form<br>text message from one facility to one or more other facilities. The<br>content of the message is the free-form text, contained in an inter-<br>facility remarks field (11c).|
|**Message Property Descriptions**|Refer to Table 5-4, below|
|**Permissible Property Values**|Refer to Table 5-4, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-4, below|

51

NAS-JMSDD-4309-001 Rev C July 10, 2018

||**General Information: GH**|
|---|---|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|1/day (Avg)|
|**Minimum/Maximum Size (bytes)**|1750/2150|

##### **5.3.4.2 Interim Altitude Status Information: HE**

||**Interim Altitude Status Message: HE**|
|---|---|
|**Message Name**|Interim Altitude Status Message: HE|
|**Message Description**|The Interim Altitude Status Information message provides interim<br>altitude status information on all active aircraft to a client during the<br>initialization process.|
|**Message Property Descriptions**|Refer to Table 5-4, below|
|**Permissible Property Values**|Refer to Table 5-4, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-4, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|3/day (Avg)|
|**Minimum/Maximum Size (bytes)**|2404/2406|

##### **5.3.4.3 Hold Status Information:  HO**

||**Hold Status Information: HO**|
|---|---|
|**Message Name**|Hold Status Information: HO|
|**Message Description**|The Hold Status Information message provides hold information<br>(holding fix, and estimated fix departure time for definite-duration<br>holds) on all active aircraft to a client during the initialization<br>process.|
|**Message Property Descriptions**|Refer to Table 5-4, below|
|**Permissible Property Values**|Refer to Table 5-4, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-4, below|

52

NAS-JMSDD-4309-001 Rev C July 10, 2018

||**Hold Status Information: HO**|
|---|---|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|1/day (Avg)|
|**Minimum/Maximum Size (bytes)**|1605/1629|

##### **5.3.4.4 ERAM Status Information:  HS**

||**ERAM Status Information: HS**|
|---|---|
|**Message Name**|ERAM Status Information: HS|
|**Message Description**|The ERAM Status Information message is sent when an ERAM status<br>change occurs.|
|**Message Property Descriptions**|Refer to Table 5-4, below|
|**Permissible Property Values**|Refer to Table 5-4, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-4, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|9/day (Avg), 2/sec (Peak)|
|**Minimum/Maximum Size (bytes)**|1601/1601|

##### **5.3.4.5 Unsuccessful Transmission Information:  UI**

|**U**|**nsuccessful Transmission Information: UI**|
|---|---|
|**Message Name**|Unsuccessful Transmission Information: UI|
|**Message Description**|The Unsuccessful Information Transmission (UI) message is sent by<br>ERAM when transmission of flight data to a remote facility is<br>unsuccessful either due to a transmission error or because<br>transmission of the flight data to the remote facility is inhibited.|
|**Message Property Descriptions**|Refer to Table 5-4, below|
|**Permissible Property Values**|Refer to Table 5-4, below|
|**Message ID (if applicable)**|NA|
|**Filter Criteria**|Refer to Table 5-4, below|
|**Applicable Topic/Queue**|FDPSDATA.IN|

53

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Un**|**successful Transmission Information: UI**|
|---|---|
|**Delivery Mode**|Nonpersistent|
|**Message Body Type**|Text|
|**Estimated Frequency**|1.2/min (Avg), 9/sec (Peak)|
|**Minimum/Maximum Size (bytes)**|2438/2445|

##### **5.3.4.6 General Information Data Properties**

**Table 5-4: General Information Data Properties**

|**Property Name**|**Description**|**Permissible Values**|
|---|---|---|
|FDPS_SourceFacility|This property, of type String,<br>indicates the source, the ARTCC, of<br>the CMS message that caused this<br>message to be published.|ZAB, ZAU, ZBW, ZDC, ZDV, ZFW, ZHU,<br>ZID, ZJX, ZKC, ZLA, ZLC, ZMA, ZME,<br>ZMP, ZNY, ZOA, ZOB, ZSE, ZTL|
|FDPS_SourceSystem|This property, of type String,<br>indicates the specific instance of<br>SFDPS that published the message. A<br>change in the value of this property<br>indicates that the producer has<br>switched from one site to the other.|ATL, SLC|
|FDPS_MessageType|This property, of type String,<br>indicates the type of message|GH, HE, HO, HS, UI|
|FDPS_DataType|This property, of type String,<br>indicates the type of data publication<br>this message is part of.|ERGMP|
|FDPS_Sensitive|This property, of type Boolean,<br>indicates whether the flight to which<br>this message applies is<br>military/sensitive or not.|TRUE – The flight is military/sensitive<br>FALSE – The flight is neither military<br>nor sensitive.  Some of the General<br>messages may contain a flightID.  If<br>they do then the value is set.|
|FDPS_Authoritative|This property, of type Boolean,<br>indicates whether the CMS message<br>that caused this message to be<br>published was sent from an Source<br>Facility or ARTCC that was the<br>authoritative or controlling Center of<br>the flight.|TRUE – Even though Airspace<br>messages do not have flight data, this<br>property must exist in order to<br>simplify NEMS filtering rules that<br>allow all users to receive the data.|
|FDPS_Restricted|This property, of type String,<br>indicates whether a message can be<br>shared with all users, only users<br>authorized to receive beacon code|This property has a value of ‘A’ for all<br>operational data messages, indicating<br>there is no beacon code information<br>in these messages. This isjust to|

54

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Property Name**|**Description**|**Permissible Values**|
|---|---|---|
||information on proposed and<br>canceled flights, or only users not<br>authorized to receive beacon code<br>information on proposed and active<br>flights.|simplify NEMS filitering rules.<br>Note: The FDPS_Sensitive property<br>still applies, and a message marked<br>sensitive (FDPS_Sensitive = ‘true’) will<br>only be shared with users authorized<br>to receive sensitive data, even though<br>the value in the FDPS_Restricted<br>property is ‘A’|

55

NAS-JMSDD-4309-001 Rev C July 10, 2018

### **5.4 Exceptions Handling**

SFDPS alerts consumers to the following exceptions when there is an interruption in the flow of published data. This alert takes the form of an error or status message published to NEMS which routes the message to every consumer connected to a topic that is receiving SFDPS data. SFDPS does not assign an error code to these messages.

When the ERAM or HADDS data source is disconnected from SFDPS, a message is sent to each consumer listing the ARTCC and the time of the disconnection. The text of the message is “HADDS Disconnect.”

When the data for an individual ARTCC is not available to SFDPS, a message is sent to each consumer once a minute listing the ARTCC, the time of the message, and the current state of the ARTCC which is the text “down”.

|**Element Name**<br>**[Status]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|Classification|This element specifies whether<br>the message will be published<br>externally or internally.|string|No|**Public**<br>All messages sent to clients will have the<br>value of Public.|**Public**|Yes|
|Time|This element specifies the time<br>the message was generated.|string|No|**Time in standard XML format.**‘YYYY-MM-<br>DDTHH:MM:SSZ’|2012-01-01T18:00:00Z|Yes|
|Status type|Specifies why the message was<br>generated.|string|No|HADDS Connection<br>HADDS Disconnect<br>HADDS Download Initiated<br>HADDS Download Complete<br>HADDS Re-initialization<br>HADDS Interface Connection<br>ARTCC Status<br>NEMS Status|**HADDS Disconnect**|Yes|
|Source|The process or component<br>that generated the message|string|No|||Yes|
|artcc|Indicates whether an ARTCC is<br>providing data or not.|string|No|**Up**<br>**Down**<br>**Unknown**|**Down**|Yes|
|software|Indicates whether a software|string|No|**Up**|**Up**|Yes|

56

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[Status]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||process is functioning or not.|||**Down**<br>**Unknown**|||
|process|Indicates that a process was<br>restarted.||No|||Yes|
|details|Additional details that may be<br>of use to a client.|string|No|**Free form text.**||Yes|
|numberofMessages|If it is included in the message,<br>this element specifies the fix<br>and calculated time of arrival<br>at each fix that describes the<br>aircraft’s ERAM converted<br>route of flight. The fix and<br>time of arrival at the fix are<br>specified in a format that<br>breaks down the fix and the<br>time in separate elements:<br>fix_68c1 and<br>crossingTime_68c2.||Yes|Sequence of elements _fix_68c1_and<br>_crossingTime_68c2_, specified between 3<br>and 326 times.||Yes|

57

NAS-JMSDD-4309-001 Rev C July 10, 2018

### **5.5 Data**

This section describes data elements and conceptual diagrams for the messages of the four En Route data publication services supported by SFDPS Java Messaging services. The tables below show cross-references to the subsection which contains the message’s detailed description.

|**EN ROUTE FLIGHT DATA PUBLICA**|**TION in Simple X**|**ML Format [Section 5.5.**|**1]**|
|---|---|---|---|
|**Message Name**|**Message**<br>**Code**|**Subsection:**<br>**Data Elements**|**Subsection:**<br>**Diagram**|
|Flight Plan Information|FH|5.5.1.2|5.5.1.3|
|Flight Amendment Information|AH|5.5.1.5|5.5.1.6|
|Converted Route Information|HX|5.5.1.8|5.5.1.9|
|Cancellation Information|CL|5.5.1.11|5.5.1.12|
|Departure Information|DH|5.5.1.14|5.5.1.15|
|Aircraft Iden<br>tification Amendment Information|IH|5.5.1.17|5.5.1.18|
|Hold Information|HH|5.5.1.20|5.5.1.21|
|Progress Report Information|PH|5.5.1.23|5.5.1.24|
|Flight Arrival Information|HV|5.5.1.26|5.5.1.27|
|Flight Plan Update Information|HU|5.5.1.29|5.5.1.30|
|Expected Departure Time Information<sup>2</sup>|ET|5.5.1.32|5.5.1.33|
|Position Update Information|HP|5.5.1.35|5.5.1.36|
|Tentative Flight Plan Information|NP|5.5.1.38|5.5.1.39|
|Tentative Aircraft Identification Amendment<br>Information|NI|5.5.1.41|5.5.1.42|
|Tentative Flight Plan Removal|NL|5.5.1.44|5.5.1.45|
|Tentative Flight Plan Amendment Information|NU|5.5.1.47|5.5.1.48|
|Batch Track Information|BATCH_TH|5.5.1.50|5.5.1.51|
|Drop Track Information|RH|5.5.1.53|5.5.1.54|
|Interim Altitude Information|LH|5.5.1.56|5.5.1.57|
|Automated Radar Terminal System (ARTS) Flow<br>Control Track/Full Data Block Information<sup>2</sup>|HZ|5.5.1.59|5.5.1.60|
|Beacon Code Reassignment|BA|5.5.1.62|5.5.1.63|
|Beacon Code Restricted|RE|5.5.1.65|5.5.1.66|
|FDB Fourth Line Information|HF|5.5.1.68|5.5.1.69|
|Point Out Information|HT|5.5.1.71|5.5.1.72|
|Inbound Point Out Information|PT|5.5.1.74|5.5.1.75|

> 2 This message could be phased out once it becomes available from its primary source (for ET, this would be TFMS; for HZ, this would be ARTS/STARS).

58

NAS-JMSDD-4309-001 Rev C

July 10, 2018

|**EN ROUTE FLIGHT DATA P**|**UBLICATION in Simple X**|**ML Format [Section 5.5.**|**1]**|
|---|---|---|---|
|**Message Name**|**Message**|**Subsection:**|**Subsection:**|
||**Code**|**Data Elements**|**Diagram**|
|Handoff Status|OH|5.5.1.77|5.5.1.78|
|Flight Plan Reconstitution|DBRTFPI|5.5.1.54|5.5.1.55|

|**EN ROUTE FLIGHT DATA PUBLICATION in FI**|**XM Format [Section 5.**|**5.1]**|
|---|---|---|
|**Message Name**|**Message Code**|**Subsection:**<br>**Data Elements**|
|Flight Plan Information|FH_FIXM|5.5.1.4|
|Flight Amendment Information|AH_FIXM|5.5.1.7|
|Converted Route Information|HX_FIXM|5.5.1.10|
|Cancellation Information|CL_FIXM|5.5.1.13|
|Departure Information|DH_FIXM|5.5.1.16|
|Aircraft Identification Amendment Information|IH_FIXM|5.5.1.19|
|Hold Information|HH_FIXM|5.5.1.22|
|Progress Report Information|PH_FIXM|5.5.1.25|
|Flight Arrival Information|HV_FIXM|5.5.1.28|
|Flight Plan Update Information|HU_FIXM|5.5.1.31|
|Expected Departure Time Information|ET_FIXM|5.5.1.34|
|Position Update Information|HP_FIXM|5.5.1.37|
|Tentative Flight Plan Information|NP_FIXM|5.5.1.40|
|Tentative Aircraft Identification Amendment<br>Information|NI_FIXM|5.5.1.43|
|Tentative Flight Plan Removal|NL_FIXM|5.5.1.46|
|Tentative Flight Plan Amendment Information|NU_FIXM|5.5.1.49|
|Batch Track Information|BATCH_TH_FIXM|5.5.1.50|
|Drop Track Information|RH_FIXM|5.5.1.55|
|Interim Altitude Information|LH_FIXM|5.5.1.58|
|Automated Radar Terminal System (ARTS) Flow Control<br>Track/Full Data Block Information|HZ_FIXM|5.5.1.61|
|Beacon Code Reassignment|BA_FIXM|5.5.1.64|
|Beacon Code Restricted|RE_FIXM|5.5.1.67|
|FDB Fourth Line Information|HF_FIXM|5.5.1.70|
|Point Out Information|HT_FIXM|5.5.1.73|
|Inbound Point Out Information|PT_FIXM|5.5.1.76|
|Handoff Status|OH_FIXM|5.5.1.79|

59

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**EN ROUTE FLIGHT DATA PUBLICAT**|**ION in FIXM Format [Section 5**|**.5.1]**|
|---|---|---|
|**Message Name**|**Message Code**|**Subsection:**|
|||**Data Elements**|
|Flight Plan Reconstitution|DBRTFPI_FIXM|5.5.1.82|

|**EN ROUTE AIRSPACE DATA PUB**|**LICATION in Simple XML F**|**ormat [Section 5.5.**|**2]**|
|---|---|---|---|
|**Message Name**|**Message Code**|**Subsection:**<br>**Data Elements**|**Subsection:**<br>**Diagram**|
|Sector Assignment Status|SH|5.5.2.2|5.5.2.3|
|Route Status|HR|5.5.2.5|5.5.2.6|
|Special Activities Airspace (SAA)|SU|5.5.2.9|5.5.2.10|
|Altimeter Setting|HA|5.5.2.12|5.5.2.13|
|Adapted Route Status Reconstitution|DBRTRI|5.5.2.14|5.5.2.15|
|Altimeter Status Reconstitution|DBRTAI|5.5.2.17|5.5.2.18|
|Sector Assignment Reconstitution|DBRTSI|5.5.2.19|5.5.2.20|

|**EN ROUTE AIR**|**SPACE DATA PUBLICATION in AIXM**|**Format [Section 5.5.2]**|
|---|---|---|
|**Message Name**|**Message Code**|**Subsection: Data Elements**|
|Route Status|HR_AIXM|5.5.2.7|
|Sector Assignment Status|SH_AIXM|5.5.2.4|
|Special Activities Airspace<br>(SAA)|SU_AIXM|5.5.2.11|
|Adapted Route Status<br>Reconstitution|DBRTRI_AIXM|5.5.2.16|
|Sector Assignment<br>Reconstitution|DBRTSI_AIXM|5.5.2.21|

|**EN ROUTE OPERATIONAL DATA PUB**|**LICATION in Simple XML**|**Format [Section 5.**|**5.3]**|
|---|---|---|---|
|**Message Name**|**Message Code**|**Subsection:**|**Subsection:**|
|||**Data Elements**|**Diagram**|
|Traffic Count Adjustment|AK|5.5.3.2|5.5.3.3|
|Instrument Approach Count Adjustment|AC|5.5.3.4|5.5.3.5|

60

NAS-JMSDD-4309-001 Rev C

July 10, 2018

|**EN ROUTE OPERATIONAL DATA PUB**|**LICATION in Simple XM**|**L Format [Section**|**5.5.3]**|
|---|---|---|---|
|Sign In Sign Out|SY|5.5.3.6|5.5.3.7|
|Beacon code Utilization|UB|5.5.3.8|5.5.3.9|
|Geographic Beacon Code Utilization|UG|5.5.3.9|5.5.3.11|

|**EN ROUTE GENERAL MESSAGE PU**|**BLICATION in Simple XML**|**Format [Section 5.**|**5.4]**|
|---|---|---|---|
|**Message Name**|**Message Code**|**Subsection:**<br>**Data Elements**|**Subsection:**<br>**Diagram**|
|General Information|GH|5.5.4.2|5.5.4.3|
|Interim Altitude Status Information|HE|0|5.5.4.5|
|Hold Status Information|HO|5.5.4.6|5.5.4.7|
|ERAM Status Information|HS|5.5.4.8|5.5.4.9|
|Unsuccessful Transmission Information|UI|5.5.4.10|5.5.4.11|

61

NAS-JMSDD-4309-001 Rev C July 10, 2018

#### **5.5.1 Flight Data Publication Service Data Elements and Diagrams**

The route element of all Flight Data Publication Service messages published in FIXM format is the element _MessageCollection_ , defined in the FIXM US Extension schema file NasMessage.xsd and depicted in the diagram below.

The _MessageCollection_ type allows aggregating messages into batches that can be sent as a group. Only the Track Information messages are batched. All the other flight messages include only one individual message.

The FIXM XPath of the data elements included in the FIXM flight message description tables below is specified relative to the element NasFlight.

62

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.1 ERFDP Service: targetNamespace**

The targetNamespace that applies to all messages in Simple XML format in the Flight Data Publication Service is: **us:gov:dot:faa:atm:enroute:entities:flightdata.**

##### **5.5.1.2 SimpleXML Flight Plan, Flight Amendment, and Flight Update [FH, AH and HU] - Data Elements**

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|Source identification that<br>includes a UTC time followed<br>by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four-digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**,<br>where the first 6<br>digits are the UTC<br>time (23:59:35<br>UTC) and the last<br>4 digits are<br>sequence number<br>of the message<br>(9001).|Yes|
|sourceTime_00e1|This element consists in the<br>time component of the<br>previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:_hh_<br>stands for the 2-digit-hour in the range<br>00-23,_mm_stands for the 2-digit minutes<br>in the range 00-59, and_ss_stands for the<br>2-digit seconds in the range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|The message sequence<br>number component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|

63

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**, such as<br>_ddd, ddL, dLd, dLL_.|**020**|No|
|eramGufi_316a|GUFI that uniquely identifies<br>each flight plan in the system.|string|No|**"[A-Z]{2}\d{5}[1-7]\d{2}"**<br>This element includes<br>10 alphanumeric characters:<br>-International Civil Aviation Organization<br>(ICAO) country code (one letter);<br>-en-route facility ID (one letter);<br>-time in seconds  of current day (five<br>digits in the range 00000-86400);<br>-sequence number (two digits).|**KB5980017**|No|
|sspId_167a|Site Specific Plan Identifier. It<br>is assigned by Instrument<br>Flight Procedures Automation<br>(IFPA) to uniquely identify a<br>flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|numberOfAircraft_03a|This element includes the<br>number of aircraft for the<br>flight followed optionally by<br>the Special Aircraft Indicator.|string|No|**"\d{0,2}[A-Z]?"**<br>The element consists of zero to two<br>digits optionally followed by one<br>uppercase letter to represent the Special<br>Aircraft Indicator. The indicator can also<br>appear on its own (without the leading<br>digits).|**3H**<br>The number of<br>aircraft is 3 and<br>the special<br>aircraft indicator<br>is**H**for Heavy Jet.|No|
|typeOfAircraft_03c|Type of aircraft.|string|No|**"[A-Z][A-Z0-9]{1,3}"**<br>The element consists of one letter<br>followed by one to three alphanumeric<br>characters.|**B747**|Yes|

64

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|airborneEquip_03e|Airborne equipment qualifier.<br>It consists of one<br>alphanumeric character.|string|No|**"[A-Z]"**<br>The element consists of one<br>alphanumeric character, that can have<br>one of the following values:<br>**A**- Transponder with no Mode C<br>**B**- Transponder with Mode C<br>**E**– FMS with Distance Measuring<br>Equipment (DME)/DME and Inertial<br>Reference Unit (IRU) position updating<br>**G**– Global Navigation Satellite System<br>(GNSS), including Global Positioning<br>System (GPS) or Wide Area<br>Augmentation System (WAAS), with en-<br>route and terminal capability<br>**X**– No transponder<br>**W**- Reduced Vertical Separation<br>Minimums (RVSM)|**E**|No|
|beaconCode_04a|Beacon code.<br>**_Note:_**As of SFDPS 1.3.1, if the<br>flightState element has a<br>value of ‘Canceled’ or<br>‘Proposed’, this element is<br>only present in the version of<br>a message with<br>FDPS_Restricted=’R’|string|No|"[0-7]{4}"<br>The element includes four octal digits<br>(i.e. 0-7). When the last two digits of the<br>four-digits are zero, the beacon code is a<br>non-discrete code.<br>A discrete code is any code not ending in<br>00.|Non-discrete VFR<br>code:<br> **2101**|No|

65

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|externalBeaconCode_04b|External beacon. It contains<br>the requested beacon code<br>when the flight plan is<br>inbound from an adjacent<br>Center or an adjacent Non-<br>U.S. Automated Facility, the<br>requested beacon code is<br>different from the assigned<br>beacon code, and the aircraft<br>is not established on the<br>assigned beacon code. Then,<br>if the facility is adapted to<br>receive Field (04b), Field 04b<br>is be transmitted.<br>**_Note:_**As of SFDPS 1.3.1, if the<br>flightState element has a<br>value of ‘Canceled’ or<br>‘Proposed’, this element is<br>only present in the version of<br>a message with<br>FDPS_Restricted=’R’|string|No|"[0-7]{4}"<br>It has the same format as element<br>beaconCode_04a.|**3434**|No|
|trueAirSpeed_05a|True airspeed expressed in<br>knots.|string|No|"\d{2,4}"<br>The format is two to four-digits, in the<br>range 01 – 3700 knots.<br>Aircraft speed is required to be specified<br>by using one of the three possible<br>elements: trueAirSpeed_05a,<br>machSpeed_05c or classifiedSpeed_05d.|**540**<br>Aircraft true<br>airspeed is 540<br>knots.|Yes, if<br>neither<br>machSpee<br>d_05c nor<br>classifiedS<br>peed_05d<br>are<br>included in<br>the<br>message.|

66

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|machSpeed_05c|Mach speed.|string|No|**“M\d{3}”**<br>The letter**M**followed by three digits.<br>The maximum value is M500.|The speed 0.85<br>Mach is<br>represented as<br>**M085**.|Yes, if<br>neither<br>trueAirSpe<br>ed_05a<br>nor<br>classifiedS<br>peed_05da<br>re included<br>in the<br>message.|
|classifiedSpeed_05d|Adapted classified speed. It is<br>not printed on flight strips.|string|No|**“SC”**|This element may<br>only include the<br>string character<br>**SC**.|Yes, if<br>neither<br>trueAirSpe<br>ed_05a<br>nor<br>machSpee<br>d_05c are<br>included in<br>the<br>message.|

67

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|coordFix_06a|The Coordination fix<br>represents the starting point<br>to begin processing the flight<br>plan route from one of the<br>following points: the<br>departure airport, the airfile<br>fix or the adjacent center<br>inbound coordination fix. For<br>ARTS III flight plans the<br>coordination fix Field 06 is<br>used as the inbound<br>coordination fix or the<br>outbound coordination fix or,<br>for an ARTS internal flight, it<br>can be the departure or<br>destination airport.|string|No|**“([A-Z0-9]{2,5})|**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)|**<br>**([A-Z0-9]{3,4}}"**<br>This element can have one of the<br>following formats:<br>Two to five alphanumeric characters for<br>a fix name.<br>The fix name as above followed by six<br>digits, for a fix radial distance.<br>Four-digits followed by an optional<br>alphabetic character, followed by a<br>virgule (‘/’), followed by four to five<br>digits followed by an optional<br>alphanumeric character for a lat/long.<br>Three to four alphanumeric characters<br>for a location identifier (LOCID).|**AB**<br>**DFW**<br>**KDFW**<br>**AB200010**<br>**SHP090015**<br>**ATOKA300040**<br>**3500/04000**<br>**3500N/04000W**|Yes|
|coordStatusTime_07d|Coordination time that<br>represents the starting time<br>in hours and minutes at the<br>coordination fix.|string|No|**"((A|D|E|P|F)[0-1][0-9][0-5][0-9) |**<br>**((A|D|E|P|F)2[0-3][0-5][0-9])”**<br>The element includes one letter<br>(possible values are**A**,**D, E**,**P**, or**F**)<br>followed by four-digits that represent<br>time as_hhmm_.|**P1020**|Yes|
|coordStatus_07d1|The coordStatus field is the<br>single letter**A**,**D**,**E**,**F**, or**P**, as<br>described for element<br>coordStatusTime_07d.|string|No|**“(A|D|E|P|F)”**|**F**|Yes|
|coordTime_07d2|Starting time at the<br>coordination fix.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:52**|Yes|
|delayTime_07e|Delay time in expressed in<br>minutes.|string|No|**“\d{3}”**<br>Three digits.|**030**|No|

68

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|assignedAlt_08a|Assigned altitude or flight<br>level expressed in hundreds<br>of feet.<br>Only one of the altitude<br>elements assignedAlt_08a,<br>assignedAlt_08b,<br>assignedAlt_08c,<br>assignedAlt_08d,<br>assignedAlt_08e,<br>assignedAlt_08f,<br>assignedAlt_08g,<br>assignedAlt_08h may be<br>included in the message.|string|No|**“(\d{2,3}) | VFR”**<br>The format consists of either two to<br>three digits, or the constant string**VFR**.<br>Three digits are required for ARTS III,<br>thus a leading zero needs to be used<br>when necessary.|Assigned altitude<br>of 34,000 feet:<br>**340**<br>Assigned altitude<br>9,000 feet ARTS<br>III:<br>**090**|No|
|assignedAlt_08b|Fixed value of**OTP**which<br>indicates VFR-ON-Top. It<br>specifies that the aircraft is<br>flying above the clouds in VFR<br>conditions.|string|No|**“OTP”**|Fixed value of<br>**OTP.**|No|
|assignedAlt_08c|VFR-ON-Top with altitude. It<br>represents an Instrument<br>Flight Rules (IFR) flight<br>operating above the clouds in<br>VFR conditions at the<br>specified assigned altitude.|string|No|“**OTP/\d{2,3}**”<br>The format is the constant string**OTP**/<br>followed by two to three digits that<br>represent the assigned altitude in<br>hundreds of feet.|Aircraft flying<br>VFR-ON-Top at<br>25,000 feet:<br>**OTP/250**|No|
|assignedAlt_08d|The assigned block of<br>altitudes for the flight to fly<br>at.|string|No|**"\d{2,3}B\d{2,3}"**<br>The format is two to three digits,<br>followed by the letter**B**, followed by two<br>to three digits. The leading and trailing<br>two to three digits define the block of<br>altitudes in hundreds of feet for the<br>flight to fly at. The lowest altitude must<br>be listed first.|Assigned altitude<br>block of 8,000<br>feet to 14,000<br>feet:<br>**80B140**|No|

69

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|assignedAlt_08e|Element used for IFR flights<br>operating above a specified<br>altitude.|string|No|**“ABV/\d{2,3}"**<br>The format consists of the string**ABV/**<br>followed by two to three digits that<br>represent the altitude in hundreds of<br>feet above which the flight is flying.|Aircraft is flying<br>above 60,000<br>feet.<br>**ABV/600**|No|
|assignedAlt_08f|Assigned<br>Altitude/FIX/Altitude element<br>specifies the altitudes to and<br>from a fix for the flight to fly<br>at.|string|No|**"(\d{2,3}/[A-Z0-9]{2,5}/\d{2,3})|**<br>**(\d{2,3}/[A-Z0-9]{2,5}\d{6}/\d{2,3}) |**<br>**(\d{2,3}/\d{4}[A-Z]?/\d{4,5}[A-**<br>**Z]?/\d{2,3})"**<br>The altitudes are specified in hundreds<br>of feet in a two to three digit format.<br>The fix is specified using the same<br>format as the coordination fix element<br>“coordFix_06a”.<br>The fix cannot be the departure or<br>arrival point.|**240/DAL350010/**<br>**220**<br>Flight flies at<br>altitude 24,000<br>feet to the fix<br>radial distance fix<br>and then descend<br>to altitude 22,000<br>feet.|No|
|assignedAlt_08g|It is used to specify that the<br>flight is flying Visual Flight<br>Rules (VFR). It can only have<br>the value**VFR**.|string|No|**“VFR”**|The string**VFR.**|No|
|assignedAlt_08h|It is used to specify that the<br>flight is flying VFR at a<br>specified altitude.|string|No|**“VFR/\d{2,3}"**<br>The format consists of the string**VFR/**<br>followed by two to three digits that<br>represent an altitude in hundreds of<br>feet.|**VFR/75**<br>The aircraft is<br>flying VFR at<br>7,500 feet.|No|

70

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|requestedAlt_09a|The element is used to<br>specify requested altitude or<br>flight level in hundreds of<br>feet.<br>Only one of the seven<br>requested altitude elements<br>(requestedAlt_09a to<br>requestedAlt_08g) may be<br>included in a proposed flight<br>message.|string|No|**“\d{2,3}"**<br>The format consists of two to three<br>digits. ARTS III requires three characters,<br>with a leading**0**when required (such as<br>090).|**340**<br>Aircraft is<br>requesting to fly<br>at 34,000 feet<br>altitude.|No|
|requestedAlt_09b|The element Requested<br>Altitude format OTP<br>represents an IFR flight<br>requesting to operate above<br>the clouds in VFR conditions.<br>OTP stands for VFR-ON-Top.|string|No|**“OTP”**|The element has<br>a fixed value of<br>**OTP**.|No|
|requestedAlt_09c|The element “Requested<br>Altitude format OTP with<br>altitude” represents a flight<br>requesting to operate VFR-<br>ON-Top at the requested<br>altitude.<br>.|string|No|**“OTP/\d{2,3}"**<br>The format consists of the string**OTP/**<br>followed by two to three digits that<br>represent the requested altitude in<br>hundreds of feet.<br>ERAM only sends ARTS III the requested<br>altitude with a format of three digits<br>(leading zeroes used when necessary, as<br>in 090) and places a special altitude<br>indicator (**U**if Heavy Jet) in element<br>numberOfAircraft_03a.|**OTP/250**<br>Flight is<br>requesting to fly<br>VFR-ON-Top at<br>25,000 feet.|No|
|requestedAlt_09d|Element used for an IFR flight<br>requesting to operate above<br>a specified altitude.|string|No|“ABV/\d{2,3}"<br>The format consists of the string**ABV/**<br>followed by two to three digits that<br>represent the requested altitude in<br>hundreds of feet.|**ABV/600**|No|

71

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|requestedAlt_09e|Element used to specify a<br>requested block of altitudes<br>or flight levels for the flight to<br>fly at. The altitudes are<br>specified in hundreds of feet.|string|No|**"\d{2,3}B\d{2,3}"**<br>The format consists of two to three<br>digits for the lowest altitude, followed<br>by the letter**B**, followed by two to three<br>digits for the highest altitude.|**250B260**<br>Flight is<br>requesting to fly<br>inside an altitude<br>block between<br>25,000 feet and<br>26,000 feet.|No|
|requestedAlt_09f|This element is used when<br>the aircraft is requesting to<br>fly VFR.|string|No|**“VFR”**<br>It can only include the fixed string “VFR.”<br>ERAM sends ARTS III the three<br>characters and also places a special<br>altitude indicator**V**(not a Heavy Jet) or<br>**W**(if a Heavy Jet) in element<br>numberOfAircraft_03a.||No|
|requestedAlt_09g|The element used to<br>represent a flight requesting<br>to fly VFR at a specified<br>altitude.|string|No|**“VFR/\d{2,3}"**<br>The format consists of the constant<br>string**VFR/**followed by two to three<br>digits that specify the requested altitude<br>in hundreds of feet.|**VFR/35**<br>Aircraft is<br>requesting to fly<br>VFR at 3,500 feet|No|
|flightPlanRoute_10a|It specifies the trajectory<br>followed by the airplane from<br>the departure point to the<br>arrival point, based on the<br>fixes and routes along that<br>trajectory.|string|No|**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-**<br>**9+\./]*\.[A-Z0-9+/\*]{2,12}_?(/\d{4})?"**<br>The element format consists of a string<br>that includes fixes and routes along the<br>trajectory flown by the airplane. The<br>fixes and routes are specified using the<br>FIX.ROUTE.FIX format, where either<br>element can be implied, such as FIX..FIX,<br>or ROUTE..ROUTE.|OKC.V14S.TUL.TU<br>L090..FYV270.FYV|Yes|

72

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|departurePoint_26a|It is used to specify the point<br>at which to start processing<br>the flight plan route as<br>follows: the departure airport<br>or the airfile point.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a<br>fix can be used for this element (fix<br>name, lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|destination_27a|It is used to specify the point<br>at which to end processing<br>the flight plan route.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a<br>fix can be used for this element (fix<br>name, lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|FAV_143b0|The element specifies the FAV<br>number containing the first<br>fix where the route alteration<br>occurs due to an AAR<br>application.|string|No|**“\d{4}”**<br>The format is four-digits.|7601|No|
|FAV_143b1|The element specifies the FAV<br>number containing the<br>second fix where the route<br>alteration occurs due to an<br>AAR application.|string|No|**“\d{4}”**<br>The format is four-digits.|7601|No|
|FAV_143b2|The element specifies the FAV<br>number containing the third<br>fix where the route alteration<br>occurs due to an AAR<br>application.|string|No|**“\d{4}”**<br>The format is four-digits.|7601|No|

73

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|FAV_143b3|The element specifies the FAV<br>number containing the fourth<br>fix where the route alteration<br>occurs due to an AAR<br>application.|string|No|**“\d{4}”**<br>The format is four-digits.|7601|No|
|ADARId_141a|If required for the flight, this<br>element specifies the ADAR<br>departure arrival route name.|string|No|**“\d{5}”**<br>The format consists of five alphanumeric<br>characters.|DA001|No|
|ADRId_141b|If required for the flight, the<br>Adapted Route indicator<br>format specifies the ADR<br>adapted departure route<br>name.|string|No|**“\d{5}”**|PD001|No|
|AARId_141c|If required for the flight, this<br>element specifies the AAR<br>adapted arrival route name.|string|No|**“\d{5}”**|PA001|No|
|ADARFld10_142a|This element contains the<br>adapted ADAR preferential<br>route in Field 10 format. The<br>Preferential Route<br>Alphanumerics are used to<br>control the flow and<br>separation of traffic departing<br>and arriving at designated<br>airports. An ADAR has the<br>complete preferential routing<br>from the departure airport to<br>the arrival airport.<br>Either this element or the<br>element ADARNonFld10_142b<br>may be included in the<br>message.|string|No|**"[A-Z0-9\./]{4,44}"**<br>Field 10 format.|SX2.PSX.V20.CRP.|No|

74

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|ADARNonFld10_142b|This element contains the<br>adapted ADAR preferential<br>route in non-Field 10 format.<br>If required for the flight and if<br>the element ADARFld10_142a<br>is not included in the<br>message, the FH message<br>contains this element for the<br>ADAR adapted route.<br>Either this element or the<br>element ADARFld10_142a<br>may be included in the<br>message.|string|No|**"[A-Z0-9\./\+&#x20;]{4,44}"**<br>A “+” delimiter precedes and follows the<br>non-Field10 elements.|+LISSE6+<br>+TS1 MEM270<br>LIT050+|No|
|ADRFld10_142c|Adapted ADR preferential<br>route in Field 10 format.<br>Either this element or the<br>element ADRNonFld10_142d<br>may be included in the<br>message.|string|No|**"[A-Z0-9\./\*]{4,84}"**<br>Field 10 format.|**.ALAMO6.HENLY.**<br>**J131.FUZ.J105.**|No|
|ADRNonFld10_142d|Adapted ADR preferential<br>route in non-Field 10 format.<br>Either this element or the<br>element ADRFld10_142c may<br>be included in the message.|string|No|**"[A-Z0-9\./\+&#x20;-]{4,84}"**<br>A “+” delimiter precedes and follows the<br>non-Field10 elements.|**+RV**<br>**J25+CRP.LISSE6**<br>Notice the non-<br>Field10 substring<br>that is enclosed<br>between “+”<br>characters.|No|
|AARFld10_142e|This element includes the<br>AAR preferential route in<br>Field 10 format.<br>Either this element or the<br>element AARNonFld10_142f<br>may be included in the<br>message.|string|No|**"[A-Z0-9\./]{4,97}"**<br>Field 10 format.|**./.BLEUZ.RYTHM3**<br>**.**|No|

75

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|AARNonFld10_142f|This element includes the<br>AAR preferential route in<br>non-Field 10 format.<br>Either this element or the<br>element AARFld10_142e may<br>be included in the message.|string|No|**"[A-Z0-9\./\+&#x20;]{4,97}"**<br>A “+” delimiter precedes and follows the<br>non-Field10 elements.|**.J25.CRP+LISSE6+**<br>Notice the non-<br>Field10 substring<br>that is enclosed<br>between “+”<br>characters.|No|
|remarks_11c|Flight plan remarks text.|string|No|The string is from 1 to 400 characters in<br>length.<br>It has an attribute called_remarktype_with<br>the possible values of interfacility or<br>intrafacility.|**OAIR EVAC**<br>**AMG/N0482F290**<br>**SQT/N0479F310**<br>**JOL+**|No|
|flightRules_908a|This element specifies the<br>flight rules as one character<br>as follows:<br>**I**= IFR<br>**V**= VFR<br>**Y**= IFR First<br>**Z**= VFR First|string|No|**“[IVYZ]”**<br>If**Y**or**Z**is used, the point or points at<br>which a change of flight rules is planned<br>should be shown in the route.|V|No|
|typeOfFlight_908b|This element specifies the<br>type of flight specified using<br>one of the following<br>characters:<br>**S**= Scheduled air transport<br>**N**= Non-scheduled air<br>transport<br>**G**= General Aviation<br>**M**= Military<br>**O**= Other flights|string|No|**“[SNGMO]”**|N|No|

76

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|wakeTurbulenceCat_909c|Wake turbulence category<br>specified using one of the<br>following characters:<br>**H**= Heavy<br>**M**= Medium<br>**L**= Light|string|No|**“[HML]”**||No|
|comNavApproachEquip_91<br>0a|Airborne Equipment<br>Qualifier: Radio<br>Communication, Navigation,<br>and Approach AID<br>Equipment.|string|No|**"([A-M,O-Z]{1,25}) | N"**<br>This element has one required plus 24<br>optional letters. The 25 possible letters<br>are the letters**A**through**Z**and each<br>letter can only be used once. If the letter<br>**N**is present, it must be the only letter<br>present.|SCHJ<br>See ICAO 4444 for<br>the complete list<br>of characters.|No|

77

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|survEquip_910b|This element represents the<br>ICAO airborne equipment<br>qualifier.|string|No|**"[NACXPIS][D]?"**<br>The format consists of up to two letters.<br>The first letter must be one of the<br>Secondary Surveillance Radar (SSR)<br>equipment letters and the second letter,<br>if used, must be the Automated<br>Dependent Surveillance (ADS) capability<br>letter**“D”**.<br>The valid values for the first letter and<br>their significance are:<br>N: Nil<br>A: Transponder Mode A<br>C: Transponder Mode A and C<br>X: Transponder Mode S without both<br>aircraft ID and pressure-altitude<br>transmission<br>P: Transponder Mode S, with pressure-<br>altitude transmission but aircraft ID<br>transmission<br>I: Transponder Mode S with aircraft ID<br>transmission but no pressure-altitude<br>transmission<br>**S**: Transponder Mode S with both<br>pressure-altitude and aircraft ID<br>transmission<br>**D**: ADS capability|SSR equipment as<br>Mode S with ADS<br>capability:<br>SD|No|

78

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|comNavApproachEquipICA<br>O2012_910c|This element is the ICOA 2012<br>version of the element<br>comNavApproachEquip_910a.|string|No|**"[A-Z][A-Z0-9]{0,63}"**<br>The valid values are:<br>N – No equipment is carried, or<br>equipment is unserviceable<br>S – Standard equipment is carried and is<br>serviceable<br>A – GBAS landing system<br>B – LPV (APV with SBAS)<br>C – LORAN C<br>D – DME<br>E1 – FMC WPR ACARS<br>E2 – D-FIS ACARS<br>E3 – PDC ACARS<br>F – ADF<br>G – GNSS<br>H – HF RTF<br>I – Inertial Navigation<br>J1 – CPDLC ATN VDL Mode 2<br>J2 – CPDLC FANS 1/A HDFL<br>J3 - CPDLC FANS 1/A VDL Mode A<br>J4 - CPDLC FANS 1/A VDL Mode 2<br>J5 - CPDLC FANS 1/A SATCOM<br>(INMARSAT)<br>**J6**- CPDLC FANS 1/A SATCOM (MTSAT)|ADE3RV|No|

79

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|comNavApproachEquipICA<br>O2012_910c (cont.)||||J7 - CPDLC FANS 1/A SATCOM (Iridium)<br>K – MLS<br>L – ILS<br>M1 – ATC RTF SATCOM (INMARSAT)<br>M2 - ATC RTF SATCOM (MTSAT)<br>M3 – ATC RTF (Iridium)<br>O – VOR<br>P1-P9 – Reserved for RCP<br>R – PBN approved<br>T – TACAN<br>U – UHF RTF<br>V – VHF RTF<br>W – RVSM approved<br>X – MNPS approved<br>Y – VHF with 8.33 kHz spacing capacity<br>Z – Other equipment carried|||

80

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|survEquipICAO2012_910d|This element is the ICAO 2012<br>equivalent of the element<br>survEquip_910b.|string|No|**“N|A|C|(C?[BDEGHILPSUVX][BDEGHILP**<br>**SUVX12]*)"**<br>Minimum element length=1<br>Maximum element length=20<br>The valid values are the following:<br>_N – No surveillance equipment or_<br>equipment unserviceable<br>A – Transponder Mode A<br>C – Transponder Mode A and C<br>E – Transponder – Mode S, including<br>aircraft identification, pressure-altitude<br>and extended squitter Automated<br>Dependent Surveillance-Broadcast (ADS-<br>B) capability<br>H – Transponder – Mode S, including<br>aircraft identification, pressure-altitude<br>and enhanced surveillance capability<br>I - Transponder – Mode S, including<br>aircraft identification, but no pressure-<br>altitude capability<br>L – Transponder – Mode S, including<br>aircraft identification, pressure-altitude,<br>extended squitter (ADS-B) and enhanced<br>surveillance capability|HB2U2V2G1|No|

81

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|survEquipICAO2012_910d<br>(cont.)||||P – Transponder – Mode S, including<br>pressure-altitude, but no aircraft<br>identification<br>S – Transponder – Mode S, including<br>both pressure-altitude and aircraft<br>identification capability<br>X – Transponder - Mode S with neither<br>aircraft identification nor pressure-<br>altitude capability<br>B1 – ADS-B with dedicated 1090 mHz<br>ADS-B “out” capability<br>B2 – ADS-B with dedicated 1090 mHz<br>ADS-B “out” and “in” capability<br>U1 - ADS-B “out” capability using UAT<br>U2 - ADS-B “out” AND “IN” capability<br>using UAT<br>V1 - ADS-B “out” capability using VDL<br>Mode 4<br>V2 - ADS-B “out” and “in” capability using<br>VDL Mode 4<br>D1 – ADS-C with FANS 1/A capabilities<br>G1 - ADS-C with ATN capabilities|||

82

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|altAero_916c|This element contains<br>Alternate Arrival Point(s) or<br>Aerodrome(s), if any. More<br>than one alternate arrival<br>points of aerodromes may be<br>specified.|string|No|**"([A-Z]{4}&#x20;?[A-Z]{0,4}) |**<br>**([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?) |**<br>**([A-Z0-9]{3,4})”**<br>The aerodrome is specified using the 4-<br>letter ICAO name or ZZZZ if no ICAO<br>location indicator has been allocated.<br>The arrival point format has to be one of<br>the fix formats described above (see<br>coordFix_06a).<br>If two or more alternatives are included,<br>they may have any of the valid formats<br>and they have to be separated by blanks.|EBBR EDDL|No|
|ICAOStoredFormat_918a|This element may only have<br>the value zero, to indicate<br>that none of the Other<br>Information elements (with<br>suffixes 918b – 918x) is<br>present in the message.|string|No|**“0”**|0|No|
|EETIndicator_918b|This element specifies<br>Significant Points or Flight<br>Information Region (FIR)<br>Boundary designators and<br>accumulated estimated<br>elapsed times to such points<br>or boundaries, when so<br>prescribed on the basis of<br>regional air navigation<br>agreements, or by the<br>appropriate Air Traffic Service<br>(ATS) authority.<br>**EET**stands for Estimated<br>Elapsed Time.|string|No|Freeform text up to a total of 3,000<br>characters.<br>The element consists of one or more<br>Significant Points with appended<br>estimated flying time from departure in<br>_hhmm_format with a blank separating<br>each occurrence of Significant Point and<br>time.|KZNY0046<br>HUBE0213|No|

83

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|RIFIndicator_918c|This element specifies the<br>route to a revised destination<br>aerodrome, followed by the<br>aerodrome location code. The<br>revised route is subject to re-<br>clearance in flight.**RIF**stands<br>for Revised in Flight.|string|No|Free-form string of up to 3,000<br>characters.<br>The destination aerodrome has to be<br>specified using the four-letter ICAO<br>location code.|DTA HEC KLAX|No|
|REGIndicator_918d|This element specifies Aircraft<br>Registration (tail number), if<br>different from the aircraft<br>identification specified in<br>element flightId-_02a.|string|No|Free-form string of up to 3000 characters.|N5258E|No|
|SELIndicator_918e|This element specifies the<br>SELCAL code. SELCAL is a<br>selective-calling radio system<br>that alerts aircraft crew to<br>incoming radio<br>communications.|string|No|Free-form string of up to 3000 characters.|ACHA<br>BRLM|No|
|OPRIndicator_918f|This field specifies the Aircraft<br>Operator, if not obvious from<br>the aircraft identification in<br>flightId_02a.|string|No|Free-form string of up to 3000 characters.|UAL|No|

84

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|STSIndicator_918g|This element specifies the<br>Reason for Special Handling<br>by ATS, such as hospital<br>aircraft.|string|No|Free-form string of up to 3000 characters.<br>The following are the only valid special<br>handling indicators:<br>**ALTRV**<br>**ATFMX**<br>**FFR**<br>**FLTCK**<br>**HAZMAT**<br>**HEAD**<br>**HOSP**<br>**HUM**<br>**MARSA**<br>**MEDEVAC**<br>**NONRVSM**<br>**SAR**<br>**STATE**<br>**NONRNP10**<br>**NO NRPN10**<br>**PROTECTED**<br>**CARGO**<br>**CARGO FLT**|ALTRV|No|
|TYPIndicator_918h|Type(s) of Aircraft, preceded<br>if necessary by number of<br>aircraft, if ZZZZ is specified in<br>the element<br>numberOfAircraft_03a.|string|No|Free-form string of up to 3000 characters.|CESNA140|No|

85

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|PERIndicator_918i|This element specifies the<br>aircraft performance data.|string|No|Single valid letter specified in PAN-OPS<br>8168 Volume 1:<br>**A**– Indicated airspeed (IAS) less than 169<br>km/h (91kt)<br>**B**– IAS between 169 km/h (91kt) and 224<br>km/h (121 kt)<br>**C**– IAS between 224 km/h (121 kt) and<br>261 km/h ( 141 kt)<br>**D**– IAS between 261 km/h ( 141 kt) and<br>307 km/h (166 kt)<br>**E**- IAS between 307 km/h (166 kt) and<br>391 km/h (211 kt)<br>**H**- Helicopters|C|No|
|COMIndicator_918j|This element contains<br>Communication Equipment<br>Data. It is used for additional<br>Communication Equipment<br>on board not specified in the<br>flightPlanRoute_10a element.|string|No|Free-form string of up to 3000 characters.|HF ONLY<br>TCAS|No|
|DATIndicator_918k|This element specifies data<br>related to data link capability.|string|No|Free-form string of up to 3000 characters.<br>Valid values are:<br>**S**– satellite data link<br>**H**– HF data link<br>**V**– VHF data link<br>**M**– SSR Mode S data link<br>One or more of the valid letters may be<br>specified in this element.|SV|No|

86

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|NAVIndicator_918l|This element contains<br>Navigation Equipment Data. It<br>is used for additional<br>Navigation Equipment not<br>specified in the<br>flightPlanRoute_10a element.|string|No|Free-form string of up to 3000 characters.|ADF ONLY|No|
|DEPIndicator_918m|This element contains the<br>name of the Departure<br>Aerodrome.|string|No|Free-form string of up to 3000 characters.|NORTON FIELD|No|
|DESTIndicator_918n|This element includes the<br>name of the destination<br>aerodrome.|string|No|Free-form string of up to 3000 characters.|MILLSPAW FARM|No|
|ALTNIndicator_918o|This element includes the<br>name of the alternate<br>destination aerodrome(s).|string|No|Free-form string of up to 3000 characters.|MILLSPAW FARM|No|
|RALTIndicator_918p|This element contains the en-<br>route alternate aerodrome(s).|string|No|Free-form string of up to 3000 characters.|JP RANCH|No|
|CODEIndicator_918q|This element specifies the<br>aircraft Controller-Pilot Data<br>Link Communications (CPDLC)<br>address.|string|No|Free-form string of up to 3000 characters.|**45FA16**|No|
|RACEIndicator_918r|This element specifies the<br>requested altitude and speed<br>en route.|string|No|Free-form string of up to 3000 characters.|**KRAFT/M080F380**|No|
|SURIndicator_918s|This element specifies the<br>surveillance applications or<br>capabilities not specified in<br>localIntendedRoute_10b.|string|No|Free-form string of up to 3000 characters.|**282B**|No|
|DLEIndicator_918t|This element specifies<br>significant en route delay or<br>holding point(s), followed by<br>length of delay.|string|No|Free-form string of up to 3000 characters.<br>The length of delay is specified in the<br>format_hhmm_.|**MDG0030**|No|

87

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|TALTIndicator_918u|This element specifies the<br>take-off alternate aerodrome.|string|No|Free-form string of up to 3000 characters.<br>Valid formats include aerodrome name or<br>any of the fix formats (i.e., lat/long, fix-<br>radial-distance, or name).|KRAFT FARM|No|
|DOFIndicator_918v|This element specifies the<br>date of flight.|string|No|Six-digit date in the format_yymmdd_.|140617|No|
|ORGNIndicator_918w|This element specifies the<br>originator’s eight-letter AFTN<br>address or other appropriate<br>contact details, in cases where<br>the originator of the flight<br>plan may not be readily<br>identified, as required by the<br>appropriate ATS authority.|string|No|Eight-letter character string.|**LEBBYNYX**|No|

88

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|PBNIndicator_918x|This element specifies the<br>Area Navigation (RNAV) or<br>Required Navigation<br>Performance (RNP) capability.<br>PBN stands for Performance<br>Based Navigation.|string|No|Up to eight two-character specifications<br>may be included, for a total of 16<br>characters. RNAV and RNP capabilities<br>are two-characters each, as follows.<br>**RNAV**specifications:<br>A1 RNAV10 (RNP 10)<br>B1 RNAV 5 all permitted sensors<br>B2 RNAV 5 GNSS<br>B3 RNAV 5 DME/DME<br>B4 RNAV 5 VOR/DME<br>B5 RNAV 5 INS or IRS<br>B6 RNAV 5 LORANC<br>C1 RNAV 2 all permitted sensors<br>C2 RNAV 2 GNSS<br>C3 RNAV 2 DME/DME<br>C4 RNAV 2 DME/DME/IRU<br>D1 RNAV 1 all permitted sensors<br>D2 RNAV 1 GNSS<br>D3 RNAV 1 DME/DME<br>D4 RNAV 1 DME/DME/IRU|B1O1|No|
|||||RNP specifications:<br>L1 RNP 4<br>O1 Basic RNP 1 all permitted sensors<br>O2 Basic RNP 1 GNSS<br>O3 Basic RNP 1 DME/DME<br>O4 Basic RNP 1 DME/DME/IRU<br>S1 RNP APCH<br>S2 RNP APCH with BAR-VNAV<br>T1 RNP AR APCH with RF (special<br>authorization required)<br>T2 RNP AR APCH without RF (special<br>authorization required)|||

89

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|RNVArrival_925a|This element specifies the<br>RNAV accuracy value for the<br>arrival phase of the flight<br>expressed in hundredths (.01)<br>nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the<br>value is 0 then the field is not included.|Accuracy of 0.3<br>nm:<br>0030|No|
|RNVEnroute_925b|This element specifies the<br>RNAV accuracy value for the<br>en route phase of the flight<br>expressed in hundredths (.01)<br>nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the<br>value is 0 then the field is not included.|Accuracy of 0.1<br>nm:<br>0010|No|
|RNVOceanic_925c|This element specifies the<br>RNAV accuracy value for the<br>oceanic phase of the flight<br>expressed in hundredths (.01)<br>nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the<br>value is 0 then the field is not included.|Accuracy of 0.1<br>nm:<br>0010|No|
|RNVDeparture_925d|This element specifies the<br>RNAV accuracy value for the<br>departure phase of the flight<br>expressed in hundredths (.01)<br>nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the<br>value is 0 then the field is not included.|Accuracy of 0.1<br>nm:<br>0010|No|
|RNVSpare1_925e|This is a spare element.|string|No|**"\d{4}"**||No|
|RNVSpare2_925f|This is a spare element.|string|No|**"\d{4}"**||No|
|RNPArrival_925g|This element specifies the<br>RNPaccuracy value for the<br>arrival phase of the flight<br>expressed in hundredths (.01)<br>nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the<br>value is 0 then the field is not included.|Accuracy of 0.3<br>nm:<br>0030|No|

90

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|RNPEnroute_925h|This element specifies the RN)<br>accuracy value for the en<br>route phase of the flight<br>expressed in hundredths (.01)<br>nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the<br>value is 0 then the field is not included.|Accuracy of 0.3<br>nm:<br>0030|No|
|RNPOceanic_925i|This element specifies the RN)<br>accuracy value for the oceanic<br>phase of the flight expressed<br>in hundredths (.01) nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the<br>value is 0 then the field is not included.|Accuracy of 0.3<br>nm:<br>0030|No|
|RNPDeparture_925j|This element specifies the RN)<br>accuracy value for the<br>departure phase of the flight<br>expressed in hundredths (.01)<br>nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the<br>value is 0 then the field is not included.|Accuracy of 0.3<br>nm:<br>0030|No|
|RNPSpare1_925k|This is a spare element.|string|No|**"\d{4}"**||No|
|RNPSpare2_925l|This is a spare element.|string|No|**"\d{4}"**||No|

91

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|ICAO1stAdaptedField18_99<br>9a<br>ICAO1stAdaptedField18_99<br>9b<br>ICAO1stAdaptedField18_99<br>9c<br>ICAO1stAdaptedField18_99<br>9d<br>ICAO1stAdaptedField18_99<br>9e<br>ICAO1stAdaptedField18_99<br>9f<br>ICAO1stAdaptedField18_99<br>9g<br>ICAO1stAdaptedField18_99<br>9h<br>ICAO1stAdaptedField18_99<br>9i<br>ICAO1stAdaptedField18_99<br>9j<br>ICAO1stAdaptedField18_99<br>9k<br>ICAO1stAdaptedField18_99<br>9l<br>ICAO1stAdaptedField18_99<br>9m<br>ICAO1stAdaptedField18_99<br>9n<br>ICAO1stAdaptedField18_99<br>9o<br>ICAO1stAdaptedField18_99<br>9p<br>ICAO1stAdaptedField18_99<br>9q<br>ICAO1stAdaptedField18_99<br>9r<br>ICAO1stAdaptedField18_99<br>9s<br>ICAO1stAdaptedField18_99<br>9t<br>ICAO1stAdaptedField18_99<br>9u|Elements having the suffix of<br>_999a through _999y contain<br>the data that is that is present<br>for the optionally adapted<br>element 918 indicators that<br>are transmitted to CMS, when<br>applicable, using a Field<br>Reference Number of 999,<br>with elements a through y.<br>They are formatted as free-<br>form text.|string|92<br>No|Free-form string of up to 3,000<br>characters.||No|

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|localIntendedRoute_10b|The Local Intended Route<br>element contains the flight<br>plan route that is coordinated<br>to penetrated facilities. It<br>consists of the flight plan<br>route with any expected-to-<br>be-applied-by-the-controlling-<br>center ADRs, ADARs or AARs<br>already applied. It is intended<br>for the clients that wish to<br>know the expected state of<br>the flight plan when the<br>current facility releases<br>control of the flight. Element<br>localIntendedRoute_10b<br>contains the filed route (field<br>10a) merged with any locally<br>applicable adapted routes<br>(preferential routes, transition<br>fixes and A-line fixes).<br>Optional Field 10b is sent to<br>ATM-IPOP, when Field 10b is<br>not the same as Field 10a.|string|No|**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-**<br>**9+\./]*\.[A-Z0-9+/\*]{2,12}_?(/\d{4})?"**<br>Minimum length = 3<br>Maximum length = 1000||No|

93

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[FH, AH, HU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|ATCIntendedRoute_10c|The ATC Intended Route<br>element contains the current<br>cleared flight plan route with<br>any unacknowledged auto<br>routes already applied. The<br>ATC Intended Route includes<br>to-be-applied AARs that are<br>not to be notified in the<br>current center. It is intended<br>for clients that wish to know<br>the currently expected route<br>of the flight across contiguous<br>ERAM airspace. Field 10c<br>contains the filed route (field<br>10a) merged with any<br>adapted routes (preferential<br>routes, transition fixes and A-<br>line fixes). Optional Field 10c<br>is sent to ATM-IPOP, when<br>parameter Merged ATC<br>Intended Route Switch<br>(MARS) is ON and if either one<br>of the following is true:<br>If Field 10b exists and Field<br>10c is not the same as Field<br>10b<br>If Field 10b does not exist and<br>Field 10c is not the same as<br>Field 10a.|string|No|"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-9+\./]*\.[A-<br>Z0-9+/\*]{2,12}_?(/\d{4})?"<br>Minimum length = 3<br>Maximum length = 1000||No|

94

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.3 Flight Plan, Flight Amendment, and Flight Update [FH, AH and HU]: Diagram**

The conceptual diagram for Flight Plan [FH], Flight Plan Amendment [AH] and Fight Plan Update [HU] are identical. Due to the size of the diagram, it has been separated into six successive figures for legibility.

95

NAS-JMSDD-4309-001 Rev C July 10, 2018

96

NAS-JMSDD-4309-001 Rev C July 10, 2018

**Figure 5-1: FH Data Diagram [parts 1,2, and 3]**

97

NAS-JMSDD-4309-001 Rev C July 10, 2018

98

NAS-JMSDD-4309-001 Rev C July 10, 2018

**Figure 5-2: FH Diagram [parts 4, 5, and 6]**

99

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.4 FIXM Flight Plan, Flight Amendment, and Flight Update [FH_FIXM, AH_FIXM and HU_FIXM] - Data Elements**

The following elements of the FH message in Simple XML format are not used in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

- coordStatusTime_07d

- comNavApproachEquip_910a

- survEquip_910b

- ICAOStoredFormat_918a

- RACEIndicator_918r

- DOFIndicator_918v

|**Name**<br>**[FH_FIXM, AH_FIXM,**<br>**HU_FIXM]**|**Name in**<br>**SimpleSchema**<br>**[FH,AH,HU]**|**Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/flightIdentification/@air<br>craftIdentification|flightId_02a|Name used by Air Traffic<br>Services units to identify<br>and communicate with an<br>aircraft.|fb:FlightIdentifierType|No|"[A-Z0-9]{7}"|AAL20|Yes|
|flight/@system|propSourceSyst<br>em|This attribute indicates<br>which SFDPS system<br>generated the message.|fb:ProvenanceSystemT<br>ype|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTime|This attribute conatins the<br>time at which the message<br>was received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the<br>code of the ARTCC (or|fb:ProvenanceCentreT<br>ype|No|xs:string|`ZAU`|Yes|

100

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||FIR) that produced the<br>data.|||||
|---|---|---|---|---|---|---|
|flight/arrival/runwayPositionA<br>ndTime/runwayTime/[estimat<br>ed|actual]/@time<br>|arrivalTime|This attribute specifies the<br>proposed or the actual<br>time of arrival at<br>destination, set according<br>to the flight state.|ff:TimeType|No<br>xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/departure/runwayPositi<br>onAndTime/runwayTime/[actu<br>al|estimated]/@time<br>|departureTime|This element specifies the<br>proposed or actual<br>departure time, set<br>according to the flight<br>state.|ff:TimeType|No<br>xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/flightStatus/@fdpsFlight<br>Status<br>|flightState|This attribute contains the<br>current status of the flight<br>as specified by SFDPS.|nas:SfdpsFlightStatusT<br>ype|Yes<br>xs:string<br>“PROPOSED|ACTIVE|COMPLETE<br>D|CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@name<br>flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@value<br>|fdpsGufi|The name value pair<br>specifies the SFDPS GUFI,<br>an identifier on every<br>message that positively<br>identifies what flight the<br>message is for.|fb:FreeTextType|No<br>xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-<br>z0-9/]+"|name="FDPS_GUFI"<br>value="us.fdps.2015-12-<br>18T16:59:10Z.000/14/10<br>0"/>|Yes|
|flight/flightPlan/@identifier<br>|eramGufi_316a|This attribute specifies the<br>unique flight plan<br>identifier.|fb:FreeTextType|No<br>xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi<br>|uuidGufi|This element contains a<br>reference that uniquely<br>identifies a flight and that<br>is independent of any<br>particular system. This<br>reference conforms to the<br>Universal Unique Identifier<br>standard.|fb:GloballyFlightIdentif<br>ierType|xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-<br>4[0-9a-fA-F]{3}\-[89aAbB][0-9a-<br>fA-F]{3}\-[0-9a-fA-F]{12}"|4aaf92be-ac0a-4dba-<br>998f-9e56f5d450b6|Yes|

101

NAS-JMSDD-4309-001 Rev C July 10, 2018

|flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@name<br>flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@value|FDPS_Sequenc<br>eNo|Sequence number assigned<br>by SFDPS to each message<br>it receives from HADDS.<br>The attribute_name_<br>includes the constant string<br>"MSG_SEQ_NO", and the<br>attribute_value_contains<br>the sequence number<br>value.|fb:FreeTextType|No<br>”MSG_SEQ_NO”<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|name="MSG_SEQ_NO"<br>value="6860416"|Yes|
|---|---|---|---|---|---|---|
|flight/flightIdentification/@sit<br>eSpecificPlanId|sspId_167a|Site Specific Plan Identifier.<br>It is assigned by<br>Instrument Flight<br>Procedures Automation<br>(IFPA) to uniquely identify<br>a flight plan in each ERAM<br>facility.|fb:CountType|No<br>**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/aircraftDescription/@air<br>craftQuantity|numberOfAircr<br>aft_03a|This element includes the<br>number of aircraft for the<br>flight.|fb:countType|No<br>**"\d{0,2}"**<br>The element consists of zero to<br>two digits.|**3**|No|
|flight/aircraftDescription/@tf<br>msSpecialAircraftQualifier|numberOfAircr<br>aft_03a-<br>Special Aircraft<br>Indicator|This element includes the<br>Special Aircraft Indicator. It<br>indicates the flight is a<br>heavy jet, B757 or, if not<br>present, a large jet and if<br>the flight is either<br>equipped or not with TCAS.<br>This indicator is used for<br>output purposes such as<br>strip printing and message<br>transfers to other facilities<br>such as Automated Radar<br>Terminal System (ARTS).<br>NOTE<br>TFMS Special Aircraft<br>Qualifier is a bad fit to<br>Special Aircraft Indicator|nas:NasSpecialAircraft<br>QualifierType|No<br>**“HEAVY_JET|TCAS|B757|HEAVY**<br>**_JET_AND_TCAS”**<br>**“HEAVY_JET”**= Capable of<br>takeoff weights of 300,000<br>pounds or more<br>**“TCAS”**= Traffic collision<br>avoidance system or traffic alert<br>and collision avoidance system<br>**“B757”**= Controllers are required<br>to apply the special wake<br>turbulence separation criteria for<br>the Boeing 757.<br>**“HEAVY_JET_AND_TCAS”**=<br>Capable of takeoff weights of<br>300,000 pounds or more and<br>traffic collision avoidance system.|**HEAVY_JET**|No|

102

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||but no other fields seem to<br>fit.||||
|---|---|---|---|---|---|
|flight/aircraftDescription/aircr<br>aftType/icaoModelIdentifier|typeOfAircraft_<br>03c|The ICAO code of the<br>aircraft type.|fb:IcaoAircraftIdentifier<br>Type|No<br>**"[A-Z][A-Z0-9]{1,3}"**<br>The element consists of one<br>letter followed by one to three<br>alphanumeric characters.|**B747**<br>Yes|
|flight/aircraftDescription/@eq<br>uipmentQualifier|airborneEquip_<br>03e|Airborne equipment<br>qualifier. A value assigned<br>to the aircraft, based on its<br>navigational equipment,<br>whether or not it has a<br>transponder, and if it has a<br>transponder, whether the<br>transponder supports<br>Mode C.|nas:NasAirborneEquip<br>mentQualifierType|No<br>**" [ ABCDGHILMNPSTUVWXYZ]"**<br>The element consists of one<br>alphanumeric character, that can<br>have one of the following values:<br>-“X”= No RVSM, No DME, No<br>transponder<br>-“T”= No RVSM, No DME,<br>Transponder with no mode C<br>-“U”= No RVSM, No DME:<br>Transponder with mode C<br>-“D”= DME: No transponder<br>-“B”= DME: Transponder with no<br>mode C<br>-“A”= DME: Transponder with<br>mode<br>-“M”= TACAN ONLY: No<br>transponder<br>-“N”= TACAN ONLY: Transponder<br>with no mode C<br>-“P”= TACAN ONLY: Transponder<br>with mode C<br>-“C”= “Y”=<br>LORAN,VORDME,INS,RNAV: No<br>transponder<br>-“I”= LORAN,VORDME,INSRNAV:<br>Transponder with mode C<br>-“H”= RVSM, Failed transponder<br>or Failed Mode C capability<br>-“S=ADVANCED RNAV,<br>TRANSPONDER, MODE C: FMS<br>with DMEDME position updating<br>-“G”= ADVANCED RNAV,<br>TRANSPONDER, MODE C: Global<br>Navigation Satellite System|**E**<br>No|

103

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||||(GNSS), including GPS or Wide<br>Area Augmentation System<br>(WAAS), with enroute and<br>terminal capability<br>-“V”= ADVANCED RNAV,<br>TRANSPONDER, MODE C:<br>Required Navigational<br>Performance (RNP). The aircraft<br>meets the RNP type prescribed<br>for the route segments, routes<br>and/or area concerned.<br>-“Z”= REDUCED VERTICAL<br>SEPARATION MINIMUM (RVSM):<br>E with RVSM<br>-“L”= REDUCED VERTICAL<br>SEPARATION MINIMUM (RVSM):<br>G with RVSM<br>-“W”= REDUCED VERTICAL<br>SEPARATION MINIMUM (RVSM):<br>RVSM|||
|---|---|---|---|---|---|---|---|
|flight/enRoute/beaconCodeAs<br>signment/currentBeaconCode|beaconCode_0<br>4a|Current assigned beacon<br>code.<br>**_Note_: **As of SFDPS R1.3.1,<br>if the<br>flight/flightStatus/@fdpsFli<br>ghtStatus attribute has a<br>value of ‘CANCELED or<br>‘PROPOSED, this element<br>is only present in the<br>version of a message with<br>FDPS_Restricted=’R’|fb:BeaconCodeType|No|"[0-7]{4}"<br>The element includes four octal<br>digits (i.e. 0-7). When the last<br>two digits of the four-digits are<br>zero, the beacon code is a non-<br>discrete code.<br>A discrete code is any code not<br>ending in 00.|Non-discrete VFR code:<br> **2101**|No|
|flight/enRoute/beaconCodeAs<br>signment/reassignedBeaconCo<br>de|externalBeacon<br>Code_04b|Reassigned beacon code.<br>Identifies the downstream<br>unit that assigned the next<br>beacon code, in the case<br>the beacon code was<br>already in use by another<br>flight at the downstream<br>unit.<br>**_Note_: **As of SFDPS R1.3.1,|fb:BeaconCodeType|No|"[0-7]{4}"<br>It has the same format as<br>currentBeaconCode.|**3434**|No|

104

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||if the<br>flight/flightStatus/@fdpsFli<br>ghtStatus attribute has a<br>value of ‘CANCELED or<br>‘PROPOSED, this element<br>is only present in the<br>version of a message with<br>FDPS_Restricted=’R’|||||
|---|---|---|---|---|---|---|
|flight/requestedAirspeed/nasA<br>irspeed<br>flight/requestedAirspeed/@uo<br>m|trueAirSpeed_0<br>5a<br>machSpeed_05<br>c|The aircraft speed<br>expressed in either true<br>airspeed or mach.|ff:<br>TrueAirSpeedOrMachT<br>ype<br>@uom:<br>ff:AirspeedMeasureTyp<br>e|No<br>**“xs:double”**<br>@uom:<br>**“KILOMETERS_PER_HOUR|KNOT**<br>**S|MACH”**<br>_nasAirspeed_is required if<br>_requestedAirspeed/classifed_is not<br>included in the message.|nasAirspeed:<br>**540**<br>uom:<br>**KNOTS**|No|
|flight/requestedAirspeed/class<br>ified|classifiedSpeed<br>_05d|Classified Speed Indicator.<br>It indicates that the speed<br>for this flight is classified<br>and is not to be recorded.|nas:ClassifiedSpeedIndi<br>catorType|No<br>**“CLASSIFIED”**<br>_classified_is required if<br>_requestedAirspeed/nasAirspeed_<br>not included in the message.|**CLASSIFIED**|No|
|flight/coordination/coordinati<br>onFix/@fix|coordFix_06a|The fix to be used in<br>conjunction with the<br>CoordinationTime so<br>processing for this flight<br>can be synchronized for<br>the next sector/facility. It<br>coordinates the flight plan<br>with the aircraft position.|_fb:SignificantPointType_<br>(abstract type)<br>_fb:FixPointType/_<br>_ff:GeographicalLocatio_<br>_nType/_<br>_fb:RelativePointType_|Yes<br>-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>**-**_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|**KBOS**|Yes|

105

NAS-JMSDD-4309-001 Rev C July 10, 2018

|flight/coordination/@coordina<br>tionTimeHandling|coordStatus_07<br>d1|The indicator for the type<br>of Coordination Time.|nas:CoordinationTimeT<br>ype|No|**“(P|D|E|A)”**<br>**“P”**= Proposed flight plan.<br>**“D”**= Aircraft has departed from<br>the departure airport.<br>**“E”**= Active aircraft.<br>**“A”**= Aircraft arrived at the<br>destination airport.|**P**|Yes|
|---|---|---|---|---|---|---|---|
|flight/coordination/@coordina<br>tionTime|coordTime_07d<br>2|Coordination Time: the<br>time to be used in<br>conjunction with the<br>Coordination Fix so<br>processing for this flight<br>can be synchronized for<br>the next sector/facility.|ff:TimeType|No|**xs:dateTime**|**2015-06-20T20:17:52**|Yes|
|flight/coordination/@delayTim<br>eToAbsorb|delayTime_07e|Delay time to absorb:<br>indicates the amount of<br>time that needs to be<br>absorbed during the flight.<br>It is corrective action for<br>meeting the goal of<br>Estimated Departure<br>Clearance Time (EDCT),<br>when the flight is already<br>active and needs to arrive<br>later than originally<br>planned.|ff:DurationTime|No|**xs:duration**|**PT30M**|No|
|flight/assignedAltitude/simple<br>flight/assignedAltitude/simple/<br>@uom|assignedAlt_08<br>a|Simple altitude: single<br>measurement above<br>reference point. It<br>represents the only NAS<br>altitude that maps directly<br>to the core ICAO altitude<br>types.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the|nas:SimpleAltitudeType<br>@uom:<br>ff:AltitudeMeasureTyp<br>e|Yes|**“xs:double”**<br>_@uom_:<br>“**FEET|METERS**”|Assigned altitude of<br>34,000 feet:<br>**34000**<br>_Uom_:<br>**FEET**|No|

106

NAS-JMSDD-4309-001 Rev C July 10, 2018

|flight/assignedAltitude/vfrOnT<br>op|assignedAlt_08<br>b|message.<br>The presence of this<br>element indicates VFR-ON-<br>Top. It specifies that the<br>aircraft is flying above the<br>clouds in VFR conditions.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the<br>message.|Nas:VfrOnTopAltitudeT<br>ype|Yes|Empty element.||No|
|---|---|---|---|---|---|---|---|
|flight/assignedAltitude/vfrOnT<br>opPlus<br>flight/assignedAltitude/vfrOnT<br>opPlus/@uom|assignedAlt_08<br>c|VFR-ON-Top with altitude.<br>It represents an<br>Instrument Flight Rules<br>(IFR) flight operating above<br>the clouds in VFR<br>conditions at the specified<br>assigned altitude.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the<br>message.|nas:VfrOnTopPlusAltitu<br>deType<br>@uom:<br>ff:AltitudeMeasureTyp<br>e|No|**“xs:double”**<br>@uom:<br>**“FEET|METRES”**|Aircraft flying VFR-ON-<br>Top at 25,000 feet:<br>**25000**<br>_uom_:**FEET**|No|
|flight/assignedAltitude/block/a<br>bove<br>flight/assignedAltitude/block/a<br>bove/@uom|assignedAlt_08<br>d|The bottom level of the<br>assigned block of altitudes<br>for the flight to fly at.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the<br>message.|ff:AltitudeType<br>@uom:<br>ff:AltitudeMeasureTyp<br>e|Yes|**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|_above:_<br>**8000**<br>_uom:_<br>**FEET**|No|
|flight/assignedAltitude/block/<br>below<br>flight/assignedAltitude/block/<br>below/@uom|assignedAlt_08<br>d|The top level of the<br>assigned block of altitudes<br>for the flight to fly at.<br>Only one of the altitude|ff:AltitudeType<br>@uom:<br>ff:AltitudeMeasureTyp|Yes|**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|_below:_<br>**14000**<br>_uom:_|No|

107

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the<br>message.|e||**FEET**||
|---|---|---|---|---|---|---|
|flight/assignedAltitude/above<br>flight/assignedAltitude/above/<br>@uom|assignedAlt_08<br>e|Element used for IFR<br>flights operating above a<br>specified altitude.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the<br>message.|nas:AboveAltitudeType<br>@uom:<br>ff:AltitudeMeasureTyp<br>e|Yes<br>**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|Aircraft is flying above<br>60,000 feet:<br>**60000**<br>**uom:**<br>**FEET**|No|
|flight/assignedAltitude/altFixAl<br>t/point|assignedAlt_08<br>f|_assignedAltitude/altFixAlt_<br>element is defined as an<br>altitude prior to a specified<br>fix, the specified fix itself,<br>and altitude post specified<br>fix. The element<br>_altFixAlt/point_defines the<br>specified fix associated<br>with the altitude.<br>The fix cannot be the<br>departure or arrival point.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the<br>message.|_fb:SignificantPointType_<br>(abstract type)<br>_fb:FixPointType/_<br>_ff:GeographicalLocatio_<br>_nType/_<br>_fb:RelativePointType_|Yes<br>-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|**MDG**|No|
|flight/assignedAltitude/altFixAl<br>t/pre<br>flight/assignedAltitude/altFixAl<br>t/pre/@uom|assignedAlt_08<br>f|_assignedAltitude/altFixAlt_<br>element is defined as an<br>altitude prior to a specified<br>fix, the specified fix itself,|ff:AltitudeType<br>uom:<br>ff:AltitudeMeasureTyp<br>e|Yes<br>**"xs:double"**<br>uom:<br>**“FEET|METRES”**|**240000**<br>**uom:**<br>**FEET**|No.|

108

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||and altitude post specified<br>fix. The element<br>_altFixAlt/pre_defines the<br>altitude before the<br>specified fix.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the<br>message.|||||
|---|---|---|---|---|---|---|
|flight/assignedAltitude/altFixAl<br>t/post<br>flight/assignedAltitude/altFixAl<br>t/post/@uom|assignedAlt_08<br>f|_assignedAltitude/altFixAlt_<br>element is defined as an<br>altitude prior to a specified<br>fix, the specified fix itself,<br>and altitude post specified<br>fix. The element<br>_altFixAlt/pre_defines the<br>altitude after the specified<br>fix.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the<br>message.|ff:AltitudeType<br>uom:<br>ff:AltitudeMeasureTyp<br>e|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**|**22000**<br>**uom:**<br>**FEET**<br>No.|
|flight/assignedAltitude/vfr|assignedAlt_08<br>g|Its presence in the<br>message specifies that the<br>flight is flying Visual Flight<br>Rules (VFR).<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the<br>message.|nas:VfrAltitudeType|Yes|**Empty element**|No|
|flight/assignedAltitude/vfrPlus<br>flight/assignedAltitude/vfrPlus<br>/@uom|assignedAlt_08<br>h|It is used to specify that<br>the flight is flying VFR at a<br>specified altitude.|nas:VfrPlusAltitudeTyp<br>e|Yes|**"xs:double"**<br>uom:|The aircraft is flying VFR<br>at 7,500 feet:<br>No|

109

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the<br>message.|uom:<br>ff:AltitudeMeasureTyp<br>e||**“FEET|METRES”**|**7500**<br>uom:<br>**FEET**||
|---|---|---|---|---|---|---|---|
|flight/requestedAltitude/simpl<br>e<br>flight/requestedAltitude/simpl<br>e/@uom|requestedAlt_0<br>9a|The element is used to<br>specify requested altitude.<br>Only one of the seven<br>requested altitude<br>elements may be included<br>in a proposed flight<br>message.|assignedAltitude/simpl<br>e:<br>nas:SimpleAltitudeType<br>uom:<br>ff:AltitudeMeasureTyp<br>e|Yes|**“xs:double”**<br>uom:<br>“**FEET|METRES**”<br>Only one of the_requestedAltitud_e<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|Aircraft is requesting to<br>fly at 34,000 feet<br>altitude:<br>**34000**|No|
|flight/requestedAltitude/vfrOn<br>Top|requestedAlt_0<br>9b|This element specifies an<br>IFR flight requesting to<br>operate above the clouds<br>in VFR conditions.|nas:VfrOnTopAltitudeT<br>ype|Yes|Empty element.<br>Only one of the_requestedAltitud_e<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|The presence of this<br>empty element<br>indicates<br>VFR-ON-Top.|No|
|flight/requestedAltitude/vfrOn<br>TopPlus<br>flight/requestedAltitude/vfrOn<br>TopPlus/@uom|requestedAlt_0<br>9c|VFR-ON-Top with altitude.<br>It represents an<br>Instrument Flight Rules<br>(IFR) flight requesting to<br>operate above the clouds<br>in VFR conditions at the<br>specified altitude.|nas:VfrOnTopPlusAltitu<br>deType|Yes|**“xs:double”**<br>uom:<br>**“FEET|METRES”**<br>Only one of the_requestedAltitud_e<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|Aircraft requesting to fly<br>VFR-ON-Top at 25,000<br>feet:<br>**25000**<br>uom:**feet**|No|
|flight/requestedAltitude/abov<br>e<br>flight/requestedAltitude/abov<br>e/@uom|requestedAlt_0<br>9d|Element used for IFR<br>flights requesting to<br>operate above a specified<br>altitude.|nas:AboveAltitudeType|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**<br>Only one of the_requestedAltitud_e<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be|Aircraft is requesting to<br>fly above 60,000 feet:<br>**60000**<br>**uom:**<br>**FEET**|No|

110

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||||included in the message.|||
|---|---|---|---|---|---|---|---|
|flight/requestedAltitude/block<br>/above<br>flight/requestedAltitude/block<br>/above/@uom|requestedAlt_0<br>9e|The bottom level of the<br>requested block of<br>altitudes for the flight to<br>fly at.|ff:AltitudeType|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**<br>Only one of the_requestedAltitud_e<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|_above:_<br>**8000**<br>_uom:_<br>**FEET**|No|
|flight/requestedAltitude/block<br>/below<br>flight/requestedAltitude/block<br>/below/@uom|requestedAlt_0<br>9e|The top level of the<br>requested block of<br>altitudes for the flight to<br>fly at.|ff:AltitudeType|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**<br>Only one of the_requestedAltitud_e<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|_below:_<br>**14000**<br>_uom:_<br>**FEET**|No|
|flight/requestedAltitude/vfr|requestedAlt_0<br>9f|Its presence in the<br>message specifies that the<br>flight is requesting to fly<br>Visual Flight Rules (VFR).|nas:VfrAltitudeType|Yes|Empty element<br>Only one of the_requestedAltitud_e<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.||No|
|flight/requestedAltitude/vfrPlu<br>s<br>flight/requestedAltitude/vfrPlu<br>s/@uom|requestedAlt_0<br>9g|This element is used to<br>represent a flight<br>requesting to fly VFR at a<br>specified altitude.|nas:VfrPlusAltitudeTyp<br>e|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**<br>Only one of the_requestedAltitud_e<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|The aircraft is<br>requesting to fly VFR at<br>7,500 feet:<br>**7500**<br>uom:<br>**feet**|N|

111

NAS-JMSDD-4309-001 Rev C July 10, 2018

|flight/agreed/route/@nasRout<br>eText|flightPlanRoute<br>_10a|This attribute is used to<br>specify the trajectory<br>followed by the airplane<br>from the departure point<br>to the arrival point, based<br>on the fixes and routes<br>along that trajectory.|fb:FreeTextType|No<br>**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-**<br>**9+\./]*\.[A-Z0-**<br>**9+/\*]{2,12}_?(/\d{4})?"**<br>The element format consists of a<br>string that includes fixes and<br>routes along the trajectory flown<br>by the airplane. The fixes and<br>routes are specified using the<br>FIX.ROUTE.FIX format, where<br>either element can be implied,<br>such as FIX..FIX, or<br>ROUTE..ROUTE.|OKC.V14S.TUL.TUL090..F<br>YV270.FYV|Yes|
|---|---|---|---|---|---|---|
|flight/departure/@departureP<br>oint|departurePoint<br>_26a|This attribute is used to<br>specify the first point or<br>other initial entity where<br>the air traffic<br>control/management<br>system route starts.|fb:FreeTextType|No<br>xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|flight/arrival/@arrivalPoint|destination_27<br>a|This attribute is used to<br>specify the final point or<br>other final entity where<br>the air traffic<br>control/management<br>system route terminates.|fb:FreeTextType|No<br>**xs:string**<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|flight/agreed/route/nasadapte<br>dArrivalRoute/nasFavNumber|FAV_143b0<br>FAV_143b1<br>FAV_143b2<br>FAV_143b3|The<br>_nasadaptedArrivalRoute_<br>element is the container<br>for_Adapted Arrival Route_<br>_(AAR)_information. This|fb:FreeTextType|No<br>**“\d{4}”**<br>The format is four-digits.|7601|No|

112

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||information consists in the<br>list of Fixed Airspace<br>Volume (FAV) numbers<br>that contain the AAR fixes.<br>The element<br>_nasadaptedArrivalRoute/n_<br>_asFavNumber_represents a<br>FAV number that is an<br>element of this list.||||||
|---|---|---|---|---|---|---|---|
|flight/agreed/route/adaptedAr<br>rivalDepartureRoute/@nasRou<br>teIdentifier|ADARId_141a/|If required for the flight,<br>this element specifies the<br>Adapted Departure Arrival<br>Route (ADAR)/ Adapted<br>Departure Route (ADR)/<br>Adapted Arrival Route<br>(AAR) name.|fb:FreeTextType|No|**[A-Z0-9/\-\?\(\)\.,=\+ ]{5}"**<br>The format consists of five<br>characters.|DA001|No|
|flight/agreed/route/adaptedD<br>epartureRoute/@nasRouteIde<br>ntifier|ADRId_141b|If required for the flight,<br>this element specifies the<br>Adapted Departure Route<br>(ADR) name.|fb:FreeTextType|No|**[A-Z0-9/\-\?\(\)\.,=\+ ]{5}"**<br>The format consists of five<br>characters.|PD001|No|
|flight/agreed/route/nasadapte<br>dArrivalRoute/@nasRouteIden<br>tifier|AARId_141c|If required for the flight,<br>this element specifies the<br>Adapted Arrival Route<br>(AAR) name.|fb:FreeTextType|No|**[A-Z0-9/\-\?\(\)\.,=\+ ]{5}"**<br>The format consists of five<br>characters.|PA001|No|
|flight/agreed/route/adaptedAr<br>rivalDepartureRoute/@nasRou<br>teAlphanumeric|ADARFld10_14<br>2a<br>ADARNonFld10<br>_142b|This element contains the<br>adapted ADAR preferential<br>route in Field 10 or non-<br>Field 10 formats. The<br>Preferential Route<br>Alphanumerics are used to<br>control the flow and<br>separation of traffic<br>departing and arriving at<br>designated airports. An<br>ADAR has the complete<br>preferential routing from<br>the departure airport to|fb:FreeTextType|No|**"([A-Z0-9\./]{4,44})|([A-Z0-**<br>**9\./\+&#x20;]{4,44})"**<br>The Field10 format is:<br>**"[A-Z0-9\./]{4,44}”**<br>The non-Field10 format is:<br>**"[A-Z0-9\./\+&#x20;]{4,44}"**<br>A “+” delimiter precedes and<br>follows the non-Field10<br>elements.|Field10 format:<br>SX2.PSX.V20.CRP<br>Non-Field10 format:<br>+LISSE6+<br>+TS1 MEM270 LIT050+|No|

113

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||the arrival airport.||||||
|---|---|---|---|---|---|---|---|
|flight/agreed/route/adaptedD<br>epartureRoute/@nasRouteAlp<br>hanumeric|ADRFld10_142c<br>ADRNonFld10_<br>142d|Adapted ADR preferential<br>route in Field 10 or non-<br>Field 10 format.|fb:FreeTextType|No|**"([A-Z0-9\./\*]{4,84}) |**<br>**([A-Z0-9\./\+&#x20;-]{4,84})"**<br>Field 10 format:<br>**"([A-Z0-9\./\*]{4,84}”**<br>Non-Field 10 format:<br>**"[A-Z0-9\./\+&#x20;-]{4,84}"**<br>A “+” delimiter precedes and<br>follows the non-Field10<br>elements.|Field 10 format:<br>**.ALAMO6.HENLY.J131.F**<br>**UZ.J105.**<br>Non-Field 10 format:<br>**+RV J25+CRP.LISSE6**|No|
|flight/agreed/route/nasadapte<br>dArrivalRoute/@nasRouteAlph<br>anumeric|AARFld10_142<br>e<br>AARNonFld10_<br>142f|This element includes the<br>AAR preferential route in<br>Field 10 or non-Field 10<br>formats.|fb:FreeTextType|No|**"([A-Z0-9\./]{4,97}) |**<br>**([A-Z0-9\./\+&#x20;]{4,97})"**<br>Field 10 format:<br>**"[A-Z0-9\./]{4,97}"**<br>Non-Field 10 format:<br>**"[A-Z0-9\./\+&#x20;]{4,97}"**<br>A “+” delimiter precedes and<br>follows the non-Field10<br>elements.|Field 10 format:<br>**./.BLEUZ.RYTHM3.**<br>Non-Field 10 format:<br>**.J25.CRP+LISSE6+**<br>Notice the non-Field10<br>substring that is<br>enclosed between “+”<br>characters.|No|
|flight/flightPlan/@flightPlanRe<br>marks|remarks_11c|NAS Flight Plan Field 11<br>remarks processed by the<br>Traffic Flow Management<br>System (TFMS) and used<br>for TFM purposes.|fb:FreeTextType|No|The string is from 1 to 400<br>characters in length.|**OAIR EVAC**<br>**AMG/N0482F290**<br>**SQT/N0479F310 JOL+**|No|
|flight/agreed/route/@initialFli<br>ghtRules|flightRules_908<br>a|The regulation, or<br>combination of regulations,<br>that governs all aspects of<br>operations under which<br>the pilot plans to fly.|fb:FlightRulesType|No|**“IFR|VFR”**<br>If**Y**or**Z**is used, the point or<br>points at which a change of flight<br>rules is planned should be shown<br>in the route.<br>NOTE<br>Can no longer represent all four|**IFR**|No|

114

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||||options (IFR, VFR, IFR First, VFR<br>First), just use first state<br>(IFR/VFR) for transitioning rules.|||
|---|---|---|---|---|---|---|---|
|flight/@flightType|typeOfFlight_9<br>08b|This element specifies the<br>type of flight that<br>represents an indication of<br>the rule under which an air<br>traffic controller provides<br>categorical handling of a<br>flight.|fx:TypeOfFlightType|No|**“MILITARY|GENERAL|SCHEDULE**<br>**D|NON_SCHEDULED|OTHER”**|**SCHEDULED**|No|
|flight/aircraftDescription/@wa<br>keTurbulence|wakeTurbulenc<br>eCat_909c|Wake turbulence category:<br>the ICAO classification of<br>the aircraft wake<br>turbulence, based on the<br>maximum certified take off<br>mass.|fx:WakeTurbulenceCat<br>egoryType|No|**“[JHML]”**<br>**J**= Super Heavy<br>**H**= Heavy<br>**M**= Medium<br>**L**= Light|**H**|No|
|flight/aircraftDescription/capa<br>bilities/@standardCapabilities|comNavApproa<br>chEquipICAO20<br>12_910c|If present, this attribute<br>indicates that aircraft has<br>the "standard" capabilities<br>for the flight.|fx:StandardCapabilitiesI<br>ndicatorType|No|**Empty attribute.**||No|
|flight/aircraftDescription/capa<br>bilities/communication/comm<br>unicationCode|comNavApproa<br>chEquipICAO20<br>12_910c|Describes the aircraft<br>communication code.|fx:CommunicationCapa<br>bilitiesType|No|**“E1|E2|E3|H|M1|M2|M3|P1|**<br>**P2| P3| P4| P5| P6| P7| P8|**<br>**P9|U|V|Y”**<br>where:<br>**E1**– FMC WPR ACARS<br>**E2**– D-FIS ACARS<br>**E3**– PDC ACARS<br>**H**– HF RTF<br>**M1**– ATC RTF SATCOM<br>(INMARSAT)<br>**M2**- ATC RTF SATCOM (MTSAT)|**E2**|No|

115

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||||**M3**– ATC RTF (Iridium)<br>**P1**-**P9**– Reserved for RCP<br>**U**– UHF RTF<br>**V**– VHF RTF<br>**Y**– VHF with 8.33 kHz spacing<br>capacity|||
|---|---|---|---|---|---|---|---|
|flight/aircraftDescription/capa<br>bilities/communication/dataLi<br>nkCode|comNavApproa<br>chEquipICAO20<br>12_910c|Data Link Communication<br>Capabilities: The<br>serviceable equipment and<br>capabilities available on<br>the aircraft at the time of<br>flight that may be used to<br>communicate data to and<br>from the aircraft.|fx: DataLinkCodeType|No|**“J[1-7]”**<br>Where:<br>**“J1”**= CPDLC VDL Mode 2<br>**“J2”**= CPDLC FANS 1/A HFDL<br>**“J3”**= CPDLC FANS 1/A VDL<br>Mode A<br>**“J4”**= CPDLC FANS 1/A VDL<br>Mode 2<br>**“J5”**= CPDLC FANS 1/A SATCOM<br>(INMARSAT)<br>**“J6”**= CPDLC FANS 1/A SATCOM<br>(MTSAT)<br>**“J7”**= CPDLC FANS 1/A SATCOM<br>(Iridium)|**J2**|No|
|flight/aircraftDescription/capa<br>bilities/navigation/navigationC<br>ode|comNavApproa<br>chEquipICAO20<br>12_910c|The serviceable navigation<br>equipment available on<br>board of aircraft at the<br>time of flight and for which<br>the flight crew is qualified.<br>This element can contain a<br>combination of the ICAO<br>codes for navigation<br>capabilities:<br>{A,B,C,D,F,G,I,K,L,O,T,W,X}.|fx:<br>NavigationCodeType|No|**“[ABCDFGIKLOTWX]+”**<br>Where:<br>**“A”**– GBAS landing system<br>**“B”**= LPV<br>**“C”**= LORAN C<br>**“D”**= DME<br>**“F”**= ADF<br>**“G”**= GNSS<br>**“I”**= Inertial Navigation<br>**“K”**= MLS<br>**“L”**= ILS<br>**“O”**= VOR<br>**“T”**= TACAN<br>**“W”**= RVSM|**W**|No|

116

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||||**“X”**= MNPS||
|---|---|---|---|---|---|---|
|flight/aircraftDescription/capa<br>bilities/surveillance/surveillanc<br>eCode|survEquipICAO<br>2012_910d|This element describes the<br>aircraft surveillance code.|fx:SurveillanceCodeTyp<br>e|No|**“[AB1B2CD1EG1HILPSU1U2V1V2**<br>**X]”**<br>Where:<br>**“A”**– Transponder Mode A<br>**“B1“**– ADS-B with dedicated<br>1090 mHz ADS-B “out” capability<br>**“B2“**– ADS-B with dedicated<br>1090 mHz ADS-B “out” and “in”<br>capability<br>**“C“**– Transponder Mode A and C<br>**“D1“**– ADS-C with FANS 1/A<br>capabilities<br>**“G1“**- ADS-C with ATN<br>capabilities<br>**“E“**– Transponder – Mode S,<br>including aircraft identification,<br>pressure-altitude and extended<br>squitter Automated Dependent<br>Surveillance-Broadcast (ADS-B)<br>capability<br>**“H“**– Transponder – Mode S,<br>including aircraft identification,<br>pressure-altitude and enhanced<br>surveillance capability<br>**“I“**- Transponder – Mode S,<br>including aircraft identification,<br>but no pressure-altitude<br>capability<br>**“L“**– Transponder – Mode S,<br>including aircraft identification,<br>pressure-altitude, extended<br>squitter (ADS-B) and enhanced<br>surveillance capability<br>**“P“**– Transponder – Mode S,<br>including pressure-altitude, but<br>no aircraft identification<br>**“S“**– Transponder – Mode S,<br>including both pressure-altitude|**B2**<br>No|

117

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||||and aircraft identification<br>capability<br>**“U1“**- ADS-B “out” capability<br>using UAT<br>**“U2“**- ADS-B “out” AND “IN”<br>capability using UAT<br>**“V1“**- ADS-B “out” capability<br>using VDL Mode 4<br>**“V2“**- ADS-B “out” and “in”<br>capability using VDL Mode 4<br>**“X“**– Transponder - Mode S with<br>neither aircraft identification nor<br>pressure-altitude capability|||
|---|---|---|---|---|---|---|---|
|flight/arrival/arrivalAerodrome<br>Alternate/@code<br>or<br>flight/arrival/arrivalAerodrome<br>Alternate/point<br>flight/arrival/arrivalAerodrome<br>Alternate/@name|altAero_916c<br>or<br>ALTNIndicator_<br>918o|ICAO designator or the<br>name of an alternate<br>aerodrome to which an<br>aircraft may proceed,<br>should it become either<br>impossible or inadvisable<br>to land at the original<br>destination aerodrome or<br>an alternate destination<br>location.More than one<br>alternate arrival<br>aerodromes may be<br>specified for a flight.|_arrivalAerodromeAlter_<br>_nate_is of abstract type:<br>_fb:AerodromeReferenc_<br>_eType_<br>that can instantiate as:<br>_ff:IcaoAerodromeRefer_<br>_enceType_<br> if the aerodrome has<br>an ICAO designator, or:<br>_fb:UnlistedReferenceTy_<br>_pe,_otherwise.<br>Type of<br>_arrivalAerodromeAlter_<br>_nate/@code_:<br>_ff:IcaoAerodromeRefer_<br>_enceType_<br>Type of<br>_arrivalAerodrome/poin_<br>_t:_<br>_fb:SignificantPointType_<br>(abstract type that can<br>instantiate as:<br>_fb:FixPointType/_<br>_ff:GeographicalLocatio_<br>_nType/_|Yes|The aerodrome is specified using<br>its 4-letter ICAO name if it has<br>one.  If no ICAO location indicator<br>has been allocated, the<br>aerodrome is identified by its<br>name ("Dallas Fort Worth") or a<br>3-character IATA Alternate<br>Identifier ("DFW") and a<br>significant point consisting of one<br>of the following data:<br>•<br>geographic location (<br>latitude and longitude),<br>or<br>•<br>location of a fix<br>specified by name, or<br>•<br>fix/radial/distance<br>(FRD).<br>If the aerodrome has an ICAO<br>designator, the attribute_@code_<br>includes the ICAO code according<br>to the format:<br> **“[A-Z]{4}”**<br>Otherwise, if no ICAO location has<br>been allocated, the unlisted<br>aerodrome is identified by its<br>name (optionally) plus a|_@code_:<br>**KDFW**<br>_@name_:<br>**MILLSPAW FARM**<br>_point/@fix:_<br>**HBZ**<br>_point/distance_(_@uom_<br>**NAUTICAL_MILES):**<br>**10.0**<br>_point/radial_(_@uom_<br>**DEGREES**):<br>**236.0**|No|

118

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||_fb:RelativePointType_)<br>Type of<br>_arrivalAerodromeAlter_<br>_nate/@name_:<br>_fb:AerodromeNameTyp_<br>_e_||significant point according to the<br>following format:<br>_-arrivalAerodrome/@name_:<br>**xs:string**<br> -for _arrivalAerodrome/point_<br>there are three ways to specify<br>the significant point_:_<br>_1)_location of  fix<br>specified by name_(_type<br>f_b:FixPointType)_:<br> **“[A-Z0-9]{2,5}”**<br>_2)_geographic location<br>specified by latitude and<br>longitude<br>_(ff:GeographicalLocationType):_<br>- list of two**xs:double**<br>(latitude followed by longitude)<br>3) fix-radial-distance<br>(_fb:RelativePointType):_<br>(a) fix:<br> **“[A-Z0-9]{2,5}”**<br>(b) distance<br>(_ff:DistanceType_):<br> **xs:double**<br>(c) radial<br>(_fb:DirectionType_):<br> **xs:double**<br> minInclusive =<br>0<br>maxInclusive<br>=360||
|---|---|---|---|---|---|---|
|flight/agreed/route/estimated<br>ElapsedTime/location|EETIndicator_9<br>18b|This element specifies the<br>location associated with<br>the elapsed time from<br>takeoff to reach a<br>significant point or Flight<br>Information Region (FIR)<br>boundary along the route<br>of the flight.|fx:ElapsedTimeLocation<br>Type|_Yes_|The_location_associated with the<br>elapsed time can be_longitude_,<br>_significant point_or_region_(Flight<br>Information Region (FIR)<br>boundary):<br>-_longitude_:<br>**xs:double**<br>-_point_:|**KZNY**<br>No|

119

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||||- fb:FixPointType<br> **“[A-Z0-9]{2,5}”**<br>- ff:GeographicalLocationType<br>List of two**xs:double**<br>(latitude followed by longitude)<br>- fb:RelativePointType<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br>ff:DistanceType<br> **xs:double**<br>- radial:<br>fb:DirectionType<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360<br> -_region_:<br> **xs:string**|||
|---|---|---|---|---|---|---|---|
|flight/agreed/route/estimated<br>ElapsedTime/@elapsedTime|EETIndicator_9<br>18b|This element specifies the<br>estimated amount of time<br>from takeoff to reach a<br>significant point or Flight<br>Information Region (FIR)<br>boundary along the route<br>of the flight.|ff:DurationType|No|**xs:duration**|**PT1H46M**|No|
|flight/routeToRevisedDestinati<br>on/route/@routeText|RIFIndicator_91<br>8c|This attribute specifies the<br>ICAO route text of a route<br>to a revised destination<br>aerodrome. The route text<br>is as depicted from the<br>flight plan.|fb:FreeTextType|No|Free-form string of up to 4,096<br>characters.<br>The destination aerodrome has to<br>be specified using the four-letter<br>ICAO location code.|**DTA HEC KLAX**|No|
|flight/aircraftDescription/@reg<br>istration|REGIndicator_9<br>18d|A unique, alphanumeric<br>string that identifies a civil<br>aircraft and consists of the<br>Aircraft Nationality or<br>Common Mark and an<br>additional alphanumeric<br>string assigned by the state<br>of registry or common|fx:AircraftRegistrationT<br>ype|No|**“[A-Z0-9]{1,7}”**<br>Up to 4,096 characters.<br>NOTE<br>Pattern ([A-Z0-9]{1,7}) does not<br>always fit incoming data - leads<br>to validation errors.|**N5258E**|No|

120

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||mark registering authority.||||||
|---|---|---|---|---|---|---|---|
|flight/aircraftDescription/capa<br>bilities/communication/@sele<br>ctiveCallingCode|SELIndicator_9<br>18e|This attribute specifies the<br>Selective Calling (SELCAL)<br>Code that consists of two<br>2-letter pairs. SELCAL is a<br>selective-calling radio<br>system that alerts aircraft<br>crew to incoming radio<br>communications. It acts as<br>a paging system for an ATS<br>unit to establish voice<br>communications with the<br>pilot of an aircraft.|fx:SelectiveCodeType|No|**“[A-HJ-MP-S]{4}”**|**ACHA**<br>**BRLM**|No|
|flight/operator/operatingOrga<br>nization/organization/@name|OPRIndicator_9<br>18f|This attribute specifies the<br>full official name of the<br>State, Organization,<br>Authority, aircraft<br>operating agency, handling<br>agency engaged in or<br>offering to engage in<br>aircraft operation.|ff:TextNameType|No|xs:string<br>NOTE<br>Always map to organization.|UAL|No|
|flight/specialHandling|STSIndicator_9<br>18g|This element specifies the<br>special handling reason: a<br>property of the flight that<br>requires ATS units to give<br>it special consideration,<br>such as hospital aircraft.<br>There could be multiple<br>special handling indicators.|fx:SpecialHandlingCode<br>Type|No|The following are the only valid<br>special handling indicators:<br>**“ALTRV|ATFMX|FFR|FLTCK|HAZ**<br>**MAT|HEAD|HOSP|HUM|MARS**<br>**A|MEDEVAC|NONRVSM|SAR|S**<br>**TATE”**|**ALTRV**|No|
|flight/aircraftDescription/aircr<br>aftType/otherModelData|TYPIndicator_9<br>18h|Other, non-ICAO,<br>identification of the<br>aircraft.|fb:FreeTextType|No|Free-form string of up to 4,096<br>characters.|**CESNA140**|No|
|flight/aircraftDescription/@air|PERIndicator_9|A coded category assigned|fx:AircraftPerformance|No|Single valid letter specified in|**C**|No|

121

NAS-JMSDD-4309-001 Rev C July 10, 2018

|craftPerformance|18i|to the aircraft based on a<br>speed directly proportional<br>to its stall speed, which<br>functions as a standardized<br>basis for relating aircraft<br>maneuverability to specific<br>instrument approach<br>procedures.|CategoryType||PAN-OPS 8168 Volume 1:<br>**“[ABCDEH]”**<br>where:<br>**A**– Indicated airspeed (IAS) less<br>than 169 km/h (91kt)<br>**B**– IAS between 169 km/h (91kt)<br>and 224 km/h (121 kt)<br>**C**– IAS between 224 km/h (121<br>kt) and 261 km/h ( 141 kt)<br>**D**– IAS between 261 km/h ( 141<br>kt) and 307 km/h (166 kt)<br>**E**- IAS between 307 km/h (166 kt)<br>and 391 km/h (211 kt)<br>**H**- Helicopters|||
|---|---|---|---|---|---|---|---|
|flight/aircraftDescription/capa<br>bilities/communication/@othe<br>rCommunicationCapabilities|COMIndicator_<br>918j|This element contains<br>additional Communication<br>Equipment available on<br>aircraft not specified in the<br>route/@nasRouteText<br>attribute.|fb:FreeTextType|No|Free-form string of up to 4,096<br>characters.|**HF ONLY**<br>**TCAS**|No|
|flight/aircraftDescription/capa<br>bilities/communication/@othe<br>rDataLinkCapabilities|DATIndicator_9<br>18k|This element specifies data<br>link capabilities available<br>on the aircraft.|fb:FreeTextType|No|**“[SHVM]{1,4}”**<br>Free-form string of up to 4,096<br>characters.<br>where:<br>**S**– satellite data link<br>**H**– HF data link<br>**V**– VHF data link<br>**M**– SSR Mode S data link<br>One or more of the valid letters<br>may be specified in this element.|**SV**|No|
|flight/aircraftDescription/capa<br>bilities/navigation/@otherNavi<br>gationCapabilities|NAVIndicator_<br>918l|This element contains<br>Navigation Equipment<br>Data. It is used for<br>additional Navigation<br>Equipment available on|string|No|Free-form string of up to 4,096<br>characters.|**ADF ONLY**|No|

122

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||board of aircraft not<br>specified in the<br>route/@nasRouteText<br>attribute.|||||
|---|---|---|---|---|---|---|
|flight/departure/departureAer<br>odrome/@name<br>flight/departure/departureAer<br>odrome/point|DEPIndicator_9<br>18m|This element contains the<br>name of the unlisted<br>aerodrome from which the<br>flight departs.<br>If the departure<br>aerodrome has an ICAO<br>designator, it is stored in<br>the attribute<br>flight/departure/@departu<br>re Point, as suggested in<br>19.|_fb:UnlistedReferenceTy_<br>_pe_|Yes|The unlisted aerodrome is<br>identified by its name ("Dallas<br>Fort Worth") or 3-character IATA<br>Alternate Identifier (such as<br>"DFW”) plus a significant point<br>(_fb:UnlistedReferenceType_)<br>according to the following<br>format:<br>-_departureAerodrome/@name_:<br>**xs:string**<br> -_departureAerodrome/point:_<br>there are three ways to specify<br>the significant point_:_<br>_1)_fix location_(_type<br>f_b:FixPointType)_:<br> **“[A-Z0-9]{2,5}”**<br>_2)_location specified by<br>latitude and longitude<br>coordinates<br>_(ff:GeographicalLocationType):_<br>- list of two**xs:double**<br>(latitude followed by longitude)<br>3) fix-radial-distance<br>(_fb:RelativePointType):_<br>(a) fix:**xs:string**with<br>pattern:<br> **“[A-Z0-9]{2,5}”**<br>(b) distance<br>(_ff:DistanceType_):<br> **xs:double**<br>(c) radial<br>(_fb:DirectionType_):<br> **xs:double**<br> minInclusive = 0<br>maxInclusive|**DFW**<br>No|

123

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||||=360|||
|---|---|---|---|---|---|---|---|
|flight/arrival/arrivalAerodrome<br>/@name<br>flight/arrival/arrivalAerodrome<br>/point<br><br>|DESTIndicator_<br>918n|This elements includes the<br>name and location of the<br>unlisted aerodrome at<br>which the flight is<br>scheduled to arrive.<br>If the arrival aerodrome<br>has an ICAO designator, it<br>is stored in the attribute<br>flight/arrival/@arrivalPoint<br>, as suggested in 19.|Abstract type:<br>fb:AerodromeReferenc<br>eType<br>that instantiates as:<br>_fb:UnlistedReferenceTy_<br>_pe_<br>Type of<br>_arrivalAerodromeAlter_<br>_nate/@name_:<br>_fb:AerodromeNameTyp_<br>_e_<br>Type of<br>_arrivalAerodrome/poin_<br>_t:_<br>_fb:SignificantPointType_<br>(abstract type that can<br>instantiate as:<br>_fb:FixPointType/_<br>_ff:GeographicalLocatio_<br>_nType/_<br>_fb:RelativePointType_)|Yes|The unlisted aerodrome is<br>identified by its name (optionally)<br>plus a significant point according<br>to the following format:<br>_-arrivalAerodrome/@name_:<br>**xs:string**<br>-for _arrivalAerodrome/point_<br>there are three ways to specify<br>the significant point_:_<br>_1)_location of  fix<br>specified by name_(_type<br>f_b:FixPointType)_:<br> **“[A-Z0-9]{2,5}”**<br>_2)_geographic location<br>specified by latitude and<br>longitude<br>_(ff:GeographicalLocationType):_<br>- list of two**xs:double**<br>(latitude followed by longitude)<br>3) fix-radial-distance<br>(_fb:RelativePointType):_<br>(a) fix:<br> **“[A-Z0-9]{2,5}”**<br> (b) distance<br>(_ff:DistanceType_):<br> **xs:double**<br>(c) radial<br>(_fb:DirectionType_):<br> **xs:double**<br> minInclusive =<br>0<br>maxInclusive<br>=360|_@name_:<br>**MILLSPAW FARM**<br>_point/@fix:_<br>**HBZ**<br>_point/distance_(_@uom_<br>**NAUTICAL_MILES):**<br>**10.0**<br>_point/radial_(_@uom_<br>**DEGREES**):<br>**236.0**|No|
|flight/enRoute/alternateAerod<br>rome<br><br>|RALTIndicator_<br>918p|This element identifiesan<br>En Route Alternate<br>Aerodrome to which a<br>flight could be diverted<br>while en route, if needed.|Abstract type:<br>_fb:AerodromeReferenc_<br>_eType_that instantiates<br>as:<br>_ff:IcaoAerodromeRefer_|Yes|The aerodrome may be identified<br>by:<br>- ICAO code:<br>_alternateAerodrome/@code_:<br> **“[A-Z]{4}”**, or:|**KDFW**<br>or:<br>_@name_:<br>**MILLSPAW FARM**|No|

124

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||Multiple alternate<br>aerodromes may be<br>specified.|_enceType_<br>if the aerodrome has<br>an ICAO designator, or<br>as:<br>_fb:UnlistedReferenceTy_<br>_pe_otherwise.<br>_@code:_<br>_ff:IcaoAerodromeRefer_<br>_enceType_)<br>_@name_:<br>AerodromeNameType<br>_point:_<br>_fb:SignificantPointType_<br>(abstract type that can<br>instantiate as:<br>_fb:FixPointType/_<br>_ff:GeographicalLocatio_<br>_nType/_<br>_fb:RelativePointType_)||- name ("Dallas Fort Worth") or<br>3-character IATA Alternate<br>Identifier (such as "DFW”) plus<br>significant point, for an unlisted<br>aerodrome_,_according to the<br>following format:<br>_-alternateAerodrome/@name_:<br>**xs:string**<br>-for _alternateAerodrome/point_<br>there are three ways to specify<br>the significant point_:_<br>_1)_location of  fix<br>specified by name_(_type<br>f_b:FixPointType)_:<br> **“[A-Z0-9]{2,5}”**<br>_2)_geographic location<br>specified by latitude and<br>longitude<br>_(ff:GeographicalLocationType):_<br>- list of two**xs:double**<br>(latitude followed by longitude)<br>3) fix-radial-distance<br>(_fb:RelativePointType):_<br>(a)_point/@fix_:<br> **“[A-Z0-9]{2,5}”**<br> (b)_point/distance_<br>(_ff:DistanceType_):<br> **xs:double**<br>(c)_point/radial_<br>(_fb:DirectionType_):<br> **xs:double**<br> minInclusive = 0<br>  maxInclusive<br>=360|_point/@fix:_<br>**HBZ**<br>_point/distance_(_@uom_<br>**NAUTICAL_MILES):**<br>**10.0**<br>_point/radial_(_@uom_<br>**DEGREES**):<br>**236.0**||
|---|---|---|---|---|---|---|---|
|flight/aircraftDescription/@air<br>craftAddress|CODEIndicator<br>_918q|A code that enables the<br>exchange of text-based<br>messages between suitably<br>equipped Air Traffic Service<br>(ATS) ground systems and<br>aircraft cockpit displays<br>(the aircraft Controller-|fx:AircraftAddressType|No|**“[0-9A-F]{6}”**|**45FA16**|No|

125

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||Pilot Data Link<br>Communications (CPDLC)<br>address).||||||
|---|---|---|---|---|---|---|---|
|flight/aircraftDescription/capa<br>bilities/surveillance/@otherSu<br>rveillanceCapabilities|SURIndicator_9<br>18s|This element specifies the<br>surveillance applications or<br>capabilities not specified in<br>the attribute<br>_flight/agreed/route/@local_<br>_IntendedRoute_.<br>.|fb:FreeTextType|No|Free-form string of up to 4096<br>characters.|**282B**|No|
|flight/agreed/route/segment/r<br>outePoint/point|DLEIndicator_9<br>18t|The element<br>_routePoint/point_specifies<br>a single point along the<br>flight route.|fb:SignificantPointType<br>(abstract type)<br>_fb:FixPointType/_<br>_ff:GeographicalLocatio_<br>_nType/_<br>_fb:RelativePointType_|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-<br>_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br>minInclusive = 0<br>maxInclusive<br>=360|**MDG**|No|
|flight/agreed/route/segment/r<br>outePoint/@delayAtPoint|DLEIndicator_9<br>18t|The attribute<br>routePoint/@_delayAtPoint_<br>specifies the length of time<br>the flight is expected to be<br>delayed at this specific<br>point en route.|ff:DurationType|No|xs:duration|**PT46M**|No|
|flight/departure/takeoffAltern|TALTIndicator_|This element specifies an|fb:AerodromeReferenc|Yes|The aerodrome may be identified|**KDFW**|No|

126

NAS-JMSDD-4309-001 Rev C July 10, 2018

|ateAerodrome|918u|alternate aerodrome at<br>which an aircraft can land,<br>should it become<br>necessary shortly after<br>takeoff, and it is not<br>possible to land at the<br>departure aerodrome.<br>Multiple alternate takeoff<br>aerodromes may be<br>specified.|eType|by:<br>- its ICAO code ("KDFW")<br>(_ff:IcaoAerodromeReferenceType_)<br>in the attribute<br>_takeoffAlternateAerodrome/@co_<br>_de,_where the format is:<br> **“[A-Z]{4}”**<br>- its name ("Dallas Fort Worth")<br>or 3-character IATA Alternate<br>Identifier (such as "DFW”)<br>_takeoffAlternateAerodrome/@na_<br>_me_(optional) and a significant<br>point<br>_takeoffAlternateAerodrome/poin_<br>_t,_for an unlisted aerodrome<br>(_fb:UnlistedReferenceType_).<br>Format for<br>_takeoffAlternateAerodrome/@na_<br>_me:_<br>**xs:string**<br>Format for<br>_takeoffAlternateAerodrome_<br>_/point_:<br>-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|
|---|---|---|---|---|

127

NAS-JMSDD-4309-001 Rev C July 10, 2018

|flight/originator/aftnAddress<br>flight/originator/flightOriginat<br>or|ORGNIndicator<br>_918w|This element contains<br>information about the<br>flight originator that<br>initiated the flight. It<br>specifies the originator’s<br>eight-letter Aeronautical<br>Fixed Telecommunication<br>Network  (AFTN) station<br>address or other<br>appropriate contact<br>details, in cases where the<br>originator of the flight plan<br>may not be readily<br>identified, as required by<br>the appropriate ATS<br>authority.|Type of<br>_originator/aftnAddress_<br>:<br>fb:AftnAddressType<br>Type of<br>_originator/flightOrigin_<br>_ator_:<br>fb:FreeTextType|No|For_aftnAddress:_<br>**“[A-Z]{8}”**<br>For _flightOriginator:_<br>Free-form string of up to 4096<br>characters.|**LEBBYNYX**|No|
|---|---|---|---|---|---|---|---|
|flight/aircraftDescription/capa<br>bilities/navigation/performanc<br>eBasedCode|PBNIndicator_9<br>18x|This element specifies a<br>coded category denoting<br>which Required Navigation<br>Performance (RNP) and<br>Area Navigation (RNAV)<br>requirements can be met<br>by the aircraft while<br>operating in the context of<br>a particular airspace when<br>supported by the<br>appropriate navigation<br>infrastructure.|fx:PerformanceBasedC<br>odeType|No|**“A1|B[1-6]|C[1-4]|D[1-**<br>**4]|L1|O[1-4]|S[1-2]|T[1-2]”**<br>_RNAV_and_RNP_capabilities are<br>two-characters each, as follows:<br>_RNAV_specifications:<br>**A1**RNAV10 (RNP 10)<br>**B1**RNAV 5 all permitted sensors<br>**B2**RNAV 5 GNSS<br>**B3**RNAV 5 DME/DME<br>**B4**RNAV 5 VOR/DME<br>**B5**RNAV 5 INS or IRS<br>**B6**RNAV 5 LORANC<br>**C1**RNAV 2 all permitted sensors<br>**C2**RNAV 2 GNSS<br>**C3**RNAV 2 DME/DME<br>**C4**RNAV 2 DME/DME/IRU<br>**D1**RNAV 1 all permitted sensors<br>**D2**RNAV 1 GNSS<br>**D3**RNAV 1 DME/DME<br>**D4**RNAV 1 DME/DME/IRU<br>_RNP_specifications:|**B1O1**|No|

128

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||||**L1**RNP 4<br>**O1**Basic RNP 1 all permitted<br>sensors<br>**O2**Basic RNP 1 GNSS<br>**O3**Basic RNP 1 DME/DME<br>**O4**Basic RNP 1 DME/DME/IRU<br>**S1**RNP APCH<br>**S2**RNP APCH with BAR-VNAV<br>**T1**RNP AR APCH with RF (special<br>authorization required)<br>**T2**RNP AR APCH without RF<br>(special authorization required)||
|---|---|---|---|---|---|---|
|flight/aircraftDescription/accur<br>acy/cmsFieldType|RNVArrival_92<br>5a<br>…<br>RNVSpare1_92<br>5e<br>RNVSpare2_92<br>5f<br>RNPArrival…_9<br>25g<br>RNPEnroute_9<br>25h<br>…<br>RNPSpare1…_9<br>25k<br>RNPSpare2…_9<br>25l|The element_cmsFieldType_<br>contains the flight’s<br>navigation accuracy value<br>for the phase of flight,<br>specified in the<br>Performance-Based<br>Navigation Phase.|_ff:DistanceType_|Yes|xs:double|**0.3**<br>No|
|flight/aircraftDescription/accur<br>acy/cmsFieldType/@type|RNVArrival_92<br>5a<br>…<br>RNVSpare1_92<br>5e<br>RNVSpare2_92<br>5f|The attribute<br>_cmsFieldType/@type_<br>specifieswhether the<br>accuracy measure in<br>Performance-Based<br>Navigation Accuracy is<br>measuring Area Navigation<br>(RNAV) or Required|nas:CmsAccuracyTypeT<br>ype|No|**“RNV|RNP”**|**RNV**<br>No|

129

NAS-JMSDD-4309-001 Rev C July 10, 2018

||RNPArrival…_9<br>25g<br>RNPEnroute_9<br>25h<br>…<br>RNPSpare1…_9<br>25k<br>RNPSpare2…_9<br>25l|Navigation Performance<br>(RNP).|||||
|---|---|---|---|---|---|---|
|flight/aircraftDescription/accur<br>acy/cmsFieldType/@phase|RNVArrival_92<br>5a<br>…<br>RNVSpare1_92<br>5e<br>RNVSpare2_92<br>5f<br>RNPArrival…_9<br>25g<br>RNPEnroute_9<br>25h<br>…<br>RNPSpare1…_9<br>25k<br>RNPSpare2…_9<br>25l|The attribute<br>_cmsFieldType/@phase_<br>specifies the phase of flight<br>for which navigation<br>performance is being<br>recorded.|nas:NasPerformanceBa<br>sedNavigationPhaseTy<br>pe|No<br>**“DEPARTURE|ARRIVAL|ENROUT**<br>**E|OCEA NIC|SPARE_1|**<br>**SPARE_2”**|**ARRIVAL**|No|
|flight/aircraftDescription/accur<br>acy/cmsFieldType/@uom|RNVArrival_92<br>5a<br>…<br>RNVSpare1_92<br>5e<br>RNVSpare2_92<br>5f<br>RNPArrival…_9<br>25g<br>RNPEnroute_9<br>25h<br>…|The attribute<br>_cmsFieldType/@uom_<br>specifies the unit of<br>measure for the flight’s<br>navigation accuracy value.|_ff:DistanceMeasureTyp_<br>_e_|No<br>**“NAUTICAL_MILES|MILES|KILO**<br>**METERS”**|**NAUTICAL_MILES**|Yes|

130

NAS-JMSDD-4309-001 Rev C July 10, 2018

||RNPSpare1…_9<br>25k<br>RNPSpare2…_9<br>25l|||||
|---|---|---|---|---|---|
|flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@name<br>flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@value|ICAO1stAdapte<br>dField18_999a<br>ICAO1stAdapte<br>dField18_999b<br>ICAO1stAdapte<br>dField18_999c<br>ICAO1stAdapte<br>dField18_999d<br>ICAO1stAdapte<br>dField18_999e<br>ICAO1stAdapte<br>dField18_999f<br>ICAO1stAdapte<br>dField18_999g<br>ICAO1stAdapte<br>dField18_999h<br>ICAO1stAdapte<br>dField18_999i<br>ICAO1stAdapte<br>dField18_999j<br>ICAO1stAdapte<br>dField18_999k<br>ICAO1stAdapte<br>dField18_999l<br>ICAO1stAdapte<br>dField18_999m<br>ICAO1stAdapte<br>dField18_999n<br>ICAO1stAdapte<br>dField18_999o<br>ICAO1stAdapte<br>dField18_999p<br>ICAO1stAdapte<br>dField18_999q|<br>Additional information<br>about a flight that does not<br>fall into other predefined<br>category. The information<br>is expressed in key-value<br>pairs. The element consists<br>of an identification<br>tag/indicator and the<br>relevant value.<br>**NOTE**<br>There are 25 fields that<br>could be stored under<br>additionalFlightInformation<br>but only 10 slots allowed in<br>FIXM.  Additionally, SFDPS<br>is planning on using some<br>of these slots for storing a<br>number SFDPS specific<br>items that did not seem to<br>be a good choice for<br>addition in the FIXM U.S.<br>Extension.  Data analysis<br>has shown no more than<br>five of these adapted field<br>18 entries tend to appear<br>in the actual data feed but<br>this is a definite risk if more<br>begin to show up.|Type of<br>_additionalFlightInforma_<br>_tion_is a list of up to 10<br>name-value pairs:<br>_fb:NameValueListType_:<br>Type of_nameValue_:<br>_fb:NameValuePairType_<br>Type for attribute<br>_name_:<br>_fb:FreeTextType_<br>Type for attribute<br>_value_:<br>_fb:FreeTextType_|<br>No|Format for_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>Format for_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>No|

131

NAS-JMSDD-4309-001 Rev C July 10, 2018

|ICAO1stAdapte<br>dField18_999r<br>ICAO1stAdapte<br>dField18_999s<br>ICAO1stAdapte<br>dField18_999t<br>ICAO1stAdapte<br>dField18_999u<br>ICAO1stAdapte<br>dField18_999v<br>ICAO1stAdapte<br>dField18_999w<br>ICAO1stAdapte<br>dField18_999x<br>ICAO1stAdapte<br>dField18_999y|||||
|---|---|---|---|---|
|flight/agreed/route/@localInte<br>ndedRoute<br>localIntendedR<br>oute_10b|The Local Intended Route<br>attribute contains the flight<br>plan route that is<br>coordinated to penetrated<br>facilities. It consists of the<br>flight plan route merged<br>with any expected-to-be-<br>applied-by-the-controlling-<br>center Adapted Departure<br>Routes (ADRs), Adapted<br>Departure Arrival Routes<br>(ADARs) or Adapted Arrival<br>Routes (AARs). It is<br>intended for the clients<br>that wish to know the<br>expected state of the flight<br>plan when the current<br>facility releases control of<br>the flight. The attribute<br>localIntendedRoute<br>contains the filed route<br>(flight/agreed/route/@nas<br>RouteText) merged with<br>any locally applicable|_fb:FreeTextType_|No|**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-**<br>**9+\./]*\.[A-Z0-**<br>**9+/\*]{2,12}_?(/\d{4})?"**<br>Minimum length = 3<br>Maximum length = 4096<br>No|

132

NAS-JMSDD-4309-001 Rev C July 10, 2018

|||adapted routes<br>(preferential routes,<br>transition fixes and A-line<br>fixes). Optional<br>localIntendedRoute is sent<br>to ATM-IPOP, when the<br>localIntendedRoute is not<br>the same as filed route<br>(flight/agreed/route/@nas<br>RouteText).||||
|---|---|---|---|---|---|
|flight/agreed/route/@atcInten<br>dedRoute|ATCIntendedRo<br>ute_10c|The ATC Intended Route<br>route attribure contains<br>the current cleared flight<br>plan route with any<br>unacknowledged auto<br>routes(preferential routes,<br>transition fixes and A-line<br>fixes)already applied. The<br>ATC Intended Route<br>includes to-be-applied<br>AARs that are not to be<br>notified in the current<br>center. It is intended for<br>clients that wish to know<br>the currently expected<br>route of the flight across<br>contiguous ERAM airspace.<br>The attribute<br>route/@atcIntendedRoute<br>contains the filed route<br>(route/@nasRouteText)<br>merged with any adapted<br>routes (preferential routes,<br>transition fixes and A-line<br>fixes). Optional<br>route/@atcIntendedRoute<br>is sent to ATM-IPOP, when<br>parameter Merged ATC<br>Intended Route Switch<br>(MARS) is ON and if either<br>one of the following is true:|_fb:FreeTextType_|No|"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-<br>9+\./]*\.[A-Z0-<br>9+/\*]{2,12}_?(/\d{4})?"<br>Minimum length = 3<br>Maximum length = 4096<br>No|

133

NAS-JMSDD-4309-001 Rev C July 10, 2018

|If|
|---|
|route/@localIntendedRout<br>e exists and<br>route/@atcIntendedRoute|
|is not the same as|
|route/@localIntendedRout<br>e|
|If|
|route/@localIntendedRout<br>e does not exist and|
|route/@atcIntendedRoute|
|is not the same as|
|route/@nasRouteText.|

##### **5.5.1.5 Flight Amendment Information [AH] – Data Elements**

See Data Elements for Flight Plan [FH]: Section 5.5.1.3.

##### **5.5.1.6 Flight Amendment Information [AH] – Diagram**

See Diagram for Flight Plan [FH]: Section 5.5.1.3.

##### **5.5.1.7 Flight Amendment Information in FIXM Format [AH_FIXM] – Data Elements**

See Data Elements for Flight Plan in FIXM Format [FH_FIXM]: Section 5.5.1.4.

134

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.8 Converted Route Information [HX] - Data Elements**

|**Element Name**<br>**[HX]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed<br>by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and the<br>last four-digits, represent the message<br>sequence number in the range [0000-<br>9999].|**2359359001**<br>where the first 6 digits<br>are the UTC time<br>(23:59:35 UTC) and the<br>last 4 digits are sequence<br>number of the message<br>(9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:_hh_<br>stands for the 2-digit-hour in the range<br>00-23,_mm_stands for the 2-digit minutes<br>in the range 00-59, and_ss_stands for the<br>2-digit seconds in the range 00-59.|**23_59_35**<br>that represents 23:59:35<br>UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O.**|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It<br>is assigned by IFPA to uniquely<br>identify a flight plan in each<br>ERAM facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|fixTimes|This element specifies the fix<br>and calculated time of arrival<br>at each fix that describes the||Yes|Sequence of_fixTime_68c_elements.<br>Minimum number of elements = 3.||Yes|

135

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HX]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||aircraft’s ERAM converted<br>route of flight.|||Maximum number of elements = 326|||
|fixTime_68c|This element contains a fix<br>and the expected time of<br>arrival at the fix in hours and<br>minutes.|string|No|**"([A-Z0-9]{2,5}/\d{4}) |**<br>**([A-Z0-9]{2,5}\d{6}/\d{4}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?/\d{4}) "**<br>The format consists of a valid<br>representation of a fix (see element<br>coordFix_06a in the FH message table),<br>followed by a virgule, and is followed by<br>time in_hhmm_format.<br>Minimum length = 7<br>Maximum length = 17|**LFT/1800**<br>**JIMIE004034/1320**|Yes|
|fixAndTime|If it is included in the message,<br>this element specifies the fix<br>and calculated time of arrival<br>at each fix that describes the<br>aircraft’s ERAM converted<br>route of flight. The fix and<br>time of arrival at the fix are<br>specified in a format that<br>breaks down the fix and the<br>time in separate elements:<br>fix_68c1 and<br>crossingTime_68c2.||Yes|Sequence of elements _fix_68c1_and<br>_crossingTime_68c2_, specified between 3<br>and 326 times.||No|
|fix_68c1|This element specifies the fix<br>component of the element<br>_fixTime_68c_.|string|No|**“([A-Z0-9]{2,5})|**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)|**<br>**([A-Z0-9]{3,4}}"**<br>The format consists of a valid<br>representation of a fix (see element<br>coordFix_06a in the FH message table).|**KDFW**<br>**3500N/04000W**|No|
|crossingTime_68c2|This element specifies the<br>time component of the<br>element_fixTime_68c_.|dateTime|No|The format is_dateTime_, and not_hhmm_as<br>it is in the_fixTime_68c_element.|**2014-06-20T20:17:52**|No|

136

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.9 Converted Route Information [HX]- Diagram**

137

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.10 Converted Route Information FIXM format (HX_FIXM) – Data Elements**

The following elements of the HX message in Simple XML format are not used in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

- FixTimes

- fixTime_68c

|**Name**<br>**[HX_FIXM]**|**Name**<br>**[HX]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|<br>**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@name<br>flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@value|FDPS_SequenceNo|Sequence number assigned<br>by SFDPS to each message<br>it receives from HADDS.<br>The attribute_name_<br>includes the constant<br>string"MSG_SEQ_NO",<br>and the attribute_value_<br>contains the sequence<br>number value.|fb:FreeTextType|No|”MSG_SEQ_NO”<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|name="MSG_SEQ<br>_NO"<br>value="6860416"|Yes|
|flight/departure/@departu<br>rePoint|FDPS_Origin/departurePoint<br>_26a|Attribute used to specify<br>the first point or other<br>initial entity where the air<br>traffic<br>control/management<br>system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name,<br>lat/long, or fix-radial-<br>distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arrivalPoint|destination_27a|The final point or other<br>final entity where the air<br>traffic|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**|**AB**<br>**DFW**<br>**KDFW**|No|

138

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HX_FIXM]**|**Name**<br>**[HX]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|<br>**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|||control/management<br>system route terminates.|||**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name,<br>lat/long, or fix-radial-<br>distance), including the<br>standard airport designators.|**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**||
|flight/operator/operatingO<br>rganization/organization/<br>@name|FDPS_FlightOperator/O<br>icator_918f|PRInd<br>Attribute used to specify<br>the full official name of the<br>State, Organization,<br>Authority, aircraft<br>operating agency, handling<br>agency engaged in or<br>offering to engage in<br>aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/flightIdentification/<br>@aircraftIdentification|flightId_02a|Name used by Air Traffic<br>Services units to identify<br>and communicate with an<br>aircraft.|fb:FlightIdentifierType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@name<br>flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@value||The flight supplemental<br>data is used to indicate<br>that a flight message is a<br>test message, by setting<br>the attribute_name_to<br>“**SIMULATED_FLIGHT**” and<br>the attribute_value_to<br>“**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLIG**<br>**HT”**<br>@value =**“true”**|No|
|flight/@system|propSourceSystem|This attribute indicates<br>which SFDPS system<br>generated the message.|fb:ProvenanceSystemType|No|xs:string<br>maxLength=128|ATL|Yes|

139

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HX_FIXM]**|**Name**<br>**[HX]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/@timestamp|propRcvdTime|This attribute conatins the<br>time at which the message<br>was received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the<br>code of the ARTCC (or<br>FIR) that produced the<br>data.|fb:ProvenanceCentreType|No|xs:string|`ZAU`|Yes|
|flight/arrival/runwayPositio<br>nAndTime/runwayTime/[es<br>timated|actual]/@time|arrivalTime|This attribute specifies the<br>proposed or the actual<br>time of arrival at<br>destination, set according<br>to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/departure/runwayPo<br>sitionAndTime/runwayTim<br>e/[actual|estimated]/@tim<br>e|departureTime|This element specifies the<br>proposed or actual<br>departure time, set<br>according to the flight<br>state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/flightStatus/@fdpsFli<br>ghtStatus|flightState|This attribute contains the<br>current status of the flight<br>as specified by SFDPS.|nas:SfdpsFlightStatusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLET<br>ED|CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@name<br>flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@value|fdpsGufi|The name value pair<br>specifies the SFDPS GUFI,<br>an identifier on every<br>message that positively<br>identifies what flight the<br>message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-<br>Za-z0-9/]+"|name="FDPS_GUF<br>I"<br>value="us.fdps.20<br>15-12-<br>18T16:59:10Z.000<br>/14/100"/>|Yes|
|flight/flightPlan/@identifie<br>r|eramGufi_316a|This attribute specifies the<br>unique flight plan<br>identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|

140

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HX_FIXM]**|**Name**<br>**[HX]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|<br>**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/gufi|uuidGufi|This element contains a<br>reference that uniquely<br>identifies a flight and that<br>is independent of any<br>particular system. This<br>reference conforms to the<br>Universal Unique Identifier<br>standard.|fb:GloballyFlightIdentifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-<br>F]{4}\-4[0-9a-fA-F]{3}\-<br>[89aAbB][0-9a-fA-F]{3}\-[0-9a-<br>fA-F]{12}"|4aaf92be-ac0a-<br>4dba-998f-<br>9e56f5d450b6|Yes|
|flight/flightIdentification/<br>@siteSpecificPlanId|sspId_167a|Site Specific Plan<br>Identifier. It is assigned by<br>Instrument Flight<br>Procedures Automation<br>(IFPA) to uniquely identify<br>a flight plan in each ERAM<br>facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/agreed/route/expan<br>dedRoute/routePoint/poin<br>t|fix_68c1|A route may contain an<br>optional expanded route<br>that consists of an ordered<br>list of expanded route<br>points.<br>The expanded route<br>represents the expansion<br>of the route into a list of<br>points which describe the<br>aircraft’s expected 2D path<br>from the departure<br>aerodrome to the arrival<br>aerodrome.<br>This element specifies a<br>single point that is part of<br>the aircraft’s expanded<br>route of flight.|fb:SignificantPointType (abstract type)<br>_fb:FixPointType/_<br>_ff:GeographicalLocationType/_<br>_fb:RelativePointType_|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-<br>_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive=0<br>maxInclusive=360|**KDFW**|No|

141

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HX_FIXM]**|**Name**<br>**[HX]**|**Element Definition**||**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|---|
|flight/agreed/route/expan<br>dedRoute/routePoint/@est<br>imatedTime|crossingTime_68c2|This element specifies the<br>estimated time over the<br>expanded route point.|ff:TimeType||No|xs:dateTime|**2014-06-**<br>**20T20:17:52**|No|

##### **5.5.1.11 Cancellation Information [CL] - Data Elements**

|**Element Name**<br>**[CL]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed<br>by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four-digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of<br>the message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|

142

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[CL]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It<br>is assigned by IFPA to uniquely<br>identify a flight plan in each<br>ERAM facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|departurePoint_26a|The departure point is the<br>point at which to start<br>processing a flight plan as<br>follows: the departure airport,<br>or the airfile point. When the<br>flight plan represents an airfile,<br>originating within this center<br>area, this element contains the<br>airfile point.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the allowed ways to represent a<br>fix can be used in this field, including the<br>standard airport designators. A fix name,<br>lat/long or fix-radial-distance can also be<br>used.|**AB**<br>**KDFW**<br>**SHP090015**<br>**3500N/04000W**|Yes|
|destination_27a|The destination is the point<br>where to end processing the<br>flight plan.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the allowed ways to represent a<br>fix can be used in this field, including the<br>standard airport designators. A fix name,<br>lat/long or fix-radial-distance can also be<br>used.|**AB**<br>**KDFW**<br>**SHP090015**<br>**3500N/04000W**|Yes|
|T_fix|The allowed ways to represent<br>a fix can be used in this field,<br>including the standard airport<br>designators.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**|**AB**<br>**KDFW**<br>**SHP090015**<br>**3500N/04000W**||

143

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.12 Cancellation Information [CL] – Diagram**

##### **5.5.1.13 Cancellation Information in FIXM Format [CL_FIXM] – Data Elements**

The following elements of the CL message in Simple XML format are not used in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

|**Name**<br>**[CL_FIXM]**|**Name**<br>**[CL]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|<br>**Format/Permissible**<br>**Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@name<br>flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@value|FDPS_SequenceNo|Sequence number assigned by SFDPS to<br>each message it receives from HADDS. The<br>attribute_name_includes the constant string<br>"MSG_SEQ_NO", and the attribute_value_<br>contains the sequence number value.|@name and @value:<br>fb:FreeTextType<br>|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive|@name="MSG_<br>SEQ_NO"<br>@value="68604<br>16"|Yes|

144

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[CL_FIXM]**|**Name**<br>**[CL]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
||||||value="999999999"|||
|flight/operator/operatingOrganization<br>/organization/@name|FDPS_FlightOperator/OPRIn<br>dicator_918f|Attribute used to specify the full official<br>name of the State, Organization, Authority,<br>aircraft operating agency, handling agency<br>engaged in or offering to engage in aircraft<br>operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/@system|propSourceSystem|This attribute indicates which SFDPS system<br>generated the message.|fb:ProvenanceSyste<br>mType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTime|This attribute conatins the time at which the<br>message was received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.02<br>8Z|Yes|
|flight/@centre|center|This attribute specifies the code of the<br>ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCentre<br>Type|No|xs:string|ZAU|Yes|
|flight/departure/runwayPositionAndTi<br>me/runwayTime/actual/@time|departureTime|This element specifies the actual departure<br>time.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/flightStatus/@fdpsFlightStatus|flightState|This attribute contains the current status of<br>the flight as specified by SFDPS.|nas:SfdpsFlightStatus<br>Type|Yes|xs:string<br>“PROPOSED|ACTIVE|COM<br>PLETED|CANCELLED|DRO<br>PPED”|ACTIVE|Yes|
|flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@name<br>flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@value|fdpsGufi|The name value pair specifies the SFDPS<br>GUFI, an identifier on every message that<br>positively identifies what flight the message<br>is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[<br>A-Za-z0-9/]+"|name="FDPS_G<br>UFI"<br>value="us.fdps.<br>2015-12-<br>18T16:59:10Z.0<br>00/14/100"/>|Yes|
|flight/flightPlan/@identifier|eramGufi_316a|This attribute specifies the unique flight plan<br>identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|This element contains a reference that<br>uniquelyidentifies a flight and that is|fb:GloballyFlightIden<br>tifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-|4aaf92be-ac0a-<br>4dba-998f-|Yes|

145

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[CL_FIXM]**|**Name**<br>**[CL]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|<br>**Format/Permissible**<br>**Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|||independent of any particular system. This<br>reference conforms to the Universal Unique<br>Identifier standard.|||F]{4}\-4[0-9a-fA-F]{3}\-<br>[89aAbB][0-9a-fA-F]{3}\-<br>[0-9a-fA-F]{12}"|9e56f5d450b6||
|flight/flightIdentification/@aircraftIde<br>ntification|flightId_02a|Name used by Air Traffic Services units to<br>identify and communicate with an aircraft.|fb:FlightIdentifierTyp<br>e|No|"[A-Z0-9]{7}"|AAL20|Yes|
|flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@name<br>flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@value||The flight supplemental data is used to<br>indicate that a flight message is a test<br>message, by setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the attribute<br>_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1,**<br>**maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_F**<br>**LIGHT”**<br>@value =**“true”**|No|
|flight/flightIdentification/@computerI<br>d|computerId_02d|A unique identification assigned by ERAM to<br>each flight plan.|fb:FreeTextType|No|**"[0-9][A-HJ-NP-Z0-9]{2}”**<br>The element includes a<br>digit, followed by two<br>alphanumeric characters<br>with the exception of the<br>letters**I**and**O**, such as<br>_ddd, ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/@siteSpecifi<br>cPlanId|sspId_167a|Site Specific Plan Identifier. It is assigned by<br>Instrument Flight Procedures Automation<br>(IFPA) to uniquely identify a flight plan in<br>each ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/departure/@departurePoint|departurePoint_26a|It is used to specify the first point or other<br>initial entity where the air traffic<br>control/management system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-**|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|

146

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[CL_FIXM]**|**Name**<br>**[CL]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|<br>**Format/Permissible**<br>**Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
||||||**Z]?)”**<br>Any of the standard ways<br>to represent a fix can be<br>used for this element (fix<br>name, lat/long, or fix-<br>radial-distance), including<br>the standard airport<br>designators.|||
|flight/arrival/@arrivalPoint|destination_27a|The final point or other final entity where<br>the air traffic control/management system<br>route terminates.|fb:FreeTextType|No|**xs:string**<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-**<br>**Z]?)”**<br>Any of the standard ways<br>to represent a fix can be<br>used for this element (fix<br>name, lat/long, or fix-<br>radial-distance), including<br>the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|

##### **5.5.1.14 Departure Information [DH] - Data Elements**

|**Element Name**<br>**[DH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed by<br>a four-digit sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four-digits, represent the<br>message sequence number in the range|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are|Yes|

147

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||[0000-9999].|sequence number of<br>the message (9001).||
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the sourceId_00e<br>element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each<br>ERAM facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|numberOfAircraft_03<br>a|This element includes the<br>number of aircraft for the flight<br>followed optionally by the<br>Special Aircraft Indicator.|string|No|**"\d{0,2}[A-Z]?"**<br>The element consists of zero to two<br>digits optionally followed by one<br>uppercase letter to represent the Special<br>Aircraft Indicator. The indicator can also<br>appear on its own (without the leading|**3H**<br>The number of<br>aircraft is 3 and the<br>special aircraft<br>indicator is**H**for<br>Heavy Jet.|No|

148

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||digits).|||
|typeOfAircraft_03c|Type of aircraft.|string|No|**"[A-Z][A-Z0-9]{1,3}"**<br>The element consists of one letter<br>followed by one to three alphanumeric<br>characters.|**B747**|Yes|
|airborneEquip_03e|Airborne equipment qualifier. It<br>consists of one alphanumeric<br>character.|string|No|**"[A-Z]"**<br>The element consists of one<br>alphanumeric character, that can have<br>one of the following values:<br>**A**- Transponder with no Mode C<br>**B**- Transponder with Mode C<br>**E**–FMS with DME/DME and IRU position<br>updating<br>**G**– GNSS, including GPS or WAAS, with<br>en-route and terminal capability<br>**X**– No transponder<br>**W**- RVSM|**E**|No|
|departurePoint_26a|The departure point is the point<br>at which to start processing a<br>flight plan as follows: the<br>departure airport, or the airfile<br>point. When the flight plan<br>represents an airfile, originating<br>within this center area, this<br>element contains the airfile<br>point.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the allowed ways to represent a<br>fix can be used in this field, including the<br>standard airport designators. A fix name,<br>lat/long or fix-radial-distance can also be<br>used.|**AB**<br>**KDFW**<br>**SHP090015**<br>**3500N/04000W**|Yes|
|coordStatusTime_07d|Coordination time that<br>represents the starting time in<br>hours and minutes at the<br>coordination fix.|string|No|**"((A|D|E|P|F)[0-1][0-9][0-5][0-9) |**<br>**((A|D|E|P|F)2[0-3][0-5][0-9])”**<br>The element includes one letter<br>(possible values are**A**,**D, E**,**P**, or**F**)<br>followed by four-digits that represent<br>time as_hhmm_.|**P1020**|Yes|
|coordStatus_07d1|The coordStatus field is the<br>single letter**A**,**D**,**E**,**F**, or**P**, as<br>described for element|string|No|**“(A|D|E|P|F)”**|**F**|Yes|

149

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||coordStatusTime_07d.||||||
|coordTime_07d2|Starting time at the<br>coordination fix.|dateTime|No||**2014-06-**<br>**20T20:17:52**|Yes|
|destination_27a|The destination is the point<br>where to end processing the<br>flight plan.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the allowed ways to represent a<br>fix can be used in this field, including the<br>standard airport designators. A fix name,<br>lat/long or fix-radial-distance can also be<br>used.|**AB**<br>**KDFW**<br>**SHP090015**<br>**3500N/04000W**|Yes|
|ETA_28a|Estimated Time of Arrival (ETA)<br>at destination in hours and<br>minutes. ETA supplied only if<br>the Estimated Time Enroute<br>(ETE) was filed with the flight<br>plan.|string|No|**“\d{4}”**<br>Four-digits representing time in format<br>_hhmm_.|**1720**|No|

150

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.15 Departure Information [DH] - Diagram**

151

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.16 Departure Information Message in FIXM Format [DH_FIXM] – Data Elements**

The following elements of the DH message in Simple XML format are not traslated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

- coordStatusTime_07d

|**Name**<br>**[DH_FIXM]**|**Name**<br>**[DH]**|**Element Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@name<br>flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@value|FDPS_S<br>equenc<br>eNo|Sequence number assigned by SFDPS to each<br>message it receives from HADDS. The attribute<br>_name_includes the constant string<br>"MSG_SEQ_NO", and the attribute_value_<br>contains the sequence number value.|@name and<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive value="999999999"|@name="MSG_S<br>EQ_NO"<br>@value="686041<br>6"|Yes|
|flight/operator/operatingOrga<br>nization/organization/@name|FDPS_Fl<br>ightOpe<br>rator/O<br>PRIndic<br>ator_91<br>8f|Attribute used to specify the full official name<br>of the State, Organization, Authority, aircraft<br>operating agency, handling agency engaged in<br>or offering to engage in aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/@system|propSo<br>urceSys<br>tem|This attribute indicates which SFDPS system<br>generated the message.|fb:ProvenanceSyst<br>emType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcv<br>dTime|This attribute conatins the time at which the<br>message was received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the code of the ARTCC<br>(or<br>FIR) that produced the data.|fb:ProvenanceCent<br>reType|No|xs:string|`ZAU`|Yes|
|flight/departure/runwayPo<br>sitionAndTime/runwayTime<br>/actual/@time|departu<br>reTime|This element specifies the actual departure<br>time.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|

152

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DH_FIXM]**|**Name**<br>**[DH]**|**Element Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/flightStatus/@fdpsFlight<br>Status|flightSta<br>te|This attribute contains the current status of<br>the flight as specified by SFDPS.|nas:SfdpsFlightStat<br>usType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETED|<br>CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@name<br>flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@value|fdpsGuf<br>i|The name value pair specifies the SFDPS GUFI,<br>an identifier on every message that positively<br>identifies what flight the message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-z0-<br>9/]+"|name="FDPS_GU<br>FI"<br>value="us.fdps.20<br>15-12-<br>18T16:59:10Z.000<br>/14/100"/>|Yes|
|flight/flightPlan/@identifier|eramGu<br>fi_316a|This attribute specifies the unique flight plan<br>identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGuf<br>i|This element contains a reference that uniquely<br>identifies a flight and that is independent of any<br>particular system. This reference conforms to<br>the Universal Unique Identifier standard.|fb:GloballyFlightId<br>entifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-4[0-<br>9a-fA-F]{3}\-[89aAbB][0-9a-fA-<br>F]{3}\-[0-9a-fA-F]{12}"|4aaf92be-ac0a-<br>4dba-998f-<br>9e56f5d450b6|Yes|
|flight/flightIdentification/@air<br>craftIdentification|flightId_<br>02a|Name used by Air Traffic Services units to<br>identify and communicate with an aircraft.|fb:FlightIdentifierT<br>ype|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@name<br>flight/supplementalData/additi<br>onalFlightInformation/nameVa<br>lue/@value||The flight supplemental data is used to indicate<br>that a flight message is a test message, by<br>setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the attribute_value_<br>to “**true**”.|@_name:_<br>_@value_:<br>fb:FreeTextType|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLI**<br>**GHT”**<br>@value =**“true”**|No|
|flight/flightIdentification/@co<br>mputerId|comput<br>erId_02<br>d|A unique identification assigned by ERAM to<br>each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**,such as_ddd,_|**020**|No|

153

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DH_FIXM]**|**Name**<br>**[DH]**|**Element Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
||||||_ddL, dLd, dLL_.|||
|flight/flightIdentification/@sit<br>eSpecificPlanId|sspId_1<br>67a|Site Specific Plan Identifier. It is assigned by<br>Instrument Flight Procedures Automation<br>(IFPA) to uniquely identify a flight plan in each<br>ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/aircraftDescription/@air<br>craftQuantity|number<br>OfAircra<br>ft_03a|Number of aircraft flying in formation in which<br>the aircrafts are governed by one flight plan.|fb:countType|No|**"\d{0,2}"**<br>The element consists of zero to two<br>digits.|**3**|No|
|flight/aircraftDescription/@tf<br>msSpecialAircraftQualifier|number<br>OfAircra<br>ft_03a-<br>Special<br>Aircraft<br>Indicato<br>r|This element includes the Special Aircraft<br>Indicator. It indicates the flight is a heavy jet,<br>B757 or, if not present, a large jet and if the<br>flight is either equipped or not with TCAS. This<br>indicator is used for output purposes such as<br>strip printing and message transfers to other<br>facilities such as Automated Radar Terminal<br>System (ARTS).<br>NOTE<br>TFMS Special Aircraft Qualifier is a bad fit to<br>Special Aircraft Indicator but no other fields<br>seem to fit.|nas:NasSpecialAirc<br>raftQualifierType|No|**“HEAVY_JET|TCAS|B757|HEAVY_J**<br>**ET_AND_TCAS”**<br>**“HEAVY_JET”**= Capable of takeoff<br>weights of 300,000 pounds or more<br>**“TCAS”**= Traffic collision avoidance<br>system or traffic alert and collision<br>avoidance system<br>**“B757”**= Controllers are required<br>to apply the special wake<br>turbulence separation criteria for<br>the Boeing 757.<br>**“HEAVY_JET_AND_TCAS”**=<br>Capable of takeoff weights of<br>300,000 pounds or more and traffic<br>collision avoidance system.|**HEAVY_JET**|No|
|flight/aircraftDescription/aircr<br>aftType/icaoModelIdentifier|typeOfA<br>ircraft_<br>03c|The ICAO code of the aircraft type.|fb:IcaoAircraftIdent<br>ifierType|No|**"[A-Z][A-Z0-9]{1,3}"**<br>The element consists of one letter<br>followed by one to three<br>alphanumeric characters.|**B747**|Yes|

154

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DH_FIXM]**<br>**Name**<br>**[DH]**|**Element Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|
|flight/aircraftDescription/@eq<br>uipmentQualifier<br>airborn<br>eEquip_<br>03e|Airborne equipment qualifier. A value assigned<br>to the aircraft, based on its navigational<br>equipment, whether or not it has a<br>transponder, and if it has a transponder,<br>whether the transponder supports Mode C.|nas:NasAirborneEq<br>uipmentQualifierTy<br>pe|No|**" [ ABCDGHILMNPSTUVWXYZ]"**<br>The element consists of one<br>alphanumeric character, that can<br>have one of the following values:<br>•<br>“X”= No RVSM, No DME,<br>No transponder<br>•<br>“T”= No RVSM, No DME,<br>Transponder with no<br>mode C<br>•<br>“U”= No RVSM, No DME:<br>Transponder with mode C<br>•<br>“D”= DME: No<br>transponder<br>•<br>“B”= DME: Transponder<br>with no mode C<br>•<br>“A”= DME: Transponder<br>with mode<br>•<br>“M”= TACAN ONLY: No<br>transponder<br>•<br>“N”= TACAN ONLY:<br>Transponder with no<br>mode C<br>•<br>“P”= TACAN ONLY:<br>Transponder with mode C<br>•<br>“C”= “Y”=<br>LORAN,VORDME,INS,RNA<br>V: No transponder<br>•<br>“I”=<br>LORAN,VORDME,INSRNA<br>V: Transponder with<br>mode C<br>•<br>“H”= RVSM, Failed<br>transponder or Failed<br>Mode C capability<br>•<br>“S=ADVANCED RNAV,<br>TRANSPONDER,MODE C:|**E**|No|

155

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DH_FIXM]**|**Name**<br>**[DH]**|**Element Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
||||||FMS with DMEDME<br>position updating<br>•<br>“G”= ADVANCED RNAV,<br>TRANSPONDER, MODE C:<br>Global Navigation<br>Satellite System (GNSS),<br>including GPS or Wide<br>Area Augmentation<br>System (WAAS), with<br>enroute and terminal<br>capability<br>•<br>“V”= ADVANCED RNAV,<br>TRANSPONDER, MODE C:<br>Required Navigational<br>Performance (RNP). The<br>aircraft meets the RNP<br>type prescribed for the<br>route segments, routes<br>and/or area concerned.<br>•<br>“Z”= REDUCED VERTICAL<br>SEPARATION MINIMUM<br>(RVSM): E with RVSM<br>•<br>“L”= REDUCED VERTICAL<br>SEPARATION MINIMUM<br>(RVSM): G with RVSM<br>“W”= REDUCED VERTICAL<br>SEPARATION MINIMUM (RVSM):<br>RVSM|||
|flight/departure/@departureP<br>oint|departu<br>rePoint<br>_26a|It is used to specify the first point or other<br>initial entity where the air traffic<br>control/management system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance),includingthe|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|

156

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DH_FIXM]**|**Name**<br>**[DH]**|**Element Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
||||||standard airport designators.|||
|flight/coordination/@coordina<br>tionTimeHandling|coordSt<br>atus_07<br>d1|The indicator for the type of Coordination Time.|nas:CoordinationTi<br>meType|No|**“(P|D|E|A)”**<br>**“P”**= Proposed flight plan.<br>**“D”**= Aircraft has departed from the<br>departure airport.<br>**“E”**= Active aircraft.<br>**“A”**= Aircraft arrived at the<br>destination airport.|**P**|Yes|
|flight/coordination/@coordina<br>tionTime|coordTi<br>me_07d<br>2|Coordination Time: the time to be used in<br>conjunction with the Coordination Fix so<br>processing for this flight can be synchronized<br>for the next sector/facility.|ff:TimeType|No|**xs:dateTime**|**2014-06-**<br>**20T20:17:52**|Yes|
|flight/arrival/@arrivalPoint|destinat<br>ion_27a|<br>The final point or other final entity where the<br>air traffic control/management system route<br>terminates.|fb:FreeTextType|No|**xs:string**<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|flight/arrival/runwayPositionA<br>ndTime/runwayTime/estimate<br>d/@time|ETA_28<br>a|Estimated Time of Arrival (ETA) at destination.<br>ETA supplied only if the Estimated Time<br>Enroute (ETE) was filed with the flight plan.|ff:TimeType|No|**xs:dateTime**|**2014-06-**<br>**20T20:17:52**|No|

157

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.17 Aircraft Identification Amendment Information [IH] - Data Elements**

|**Element Name**<br>**[IH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_)<br>and the last four-digits, represent the<br>message sequence number in the<br>range [0000-9999].|**2359359001**<br>where the first 6<br>digits are the UTC<br>time (23:59:35 UTC)<br>and the last 4 digits<br>represent the<br>sequence number of<br>the message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format_hh_mm_ss_, where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-<br>digit minutes in the range 00-59, and<br>_ss_stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of<br>the sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|9001|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed<br>by two alphanumeric characters with<br>the exception of the letters**I**and**O**.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|

158

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[IH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||facility.||||||
|newFlightId_02aN|The new Aircraft ID, or flight ID<br>(also called Call Sign), that has been<br>changed by the IH message.|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>It has a variable format, starting with<br>one uppercase alphabetic character,<br>followed by one to six alphanumeric<br>characters. When it is only two<br>characters long, the format must be<br>one letter followed by one digit, such<br>as**A1**for Air Force One.|**DAL52**|Yes|
|newComputerId_02d<br>N|This element contains the new<br>Computer ID that has been<br>changed by the IH message.|string|No|**"([0-9][A-HJ-NP-Z0-9]{2}) |**<br>**([A-HJ-NP-Z]{3}) |**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The computer ID is represented by<br>three alphanumeric characters, as<br>specified by the pattern above The<br>letters I and**O**are prohibited. One<br>special all alphabetic code may be<br>used, literally, XXX. This is only used<br>in DA (Data Accept) messages in<br>response to an ARTS VFR flight plan<br>input.|**436**|No|
|newSspId_167aN|This element contains the new Site<br>Specific Plan Identifier that has<br>been changed by the IH message.|string|No|**"\d{1,4}"**<br>The format consists of one- to four-<br>digit string in a range from 0 – 4000.||No|
|departurePoint_26a|The departure point is the point at<br>which to start processing a flight<br>plan as follows: the departure<br>airport, or the airfile point. When<br>the flight plan represents an airfile,<br>originating within this center area,<br>this element contains the airfile<br>point.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the allowed ways to represent<br>a fix can be used in this field, including<br>the standard airport designators. A fix<br>name, lat/long or fix-radial-distance<br>can also be used.|**AB**<br>**KDFW**<br>**SHP090015**<br>**3500N/04000W**|Yes|
|destination_27a|The destination is the point where<br>to end processing the flight plan.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**|**AB**<br>**KDFW**<br>**SHP090015**|Yes|

159

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[IH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||Any of the allowed ways to represent<br>a fix can be used in this field, including<br>the standard airport designators. A fix<br>name, lat/long or fix-radial-distance<br>can also be used.|**3500N/04000W**||

##### **5.5.1.18 Aircraft Identification Amendment Information [IH] - Diagram**

##### **5.5.1.19 Flight Identification Amendment Information Message in FIXM Format [IH_FIXM] – Data Elements**

The following elements of the IH message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

160

NAS-JMSDD-4309-001 Rev C July 10, 2018

- sourceTime_00e1

- sourceSeqNo_00e2

|**Name**<br>**[IH_FIXM]**|**Name**<br>**[IH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additionalFligh<br>tInformation/nameValue/@name<br>flight/supplementalData/additionalFligh<br>tInformation/nameValue/@value<br><br>|FDPS_Sequence<br>No|Sequence number assigned by<br>SFDPS to each message it receives<br>from HADDS. The attribute name<br>includes the constant string<br>"MSG_SEQ_NO", and the attribute<br>value contains the sequence<br>number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive value="999999999"|@name="MSG_SEQ_<br>NO"<br>@value="6860416"|Yes|
|flight/operator/operatingOrganization/<br>organization/@name<br><br><br>|FDPS_FlightOpe<br>rator/OPRIndica<br>tor_918f|Attribute used to specify the full<br>official name of the State,<br>Organization, Authority, aircraft<br>operating agency, handling agency<br>engaged in or offering to engage in<br>aircraft operation.|ff:TextNameTyp<br>e|No|xs:string|UAL|No|
|flight/@system<br><br>|propSourceSyst<br>em|This attribute indicates which<br>SFDPS system generated the<br>message.|fb:ProvenanceS<br>ystemType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp<br>|propRcvdTime|This attribute conatins the time at<br>which the message was received by<br>SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre<br>|center|This attribute specifies the code of<br>the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceC<br>entreType|No|xs:string|ZAU|Yes|
|flight/arrival/runwayPositionAndTime/r<br>unwayTime/[estimated|actual]/@time<br>|arrivalTime|This attribute specifies the<br>proposed or the actual time of<br>arrival at destination, set according<br>to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/departure/runwayPositionAndTi<br>me/runwayTime/[actual|estimated]/@t<br>ime<br>|departureTime|This element specifies the<br>proposed or actual departure time,<br>set according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|

161

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[IH_FIXM]**|**Name**<br>**[IH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|flight/flightStatus/@fdpsFlightStatus<br>|flightState|This attribute contains the current<br>status of the flight as specified by<br>SFDPS.|nas:SfdpsFlightS<br>tatusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETED|CA<br>NCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/additionalFligh<br>tInformation/nameValue/@name<br>flight/supplementalData/additionalFligh<br>tInformation/nameValue/@value<br>|fdpsGufi|The name value pair specifies the<br>SFDPS GUFI, an identifier on every<br>message that positively identifies<br>what flight the message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-z0-<br>9/]+"|name="FDPS_GUFI"<br>value="us.fdps.2015-<br>12-<br>18T16:59:10Z.000/1<br>4/100"/>|Yes|
|flight/flightPlan/@identifier<br>|eramGufi_316a|This attribute specifies the unique<br>flight plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi<br>|uuidGufi|This element contains a reference<br>that uniquely identifies a flight and<br>that is independent of any<br>particular system. This reference<br>conforms to the Universal Unique<br>Identifier standard.|fb:GloballyFlight<br>IdentifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-4[0-<br>9a-fA-F]{3}\-[89aAbB][0-9a-fA-F]{3}\-<br>[0-9a-fA-F]{12}"|4aaf92be-ac0a-4dba-<br>998f-9e56f5d450b6|Yes|
|flight/flightIdentificationPrevious/@co<br>mputerId<br><br>|computerId_02<br>d|A unique identification assigned by<br>ERAM to each flight plan prior to<br>the modification included in the<br>IH_FIXM message.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of the<br>letters**I**and**O**, such as_ddd, ddL, dLd,_<br>_dLL_.|**020**|No|
|flight/flightIdentificationPrevious/@site<br>SpecificPlanId<br>|sspId_167a|Site Specific Plan Identifier prior to<br>the modification included in the<br>IH_FIXM message. The Site Specific<br>Plan Identifier is assigned by<br>Instrument Flight Procedures<br>Automation (IFPA) to uniquely<br>identifya flightplan in each ERAM|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|

162

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[IH_FIXM]**|**Name**<br>**[IH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|||facility.||||||
|flight/flightIdentificationPrevious/@airc<br>raftIdentification<br>|flightId_02a|The aircraft identification, or flight<br>ID (also called Call Sign) prior to the<br>modification included in the<br>IH_FIXM message.|fb:FlightIdentifi<br>erType|No|**" [A-Z0-9]{1,7}"**|**AAL20**|Yes|
|flight/supplementalData/additionalFligh<br>tInformation/nameValue/@name<br>flight/supplementalData/additionalFligh<br>tInformation/nameValue/@value||The flight supplemental data is<br>used to indicate that a flight<br>message is a test message, by<br>setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the<br>attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLIGH**<br>**T”**<br>@value =**“true”**|No|
|flight/flightIdentification/@aircraftIdent<br>ification<br><br>|newFlightId_02<br>aN|The new Aircraft ID, or flight ID<br>(also called Call Sign), that has been<br>changed by the IH_FIXM message.|fb:FlightIdentifi<br>erType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/flightIdentification/@computerId<br>|newComputerI<br>d_02dN|This element contains the new<br>Computer ID that has been<br>changed by the IH_FIXM message.<br>The computer ID is a unique<br>identification assigned by ERAM to<br>each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of the<br>letters**I**and**O**, such as_ddd, ddL, dLd,_<br>_dLL_.|**020**|No|
|flight/flightIdentification/@siteSpecificP<br>lanId<br><br>|newSspId_167a<br>N|This element contains the new Site<br>Specific Plan Identifier that has<br>been changed by the IH_FIXM<br>message.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/departure/@departurePoint<br><br>|departurePoint<br>_26a|It is used to specify the first point<br>or other initial entity where the air<br>traffic control/management system<br>route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for this<br>element(fix name,lat/long,or fix-|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|

163

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[IH_FIXM]**|**Name**<br>**[IH]**<br>**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||radial-distance), including the<br>standard airport designators.|||
|flight/arrival/@arrivalPoint|destination_27a The final point or other final entity<br>where the air traffic<br>control/management system route<br>terminates.|fb:FreeTextType|No|**xs:string**<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|

##### **5.5.1.20 Hold Information [HH] – Data Elements**

|**Element Name**<br>**[HH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four-digits, represent the<br>message sequence number in the<br>range [0000-9999].|**2359359001**, where<br>the first 6 digits are the<br>UTC time (23:59:35<br>UTC) and the last 4<br>digits are sequence<br>number of the message<br>(9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format_hh_mm_ss_, where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|23_59_35<br>that represents<br>23:59:35 UTC|Yes|

164

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of<br>the sourceId_00e element.|string|No|**“\d{4}”**<br>**Four-digit number in the range [0000-**<br>**9999].**|9001|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed<br>by two alphanumeric characters with<br>the exception of the letters**I**and**O**, as<br>specified by the pattern above.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|holdDataFix_21a|This element specifies the position<br>location for the flight to hold along<br>the filed route of flight. If the<br>message does not include the<br>optional_holdDataTime_21d_<br>element, the flight goes into an<br>indefinite hold status when the<br>flight arrives at the hold fix.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the valid fix formats can be<br>used, as described for<br>_coordFix_06a_element.|**AB**<br>**KDFW**<br>**SHP090015**<br>**3500N/04000W**|No|
|holdDataTime_21d|This element specifies the time the<br>flight can expect further clearance<br>at the holding location specified in<br>the element_holdDataFix_21a_. This<br>element can only be included in<br>the HH messages if the element<br>_holdDataFix_21a_is also included.|dateTime|No||**2014-06-20T20:17:52**|No|
|holdDataAction_21<br>e|This element is used in a Hold<br>message to terminate an existing<br>stored hold.|string|No|**[C]**<br>This element can only specify the<br>letter C.|**C**|No|

165

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HH]**|**Element Definition**<br>It can only be included in a Hold<br>message if the element<br>_holdDataFix_21a_is not included.|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|

##### **5.5.1.21 Hold Information [HH] - Diagram**

##### **5.5.1.22 Hold Information Message in FIXM Format [HH_FIXM] – Data Elements**

The following elements of the HH message in Simple XML format are not used in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

166

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HH_FIXM]**|**Name**<br>**[HH]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@name<br>flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@value|FDPS_Sequence<br>No|Sequence number assigned by<br>SFDPS to each message it<br>receives from HADDS. The<br>attribute_name_includes the<br>constant string<br>"MSG_SEQ_NO", and the<br>attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|@name="MSG_<br>SEQ_NO"<br>@value="68604<br>16"|Yes|
|flight/departure/@departurePoint|FDPS_Origin/de<br>parturePoint_2<br>6a|Attribute used to specify the<br>first point or other initial entity<br>where the air traffic<br>control/management system<br>route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arrivalPoint|FDPS_DestId/d<br>estination_27a|The final point or other final<br>entity where the air traffic<br>control/management system<br>route terminates.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/operator/operatingOrganization<br>/organization/@name|FDPS_FlightOpe<br>rator/OPRIndic<br>ator_918f|Attribute used to specify the<br>full official name of the State,<br>Organization, Authority, aircraft<br>operating agency, handling<br>agency engaged in or offering<br>to engage in aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/@system|propSourceSyst|This attribute indicates which|fb:ProvenanceSystemType|No|xs:string|ATL|Yes|

167

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HH_FIXM]**|**Name**<br>**[HH]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||em|SFDPS system generated the<br>message.|||maxLength=128|||
|flight/@timestamp|propRcvdTime|This attribute conatins the time<br>at which the message was<br>received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.02<br>8Z|Yes|
|flight/@centre|center|This attribute specifies the code<br>of the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCentreType|No|xs:string|ZAU|Yes|
|flight/arrival/runwayPositionAndTime<br>/runwayTime/estimated/@time|arrivalTime|This attribute specifies the<br>proposed or the actual time of<br>arrival at destination, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/departure/runwayPositionAndT<br>ime/runwayTime/actual/@time|departureTime|This element specifies the<br>proposed or actual departure<br>time, set according to the flight<br>state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/flightStatus/@fdpsFlightStatus|flightState|This attribute contains the<br>current status of the flight as<br>specified by SFDPS.|nas:SfdpsFlightStatusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETE<br>D|CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@name<br>flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@value|fdpsGufi|The name value pair specifies<br>the SFDPS GUFI, an identifier on<br>every message that positively<br>identifies what flight the<br>message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-<br>z0-9/]+"|name="FDPS_G<br>UFI"<br>value="us.fdps.<br>2015-12-<br>18T16:59:10Z.0<br>00/14/100"/>|Yes|
|flight/flightPlan/@identifier|eramGufi_316a|This attribute specifies the<br>unique flight plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|This element contains a<br>reference that uniquely<br>identifies a flight and that is|fb:GloballyFlightIdentifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-<br>4[0-9a-fA-F]{3}\-[89aAbB][0-9a-|4aaf92be-ac0a-<br>4dba-998f-<br>9e56f5d450b6|Yes|

168

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HH_FIXM]**|**Name**<br>**[HH]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||independent of any particular<br>system. This reference<br>conforms to the Universal<br>Unique Identifier standard.|||fA-F]{3}\-[0-9a-fA-F]{12}"|||
|flight/flightIdentification/@aircraftIde<br>ntification|flightId_02a|Name used by Air Traffic<br>Services units to identify and<br>communicate with an aircraft.|fb:FlightIdentifierType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@name<br>flight/supplementalData/additionalFli<br>ghtInformation/nameValue/@value||The flight supplemental data is<br>used to indicate that a flight<br>message is a test message, by<br>setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the<br>attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_F**<br>**LIGHT”**<br>@value =**“true”**|No|
|flight/flightIdentification/@computerI<br>d|computerId_02<br>d|A unique identification assigned<br>by ERAM to each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/@siteSpecifi<br>cPlanId|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by Instrument Flight<br>Procedures Automation (IFPA)<br>to uniquely identify a flight plan<br>in each ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/agreed/route/holdFix|holdDataFix_21<br>a|This element specifies the<br>position location for the flight to<br>hold along the filed route of<br>flight. If the message does not<br>include the optional attribute|fb:SignificantPointType (abstract type)<br>_fb:FixPointType/_<br>_ff:GeographicalLocationType/_<br>_fb:RelativePointType_|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_|**KBOS**<br>flight/status/@a<br>irborneHold is<br>always set to<br>“**AIRBORNE_HO**|No|

169

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HH_FIXM]**|**Name**<br>**[HH]**|**Element Definition**||**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|---|
|||_flight/enRoute/expectedFurther_<br>_ClearanceTime/@time_, the<br>flight goes into an indefinite<br>hold status when the flight<br>arrives at the hold fix. The<br>attribute<br>_flight/status/@airborneHold_is<br>set to “**AIRBORNE_HOLD**” when<br>the element<br>_flight/agreed/route/holdFix_is<br>included.||||- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|**LD**” if holdFix<br>specified.||
|flight/enRoute/expectedFurtherClear<br>anceTime/@time|holdDataTime_<br>21d|This element specifies the time<br>the flight can expect further<br>clearance at the holding<br>location specified in the<br>element<br>flight/agreed/route/holdFix.<br>This element can only be<br>included in the HH_FIXM<br>messages if the element<br>flight/agreed/route/holdFix is<br>also included.|ff:TimeType||No|xs:dateTime|**2014-06-**<br>**20T20:17:52**|No|
|flight/status/@airborneHold|holdDataAction<br>_21e|This attribute specifies whether<br>or not the aircraft is in an<br>airborne hold.<br>If the aircraft is in an airborne<br>hold, the element<br>flight/agreed/route/holdFix<br>needs to specify the position<br>location for the flight to hold<br>alongthe filed route of flight.|fx:AirborneHol|dIndicatorType|No|**“AIRBORNE_HOLD|NON_AIRBO**<br>**RNE_HOLD”**|**“AIRBORNE_HO**<br>**LD”**|No|

170

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.23 Progress Report Information [PH] – Data Elements**

|**Element Name**<br>**[PH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed<br>by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four-digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of<br>the message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format_hh_mm_ss_, where:_hh_<br>stands for the 2-digit-hour in the range<br>00-23,_mm_stands for the 2-digit minutes<br>in the range 00-59, and ss stands for the<br>2-digit seconds in the range 00-59.|23_59_35<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|9001|Yes|
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It<br>is assigned by IFPA to uniquely<br>identify a flight plan in each<br>ERAM facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|progressReportFix_18a|This element specifies the<br>position location report of the<br>flight alongthe filed route of|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**|**AB**<br>**KDFW**|Yes|

171

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[PH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||flight.|||**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>It uses the standard fix formats, as<br>specified for the element<br>_coordFix_06a_`.`|**SHP090015**||
|progressReportTime_18<br>d|This element specifies the time<br>of the flight arriving at the fix<br>specified in element<br>_progressReportFix_18a_,<br>above.|dateTime|No||**2014-10-**<br>**31T22:30:00**|Yes|

##### **5.5.1.24 Progress Report Information [PH] - Diagram**

##### **5.5.1.25 Progress Report Information Message in FIXM Format [PH_FIXM] – Data Elements**

The following elements of the PH message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

172

NAS-JMSDD-4309-001 Rev C July 10, 2018

- sourceTime_00e1

- sourceSeqNo_00e2

|**Name**<br>**[PH_FIXM]**|**Name**<br>**[PH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additional<br>FlightInformation/nameValue/@na<br>me<br>flight/supplementalData/additional<br>FlightInformation/nameValue/@val<br>ue|FDPS_Sequence<br>No|Sequence number assigned by<br>SFDPS to each message it<br>receives from HADDS. The<br>attribute_name_includes the<br>constant string<br>"MSG_SEQ_NO", and the<br>attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive value="999999999"|@name="MSG_SEQ_<br>NO"<br>@value="6860416"|Yes|
|flight/departure/@departurePoint|FDPS_Origin/dep<br>arturePoint_26a|Attribute used to specify the<br>first point or other initial<br>entity where the air traffic<br>control/management system<br>route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a<br>fix can be used for this element (fix<br>name, lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arrivalPoint|FDPS_DestId/des<br>tination_27a|The final point or other final<br>entity where the air traffic<br>control/management system<br>route terminates.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a<br>fix can be used for this element (fix<br>name, lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/operator/operatingOrganizati<br>on/organization/@name|FDPS_FlightOper<br>ator/OPRIndicato<br>r_918f|Attribute used to specify the<br>full official name of the State,<br>Organization, Authority,|ff:TextNameTyp<br>e|No|xs:string|UAL|No|

173

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[PH_FIXM]**|**Name**<br>**[PH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|||aircraft operating agency,<br>handling agency engaged in or<br>offering to engage in aircraft<br>operation.||||||
|flight/@system|propSourceSyste<br>m|This attribute indicates which<br>SFDPS system generated the<br>message.|fb:ProvenanceS<br>ystemType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTime|This attribute conatins the<br>time at which the message was<br>received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the<br>code of the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceC<br>entreType|No|xs:string|ZAU|Yes|
|flight/arrival/runwayPositionAndTi<br>me/runwayTime/[estimated|actual<br>]/@time|arrivalTime|This attribute specifies the<br>proposed or the actual time of<br>arrival at destination, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/departure/runwayPositionAn<br>dTime/runwayTime/[actual|estima<br>ted]/@time|departureTime|This element specifies the<br>proposed or actual departure<br>time, set according to the<br>flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/flightStatus/@fdpsFlightStatu<br>s|flightState|This attribute contains the<br>current status of the flight as<br>specified by SFDPS.|nas:SfdpsFlightS<br>tatusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETED|CANC<br>ELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/additional<br>FlightInformation/nameValue/@na<br>me<br>flight/supplementalData/additional<br>FlightInformation/nameValue/@val<br>ue|fdpsGufi|The name value pair specifies<br>the SFDPS GUFI, an identifier<br>on every message that<br>positively identifies what flight<br>the message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-z0-9/]+"|name="FDPS_GUFI"<br>value="us.fdps.2015-<br>12-<br>18T16:59:10Z.000/1<br>4/100"/>|Yes|
|flight/flightPlan/@identifier|eramGufi_316a|This attribute specifies the|fb:FreeTextType|No|xs:string|"KU68378100"|No|

174

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[PH_FIXM]**<br>**Name**<br>**[PH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||unique flight plan identifier.|||"[A-Z]{2}\d{5}[1-7]\d{2}"|||
|flight/gufi<br>uuidGufi|This element contains a<br>reference that uniquely<br>identifies a flight and that is<br>independent of any particular<br>system. This reference<br>conforms to the Universal<br>Unique Identifier standard.|fb:GloballyFlight<br>IdentifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-4[0-9a-<br>fA-F]{3}\-[89aAbB][0-9a-fA-F]{3}\-[0-9a-<br>fA-F]{12}"|4aaf92be-ac0a-4dba-<br>998f-9e56f5d450b6|Yes|
|flight/flightIdentification/@aircraftI<br>dentification<br>flightId_02a|Name used by Air Traffic<br>Services units to identify and<br>communicate with an aircraft.|fb:FlightIdentifi<br>erType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additional<br>FlightInformation/nameValue/@na<br>me<br>flight/supplementalData/additional<br>FlightInformation/nameValue/@val<br>ue|The flight supplemental data is<br>used to indicate that a flight<br>message is a test message, by<br>setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the<br>attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLIGH**<br>**T”**<br>@value =**“true”**|No|
|flight/flightIdentification/@comput<br>erId<br>computerId_02d|A unique identification<br>assigned by ERAM to each<br>flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**, such as<br>_ddd, ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/@siteSpe<br>cificPlanId<br>sspId_167a|Site Specific Plan Identifier. It<br>is assigned by Instrument<br>Flight Procedures Automation<br>(IFPA) to uniquely identify a<br>flight plan in each ERAM<br>facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/enRoute/position/position<br>progressReportFi<br>x_18a|This element specifies the<br>position location report of the|fb:SignificantPoi<br>ntType (abstract|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**|**KBOS**|Yes|

175

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[PH_FIXM]**|**Name**<br>**[PH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|||flight along the filed route of<br>flight.|type)<br>_fb:FixPointType/_<br>_ff:GeographicalL_<br>_ocationType/_<br>_fb:RelativePoint_<br>_Type_||-_ff:GeographicalLocationType_<br>List of two**xs:double**(latitude<br>followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive =360|||
|flight/enRoute/position/@reportSo<br>urce|progressReportFi<br>x_18a|The source of the current<br>position report information.|fx:PositionRepor<br>tType|No|**“PROGRESS_REPORT”**|**PROGRESS_REPORT**|No|
|flight/enRoute/position/@position<br>Time|progressReportTi<br>me_18d|This element specifies the time<br>of the flight arriving at the fix<br>specified in element<br>_flight/enRoute/position/positio_<br>_n_,above.|ff:TimeType|No|xs:dateTime|**2014-10-**<br>**31T22:30:00**|Yes|

##### **5.5.1.26 Flight Arrival Information [HV] – Data Elements**

|**Element Name**<br>**[HV]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four-digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of|Yes|

176

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HV]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||||||the message (9001).||
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format_hh_mm_ss_, where:_hh_<br>stands for the 2-digit-hour in the range<br>00-23,_mm_stands for the 2-digit minutes<br>in the range 00-59, and_ss_stands for the<br>2-digit seconds in the range 00-59.|23_59_35<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of<br>the sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|9001|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|departurePoint_26<br>a|This element specifies the point at<br>which to start processing the flight<br>plan|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>It uses the standard fix formats, as<br>specified for the element_coordFix_06a_`.`|**AB**<br>**KDFW**<br>**SHP090015**<br>3500N/04000W|Yes|
|destination_27a|This element specifies the<br>destination, which is the point at<br>which to end processing the flight<br>plan.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>It uses the standard fix formats, as<br>specified for the element_coordFix_06a_`.`|**AB**<br>**KDFW**<br>**SHP090015**<br>3500N/04000W|Yes|
|arrivalTime_28b|This element specifies the reported|string|No|**“[A-Z]\d{4}”**|**A2020**|Yes|

177

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HV]**|**Element Definition**|**Type**|**Complex?**<br>**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|
||time of arrival.||where the first letter can be**A**or**E**, as<br>follows:|||
||||**A:**if time received in field 00 of TB<br>message caused flight to be dropped;|||
||||**E:**if flight dropped by application of AFDI<br>or EFDI.|||
||||The four-digits specify time in_hhmm_<br>format.|||

178

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.27 Flight Arrival Information [HV] - Diagram**

##### **5.5.1.28 Flight Arrival Information Message in FIXM Format [HV_FIXM] – Data Elements**

The following elements of the HV message in Simple XML format are not used in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

|**Name**<br>**[HV_FIXM]**|**Name**<br>**[HV]**|**Element Definition**||**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|---|
|flight/supplementalData/additionalFl|FDPS_Sequenc|Sequence number assigned by|@name:||No|@name=”MSG_SEQ_NO”|name="MSG_SE|Yes|
|ightInformation/nameValue/@name|eNo|SFDPS to each message it receives|||||Q_NO"||

179

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HV_FIXM]**|**Name**<br>**[HV]**|**Element Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additionalFl<br>ightInformation/nameValue/@value||from HADDS. The attribute_name_<br>includes the constant string<br>"MSG_SEQ_NO", and the attribute<br>_value_contains the sequence<br>number value.|@value:<br>fb:FreeTextType||@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|value="6860416"||
|flight/operator/operatingOrganizatio<br>n/organization/@name|FDPS_FlightOp<br>erator/OPRIndi<br>cator_918f|Attribute used to specify the full<br>official name of the State,<br>Organization, Authority, aircraft<br>operating agency, handling agency<br>engaged in or offering to engage in<br>aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/@system|propSourceSys<br>tem|This attribute indicates which<br>SFDPS system generated the<br>message.|fb:ProvenanceSystemType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTime|This attribute conatins the time at<br>which the message was received by<br>SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028<br>Z|Yes|
|flight/@centre|center|This attribute specifies the code of<br>the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCentreType|No|xs:string|ZAU|Yes|
|flight/departure/runwayPositionAnd<br>Time/runwayTime/actual/@time|departureTime|This element specifies the<br>proposed or actual departure time,<br>set according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/flightStatus/@fdpsFlightStatus|flightState|This attribute contains the current<br>status of the flight as specified by<br>SFDPS.|nas:SfdpsFlightStatusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETE<br>D|CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/additionalFl<br>ightInformation/nameValue/@name<br>flight/supplementalData/additionalFl<br>ightInformation/nameValue/@value|fdpsGufi|The name value pair specifies the<br>SFDPS GUFI, an identifier on every<br>message that positively identifies<br>what flight the message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-<br>z0-9/]+"|name="FDPS_GU<br>FI"<br>value="us.fdps.2<br>015-12-<br>18T16:59:10Z.00<br>0/14/100"/>|Yes|

180

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HV_FIXM]**|**Name**<br>**[HV]**|**Element Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/flightPlan/@identifier|eramGufi_316<br>a|This attribute specifies the unique<br>flight plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|This element contains a reference<br>that uniquely identifies a flight and<br>that is independent of any<br>particular system. This reference<br>conforms to the Universal Unique<br>Identifier standard.|fb:GloballyFlightIdentifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-<br>4[0-9a-fA-F]{3}\-[89aAbB][0-9a-<br>fA-F]{3}\-[0-9a-fA-F]{12}"|4aaf92be-ac0a-<br>4dba-998f-<br>9e56f5d450b6|Yes|
|flight/flightIdentification/@aircraftId<br>entification|flightId_02a|Name used by Air Traffic Services<br>units to identify and communicate<br>with an aircraft.|fb:FlightIdentifierType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@name<br>flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@value||The flight supplemental data is<br>used to indicate that a flight<br>message is a test message, by<br>setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the<br>attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLI**<br>**GHT”**<br>@value =**“true”**|No|
|flight/flightIdentification/@compute<br>rId|computerId_02<br>d|A unique identification assigned by<br>ERAM to each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/@siteSpecif<br>icPlanId|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by Instrument Flight<br>Procedures Automation (IFPA) to<br>uniquely identify a flight plan in<br>each ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|

181

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HV_FIXM]**|**Name**<br>**[HV]**|**Element Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/departure/@departurePoint|departurePoint<br>_26a|It is used to specify the first point<br>or other initial entity where the air<br>traffic control/management<br>system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name,<br>lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|flight/arrival/@arrivalPoint|destination_27<br>a|The final point or other final entity<br>where the air traffic<br>control/management system route<br>terminates.|fb:FreeTextType|No|**xs:string**<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name,<br>lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|flight/arrival/runwayPositionAndTim<br>e/runwayTime/actual/@time|arrivalTime_28<br>b|This element specifies the actual<br>time at which the aircraft lands on<br>runway.|ff:TimeType|No|**xs:dateTime**|**2015-06-**<br>**20T20:17:52**|Yes|

##### **5.5.1.29 Flight Plan Update Information [HU] – Data Elements**

See Data Elements for Flight Plan [FH]: Section 5.5.1.2.

182

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.30 Flight Plan Update Information [HU] - Diagram**

See Diagram for Flight Plan [FH]: Section 5.5.1.2.

##### **5.5.1.31 Flight Plan Update Information Message in FIXM Format [HU_FIXM] – Data Elements**

See Data Elements for Flight Plan Message in FIXM Format [FH_FIXM]: Section 5.5.1.4

##### **5.5.1.32 Expected Departure Time Information [ET] – Data Elements**

|**Element Name**<br>**[ET]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four-digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of<br>the message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format_hh_mm_ss_, where:_hh_<br>stands for the 2-digit-hour in the range<br>00-23,_mm_stands for the 2-digit minutes<br>in the range 00-59, and_ss_stands for the<br>2-digit seconds in the range 00-59.|23_59_35<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the sourceId_00e<br>element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|9001|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters**.**|**AAL20**|Yes|

183

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[ET]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**, as<br>specified by the pattern above.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|EDCT_92a|This element specifies the<br>Estimated Departure Clearance<br>Time.|string|No|**“\d{4}”**<br>Time expressed in_hhmm_format.|**1722**|Either this<br>element or the<br>element<br>_cancellationIndi_<br>_cator_92b_has<br>to be included<br>in the ET<br>message.|
|cancellationIndicator_92<br>b|This element is used to cancel the<br>EDCT for an aircraft|string|No|**“C”**<br>This element can only specify the letter<br>C.||Either this<br>element or the<br>element<br>EDCT_92a has<br>to be included<br>in the ET<br>message.|

184

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.33 Expected Departure Time Information [ET] - Diagram**

##### **5.5.1.34 Expected Departure Time Information Message in FIXM Format [ET_FIXM] – Data Elements**

The following elements of the ET message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

|**Name**<br>**[ET_FIXM]**|**Name**<br>**[ET]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requir**<br>**ed?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additionalFlightIn<br>formation/nameValue/@name<br>flight/supplementalData/additionalFlightIn<br>formation/nameValue/@value|FDPS_Sequen<br>ceNo|Sequence number assigned<br>by SFDPS to each message<br>it receives from HADDS.<br>The attribute_name_<br>includes the constant string|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger|@name="MSG_SEQ_<br>NO"<br>@value="6860416"|Yes|

185

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[ET_FIXM]**|**Name**<br>**[ET]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requir**<br>**ed?**|
|---|---|---|---|---|---|---|---|
|||"MSG_SEQ_NO", and the<br>attribute_value_contains the<br>sequence number value.|||xs:maxInclusive<br>value="999999999"|||
|flight/departure/@departurePoint|FDPS_Origin/d<br>eparturePoint<br>_26a|Attribute used to specify<br>the first point or other<br>initial entity where the air<br>traffic<br>control/management<br>system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name,<br>lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arrivalPoint|FDPS_DestId/<br>destination_2<br>7a|The final point or other<br>final entity where the air<br>traffic<br>control/management<br>system route terminates.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name,<br>lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/operator/operatingOrganization/org<br>anization/@name|FDPS_FlightOp<br>erator/OPRInd<br>icator_918f|Attribute used to specify<br>the full official name of the<br>State, Organization,<br>Authority, aircraft<br>operating agency, handling<br>agency engaged in or<br>offering to engage in<br>aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/@system|propSourceSy<br>stem|This attribute indicates<br>which SFDPS system|fb:ProvenanceSystemType|No|xs:string<br>maxLength=128|ATL|Yes|

186

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[ET_FIXM]**|**Name**<br>**[ET]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requir**<br>**ed?**|
|---|---|---|---|---|---|---|---|
|||generated the message.||||||
|flight/@timestamp|propRcvdTime|This attribute conatins the<br>time at which the message<br>was received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the<br>code of the ARTCC (or<br>FIR) that produced the<br>data.|fb:ProvenanceCentreType|No|xs:string|ZAU|Yes|
|flight/arrival/runwayPositionAndTime/run<br>wayTime/estimated/@time|arrivalTime|This attribute specifies the<br>proposed or the actual<br>time of arrival at<br>destination, set according<br>to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/departure/runwayPositionAndTime/r<br>unwayTime/[actual|estimated]/@time|departureTim<br>e|This element specifies the<br>proposed or actual<br>departure time, set<br>according to the flight<br>state.|ff:TimeType|No|xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/flightStatus/@fdpsFlightStatus|flightState|This attribute contains the<br>current status of the flight<br>as specified by SFDPS.|nas:SfdpsFlightStatusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETE<br>D|CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/additionalFlightIn<br>formation/nameValue/@name<br>flight/supplementalData/additionalFlightIn<br>formation/nameValue/@value|fdpsGufi|The name value pair<br>specifies the SFDPS GUFI,<br>an identifier on every<br>message that positively<br>identifies what flight the<br>message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-<br>z0-9/]+"|name="FDPS_GUFI"<br>value="us.fdps.2015-<br>12-<br>18T16:59:10Z.000/14/<br>100"/>|Yes|
|flight/flightPlan/@identifier|eramGufi_316<br>a|This attribute specifies the<br>unique flight plan<br>identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|This element contains a<br>reference that uniquely|fb:GloballyFlightIdentifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-|4aaf92be-ac0a-4dba-<br>998f-9e56f5d450b6|Yes|

187

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[ET_FIXM]**|**Name**<br>**[ET]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requir**<br>**ed?**|
|---|---|---|---|---|---|---|---|
|||identifies a flight and that is<br>independent of any<br>particular system. This<br>reference conforms to the<br>Universal Unique Identifier<br>standard.|||4[0-9a-fA-F]{3}\-[89aAbB][0-9a-<br>fA-F]{3}\-[0-9a-fA-F]{12}"|||
|flight/flightIdentification/@aircraftIdentific<br>ation|flightId_02a|Name used by Air Traffic<br>Services units to identify<br>and communicate with an<br>aircraft.|fb:FlightIdentifierType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additionalFlightIn<br>formation/nameValue/@name<br>flight/supplementalData/additionalFlightIn<br>formation/nameValue/@value||The flight supplemental<br>data is used to indicate that<br>a flight message is a test<br>message, by setting the<br>attribute_name_to<br>“**SIMULATED_FLIGHT**” and<br>the attribute_value_to<br>“**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|No|
|flight/flightIdentification/@computerId|computerId_0<br>2d|A unique identification<br>assigned by ERAM to each<br>flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/@siteSpecificPlan<br>Id|sspId_167a|Site Specific Plan Identifier.<br>It is assigned by Instrument<br>Flight Procedures<br>Automation (IFPA) to<br>uniquelyidentifya flight|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|

188

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[ET_FIXM]**|**Name**<br>**[ET]**|**Element Defin**|**ition**|**Type**<br>**Co**<br>**mpl**<br>**ex?**|**Format/Perm**|**issible Values**|**Example**|**Requir**<br>**ed?**|
|---|---|---|---|---|---|---|---|---|
|||plan in each ERAM|facility.||||||
|flight/departure/runwayPositio<br>unwayTime/controlled/@time|nAndTime/r<br>EDCT_92a|This element speci<br>time (Estimated D<br>Clearance Time) a<br>required to take o<br>the runway as a re<br>tactical slot allocat<br>Traffic Manageme<br>Initiative.|fies the<br>eparture<br>flight is<br>ff from<br>sult of a<br>ion or<br>nt|ff:TimeType<br>No|**dateTime**|**2014-**|**06-20T20:17:52**|No|
|flight/departure/runwayPositio<br>unwayTime/controlled|nAndTime/r<br>cancellationIn<br>dicator_92|When used to can<br>EDCT for an aircra<br>value of this elem<br>to NULL.|cel the<br>ft, the<br>ent is set|Value set to NULL:<br>xsi:nil=”true”<br>Yes|NULL|||No|
|**5.5.1.35 Po**<br>**Element Name**<br>**[HP]**|**sition Update Inf**<br>**Element Definition**|**ormation [H**<br> <br>**Type**|**P] –**<br>**Compl**|**Data Elements**<br>**ex?**<br>**Format/Permissible V**|**alues**|**Example**|**Required?**||
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time follo<br>a four-digit sequence num|<br> <br>wed by<br>ber.<br>string|No|**“\d{10}”**<br>Ten digits, of which the first 6 dig<br>the UTC time (_hhmmss_) and the l<br>represent the message sequence<br>range [0000-9999].|its represent<br>ast four-digits,<br>number in the|**2359359001**, where<br>the first 6 digits are the<br>UTC time (23:59:35<br>UTC) and the last 4<br>digits are sequence<br>number of the message<br>(9001).|<br>Yes||
|sourceTime_00e1|This element specifies the<br>component of the previo<br>element, sourceId_00e.|time<br>us<br>string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_w<br>stands for the 2-digit-hour in the<br>_mm_stands for the 2-digit minut<br>00-59, and_ss_stands for the 2-di<br>the range 00-59.|here:_hh_<br>range 00-23,<br>es in the range<br>git seconds in|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes||
|sourceSeqNo_00e2|This element specifies the<br>message sequence numb|<br>er<br>string|No|**“\d{4}”**<br>Four-digit number in the range [0|000-9999].|**9001**|Yes||

189

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HP]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||component of the sourceId_00e<br>element.||||||
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character followed<br>by one to six alphanumeric characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by two<br>alphanumeric characters with the exception of<br>the letters**I**and**O**, as specified by the pattern<br>above.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each<br>ERAM facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|coordFix_06a|The Coordination fix represents<br>the starting point to begin<br>processing the flight plan route<br>from one of the following<br>points: the departure airport,<br>the airfile fix or the adjacent<br>center inbound coordination<br>fix. For ARTS III flight plans the<br>coordination fix Field 06 is used<br>as the inbound coordination fix<br>or the outbound coordination<br>fix or, for an ARTS internal<br>flight, it can be the departure or<br>destination airport.|string|No|**“([A-Z0-9]{2,5})|**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)|**<br>**([A-Z0-9]{3,4}}"**<br>This element can have one of the following<br>formats:<br>Two to five alphanumeric characters for a fix<br>name.<br>The fix name as above followed by six digits,<br>for a fix radial distance.<br>Four-digits followed by an optional alphabetic<br>character, followed by a virgule (‘/’), followed<br>by four to five digits followed by an optional<br>alphanumeric character for a lat/long.<br>Three to four alphanumeric characters for a<br>location identifier (LOCID).|**AB**<br>**DFW**<br>**KDFW**<br>**AB200010**<br>**SHP090015**<br>**ATOKA300040**<br>**3500/04000**<br>**3500N/04000W**|Yes|
|coordStatusTime_07<br>d|Coordination time that<br>represents the starting time in<br>hours and minutes at the<br>coordination fix.|string|No|**"((A|D|E|P|F)[0-1][0-9][0-5][0-9) |**<br>**((A|D|E|P|F)2[0-3][0-5][0-9])”**<br>The element includes one letter (possible<br>values are**A**, **D, E**, **P**,or**F**)followed byfour-|**P1020**|Yes|

190

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HP]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||digits that represent time as_hhmm_.|||
|coordStatus_07d1|The coordStatus field is the<br>single letter**A**,**D**,**E**,**F**, or**P**, as<br>described for element<br>coordStatusTime_07d.|string|No|**“(A|D|E|P|F)”**|**F**|Yes|
|coordTime_07d2|Starting time at the<br>coordination fix.|dateTime|No||**2015-06-20T20:17:52**|Yes|
|delayTime_07e|This element is used to provide<br>an optional delay time.|string|No|**“\d{3}”**<br>Three digits representing time in minutes.|**030**|No|

191

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.36 Position Update Information [HP] - Diagram**

##### **5.5.1.37 Position Update Information Message in FIXM Format [HP_FIXM] – Data Elements**

The following elements of the HP message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

- coordStatusTime_07d

|**Name**|**Name**|**Element Definition**|**Type**|**Co**|**Format/Permissible Values**|**Example**|**Requ**|
|---|---|---|---|---|---|---|---|
|**[HP_FIXM]**|**[HP]**|||**mpl**<br>**ex?**|||**ired?**|

192

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HP_FIXM]**|**Name**<br>**[HP]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|flight/supplementalData/additionalFlightI<br>nformation/nameValue/@name<br>flight/supplementalData/additionalFlightI<br>nformation/nameValue/@value|FDPS_Sequence<br>No|Sequence number assigned<br>by SFDPS to each message it<br>receives from HADDS. The<br>attribute_name_includes the<br>constant string<br>"MSG_SEQ_NO", and the<br>attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No<br>@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive value="999999999"|@name="<br>MSG_SEQ_<br>NO"<br>@value="6<br>860416"|Yes|
|flight/departure/@departurePoint|FDPS_Origin/de<br>parturePoint_26<br>a|Attribute used to specify the<br>first point or other initial<br>entity where the air traffic<br>control/management system<br>route starts.|fb:FreeTextType|No<br>xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300**<br>**040**<br>**3500N/040**<br>**00W**|No|
|flight/arrival/@arrivalPoint|FDPS_DestId/de<br>stination_27a|The final point or other final<br>entity where the air traffic<br>control/management system<br>route terminates.|fb:FreeTextType|No<br>xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300**<br>**040**<br>**3500N/040**<br>**00W**|No|
|flight/operator/operatingOrganization/or<br>ganization/@name|FDPS_FlightOper<br>ator/OPRIndicat<br>or_918f|Attribute used to specify the<br>full official name of the State,<br>Organization, Authority,<br>aircraft operating agency,<br>handling agency engaged in<br>or offering to engage in<br>aircraft operation.|ff:TextNameType|No<br>xs:string|UAL|No|

193

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HP_FIXM]**|**Name**<br>**[HP]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|flight/@system|propSourceSyste<br>m|This attribute indicates which<br>SFDPS system generated the<br>message.|fb:ProvenanceSystemType|No<br>xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTime|This attribute conatins the<br>time at which the message<br>was received by SFDPS.|ff:TimeType|No<br>xs:dateTime|2015-12-<br>18T22:19:0<br>2.028Z|Yes|
|flight/@centre|center|This attribute specifies the<br>code of the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCentreType|No<br>xs:string|`ZAU`|Yes|
|flight/arrival/runwayPositionAndTime/ru<br>nwayTime/actual/@time|arrivalTime|This attribute specifies the<br>proposed or the actual time<br>of arrival at destination, set<br>according to the flight state.|ff:TimeType|No<br>xs:dateTime|2014-06-<br>20T20:17:5<br>2|Yes|
|flight/departure/runwayPositionAndTime<br>/runwayTime/estimated/@time|departureTime|This element specifies the<br>proposed or actual departure<br>time, set according to the<br>flight state.|ff:TimeType|No<br>xs:dateTime|2014-06-<br>20T20:17:5<br>2|Yes|
|flight/flightStatus/@fdpsFlightStatus|flightState|This attribute contains the<br>current status of the flight as<br>specified by SFDPS.|nas:SfdpsFlightStatusType|Yes<br>xs:string<br>“PROPOSED|ACTIVE|COMPLETED|<br>CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/additionalFlightI<br>nformation/nameValue/@name<br>flight/supplementalData/additionalFlightI<br>nformation/nameValue/@value|fdpsGufi|The name value pair specifies<br>the SFDPS GUFI, an identifier<br>on every message that<br>positively identifies what<br>flight the message is for.|fb:FreeTextType|No<br>xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-z0-<br>9/]+"|name="FD<br>PS_GUFI"<br>value="us.f<br>dps.2015-<br>12-<br>18T16:59:1<br>0Z.000/14/<br>100"/>|Yes|
|flight/flightPlan/@identifier|eramGufi_316a|This attribute specifies the<br>unique flight plan identifier.|fb:FreeTextType|No<br>xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU683781<br>00"|No|
|flight/gufi|uuidGufi|This element contains a<br>reference that uniquely|fb:GloballyFlightIdentifierType|xs:string|4aaf92be-|Yes|

194

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HP_FIXM]**|**Name**<br>**[HP]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|||identifies a flight and that is<br>independent of any particular<br>system. This reference<br>conforms to the Universal<br>Unique Identifier standard.||"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-4[0-<br>9a-fA-F]{3}\-[89aAbB][0-9a-fA-<br>F]{3}\-[0-9a-fA-F]{12}"|ac0a-4dba-<br>998f-<br>9e56f5d45<br>0b6||
|flight/flightIdentification/@aircraftIdentifi<br>cation|flightId_02a|Name used by Air Traffic<br>Services units to identify and<br>communicate with an<br>aircraft.|fb:FlightIdentifierType|No<br>**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additionalFlightI<br>nformation/nameValue/@name<br>flight/supplementalData/additionalFlightI<br>nformation/nameValue/@value||The flight supplemental data<br>is used to indicate that a<br>flight message is a test<br>message, by setting the<br>attribute_name_to<br>“**SIMULATED_FLIGHT**” and<br>the attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No<br>_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULAT**<br>**ED_FLIGHT**<br>**”**<br>@value =<br>**“true”**|No|
|flight/flightIdentification/@computerId|computerId_02d|A unique identification<br>assigned by ERAM to each<br>flight plan.|fb:FreeTextType|No<br>**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/@siteSpecificPla<br>nId|sspId_167a|Site Specific Plan Identifier. It<br>is assigned by Instrument<br>Flight Procedures<br>Automation (IFPA) to<br>uniquely identify a flight plan<br>in each ERAM facility.|fb:CountType|No<br>**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/coordination/coordinationFix|coordFix_06a|The fix to be used in|fb:SignificantPointType (abstract type)|Yes<br>-_fb:FixPointType_|**MDG**|Yes|

195

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HP_FIXM]**|**Name**<br>**[HP]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|||conjunction with the<br>Coordination Time so that the<br>processing for this flight (and<br>its trajectory) can be<br>synchronized for the next<br>sector/facility.|_fb:FixPointType/_<br>_ff:GeographicalLocationType/_<br>_fb:RelativePointType_|**“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**(latitude<br>followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive =360|||
|flight/coordination/@coordinationTimeH<br>andling|coordStatus_07d<br>1|The indicator for the type of<br>Coordination Time.|nas:CoordinationTimeType|No<br>**“(P|D|E|A)”**<br>**“P”**= Proposed flight plan.<br>**“D”**= Aircraft has departed from the<br>departure airport.<br>**“E”**= Active aircraft.<br>**“A”**= Aircraft arrived at the<br>destination airport.|<br>**P**|Yes|
|flight/coordination/@coordinationTime|coordTime_07d2|Coordination Time: the time<br>to be used in conjunction<br>with the Coordination Fix so<br>processing for this flight can<br>be synchronized for the next<br>sector/facility.|ff:TimeType|No<br>**dateTime**|**2015-07-**<br>**27T20:17:5**<br>**2**|Yes|
|flight/coordination/@delayTimeToAbsorb|delayTime_07e|Delay time to absorb:<br>indicates the amount of time<br>that needs to be absorbed<br>during the flight. It is<br>corrective action for meeting<br>the goal of Estimated<br>Departure Clearance Time<br>(EDCT),when the flight is|ff:DurationTime|No<br>**xs:duration**|**PT30M**|No|

196

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HP_FIXM]**|**Name**<br>**[HP]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||already active and needs to<br>arrive later than originally<br>planned.||||||

##### **5.5.1.38 Tentative Flight Plan Information [NP] – Data Elements**

|**Element Name**<br>**[NP]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC time<br>followed by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four-digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of<br>the message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called Call<br>Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**|**020**|No|

197

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NP]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**, as<br>specified by the pattern above.|||
|eramGufi_316a|GUFI that uniquely identifies each flight<br>in the system.|string|No|**"[A-Z]{2}\d{5}[1-7]\d{2}"**<br>This element includes<br>10 alphanumeric characters:<br>-ICAO country code (one letter);<br>-en-route facility ID (one letter);<br>-time in seconds  of current day (five<br>digits in the range 00000-86400);<br>-sequence number (two digits).|**KB5980017**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely identify a<br>flight plan in each ERAM facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|numberOfAircraft_03a|This element includes the number of<br>aircraft for the flight followed<br>optionally by the Special Aircraft<br>Indicator.|string|No|**"\d{0,2}[A-Z]?"**<br>The element consists of zero to two<br>digits optionally followed by one<br>uppercase letter to represent the Special<br>Aircraft Indicator. The indicator can also<br>appear on its own (without the leading<br>digits).|**3H**<br>The number of<br>aircraft is 3 and the<br>special aircraft<br>indicator is**H**for<br>Heavy Jet.|No|
|typeOfAircraft_03c|Type of aircraft.|string|No|**"[A-Z][A-Z0-9]{1,3}"**<br>The element consists of one letter<br>followed by one to three alphanumeric<br>characters.|**B747**|Yes|
|airborneEquip_03e|Airborne equipment qualifier. It<br>consists of one alphanumeric<br>character.|string|No|**"[A-Z]"**<br>The element consists of one<br>alphanumeric character, that can have<br>one of the following values:<br>**A**- Transponder with no Mode C<br>**B**- Transponder with Mode C|**E**|No|

198

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NP]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||**E**– FMS with DME/DME and IRU<br>position updating<br>**G**– GNSS, including GPS or WAAS, with<br>en-route and terminal capability<br>**X**– No transponder<br>**W**- RVSM|||
|beaconCode_04a|Beacon code.<br>**_Note_:**As of SFDPS 1.3.1, if the<br>flightState element has a value of<br>‘Canceled’ or ‘Proposed’, this element<br>is only present in the version of a<br>message with FDPS_Restricted=’R’|string|No|**"[0-7]{4}"**<br>The element includes four octal digits<br>(i.e. 0-7). When the last two digits of the<br>four-digits are zero, the beacon code is<br>a non-discrete code.<br>A discrete code is any code not ending<br>in 00.|Non-discrete VFR<br>code:<br> **2101**|No|
|trueAirSpeed_05a|True airspeed expressed in knots.|string|No|**"\d{2,4}"**<br>The format is two to four-digits, in the<br>range 01 – 3700 knots.<br>Aircraft speed is required to be specified<br>by using one of the three possible<br>elements: trueAirSpeed_05a,<br>machSpeed_05c or classifiedSpeed_05d.|**540**<br>Aircraft true airspeed<br>is 540 knots.|<br>Yes, if neither<br>machSpeed_05c<br>nor<br>classifiedSpeed<br>_05d are<br>included in the<br>message.|
|machSpeed_05c|Mach speed.|string|No|**“M\d{3}”**<br>The letter**M**followed by three digits.<br>The maximum value is M500.|The speed 0.85<br>Mach is represented<br>as**M085**.|Yes, if neither<br>trueAirSpeed_0<br>5a nor<br>classifiedSpeed<br>_05dare<br>included in the<br>message.|
|classifiedSpeed_05d|Adapted classified speed. It is not<br>printed on flight strips.|string|No|**“SC”**|This element may<br>only include the<br>string character**SC**.|Yes, if neither<br>trueAirSpeed_0<br>5a nor<br>machSpeed_05c<br>are included in<br>the message.|
|assignedAlt_08a|Assigned altitude or flight level<br>expressed in hundreds of feet.|string|No|**“(\d{2,3}) | VFR”**<br>The format consists of either two to|Assigned altitude of<br>34,000 feet:|No|

199

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NP]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||Only one of the altitude elements<br>assignedAlt_08a, assignedAlt_08b,<br>assignedAlt_08c, assignedAlt_08d,<br>assignedAlt_08e, assignedAlt_08f,<br>assignedAlt_08g, assignedAlt_08h may<br>be included in the message.|||three digits, or the constant string**VFR**.<br>Three digits are required for ARTS III,<br>thus a leading zero needs to be used<br>when necessary.|**340**<br>Assigned altitude<br>9,000 feet ARTS III:<br>**090**||
|assignedAlt_08b|Fixed value of**OTP**which indicates<br>VFR-ON-Top. It specifies that the<br>aircraft is flying above the clouds in<br>VFR conditions.<br>It may only be specified if none of the<br>other assignedAtl_08 elements is<br>included in the message.|string|No|**“OTP”**|Fixed value of**OTP.**|No|
|assignedAlt_08c|VFR-ON-Top with altitude. It<br>represents an IFR flight operating<br>above the clouds in VFR conditions at<br>the specified assigned altitude.<br>It may only be specified if none of the<br>other assignedAtl_08 elements is<br>included in the message.|string|No|“**OTP/\d{2,3}**”<br>The format is the constant string**OTP**/<br>followed by two to three digits that<br>represent the assigned altitude in<br>hundreds of feet.|Aircraft flying VFR-<br>ON-Top at 25,000<br>feet:<br>**OTP/250**|No|
|assignedAlt_08d|The assigned block of altitudes for the<br>flight to fly at.<br>It may only be specified if none of the<br>other assignedAtl_08 elements is<br>included in the message.|string|No|**"\d{2,3}B\d{2,3}"**<br>The format is two to three digits,<br>followed by the letter**B**, followed by<br>two to three digits. The leading and<br>trailing two to three digits define the<br>block of altitudes in hundreds of feet for<br>the flight to fly at. The lowest altitude<br>must be listed first.|Assigned altitude<br>block of 8,000 feet<br>to 14,000 feet:<br>**80B140**|No|
|assignedAlt_08e|Element used for IFR flights operating<br>above a specified altitude.<br>It may only be specified if none of the<br>other assignedAtl_08 elements is<br>included in the message.|string|No|**“ABV/\d{2,3}"**<br>The format consists of the string**ABV/**<br>followed by two to three digits that<br>represent the altitude in hundreds of<br>feet above which the flight is flying.|Aircraft is flying<br>above 60,000 feet.<br>**ABV/600**|No|
|assignedAlt_08f|Assigned Altitude/FIX/Altitude element<br>specifies the altitudes to and from a fix<br>for the flight to fly at.|string|No|**"(\d{2,3}/[A-Z0-9]{2,5}/\d{2,3})|**<br>**(\d{2,3}/[A-Z0-9]{2,5}\d{6}/\d{2,3}) |**<br>**(\d{2,3}/\d{4}[A-Z]?/\d{4,5}[A-**|**240/DAL350010/220**<br>Flight flies at altitude<br>24,000 feet to the fix|No|

200

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NP]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||It may only be specified if none of the<br>other assignedAtl_08 elements is<br>included in the message.|||**Z]?/\d{2,3})"**<br>The altitudes are specified in hundreds<br>of feet in a two to three digit format.<br>The fix is specified using the same<br>format as the coordination fix element<br>“coordFix_06a”.<br>The fix cannot be the departure or<br>arrival point.|radial distance fix<br>and then descend to<br>altitude 22,000 feet.||
|assignedAlt_08g|It is used to specify that the flight is<br>flying Visual Flight Rules (VFR). It can<br>only have the value**VFR**.<br>It may only be specified if none of the<br>other assignedAtl_08 elements is<br>included in the message.|string|No|**“VFR”**|The string**VFR.**|No|
|assignedAlt_08h|It is used to specify that the flight is<br>flying VFR at a specified altitude.<br>It may only be specified if none of the<br>other assignedAtl_08 elements is<br>included in the message.|string|No|**“VFR/\d{2,3}"**<br>The format consists of the string**VFR/**<br>followed by two to three digits that<br>represent an altitude in hundreds of<br>feet.|**VFR/75**<br>The aircraft is flying<br>VFR at 7,500 feet.|No|
|reportedAlt_54a|The element is used to specify the<br>reported altitude. For aircraft with<br>operative Mode C capability, this<br>element contains the Mode C altitude.<br>For aircraft without Mode C capability<br>or with non-operative Mode C<br>capability, this element may contain<br>the controller reported altitude. If there<br>is no Mode C or controller reported<br>altitude, or the reported altitude is<br>negative, this element contains “0” or<br>"000" or is optional.|string|No|**"\d{1,3}"**<br>The format consists of one to three<br>digits that represent the reported<br>aircraft altitude in hundreds of feet.<br>Leading zeroes may be inserted for<br>altitudes of less than 3 digits.|**310**<br>The aircraft reported<br>altitude is 31,000<br>feet.|No|
|reportedAlt_54b|This field is the reported altitude B4<br>indicator. The ERAM controllers’ full<br>data block used for tracking an aircraft<br>has a special indicator for the B4<br>character of the full data block.|string|No|**“[ABCFNTVX^v+-/]”**<br>The format of this element is one<br>character as follows:<br>A - Reported altitude (controller<br>entered) equals single assigned altitude.|**B**|No|

201

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NP]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||B - Beacon reported altitude is in<br>conformance or controller entered<br>reported altitude is in the block for an<br>aircraft which has been assigned an<br>altitude block (B1 to B3 - low altitude<br>limit of block and C1 to C3=high altitude<br>limit of block).<br>C - Beacon reported altitude is within<br>Altitude Conformance Limits feet.<br>F - Reported altitude (controller entered)<br>equals first altitude or (beacon reported)<br>is within Altitude Conformance Limits of<br>first altitude when assigned altitude is<br>(d)dd/fix/(d)dd and the first altitude is<br>displayed in Field B.<br>N - No beacon reported altitude has<br>been received for the aircraft; no<br>controller entered reported altitude<br>exists for the aircraft; or the aircraft’s<br>rate of change is questionable and<br>Computed Rate of Change is being used<br>to make further conformance checks.<br>T - Interim altitude is currently being<br>displayed in the assigned altitude field<br>(B1 through B3).<br>V - Beacon reported or controller<br>entered reported altitude, when no<br>assigned altitude exists for the aircraft.<br>X - Beacon reported altitude becomes<br>disestablished. (C1-C3 also contains `X'<br>character.)<br>^ - Beacon reported or controller<br>entered reported altitude is below<br>assigned altitude when flight is climbing<br>v - Beacon reported or controller<br>entered reported altitude is above<br>assigned altitude when flight is<br>descending|||

202

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NP]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||+ - Beacon reported altitude exceeds<br>upper conformance limit for an aircraft<br>which has reached it assigned altitude or<br>the controller entered reported altitude<br>exceeds the assigned altitude for a non-<br>Mode C aircraft which has previously<br>been reported at the assigned altitude.<br>- - Beacon reported altitude is less than<br>lower conformance limit for an aircraft<br>which has reached its assigned altitude<br>or the controller entered reported<br>altitude is less than the assigned altitude<br>for a non-Mode C aircraft which has<br>previously been reported at the assigned<br>altitude.<br>/ - Flight type is `**OTP**' or `**VFR**’|||
|reportedAlt_54c|The element specifies the reported<br>altitude C4 indicator.<br>The ERAM controllers full data block<br>used for tracking an aircraft has a<br>special indicator for the C4 character of<br>the full data block as follows: If the<br>aircraft is not responding with the<br>Mode C altitude, the controller entered<br>reported altitude is displayed in<br>_reportedAlt_54c_with a pound sign (#)<br>or X in position C4 whenever (1) the<br>controller entered reported altitude<br>does not equal the assigned altitude or<br>is not within the assigned altitude<br>block, (2) no assigned altitude has been<br>entered, or (3) the assigned altitude is<br>VFR, VFR/(d)dd, OTP, or OTP/(d)dd. In<br>either case for a Mode C reported<br>altitude or a controller reported<br>altitude, when an interim altitude is<br>displayed in_reportedAlt_54b_<br>the B4 characterposition contains the|string|No|**“[#X]”**|**#**|No|

203

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NP]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||letter “T” and the reported altitude, or<br>either the lower or upper altitude of an<br>assigned block altitude is displayed in<br>_reportedAlt_54c_. In the case where a<br>controller entered reported altitude<br>exists, a pound sign (#) or X is displayed<br>in the C4 position.||||||
|interimAlt_76b|This element specifies the interim<br>altitude for the flight in hundreds of<br>feet. It is included in the message if an<br>interim altitude is assigned.|string|No|**"\d{1,3}"**|**240**|No|

204

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.39 Tentative Flight Plan Information [NP] - Diagram**

205

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.40 Tentative Flight Plan Information in FIXM Format [NP_FIXM] – Data Elements**

The following elements of the NP message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

- reportedAlt_54b

- reportedAlt_54c

|**Name**<br>**[NP_FIXM]**|**Name**<br>**[NP]**|**Element Definition**|**Type**|**Com**<br>**plex?**<br>**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|flight/supplementalData/additio<br>nalFlightInformation/nameValu<br>e/@name<br>flight/supplementalData/additio<br>nalFlightInformation/nameValu<br>e/@value|_FDPS_Seq_<br>_uenceNo_|Sequence number assigned by SFDPS to<br>each message it receives from HADDS.<br>The attribute_name_includes the constant<br>string"MSG_SEQ_NO", and the attribute<br>_value_contains the sequence number<br>value.|@name:<br>@value:<br>fb:FreeTextType|No<br>@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive value="999999999"|@name="<br>MSG_SEQ_<br>NO"<br>@value="6<br>860416"|Yes|
|flight/departure/@departurePo<br>int|_FDPS_Orig_<br>_in/departu_<br>_rePoint_2_<br>_6a_|Attribute used to specify the first point<br>or other initial entity where the air traffic<br>control/management system route<br>starts.|fb:FreeTextType|No<br>xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a fix can be<br>used for this element (fix name, lat/long, or fix-<br>radial-distance), including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300**<br>**040**<br>**3500N/040**<br>**00W**|No|
|flight/arrival/@arrivalPoint|_FDPS_Dest_<br>_Id/destina_<br>_tion_27a_|The final point or other final entity where<br>the air traffic control/management<br>system route terminates.|fb:FreeTextType|No<br>xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a fix can be<br>used for this element (fix name, lat/long, or fix-<br>radial-distance), including the standard airport|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300**<br>**040**<br>**3500N/040**<br>**00W**|No|

206

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NP_FIXM]**|**Name**<br>**[NP]**|**Element Definition**|**Type**|**Com**<br>**plex?**|<br>**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
||||||designators.|||
|flight/operator/operatingOrgani<br>zation/organization/@name|_FDPS_Flig_<br>_htOperato_<br>_r/OPRIndic_<br>_ator_918f_|Attribute used to specify the full official<br>name of the State, Organization,<br>Authority, aircraft operating agency,<br>handling agency engaged in or offering to<br>engage in aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/@system|propSourc<br>eSystem|This attribute indicates which SFDPS<br>system generated the message.|fb:ProvenanceSyst<br>emType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdT<br>ime|This attribute conatins the time at which<br>the message was received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:0<br>2.028Z|Yes|
|flight/@centre|center|This attribute specifies the code of the<br>ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCent<br>reType|No|xs:string|ZAU|Yes|
|flight/arrival/runwayPositionAn<br>dTime/runwayTime/estimated/<br>@time|arrivalTim<br>e|This attribute specifies the proposed or<br>the actual time of arrival at destination,<br>set according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:5<br>2|Yes|
|flight/departure/runwayPositio<br>nAndTime/runwayTime/estimat<br>ed/@time|departure<br>Time|This element specifies the proposed or<br>actual departure time, set according to<br>the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:5<br>2|Yes|
|flight/flightStatus/@fdpsFlightSt<br>atus|flightState|This attribute contains the current status<br>of the flight as specified by SFDPS.|nas:SfdpsFlightStat<br>usType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETED|CANCELLED|DRO<br>PPED”|ACTIVE|Yes|
|flight/supplementalData/additio<br>nalFlightInformation/nameValu<br>e/@name<br>flight/supplementalData/additio<br>nalFlightInformation/nameValu<br>e/@value|fdpsGufi|The name value pair specifies the SFDPS<br>GUFI, an identifier on every message that<br>positively identifies what flight the<br>message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-<br>Za-z0-9/]+"|name="FD<br>PS_GUFI"<br>value="us.f<br>dps.2015-<br>12-<br>18T16:59:1|Yes|

207

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NP_FIXM]**|**Name**<br>**[NP]**|**Element Definition**|**Type**|**Com**<br>**plex?**|<br>**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|||||||0Z.000/14/<br>100"/>||
|flight/flightPlan/@identifier|eramGufi_<br>316a|This attribute specifies the unique flight<br>plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU683781<br>00"|No|
|flight/gufi|uuidGufi|This element contains a reference that<br>uniquely identifies a flight and that is<br>independent of any particular system.<br>This reference conforms to the Universal<br>Unique Identifier standard.|fb:GloballyFlightId<br>entifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-4[0-9a-fA-F]{3}\-<br>[89aAbB][0-9a-fA-F]{3}\-[0-9a-fA-F]{12}"|4aaf92be-<br>ac0a-4dba-<br>998f-<br>9e56f5d45<br>0b6|Yes|
|flight/flightIdentification/@aircr<br>aftIdentification|flightId_0<br>2a|Name used by Air Traffic Services units to<br>identify and communicate with an<br>aircraft.|fb:FlightIdentifierT<br>ype|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additio<br>nalFlightInformation/nameValu<br>e/@name<br>flight/supplementalData/additio<br>nalFlightInformation/nameValu<br>e/@value||The flight supplemental data is used to<br>indicate that a flight message is a test<br>message, by setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the attribute<br>_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULAT**<br>**ED_FLIGHT**<br>**”**<br>@value =<br>**“true”**|No|
|flight/flightIdentification/@siteS<br>pecificPlanId|sspId_167<br>a|Site Specific Plan Identifier. It is assigned<br>by Instrument Flight Procedures<br>Automation (IFPA) to uniquely identify a<br>flight plan in each ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/aircraftDescription/@aircr<br>aftQuantity|numberOf<br>Aircraft_0<br>3a|This element includes the number of<br>aircraft for the flight.|fb:countType|No|**"\d{0,2}"**<br>The element consists of zero to two digits.|**3**|No|
|flight/aircraftDescription/@tfms<br>SpecialAircraftQualifier|numberOf<br>Aircraft_0<br>3a- Special|<br>This element includes the Special Aircraft<br>Indicator. It indicates the flight is a heavy<br>jet,B757 or,if notpresent,a largejet and|nas:NasSpecialAirc<br>raftQualifierType|No|**“HEAVY_JET|TCAS|B757|HEAVY_JET_AND_TCAS”**<br>**“HEAVY_JET”**= Capable of takeoff weights of<br>300,000 pounds or more|**HEAVY_JET**|No|

208

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NP_FIXM]**|**Name**<br>**[NP]**|**Element Definition**|**Type**|**Com**<br>**plex?**|<br>**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|<br>|Aircraft<br>Indicator|if the flight is either equipped or not with<br>TCAS. This indicator is used for output<br>purposes such as strip printing and<br>message transfers to other facilities such<br>as Automated Radar Terminal System<br>(ARTS).<br>NOTE<br>TFMS Special Aircraft Qualifier is a bad fit<br>to Special Aircraft Indicator but no other<br>fields seem to fit.|||**“TCAS”**= Traffic collision avoidance system or traffic<br>alert and collision avoidance system<br>**“B757”**= Controllers are required to apply the<br>special wake turbulence separation criteria for the<br>Boeing 757.<br>**“HEAVY_JET_AND_TCAS”**= Capable of takeoff<br>weights of 300,000 pounds or more and traffic<br>collision avoidance system.|||
|flight/aircraftDescription/aircraf<br>tType/icaoModelIdentifier<br><br>|typeOfAirc<br>raft_03c|The ICAO code of the aircraft type.|fb:IcaoAircraftIden<br>tifierType|No|**"[A-Z][A-Z0-9]{1,3}"**<br>The element consists of one letter followed by one<br>to three alphanumeric characters.|**B747**|Yes|

209

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NP_FIXM]**|**Name**<br>**[NP]**|**Element Definition**|**Type**|**Com**<br>**plex?**<br>**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|flight/aircraftDescription/@equi<br>pmentQualifier|airborneE<br>quip_03e|Airborne equipment qualifier. A value<br>assigned to the aircraft, based on its<br>navigational equipment, whether or not<br>it has a transponder, and if it has a<br>transponder, whether the transponder<br>supports Mode C.|nas:NasAirborneEq<br>uipmentQualifierT<br>ype|No<br>**" [ ABCDGHILMNPSTUVWXYZ]"**<br>The element consists of one alphanumeric character,<br>that can have one of the following values:<br>•<br>“X”= No RVSM, No DME, No transponder<br>•<br>“T”= No RVSM, No DME, Transponder with<br>no mode C<br>•<br>“U”= No RVSM, No DME: Transponder<br>with mode C<br>•<br>“D”= DME: No transponder<br>•<br>“B”= DME: Transponder with no mode C<br>•<br>“A”= DME: Transponder with mode<br>•<br>“M”= TACAN ONLY: No transponder<br>•<br>“N”= TACAN ONLY: Transponder with no<br>mode C<br>•<br>“P”= TACAN ONLY: Transponder with<br>mode C<br>•<br>“C”= “Y”= LORAN,VORDME,INS,RNAV: No<br>transponder<br>•<br>“I”= LORAN,VORDME,INSRNAV:<br>Transponder with mode C<br>•<br>“H”= RVSM, Failed transponder or Failed<br>Mode C capability<br>•<br>“S=ADVANCED RNAV, TRANSPONDER,<br>MODE C: FMS with DMEDME position<br>updating<br>•<br>“G”= ADVANCED RNAV, TRANSPONDER,<br>MODE C: Global Navigation Satellite<br>System (GNSS), including GPS or Wide Area<br>Augmentation System (WAAS), with<br>enroute and terminal capability<br>•<br>“V”= ADVANCED RNAV, TRANSPONDER,<br>MODE C: Required Navigational<br>Performance (RNP). The aircraft meets the<br>RNP type prescribed for the route<br>segments, routes and/or area concerned.<br>•<br>“Z”= REDUCED VERTICAL SEPARATION<br>MINIMUM(RVSM): E with RVSM|**E**|No|

210

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NP_FIXM]**|**Name**<br>**[NP]**|**Element Definition**|**Type**|**Com**<br>**plex?**|<br>**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
||||||•<br>“L”= REDUCED VERTICAL SEPARATION<br>MINIMUM (RVSM): G with RVSM<br>“W”= REDUCED VERTICAL SEPARATION MINIMUM<br>(RVSM): RVSM|||
|flight/enRoute/beaconCodeAssi<br>gnment/currentBeaconCode|beaconCo<br>de_04a|The current assigned four-character<br>numeric code transmitted by the aircraft<br>transponder in response to a secondary<br>surveillance radar interrogation signal<br>which is used to assist air traffic<br>controllers to identify aircraft.<br>Note: As of SFDPS R1.3.1, if the<br>flight/flightStatus/@fdpsFlightStatus<br>attribute has a value of ‘CANCELED or<br>‘PROPOSED, this element is only present<br>in the version of a message with<br>FDPS_Restricted=’R’|fb:BeaconCodeTyp<br>e|No|"[0-7]{4}"<br>The element includes four octal digits (i.e. 0-7).<br>When the last two digits of the four-digits are zero,<br>the beacon code is a non-discrete code.<br>A discrete code is any code not ending in 00.|Non-<br>discrete<br>VFR code:<br> **2101**|No|
|flight/requestedAirspeed/nasAir<br>speed<br>flight/requestedAirspeed/@uo<br>m|trueAirSpe<br>ed_05a<br>machSpee<br>d_05c|The aircraft speed expressed in either<br>true airspeed or mach.|nasAirspeed:<br>ff:<br>TrueAirSpeedOrM<br>achType<br>uom:<br>ff:AirspeedMeasur<br>eType|No|nasAirspeed:<br>**“xs:double”**<br>uom:<br>**“KILOMETERS_PER_HOUR|KNOTS|MACH”**<br>This element is required if<br>requestedAirspeed/classifed is not included in the<br>message.|nasAirspee<br>d:<br>**540**<br>uom:<br>**KNOTS**|Yes|
|flight/requestedAirspeed/classif<br>ied|classifiedS<br>peed_05d|Classified Speed Indicator. It indicates<br>that the speed for this flight is classified<br>and is not to be recorded.|nas:ClassifiedSpee<br>dIndicatorType|No|**“CLASSIFIED”**<br>This element is required if<br>requestedAirspeed/nasAirspeed not included in the<br>message.|**CLASSIFIED**|Yes|
|flight/assignedAltitude/simple<br>flight/assignedAltitude/simple/<br>@uom<br>flight/assignedAltitude/simple/<br>@ref|assignedAl<br>t_08a|Simple altitude: single measurement<br>above reference point. It represents the<br>only NAS altitude that maps directly to<br>the core ICAO altitude types.|assignedAltitude/si<br>mple:<br>nas:SimpleAltitude<br>Type<br>uom:<br>ff:AltitudeMeasure<br>Type<br>ref:|Yes|**“xs:double”**<br>uom:<br>“**FEET|METERS**”<br>ref:<br>**“MEAN_SEA_LEVEL| FLIGHT_LEVEL”**<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the message.|Assigned<br>altitude of<br>34,000<br>feet:<br>**34000**<br>Uom:<br>**FEET**<br>Ref:|No|

211

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NP_FIXM]**|**Name**<br>**[NP]**|**Element Definition**|**Type**|**Com**<br>**plex?**|<br>**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
||||ff:AltitudeReferenc<br>eType|||**MEAN_SE**<br>**A_LEVEL**||
|flight/assignedAltitude/vfrOnTo<br>p|assignedAl<br>t_08b|The presence of this element indicates<br>VFR-ON-Top. It specifies that the aircraft<br>is flying above the clouds in VFR<br>conditions.|Nas:VfrOnTopAltit<br>udeType|Yes|Empty element.<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the message.||No|
|flight/assignedAltitude/vfrOnTo<br>pPlus<br>flight/assignedAltitude/vfrOnTo<br>pPlus/@uom|assignedAl<br>t_08c|VFR-ON-Top with altitude. It represents<br>an Instrument Flight Rules (IFR) flight<br>operating above the clouds in VFR<br>conditions at the specified assigned<br>altitude.|nas:VfrOnTopPlusA<br>ltitudeType|No|**“xs:double”**<br>uom:<br>**“FEET|METRES”**<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the message.|Aircraft<br>flying VFR-<br>ON-Top at<br>25,000<br>feet:<br>**25000**<br>uom:**feet**|No|
|flight/assignedAltitude/block/ab<br>ove<br>flight/assignedAltitude/block/ab<br>ove/@uom|assignedAl<br>t_08d|The bottom level of the assigned block of<br>altitudes for the flight to fly at.|ff:AltitudeType|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the message.|_above:_<br>**8000**<br>_uom:_<br>**FEET**|No|
|flight/assignedAltitude/block/b<br>elow<br>flight/assignedAltitude/block/b<br>elow/@uom|assignedAl<br>t_08d|The top level of the assigned block of<br>altitudes for the flight to fly at.|ff:AltitudeType|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the message.|_below:_<br>**14000**<br>_uom:_<br>**FEET**|No|
|flight/assignedAltitude/above<br>flight/assignedAltitude/above/<br>@uom|assignedAl<br>t_08e|Element used for IFR flights operating<br>above a specified altitude.|nas:AboveAltitude<br>Type|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the message.|Aircraft is<br>flying<br>above<br>60,000<br>feet:<br>**60000**|No|

212

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NP_FIXM]**|**Name**<br>**[NP]**|**Element Definition**|**Type**|**Com**<br>**plex?**|<br>**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|||||||**uom:**<br>**FEET**||
|flight/assignedAltitude/altFixAlt<br>/point|assignedAl<br>t_08f|_assignedAltitude/altFixAlt_element is<br>defined as an altitude prior to a specified<br>fix, the specified fix itself, and altitude<br>post specified fix. The element<br>_altFixAlt/point_defines the specified fix<br>associated with the altitude.<br>The fix cannot be the departure or arrival<br>point.|fb:SignificantPoint<br>Type (abstract<br>type)<br>_fb:FixPointType/_<br>_ff:GeographicalLoc_<br>_ationType/_<br>_fb:RelativePointTy_<br>_pe_|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**(latitude followed by<br>longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive =360<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the message.|**MDG**|No|
|flight/assignedAltitude/altFixAlt<br>/pre<br>flight/assignedAltitude/altFixAlt<br>/pre/@uom|assignedAl<br>t_08f|_assignedAltitude/altFixAlt_element is<br>defined as an altitude prior to a specified<br>fix, the specified fix itself, and altitude<br>post specified fix. The element<br>_altFixAlt/pre_defines the altitude before<br>the specified fix.|ff:AltitudeType|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the message.|**240000**<br>**uom:**<br>**FEET**|No|
|flight/assignedAltitude/altFixAlt<br>/post<br>flight/assignedAltitude/altFixAlt<br>/post/@uom|assignedAl<br>t_08f|_assignedAltitude/altFixAlt_element is<br>defined as an altitude prior to a specified<br>fix, the specified fix itself, and altitude<br>post specified fix. The element<br>_altFixAlt/pre_defines the altitude after<br>the specified fix.|ff:AltitudeType|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the message.|**22000**<br>**uom:**<br>**FEET**|No.|
|flight/assignedAltitude/vfr|assignedAl<br>t_08g|Its presence in the message specifies that<br>the flight is flying Visual Flight Rules<br>(VFR).|nas:VfrAltitudeTyp<br>e|Yes|**Empty element**<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_, _block_, _above_, _altFixAlt_, _vfr_, _vfrPlus_may||No|

213

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NP_FIXM]**|**Name**<br>**[NP]**|**Element Definition**|**Type**|**Com**<br>**plex?**|<br>**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
||||||be included in the message.|||
|flight/assignedAltitude/vfrPlus<br>flight/assignedAltitude/vfrPlus/<br>@uom|assignedAl<br>t_08h|It is used to specify that the flight is flying<br>VFR at a specified altitude.|nas:VfrPlusAltitude<br>Type|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**<br>Only one of the altitude elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_may<br>be included in the message.|The<br>aircraft is<br>flying VFR<br>at 7,500<br>feet:<br>**7500**<br>uom:<br>**feet**|No|
|flight/enRoute/position/altitude<br>flight/enRoute/position/altitude<br>/@uom|reportedA<br>lt_54a|The element is used to specify the<br>reported altitude. For aircraft with<br>operative Mode C capability, this element<br>contains the Mode C altitude. For aircraft<br>without Mode C capability or with non-<br>operative Mode C capability, this element<br>may contain the controller reported<br>altitude.|ff:AltitudeType|Yes|**xs:double**<br>**@uom:**<br>**“FEET|METRES”**|**31000**<br>**FEET**<br>The<br>aircraft<br>reported<br>altitude is<br>31,000<br>feet.|No|
|flight/interimAltitude<br>flight/interimAltitude/@uom|interimAlt<br>_76b|This element specifies the interim altitude<br>the flight is cleared to maintain different<br>from that in the flight plan.<br>The attribute_uom_specifies the unit of<br>measure for the_interimAltitude_element:<br>FEET/METRES.|Type of<br>_interimAltitude_:<br>nas:SimpleAltitude<br>Type<br>Type of<br>_interimAltitude/@_<br>_uom:_<br>_ff:AltitudeMeasure_<br>_Type_|Yes<br>@ou<br>m:<br>No|_interimAltitude_:<br>xs:double<br>_@uom:_<br>**“FEET|METRES”**|**240000**<br>**FEET**|No|

##### **5.5.1.41 Tentative Aircraft Identification Amendment Information [NI] – Data Elements**

|**Element Name**<br>**[NI]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|

214

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NI]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_)<br>and the last four-digits, represent<br>the message sequence number in<br>the range [0000-9999].|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of<br>the message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format_hh_mm_ss_,<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_stands<br>for the 2-digit minutes in the range<br>00-59, and_ss_stands for the 2-digit<br>seconds in the range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic<br>character followed by one to six<br>alphanumeric characters.|AAL20|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, as specified by<br>the pattern above.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely identify<br>a flight plan in each ERAM facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|newFlightId_02aN|The new Aircraft ID, or flight ID (also<br>called Call Sign), that has been<br>changed by the NI message.|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>It has a variable format, starting<br>with one uppercase alphabetic<br>character,followed byone to six|**DAL52**|Yes|

215

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NI]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||alphanumeric characters. When it<br>is only two characters long, the<br>format must be one letter followed<br>by one digit, such as A1 for Air<br>Force One.|||
|newComputerId_02d<br>N|This element contains the new<br>Computer ID that has been changed<br>by the NI message.|string|No|**"([0-9][A-HJ-NP-Z0-9]{2}) |**<br>**([A-HJ-NP-Z]{3}) |**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The computer ID is represented by<br>three alphanumeric characters, as<br>specified by the pattern above.<br>The letters**I**and**O**are prohibited.<br>One special all alphabetic code<br>may be used, literally, XXX. This is<br>only used in DA (Data Accept)<br>messages in response to an ARTS<br>VFR flight plan input.|**436**|No|
|newSspId_167aN|This element contains the new Site<br>Specific Plan Identifier that has been<br>changed by the NI message.|string|No|**"\d{1,4}"**<br>The format consists of one- to four-<br>digit string in a range from 0 –<br>4000.|32|No|

216

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.42 Tentative Aircraft Identification Amendment Information [NI] - Diagram**

##### **5.5.1.43 Tentative Aircraft Identification Amendment Information Message in FIXM Format [NI_FIXM] – Data Elements**

The following elements of the NI message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

|**Name**<br>**[NI_FIXM]**|**Name**<br>**[NI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Exampl**<br>**e**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/flightIdentificationPrevious/@<br>aircraftIdentification|flightId_<br>02a|Name used by Air Traffic Services<br>units to identify and communicate<br>with an aircraft.|fb:FlightIdentifierTy<br>pe|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|

217

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NI_FIXM]**|**Name**<br>**[NI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Exampl**<br>**e**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additionalF<br>lightInformation/nameValue/@nam<br>e<br>flight/supplementalData/additionalF<br>lightInformation/nameValue/@valu<br>e|FDPS_S<br>equenc<br>eNo|Sequence number assigned by SFDPS<br>to each message it receives from<br>HADDS. The attribute_name_includes<br>the constant string "MSG_SEQ_NO",<br>and the attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|@name<br>="MSG<br>_SEQ_<br>NO"<br>@value<br>="6860<br>416"|Yes|
|flight/departure/@departurePoint|FDPS_O<br>rigin/de<br>parture<br>Point_2<br>6a|Attribute used to specify the first<br>point or other initial entity where the<br>air traffic control/management<br>system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used<br>for this element (fix name,<br>lat/long, or fix-radial-<br>distance), including the<br>standard airport<br>designators.|<br>**AB**<br>**DFW**<br>**KDFW**<br>**SHP090**<br>**015**<br>**ATOKA**<br>**300040**<br>**3500N/**<br>**04000**<br>**W**|No|
|flight/arrival/@arrivalPoint|FDPS_D<br>estId/de<br>stinatio<br>n_27a|The final point or other final entity<br>where the air traffic<br>control/management system route<br>terminates.|fb:FreeTextType|No|xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used<br>for this element (fix name,<br>lat/long, or fix-radial-<br>distance), including the<br>standard airport<br>designators.|<br>**AB**<br>**DFW**<br>**KDFW**<br>**SHP090**<br>**015**<br>**ATOKA**<br>**300040**<br>**3500N/**<br>**04000**<br>**W**|No|
|flight/operator/operatingOrganizati<br>on/organization/@name|FDPS_Fl<br>ightOpe|Attribute used to specify the full<br>official name of the State,|ff:TextNameType|No|xs:string|UAL|No|

218

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NI_FIXM]**|**Name**<br>**[NI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Exampl**<br>**e**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
||rator/O<br>PRIndic<br>ator_91<br>8f|Organization, Authority, aircraft<br>operating agency, handling agency<br>engaged in or offering to engage in<br>aircraft operation.||||||
|flight/@system|propSou<br>rceSyste<br>m|This attribute indicates which SFDPS<br>system generated the message.|fb:ProvenanceSyste<br>mType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcv<br>dTime|This attribute conatins the time at<br>which the message was received by<br>SFDPS.|ff:TimeType|No|xs:dateTime|2015-<br>12-<br>18T22:<br>19:02.0<br>28Z|Yes|
|flight/@centre|center|This attribute specifies the code of the<br>ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCentr<br>eType|No|xs:string|ZAU|Yes|
|flight/arrival/runwayPositionAndTim<br>e/runwayTime/[estimated|actual]/<br>@time|arrivalTi<br>me|This attribute specifies the proposed<br>or the actual time of arrival at<br>destination, set according to the flight<br>state.|ff:TimeType|No|xs:dateTime|2014-<br>06-<br>20T20:<br>17:52|Yes|
|flight/departure/runwayPositionAnd<br>Time/runwayTime/[actual|estimate<br>d]/@time|departu<br>reTime|This element specifies the proposed<br>or actual departure time, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-<br>06-<br>20T20:<br>17:52|Yes|
|flight/flightStatus/@fdpsFlightStatus|flightSta<br>te|This attribute contains the current<br>status of the flight as specified by<br>SFDPS.|nas:SfdpsFlightStat<br>usType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPL<br>ETED|CANCELLED|DROPPED<br>”|ACTIVE|Yes|
|flight/supplementalData/additionalF<br>lightInformation/nameValue/@nam|fdpsGufi|The name value pair specifies the<br>SFDPS GUFI, an identifier on every|fb:FreeTextType|No|xs:string<br>@name:|name="<br>FDPS_G|Yes|
|e<br>flight/supplementalData/additionalF||message that positively identifies<br>what flight the message is for.|||"FDPS_GUFI"|UFI"<br>value="||

219

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NI_FIXM]**|**Name**<br>**[NI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Exampl**<br>**e**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|lightInformation/nameValue/@valu<br>e|||||@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-<br>Za-z0-9/]+"|us.fdps.<br>2015-<br>12-<br>18T16:<br>59:10Z.<br>000/14<br>/100"/>||
|flight/flightPlan/@identifier|eramGu<br>fi_316a|This attribute specifies the unique<br>flight plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU683<br>78100"|No|
|flight/gufi|uuidGuf<br>i|This element contains a reference that<br>uniquely identifies a flight and that is<br>independent of any particular system.<br>This reference conforms to the<br>Universal Unique Identifier standard.|fb:GloballyFlightIde<br>ntifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-<br>F]{4}\-4[0-9a-fA-F]{3}\-<br>[89aAbB][0-9a-fA-F]{3}\-[0-<br>9a-fA-F]{12}"|4aaf92<br>be-<br>ac0a-<br>4dba-<br>998f-<br>9e56f5<br>d450b6|Yes|
|flight/flightIdentificationPrevious/@<br>computerId|comput<br>erId_02<br>d|A unique identification assigned by<br>ERAM to each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two<br>alphanumeric characters<br>with the exception of the<br>letters**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.|<br>**020**|No|
|flight/flightIdentificationPrevious/@<br>siteSpecificPlanId|sspId_1<br>67a|Site Specific Plan Identifier. It is<br>assigned by Instrument Flight<br>Procedures Automation (IFPA) to<br>uniquely identify a flight plan in each<br>ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/flightIdentification/@aircraftId<br>entification|newFlig<br>htId_02<br>aN|The new Aircraft ID, or flight ID (also<br>called Call Sign), that has been<br>changed by the NI_FIXM message.|fb:FlightIdentifierTy<br>pe|No|**"[A-Z0-9]{7}"**|**AAL100**|Yes|

220

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NI_FIXM]**|**Name**<br>**[NI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Exampl**<br>**e**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@name<br>flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@value||The flight supplemental data is used<br>to indicate that a flight message is a<br>test message, by setting the attribute<br>_name_to “**SIMULATED_FLIGHT**” and<br>the attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1,**<br>**maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name<br>=<br>**“SIMUL**<br>**ATED_F**<br>**LIGHT”**<br>@value<br>=<br>**“true”**|No|
|flight/flightIdentification/@compute<br>rId|newCo<br>mputerI<br>d_02dN|<br>This element contains the new<br>Computer ID that has been changed<br>by the NI_FIXM message.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two<br>alphanumeric characters<br>with the exception of the<br>letters**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.|<br>**030**|No|
|flight/flightIdentification/@siteSpeci<br>ficPlanId|newSspI<br>d_167a<br>N|This element contains the new Site<br>Specific Plan Identifier that has been<br>changed by the NI_FIXM message.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**32**|No|

##### **5.5.1.44 Tentative Flight Plan Removal [NL] – Data Elements**

|**Element Name**<br>**[NL]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four- digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6<br>digits represent the UTC time<br>(_hhmmss_)and the last four digits,|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and|Yes|

221

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NL]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||represent the message sequence<br>number in the range [0000-9999].|the last 4 digits are<br>sequence number of<br>the message (9001).||
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format_hh_mm_ss_,<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_<br>stands for the 2-digit minutes in<br>the range 00-59, and_ss_stands for<br>the 2-digit seconds in the range<br>00-59.|23_59_35<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the sourceId_00e<br>element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|9001|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One upper-case alphabetic<br>character followed by one to six<br>alphanumeric characters.|AAL20|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, as specified by<br>the pattern above.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|
|mergedFPStatus_339a|This field contains the tentative<br>flight plan merge status. The<br>merge status must be one of the<br>following:<br>N - deletion without merge – the|string|No|**“[NSD]”**<br>One of the letters**N**,**S**, or**D**.|**N**<br>**S**<br>**D**|Yes|

222

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NL]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||tentative plan is deleted without<br>merge<br>S* - merge – an active plan is<br>merged into the tentative flight<br>plan; the flight has the same CID<br>and Site Specific Plan Identifier as<br>the tentative plan<br>D* - merge – a proposed plan is<br>activated and the tentative flight<br>plan is merged into the activated<br>plan; the flight has the CID and<br>Site Specific Plan Identifier of the<br>activated plan which are different<br>from the tentative plan.<br>* Note: For field value S, an FH is<br>sent for the merged flight plan. For<br>value D, an AH or DH message is<br>sent for the activated flight plan.||||||
|mergedFPComputerId_341<br>a|This element specifies the merged<br>flight plan computer ID.|string|No|**"\d[A-Z0-9][A-Z0-9]"**<br>The format consists of one digit<br>followed by two alphanumeric<br>characters.|**9PP**<br>**45A**<br>**522**|No|
|mergedFPSspId_342a|This element contains the merged<br>flight plan site-specific identifier. If<br>the merge is of an active flight into<br>the tentative flight,<br>(_mergedFPStatus_339a_=S), the<br>SSPID is the same as the tentative.<br>If the merge is due to activation of<br>a proposed flight plan,<br>(_mergedFPStatus_339a_=D), the<br>SSPID is that of the activated flight<br>plan.|string|No|**"\d{1,4}"**|**25**<br>**5289**|No|

223

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.45 Tentative Flight Plan Removal [NL] - Diagram**

##### **5.5.1.46 Tentative Flight Plan Removal Message in FIXM Format [NL_FIXM]**

The following elements of the NL message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

- mergedFPStatus_339a

|**Name**<br>**[NL_FIXM]**|**Name**<br>**[NL]**|**Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additio|FDPS_Se|Sequence number assigned by|@name:|No|@name:|@name="MSG_|Yes|
|nalFlightInformation/nameValue<br>/@name<br>flight/supplementalData/additio|quenceN<br>o|SFDPS to each message it<br>receives from HADDS. The<br>attribute_name_includes the|@value:<br>fb:FreeTextT||”MSG_SEQ_NO”<br>@value:|SEQ_NO"<br>@value="68604<br>16"||

224

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NL_FIXM]**|**Name**<br>**[NL]**|**Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|nalFlightInformation/nameValue<br>/@value||constant string<br>"MSG_SEQ_NO", and the<br>attribute_value_contains the<br>sequence number value.|ype||xs:nonNegativeIntege<br>r<br>xs:maxInclusive<br>value="999999999"|||
|flight/departure/@departurePoi<br>nt|FDPS_Ori<br>gin/depa<br>rturePoin<br>t_26a|Attribute used to specify the<br>first point or other initial entity<br>where the air traffic<br>control/management system<br>route starts.|fb:FreeTextT<br>ype|No|xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-**<br>**Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard<br>ways to represent a<br>fix can be used for<br>this element (fix<br>name, lat/long, or fix-<br>radial-distance),<br>including the<br>standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arrivalPoint|FDPS_De<br>stId/desti<br>nation_2<br>7a|The final point or other final<br>entity where the air traffic<br>control/management system<br>route terminates.|fb:FreeTextT<br>ype|No|xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-**<br>**Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard<br>ways to represent a<br>fix can be used for<br>this element (fix<br>name, lat/long, or fix-<br>radial-distance),<br>including the<br>standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|

225

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NL_FIXM]**|**Name**<br>**[NL]**|**Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/operator/operatingOrganiz<br>ation/organization/@name|FDPS_Flig<br>htOperat<br>or/OPRIn<br>dicator_9<br>18f|Attribute used to specify the<br>full official name of the State,<br>Organization, Authority, aircraft<br>operating agency, handling<br>agency engaged in or offering<br>to engage in aircraft operation.|ff:TextName<br>Type|No|xs:string|UAL|No|
|flight/@system|propSour<br>ceSystem|This attribute indicates which<br>SFDPS system generated the<br>message.|fb:Provenan<br>ceSystemTy<br>pe|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvd<br>Time|This attribute conatins the time<br>at which the message was<br>received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.02<br>8Z|Yes|
|flight/@centre|center|This attribute specifies the code<br>of the ARTCC (or<br>FIR) that produced the data.|fb:Provenan<br>ceCentreTyp<br>e|No|xs:string|`ZAU`|Yes|
|flight/arrival/runwayPositionAnd<br>Time/runwayTime/[estimated|ac<br>tual]/@time|arrivalTi<br>me|This attribute specifies the<br>proposed or the actual time of<br>arrival at destination, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/departure/runwayPosition<br>AndTime/runwayTime/[actual|es<br>timated]/@time|departur<br>eTime|This element specifies the<br>proposed or actual departure<br>time, set according to the flight<br>state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/flightStatus/@fdpsFlightSta<br>tus|flightStat<br>e|This attribute contains the<br>current status of the flight as<br>specified by SFDPS.|nas:SfdpsFli<br>ghtStatusTy<br>pe|Yes|xs:string<br>“PROPOSED|ACTIVE|<br>COMPLETED|CANCELL<br>ED|DROPPED”|ACTIVE|Yes|

226

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NL_FIXM]**|**Name**<br>**[NL]**|**Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@name<br>flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@value|fdpsGufi|The name value pair specifies<br>the SFDPS GUFI, an identifier on<br>every message that positively<br>identifies what flight the<br>message is for.|fb:FreeTextT<br>ype|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-<br>\d{2}-<br>\d{2}T\d{2}:\d{2}:\d<br>{2}Z\.[A-Za-z0-9/]+"|name="FDPS_G<br>UFI"<br>value="us.fdps.<br>2015-12-<br>18T16:59:10Z.0<br>00/14/100"/>|Yes|
|flight/flightPlan/@identifier|eramGufi<br>_316a|This attribute specifies the<br>unique flight plan identifier.|fb:FreeTextT<br>ype|No|xs:string<br>"[A-Z]{2}\d{5}[1-<br>7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|<sup>This element contains a</sup><br>reference that uniquely<br>identifies a flight and that is<br>independent of any particular<br>system. This reference<br>conforms to the Universal<br>Unique Identifier standard.|fb:GloballyFl<br>ightIdentifie<br>rType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-<br>fA-F]{4}\-4[0-9a-fA-<br>F]{3}\-[89aAbB][0-9a-<br>fA-F]{3}\-[0-9a-fA-<br>F]{12}"|4aaf92be-ac0a-<br>4dba-998f-<br>9e56f5d450b6|Yes|
|flight/flightIdentification/@aircra<br>ftIdentification|flightId_0<br>2a|Name used by Air Traffic<br>Services units to identify and<br>communicate with an aircraft.|fb:FlightIden<br>tifierType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@name<br>flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@value||The flight supplemental data is<br>used to indicate that a flight<br>message is a test message, by<br>setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the<br>attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextT_<br>_ype_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1,**<br>**maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_F**<br>**LIGHT”**<br>@value =**“true”**|No|

227

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NL_FIXM]**|**Name**<br>**[NL]**|**Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/flightIdentification/@comp<br>uterId|compute<br>rId_02d|A unique identification assigned<br>by ERAM to each flight plan.<br>This element specifies the<br>computer ID (CID) of the<br>tentative flight plan when the<br>tentative flight plan is deleted<br>without a merge, or when an<br>active flight plan is merged into<br>the tentative flight plan. The<br>merged flight plan SSPID and<br>CID and the tentative flight plan<br>SSPID and CID are the same in<br>the latter case and the element<br>_flight/flightIdentificationPreviou_<br>_s_is not included in the message.|fb:FreeTextT<br>ype|No|**"([0-9][A-HJ-NP-Z0-**<br>**9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-**<br>**9])"**<br>The element includes<br>a digit, followed by<br>two alphanumeric<br>characters with the<br>exception of the<br>letters**I**and**O**, such<br>as_ddd, ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentificationPrevious<br>/@computerId|compute<br>rId_02d|When the tentative flight plan<br>merge consists in a proposed<br>flight plan being activated and<br>the tentative flight plan being<br>merged into the activated flight<br>plan, the flight has the CID of<br>the activated plan which is<br>different from the CID of the<br>tentative flight plan. This<br>attribute specifies the CID of the<br>tentative flight plan, while the<br>attribute<br>flight/flightIdentification/@com<br>puterId specifies the merged<br>flightplan computer ID.|fb:FreeTextT<br>ype|No|**"([0-9][A-HJ-NP-Z0-**<br>**9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-**<br>**9])"**<br>The element includes<br>a digit, followed by<br>two alphanumeric<br>characters with the<br>exception of the<br>letters**I**and**O**, such<br>as_ddd, ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/@siteS<br>pecificPlanId|sspId_16<br>7a|Site Specific Plan Identifier<br>(SSPID). It is assigned by<br>Instrument Flight Procedures<br>Automation (IFPA) to uniquely<br>identify a flight plan in each<br>ERAM facility. This element<br>specifies the SSPID of the<br>tentative flight plan when the<br>tentative flightplan is deleted|fb:CountTyp<br>e|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|

228

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NL_FIXM]**|**Name**<br>**[NL]**|**Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||without a merge, or when an<br>active flight plan is merged into<br>the tentative flight plan. The<br>merged flight plan SSPID and<br>CID and the tentative flight plan<br>SSPID and CID are the same in<br>the latter case and the element<br>_flight/flightIdentificationPreviou_<br>_s_is not included in the message.||||||
|flight/flightIdentificationPrevious<br>/@siteSpecificPlanId|sspId_16<br>7a|When the tentative flight plan<br>merge consists in a proposed<br>flight plan being activated and<br>the tentative flight plan being<br>merged into the activated flight<br>plan, the flight has the SSPID of<br>the activated plan which is<br>different from the SSPID of the<br>tentative flight plan. This<br>attribute specifies the SSPID of<br>the tentative flight plan, while<br>the attribute<br>_flight/flightIdentification/@_<br>_siteSpecificPlanId_specifies the<br>merged flightplan SSPID.|fb:CountTyp<br>e|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/flightIdentification/@comp<br>uterId|mergedF<br>PComput<br>erId_341<br>a|This element specifies the<br>merged flight plan computer ID.|fb:FreeTextT<br>ype|No|**"([0-9][A-HJ-NP-Z0-**<br>**9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-**<br>**9])"**<br>The element includes<br>a digit, followed by<br>two alphanumeric<br>characters with the<br>exception of the<br>letters**I**and**O**, such<br>as_ddd, ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/@siteS<br>pecificPlanId|mergedF<br>PSspId_3<br>42a|This element contains the<br>merged flight plan site-specific<br>identifier. If the merge is of an|fb:CountTyp<br>e|No|**"\d{1,4}"**<br>One to four-digits.|**25**|No|

229

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NL_FIXM]**|**Name**<br>**[NL]**|**Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||active flight into the tentative<br>flight, the SSPID is the same as<br>the tentative. If the merge is<br>due to activation of a proposed<br>flight plan), the SSPID is that of<br>the activated flight plan.||||||

##### **5.5.1.47 Tentative Flight Plan Amendment Information [NU] – Data Elements**

|**Element Name**<br>**[NU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed by<br>a four-digit sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**<br>where the first 6 digits<br>are the UTC time<br>(23:59:35 UTC) and the<br>last 4 digits are<br>sequence number of<br>the message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the sourceId_00e<br>element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed byone to six alphanumeric|**AAL20**|Yes|

230

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||characters.|||
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**, as<br>specified by the pattern above.|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each<br>ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|
|numberOfAircraft_03<br>a|This element includes the<br>number of aircraft for the flight<br>followed optionally by the<br>Special Aircraft Indicator.|string|No|**"\d{0,2}[A-Z]?"**<br>The element consists of zero to two<br>digits optionally followed by one<br>uppercase letter to represent the Special<br>Aircraft Indicator. The indicator can also<br>appear on its own (without the leading<br>digits).|**3H**<br>The number of aircraft<br>is 3 and the special<br>aircraft indicator is**H**<br>for Heavy Jet.|No|
|typeOfAircraft_03c|Type of aircraft.|string|No|**"[A-Z][A-Z0-9]{1,3}"**<br>The element consists of one letter<br>followed by one to three alphanumeric<br>characters.|**B747**|Yes|
|airborneEquip_03e|Airborne equipment qualifier. It<br>consists of one alphanumeric<br>character.|string|No|**"[A-Z]"**<br>The element consists of one<br>alphanumeric character, that can have<br>one of the following values:<br>**A**- Transponder with no Mode C<br>**B**- Transponder with Mode C<br>**E**– FMS with DME/DME and IRU<br>position updating<br>**G**– GNSS, including GPS or WAAS, with<br>en-route and terminal capability<br>**X**– No transponder<br>**W**- RVSM|**E**|No|
|beaconCode_04a|Beacon code.|string|No|**"[0-7]{4}"**|Non-discrete VFR|No|

231

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||**_Note_:** As of SFDPS 1.3.1, if the<br>flightState element has a value<br>of ‘Canceled’ or ‘Proposed’, this<br>element is only present in the<br>version of a message with<br>FDPS_Restricted=’R’|||The element includes four octal digits<br>(i.e. 0-7). When the last two digits of the<br>four digits are zero, the beacon code is a<br>non-discrete code.<br>A discrete code is any code not ending in<br>00.|code:<br> **2101**||
|trueAirSpeed_05a|True airspeed expressed in<br>knots.|string|No|**"\d{2,4}"**<br>The format is two to four digits, in the<br>range 01 – 3700 knots.<br>Aircraft speed is required to be specified<br>by using one of the three possible<br>elements: trueAirSpeed_05a,<br>machSpeed_05c or classifiedSpeed_05d.|**540**<br>Aircraft true airspeed<br>is 540 knots.|Yes, if neither<br>machSpeed_05c nor<br>classifiedSpeed_05d<br>are included in the<br>message.|
|machSpeed_05c|Mach speed.|string|No|**“M\d{3}”**<br>The letter**M**followed by three digits.<br>The maximum value is M500.|The speed 0.85 Mach<br>is represented as<br>**M085**.|Yes, if neither<br>trueAirSpeed_05a<br>nor<br>classifiedSpeed_05d<br>are included in the<br>message.|
|classifiedSpeed_05d|Adapted classified speed. It is<br>not printed on flight strips.|string|No|**“SC”**|This element may only<br>include the string<br>character**SC**.|Yes, if neither<br>trueAirSpeed_05a<br>nor machSpeed_05c<br>are included in the<br>message.|
|assignedAlt_08a|Assigned altitude or flight level<br>expressed in hundreds of feet.<br>Only one of the altitude<br>elements assignedAlt_08a,<br>assignedAlt_08b,<br>assignedAlt_08c,<br>assignedAlt_08d,<br>assignedAlt_08e,<br>assignedAlt_08f,<br>assignedAlt_08g,<br>assignedAlt_08h may be<br>included in the message.|string|No|**“(\d{2,3}) | VFR”**<br>The format consists of either two to<br>three digits, or the constant string**VFR**.<br>Three digits are required for ARTS III,<br>thus a leading zero needs to be used<br>when necessary.|Assigned altitude of<br>34,000 feet:<br>**340**<br>Assigned altitude<br>9,000 feet ARTS III:<br>**090**|No|

232

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|assignedAlt_08b|Fixed value of**OTP**which<br>indicates VFR-ON-Top. It<br>specifies that the aircraft is<br>flying above the clouds in VFR<br>conditions.<br>It may only be specified if none<br>of the other assignedAtl_08<br>elements is included in the<br>message.|string|No|**“OTP”**|Fixed value of**OTP.**|No|
|assignedAlt_08c|VFR-ON-Top with altitude. It<br>represents an IFR flight<br>operating above the clouds in<br>VFR conditions at the specified<br>assigned altitude.<br>It may only be specified if none<br>of the other assignedAtl_08<br>elements is included in the<br>message.|string|No|“**OTP/\d{2,3}**”<br>The format is the constant string**OTP**/<br>followed by two to three digits that<br>represent the assigned altitude in<br>hundreds of feet.|Aircraft flying VFR-ON-<br>Top at 25,000 feet:<br>**OTP/250**|No|
|assignedAlt_08d|The assigned block of altitudes<br>for the flight to fly at.<br>It may only be specified if none<br>of the other assignedAtl_08<br>elements is included in the<br>message.|string|No|**"\d{2,3}B\d{2,3}"**<br>The format is two to three digits,<br>followed by the letter**B**, followed by<br>two to three digits. The leading and<br>trailing two to three digits define the<br>block of altitudes in hundreds of feet for<br>the flight to fly at. The lowest altitude<br>must be listed first.|Assigned altitude<br>block of 8,000 feet to<br>14,000 feet:<br>**80B140**|No|
|assignedAlt_08e|Element used for IFR flights<br>operating above a specified<br>altitude.<br>It may only be specified if none<br>of the other assignedAtl_08<br>elements is included in the<br>message.|string|No|**“ABV/\d{2,3}"**<br>The format consists of the string**ABV/**<br>followed by two to three digits that<br>represent the altitude in hundreds of<br>feet above which the flight is flying.|Aircraft is flying above<br>60,000 feet.<br>**ABV/600**|No|
|assignedAlt_08f|Assigned Altitude/FIX/Altitude<br>element specifies the altitudes<br>to and from a fix for the flight|string|No|**"(\d{2,3}/[A-Z0-9]{2,5}/\d{2,3})|**<br>**(\d{2,3}/[A-Z0-9]{2,5}\d{6}/\d{2,3}) |**<br>**(\d{2,3}/\d{4}[A-Z]?/\d{4,5}[A-**|**240/DAL350010/220**<br>Flight flies at altitude<br>24,000 feet to the fix|No|

233

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||to fly at.<br>It may only be specified if none<br>of the other assignedAtl_08<br>elements is included in the<br>message.|||**Z]?/\d{2,3})"**<br>The altitudes are specified in hundreds<br>of feet in a two to three digit format.<br>The fix is specified using the same<br>format as the coordination fix element<br>“coordFix_06a”.<br>The fix cannot be the departure or<br>arrival point.|radial distance fix and<br>then descend to<br>altitude 22,000 feet.||
|assignedAlt_08g|It is used to specify that the<br>flight is flying Visual Flight Rules<br>(VFR). It can only have the<br>value**VFR**.<br>It may only be specified if none<br>of the other assignedAtl_08<br>elements is included in the<br>message.|string|No|**“VFR”**|The string**VFR.**|No|
|assignedAlt_08h|It is used to specify that the<br>flight is flying VFR at a specified<br>altitude.<br>It may only be specified if none<br>of the other assignedAtl_08<br>elements is included in the<br>message.|string|No|**“VFR/\d{2,3}"**<br>The format consists of the string**VFR/**<br>followed by two to three digits that<br>represent an altitude in hundreds of<br>feet.|**VFR/75**<br>The aircraft is flying<br>VFR at 7,500 feet.|No|
|reportedAlt_54a|The element is used to specify<br>the reported altitude. For<br>aircraft with operative Mode C<br>capability, this element contains<br>the Mode C altitude. For aircraft<br>without Mode C capability or<br>with non-operative Mode C<br>capability, this element may<br>contain the controller reported<br>altitude. If there is no Mode C<br>or controller reported altitude,<br>or the reported altitude is<br>negative,this element contains|string|No|**"\d{1,3}"**<br>The format consists of one to three<br>digits that represent the reported<br>aircraft altitude in hundreds of feet.<br>Leading zeros may be inserted for<br>altitudes of less than 3 digits.|**310**<br>The aircraft reported<br>altitude is 31,000 feet.|No|

234

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||“0” or "000" or is optional.||||||
|reportedAlt_54b|This field is the reported<br>altitude B4 indicator. The ERAM<br>controllers’ full data block used<br>for tracking an aircraft has a<br>special indicator for the B4<br>character of the full data block.|string|No|**“[ABCFNTVX^v+-/]”**<br>The format of this element is one<br>character as follows:<br>A - Reported altitude (controller entered)<br>equals single assigned altitude.<br>B - Beacon reported altitude is in<br>conformance or controller entered<br>reported altitude is in the block for an<br>aircraft which has been assigned an<br>altitude block (B1 to B3 - low altitude<br>limit of block and C1 to C3=high altitude<br>limit of block).<br>C - Beacon reported altitude is within<br>Altitude Conformance Limits feet.<br>F - Reported altitude (controller entered)<br>equals first altitude or (beacon reported)<br>is within Altitude Conformance Limits of<br>first altitude when assigned altitude is<br>(d)dd/fix/(d)dd and the first altitude is<br>displayed in Field B.<br>N - No beacon reported altitude has<br>been received for the aircraft; no<br>controller entered reported altitude<br>exists for the aircraft; or the aircraft’s<br>rate of change is questionable and<br>Computed Rate of Change is being used<br>to make further conformance checks.<br>T - Interim altitude is currently being<br>displayed in the assigned altitude field<br>(B1 through B3).<br>V - Beacon reported or controller<br>entered reported altitude, when no<br>assigned altitude exists for the aircraft.<br>X - Beacon reported altitude becomes<br>disestablished. (C1-C3 also contains `X'<br>character.)|**B**|No|

235

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||^ - Beacon reported or controller<br>entered reported altitude is below<br>assigned altitude when flight is climbing<br>v - Beacon reported or controller entered<br>reported altitude is above assigned<br>altitude when flight is descending<br>+ - Beacon reported altitude exceeds<br>upper conformance limit for an aircraft<br>which has reached it assigned altitude or<br>the controller entered reported altitude<br>exceeds the assigned altitude for a non-<br>Mode C aircraft which has previously<br>been reported at the assigned altitude.<br>- - Beacon reported altitude is less than<br>lower conformance limit for an aircraft<br>which has reached its assigned altitude<br>or the controller entered reported<br>altitude is less than the assigned altitude<br>for a non-Mode C aircraft which has<br>previously been reported at the assigned<br>altitude.<br>/ - Flight type is `OTP' or `VFR’|||
|reportedAlt_54c|The element specifies the<br>reported altitude C4 indicator.<br>The ERAM controllers full data<br>block used for tracking an<br>aircraft has a special indicator<br>for the C4 character of the full<br>data block as follows: If the<br>aircraft is not responding with<br>the Mode C altitude, the<br>controller entered reported<br>altitude is displayed in<br>_reportedAlt_54c_with a pound<br>sign(#)or X inposition C4|string|No|**“[#X]”**|**#**|No|

236

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[NU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||whenever (1) the controller<br>entered reported altitude does<br>not equal the assigned altitude<br>or is not within the assigned<br>altitude block, (2) no assigned<br>altitude has been entered, or (3)<br>the assigned altitude is VFR,<br>VFR/(d)dd, OTP, or OTP/(d)dd.<br>In either case for a Mode C<br>reported altitude or a controller<br>reported altitude, when an<br>interim altitude is displayed in<br>_reportedAlt_54b_<br>the B4 character position<br>contains the letter “T” and the<br>reported altitude, or either the<br>lower or upper altitude of an<br>assigned block altitude is<br>displayed in_reportedAlt_54c_. In<br>the case where a controller<br>entered reported altitude exists,<br>a pound sign (#) or X is<br>displayed in the C4 position.||||||
|interimAlt_76b|This element specifies the<br>interim altitude for the flight in<br>hundreds of feet. It is included<br>in the message if an interim<br>altitude is assigned.|string|No|**"\d{1,3}"**|**240**|No|

237

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.48 Tentative Flight Plan Amendment Information [NU] - Diagram**

238

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.49 Tentative Flight Plan Amendment Information Message in FIXM Format [NU_FIXM] – Data Elements**

The following elements of the NU message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

- reportedAlt_54b

- reportedAlt_54c

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|flight/supplementalData/additiona<br>lFlightInformation/nameValue/@n<br>ame<br>flight/supplementalData/additiona<br>lFlightInformation/nameValue/@v<br>alue<br><br><br>|FDPS_S<br>equenc<br>eNo|Sequence number assigned<br>by SFDPS to each message it<br>receives from HADDS. The<br>attribute_name_includes the<br>constant string<br>"MSG_SEQ_NO", and the<br>attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No<br>@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive value="999999999"|@name="MSG_S<br>EQ_NO"<br>@value="686041<br>6"|Yes|
|flight/departure/@departurePoint<br><br><br><br>|FDPS_O<br>rigin/de<br>parture<br>Point_2<br>6a|Attribute used to specify the<br>first point or other initial<br>entity where the air traffic<br>control/management system<br>route starts.|fb:FreeTextType|No<br>xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a fix can be<br>used for this element (fix name, lat/long, or fix-radial-<br>distance), including the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arrivalPoint<br><br>|FDPS_D<br>estId/de|The final point or other final<br>entity where the air traffic|fb:FreeTextType|No<br>xs:string<br>minLength=2, maxLength=12|**AB**<br>**DFW**|No|

239

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
||stinatio<br>n_27a|control/management system<br>route terminates.||**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a fix can be<br>used for this element (fix name, lat/long, or fix-radial-<br>distance), including the standard airport designators.|**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**||
|flight/operator/operatingOrganiza<br>tion/organization/@name|FDPS_Fl<br>ightOpe<br>rator/O<br>PRIndic<br>ator_91<br>8f|Attribute used to specify the<br>full official name of the State,<br>Organization, Authority,<br>aircraft operating agency,<br>handling agency engaged in<br>or offering to engage in<br>aircraft operation.|ff:TextNameTyp<br>e|No<br>xs:string|UAL|No|
|flight/@system|propSou<br>rceSyste<br>m|This attribute indicates which<br>SFDPS system generated the<br>message.|fb:ProvenanceS<br>ystemType|No<br>xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcv<br>dTime|This attribute conatins the<br>time at which the message<br>was received by SFDPS.|ff:TimeType|No<br>xs:dateTime|2015-12-<br>18T22:19:02.028<br>Z|Yes|
|flight/@centre|center|This attribute specifies the<br>code of the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceC<br>entreType|No<br>xs:string|ZAU|Yes|
|flight/arrival/runwayPositionAndTi<br>me/runwayTime/estimated/@tim<br>e|arrivalTi<br>me|This attribute specifies the<br>proposed or the actual time<br>of arrival at destination, set<br>according to the flight state.|ff:TimeType|No<br>xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/departure/runwayPositionA<br>ndTime/runwayTime/[actual|esti<br>mated]/@time|departu<br>reTime|This element specifies the<br>proposed or actual departure<br>time, set according to the<br>flight state.|ff:TimeType|No<br>xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/flightStatus/@fdpsFlightStat<br>us|flightSta<br>te|This attribute contains the<br>current status of the flight as<br>specified by SFDPS.|nas:SfdpsFlightS<br>tatusType|Yes<br>xs:string<br>“PROPOSED|ACTIVE|COMPLETED|CANCELLED|DROP|ACTIVE|Yes|

240

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|||||PED”|||
|flight/supplementalData/additiona<br>lFlightInformation/nameValue/@n<br>ame<br>flight/supplementalData/additiona<br>lFlightInformation/nameValue/@v<br>alue<br>|fdpsGufi|The name value pair specifies<br>the SFDPS GUFI, an identifier<br>on every message that<br>positively identifies what<br>flight the message is for.|fb:FreeTextType|No<br>xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-<br>z0-9/]+"|name="FDPS_GU<br>FI"<br>value="us.fdps.2<br>015-12-<br>18T16:59:10Z.00<br>0/14/100"/>|Yes|
|flight/flightPlan/@identifier<br><br>|eramGu<br>fi_316a|This attribute specifies the<br>unique flight plan identifier.|fb:FreeTextType|No<br>xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi<br><br>|uuidGuf<br>i|This element contains a<br>reference that uniquely<br>identifies a flight and that is<br>independent of any particular<br>system. This reference<br>conforms to the Universal<br>Unique Identifier standard.|fb:GloballyFlight<br>IdentifierType|xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-4[0-9a-fA-F]{3}\-<br>[89aAbB][0-9a-fA-F]{3}\-[0-9a-fA-F]{12}"|4aaf92be-ac0a-<br>4dba-998f-<br>9e56f5d450b6|Yes|
|flight/flightIdentification/@aircraf<br>tIdentification<br><br>|flightId_<br>02a|Name used by Air Traffic<br>Services units to identify and<br>communicate with an<br>aircraft.|fb:FlightIdentifi<br>erType|No<br>**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additiona<br>lFlightInformation/nameValue/@n<br>ame<br>flight/supplementalData/additiona<br>lFlightInformation/nameValue/@v<br>alue||The flight supplemental data<br>is used to indicate that a<br>flight message is a test<br>message, by setting the<br>attribute_name_to<br>“**SIMULATED_FLIGHT**” and<br>the attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No<br>_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLI**<br>**GHT”**<br>@value =**“true”**|No|
|flight/flightIdentification/@compu<br>terId<br><br>|comput<br>erId_02|A unique identification<br>assigned by ERAM to each|fb:FreeTextType|No<br>**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**|**020**|No|

241

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
||d|flight plan.||The element includes a digit, followed by two<br>alphanumeric characters with the exception of the<br>letters**I**and**O**, such as_ddd, ddL, dLd, dLL_.|||
|flight/flightIdentification/@siteSp<br>ecificPlanId|sspId_1<br>67a|Site Specific Plan Identifier. It<br>is assigned by Instrument<br>Flight Procedures<br>Automation (IFPA) to<br>uniquely identify a flight plan<br>in each ERAM facility.|fb:CountType|No<br>**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/aircraftDescription/@aircraf<br>tQuantity|number<br>OfAircra<br>ft_03a|This element includes the<br>number of aircraft for the<br>flight.|fb:countType|No<br>**"\d{0,2}"**<br>The element consists of zero to two digits.|**3**|No|
|flight/aircraftDescription/@tfmsSp<br>ecialAircraftQualifier|number<br>OfAircra<br>ft_03a-<br>Special<br>Aircraft<br>Indicato<br>r|This element includes the<br>Special Aircraft Indicator. It<br>indicates the flight is a heavy<br>jet, B757 or, if not present, a<br>large jet and if the flight is<br>either equipped or not with<br>TCAS. This indicator is used<br>for output purposes such as<br>strip printing and message<br>transfers to other facilities<br>such as Automated Radar<br>Terminal System (ARTS).<br>NOTE<br>TFMS Special Aircraft<br>Qualifier is a bad fit to Special<br>Aircraft Indicator but no<br>other fields seem to fit.|nas:NasSpecialA<br>ircraftQualifierT<br>ype|No<br>**“HEAVY_JET|TCAS|B757|HEAVY_JET_AND_TCAS”**<br>**“HEAVY_JET”**=Capable of takeoff weights of<br>300,000 pounds or more<br>**“TCAS”**=Traffic collision avoidance system or<br>traffic alert and collision avoidance system<br>**“B757”**=Controllers are required to apply the<br>special wake turbulence separation criteria for the<br>Boeing 757.<br>**“HEAVY_JET_AND_TCAS”**=Capable of takeoff<br>weights of 300,000 pounds or more and traffic<br>collision avoidance system.|**HEAVY_JET**|No|
|flight/aircraftDescription/aircraftT<br>ype/icaoModelIdentifier|typeOfA<br>ircraft_<br>03c|The ICAO code of the aircraft<br>type.|fb:IcaoAircraftId<br>entifierType|No<br>**"[A-Z][A-Z0-9]{1,3}"**<br>The element consists of one letter followed by one to<br>three alphanumeric characters.|**B747**|Yes|

242

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|flight/aircraftDescription/@equip<br>mentQualifier|airborn<br>eEquip_<br>03e|Airborne equipment<br>qualifier. A value assigned to<br>the aircraft, based on its<br>navigational equipment,<br>whether or not it has a<br>transponder, and if it has a<br>transponder, whether the<br>transponder supports Mode<br>C.|nas:NasAirborne<br>EquipmentQuali<br>fierType|No<br>**" [ ABCDGHILMNPSTUVWXYZ]"**<br>The element consists of one alphanumeric character,<br>that can have one of the following values:<br>•<br>“X”= No RVSM, No DME, No transponder<br>•<br>“T”= No RVSM, No DME, Transponder with<br>no mode C<br>•<br>“U”= No RVSM, No DME: Transponder with<br>mode C<br>•<br>“D”= DME: No transponder<br>•<br>“B”= DME: Transponder with no mode C<br>•<br>“A”= DME: Transponder with mode<br>•<br>“M”= TACAN ONLY: No transponder<br>•<br>“N”= TACAN ONLY: Transponder with no<br>mode C<br>•<br>“P”= TACAN ONLY: Transponder with mode<br>C<br>•<br>“C”= “Y”= LORAN,VORDME,INS,RNAV: No<br>transponder<br>•<br>“I”= LORAN,VORDME,INSRNAV:<br>Transponder with mode C<br>•<br>“H”= RVSM, Failed transponder or Failed<br>Mode C capability<br>•<br>“S=ADVANCED RNAV, TRANSPONDER,<br>MODE C: FMS with DMEDME position<br>updating<br>•<br>“G”= ADVANCED RNAV, TRANSPONDER,<br>MODE C: Global Navigation Satellite System<br>(GNSS), including GPS or Wide Area<br>Augmentation System (WAAS), with enroute<br>and terminal capability<br>•<br>“V”= ADVANCED RNAV, TRANSPONDER,<br>MODE C: Required Navigational<br>Performance (RNP). The aircraft meets the<br>RNP type prescribed for the route segments,<br>routes and/or area concerned.<br>•<br>“Z”= REDUCED VERTICAL SEPARATION|**E**|No|

243

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|||||MINIMUM (RVSM): E with RVSM<br>•<br>“L”= REDUCED VERTICAL \ SEPARATION<br>MINIMUM (RVSM): G with RVSM<br>“W”= REDUCED VERTICAL SEPARATION MINIMUM<br>(RVSM): RVSM|||
|flight/enRoute/beaconCodeAssign<br>ment/currentBeaconCode|beacon<br>Code_0<br>4a|Current assigned beacon<br>code.<br>**_Note_: **As of SFDPS R1.3.1, if<br>the<br>flight/flightStatus/@fdpsFlig<br>htStatus attribute has a value<br>of ‘CANCELED or ‘PROPOSED,<br>this element is only present<br>in the version of a message<br>with FDPS_Restricted=’R’|fb:BeaconCodeT<br>ype|No<br>"[0-7]{4}"<br>The element includes four octal digits (i.e. 0-7). When<br>the last two digits of the four-digits are zero, the<br>beacon code is a non-discrete code.<br>A discrete code is any code not ending in 00|Non-discrete VFR<br>code:<br> **2101**|No|
|flight/requestedAirspeed/nasAirsp<br>eed<br>flight/requestedAirspeed/@uom|trueAirS<br>peed_0<br>5a<br>machSp<br>eed_05<br>c|The aircraft speed expressed<br>in either true airspeed or<br>mach.<br>The attribute uom contains<br>the unit of measure.|ff:<br>TrueAirSpeedOr<br>MachType<br>uom:<br>ff:AirspeedMeas<br>ureType|No<br>**“xs:double”**<br>uom:<br>**“KILOMETERS_PER_HOUR|KNOTS|MACH”**<br>This element is required if requestedAirspeed/classifed<br>is not included in the message.|**540**<br>@uom=**KNOTS**|No<br>uom:<br>Yes|
|flight/requestedAirspeed/classifie<br>d|classifie<br>dSpeed<br>_05d|Classified Speed Indicator. It<br>indicates that the speed for<br>this flight is classified and is<br>not to be recorded.|nas:ClassifiedSp<br>eedIndicatorTyp<br>e|No<br>**“CLASSIFIED”**<br>This element is required if<br>requestedAirspeed/nasAirspeed is not included in the<br>message.|**CLASSIFIED**|No|
|flight/assignedAltitude/simple<br>flight/assignedAltitude/simple/@u<br>om|assigne<br>dAlt_08<br>a|Simple altitude: single<br>measurement above<br>reference point. It represents<br>the only NAS altitude that<br>maps directly to the core<br>ICAO altitude types.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_, _vfr_, _vfrPlus_maybe|nas:SimpleAltitu<br>deType<br>uom:<br>ff:AltitudeMeas<br>ureType|Yes<br>**“xs:double”**<br>uom:<br>“**FEET|METERS**”|Assigned altitude<br>of 34,000 feet:<br>**34000**<br>@uom =**FEET**|No<br>uom:<br>Yes|

244

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|||included in the message.<br>The attribute_uom_contains<br>the unit of measure for the<br>element<br>_assignedAltitude/simple_.|||||
|flight/assignedAltitude/vfrOnTop|assigne<br>dAlt_08<br>b|The presence of this element<br>indicates VFR-ON-Top. It<br>specifies that the aircraft is<br>flying above the clouds in<br>VFR conditions.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|Nas:VfrOnTopAl<br>titudeType|Yes<br>Empty element.||No|
|flight/assignedAltitude/vfrOnTopP<br>lus<br>flight/assignedAltitude/vfrOnTopP<br>lus/@uom|assigne<br>dAlt_08<br>c|VFR-ON-Top with altitude. It<br>represents an Instrument<br>Flight Rules (IFR) flight<br>operating above the clouds<br>in VFR conditions at the<br>specified assigned altitude.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.<br>The attribute_uom_specifies<br>the unit of measure for the<br>_vfrOnTopPlus_element.|nas:VfrOnTopPl<br>usAltitudeType<br>uom:<br>ff:AltitudeMeas<br>ureType|No<br>**“xs:double”**<br>uom:<br>“**FEET|METERS**”|Aircraft flying<br>VFR-ON-Top at<br>25,000 feet:<br>**25000**<br>@uom =**FEET**|No<br>uom:<br>Yes|
|flight/assignedAltitude/block/abov<br>e<br>flight/assignedAltitude/block/abov<br>e/@uom|assigne<br>dAlt_08<br>d|The bottom level of the<br>assigned block of altitudes<br>for the flight to fly at.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_, _vfr_, _vfrPlus_maybe|ff:AltitudeType<br>uom:<br>ff:AltitudeMeas<br>ureType|Yes<br>**"xs:double"**<br>uom:<br>“**FEET|METERS**”|_above:_<br>**8000**<br>@uom =**FEET**|No<br>uom:<br>Yes|

245

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|||included in the message.<br>The attribute_uom_specifies<br>the unit of measure for the<br>_assignedAltitude/block/above_<br>element.|||||
|flight/assignedAltitude/block/belo<br>w<br>flight/assignedAltitude/block/belo<br>w/@uom|assigne<br>dAlt_08<br>d|The top level of the assigned<br>block of altitudes for the<br>flight to fly at.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.<br>The attribute_uom_specifies<br>the unit of measure for the<br>_assignedAltitude/block/below_<br>element.|ff:AltitudeType<br>uom:<br>ff:AltitudeMeas<br>ureType|Yes<br>**"xs:double"**<br>uom:<br>**“FEET|METRES”**|_below:_<br>**14000**<br>@uom =**FEET**|No<br>uom:<br>Yes|
|flight/assignedAltitude/above<br>flight/assignedAltitude/above/@u<br>om|assigne<br>dAlt_08<br>e|Element used for IFR flights<br>operating above a specified<br>altitude.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.<br>The attribute_uom_specifies<br>the unit of measure for the<br>_assignedAltitude/above_<br>element.|nas:AboveAltitu<br>deType<br>uom:<br>ff:AltitudeMeas<br>ureType|Yes<br>**"xs:double"**<br>uom:<br>**“FEET|METRES”**|Aircraft is flying<br>above 60,000<br>feet:<br>**60000**<br>@uom =**FEET**|No<br>uom:<br>Yes|
|flight/assignedAltitude/altFixAlt/p<br>oint|assigne<br>dAlt_08<br>f|The element<br>_assignedAltitude/altFixAlt_is<br>defined as an altitude prior<br>to a specified fix, the<br>specified fix itself, and<br>altitude post specified fix.<br>The element_altFixAlt/point_|fb:SignificantPoi<br>ntType (abstract<br>type)<br>_fb:FixPointType/_<br>_ff:GeographicalL_<br>_ocationType/_<br>_fb:RelativePoint_|Yes<br>-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**(latitude followed by<br>longitude)<br>-_fb:RelativePointType_<br>- fix:|**MDG**|No|

246

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|||defines the specified fix<br>associated with the altitude.<br>The fix cannot be the<br>departure or arrival point.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|_Type_|**“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive =360|||
|flight/assignedAltitude/altFixAlt/p<br>re<br>flight/assignedAltitude/altFixAlt/p<br>re/@uom|assigne<br>dAlt_08<br>f|The element<br>_assignedAltitude/altFixAlt_is<br>defined as an altitude prior<br>to a specified fix, the<br>specified fix itself, and<br>altitude post specified fix.<br>The element_altFixAlt/pre_<br>defines the altitude before<br>the specified fix.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.<br>The attribute_uom_specifies<br>the unit of measure for the<br>_assignedAltitude/above_<br>element.|ff:AltitudeType<br>uom:<br>ff:AltitudeMeas<br>ureType|Yes<br>**"xs:double"**<br>uom:<br>**“FEET|METRES”**|**240000**<br>@uom =**FEET**|No.<br>uom:<br>Yes|
|flight/assignedAltitude/altFixAlt/p<br>ost<br>flight/assignedAltitude/altFixAlt/p<br>ost/@uom|assigne<br>dAlt_08<br>f|The element<br>_assignedAltitude/altFixAlt_is<br>defined as an altitude prior<br>to a specified fix, the<br>specified fix itself, and<br>altitudepost specified fix.|ff:AltitudeType<br>uom:<br>ff:AltitudeMeas<br>ureType|Yes<br>**"xs:double"**<br>uom:<br>**“FEET|METRES”**|**22000**<br>@uom =**FEET**|No.<br>uom:<br>Yes|

247

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|||The element_altFixAlt/pre_<br>defines the altitude after the<br>specified fix.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.<br>The attribute_uom_specifies<br>the unit of measure for the<br>_altFixAlt/post_element.|||||
|flight/assignedAltitude/vfr|assigne<br>dAlt_08<br>g|The presence of this element<br>in the message specifies that<br>the flight is flying Visual<br>Flight Rules (VFR).<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|nas:VfrAltitudeT<br>ype|Yes<br>**Empty element**||No|
|flight/assignedAltitude/vfrPlus<br>flight/assignedAltitude/vfrPlus/@<br>uom|assigne<br>dAlt_08<br>h|It is used to specify that the<br>flight is flying VFR at a<br>specified altitude.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.<br>The attribute_uom_specifies<br>the unit of measure for the<br>_assignedAltitude_/vfrPlus<br>element.|nas:VfrPlusAltitu<br>deType<br>uom:<br>ff:AltitudeMeas<br>ureType|Yes<br>**"xs:double"**<br>uom:<br>**“FEET|METRES”**|The aircraft is<br>flying VFR at<br>7,500 feet:<br>**7500**<br>@uom =**FEET**|No<br>uom:<br>Yes|
|flight/enRoute/position/altitude<br>flight/enRoute/position/altitude/<br>@uom|reporte<br>dAlt_54<br>a|The element is used to<br>specify the reported altitude.<br>For aircraft with operative<br>Mode C capability, this|ff:AltitudeType<br>uom:<br>ff:AltitudeMeas<br>ureType|Yes<br>**xs:double**<br>uom:<br>**“FEET|METRES”**|**31000**<br>@uom =**FEET**<br>The aircraft|No<br>uom:<br>Yes|

248

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[NU_FIXM]**|**Name**<br>**[NU]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|||element contains the Mode C<br>altitude. For aircraft without<br>Mode C capability or with<br>non-operative Mode C<br>capability, this element may<br>contain the controller<br>reported altitude.<br>The attribute_uom_specifies<br>the unit of measure for the<br>_altitude_element.|||reported altitude<br>is 31,000 feet.||
|flight/interimAltitude<br>flight/interimAltitude/@uom|interim<br>Alt_76b|<br>This element specifies the<br>interim altitude the flight is<br>cleared to maintain different<br>from that in the flight plan.<br>The attribute_uom_specifies<br>the unit of measure for the<br>_interimAltitude_element:<br>FEET/METRES.|nas:SimpleAltitu<br>deType<br>uom:<br>ff:AltitudeMeas<br>ureType|Yes<br>xs:double<br>uom:<br>**“FEET|METRES”**|**240000**<br>@uom =**FEET**|No|

249

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.50 Batch Track Information [BATCH_TH] – Data Elements**

|**Element Name**<br>**[BATCH_TH]**|**Element Definition**|**Type**|**Com**<br>**plex**<br>**?**|**Format/Permissible Values**|**Example**|**Requir**<br>**ed?**|
|---|---|---|---|---|---|---|
|numberOfMsgs|This element specifies the number<br>of individual Track Information<br>messages (TH) contained in the<br>message.|int|No||**7**|Yes|
|singleTH/THmetadata/<br>propFlightId|This element specifies the flight<br>identification (aircraft id, call sign) of<br>the flight to which the message<br>pertains.It represents a property of<br>the individual TH message within<br>the BATCH_TH message.|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|No|
|singleTH/THmetadata/<br>propFlightOperator|This element specifies the Aircraft<br>Operator, if not obvious from the<br>aircraft identification in<br>propFlightId. It represents a<br>property of the individual TH<br>message within the BATCH_TH<br>message.|string|No|Free-form string of up to 3000<br>characters.|**UAL**|No|
|singleTH/THmetadata/<br>propOrigin|This element specifies the origin of<br>the flight to which the message<br>pertains. It represents a property of<br>the individual TH message within<br>the BATCH_TH message.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a<br>fix can be used for this element (fix<br>name, lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|singleTH/THmetadata/<br>propDestination|This element specifies the<br>destination of the flight to which the<br>message pertains.  It represents a<br>property of the individual TH<br>message within the BATCH_TH<br>message.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a<br>fix can be used for this element (fix<br>name, lat/long, or fix-radial-distance),<br>includingthe standard airport|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|

250

NAS-JMSDD-4309-001 Rev C July 10, 2018

|singleTH/THmetadata/<br>propRcvdTime|This element specifies the time at<br>which the message was received by<br>SFDPS, in XML dateTime format. It<br>represents a property of the<br>individual TH message within the<br>BATCH_TH message.|xs:dateTime|No|designators.|**2016-01-06T17:59:57.630Z**|Yes|
|---|---|---|---|---|---|---|
|singleTH/THmetadata/<br>propRcvdTimeEpoch|This element specifies the time at<br>which the message was received by<br>SFDPS, in the form of number of<br>seconds since January 1, 1970. It<br>represents a property of the<br>individual TH message within the<br>BATCH_TH message.|xs:double|No||**1452103197.630377**|Yes|
|singleTH/THmetadata/<br>propSentTime|This element specifies the time at<br>which the message was sent from<br>SFDPS to NEMS, in XML dateTime<br>format.  It represents a property of<br>the individual TH message within<br>the BATCH_TH message.|xs:dateTime|No||**2016-01-06T18:00:00.789Z**|Yes|
|singleTH/THmetadata/<br>propSentTimeEpoch|This element specifies the time at<br>which the message was sent from<br>SFDPS to NEMS, in the form of<br>number of seconds since January 1,<br>1970.  It represents a property of<br>the individual TH message within<br>the BATCH_TH message.|xs:double|No||**1452103200.789000**|Yes|
|singleTH/THmetadata/<br>propSeqNo|This element specifies the messages<br>sequence number. It represents a<br>property of the individual TH<br>message within the BATCH_TH<br>message.  It represents a property<br>of the individual TH message within<br>the BATCH_TH message.|string|No|xs:nonNegativeInteger<br>xs:maxInclusive value="999999999"||No|
|singleTH/THmetadata/<br>propTestMsg|This element represents a property<br>of the individual TH message within<br>the BATCH_TH message.|boolean|No||**false**|No|
|singleTH/THmetadata/|This element allows Track (TH)|boolean|No||**true**|No|

251

NAS-JMSDD-4309-001 Rev C July 10, 2018

|propOneMinFreq|messages to be distributed to a<br>client at one-minute intervals,<br>rather than at their actual<br>frequency, which is twelve seconds.<br>This property should be set on every<br>fifth TH message.||||||
|---|---|---|---|---|---|---|
|singleTH/THmetadata/<br>msgTimes/arrivalTime|This element specifies the arrival<br>time of the flight, in XML dateTime<br>format.  It represents a property of<br>the individual TH message within<br>the BATCH_TH message.|dateTime|No||**2015-12-30T19:21:00Z**|No|
|singleTH/THmetadata/<br>msgTimes/arrivalTimeE<br>poch|This element specifies the arrival<br>time of the flight, in the form of<br>number of seconds since January 1,<br>1970.  It represents a property of<br>the individual TH message within<br>the BATCH_TH message.|long|No||**1451503260000**|No|
|singleTH/THmetadata/<br>msgTimes/departureTi<br>me|This element specifies the departure<br>time of the flight, in XML dateTime<br>format.  It represents a property of<br>the individual TH message within<br>the BATCH_TH message.|dateTime|No||**2015-12-30T17:31:00Z**|No|
|singleTH/THmetadata/<br>msgTimes/departureTi<br>meEpoch|This element specifies the departure<br>time of the flight, in the form of<br>number of seconds since January 1,<br>1970.  It represents a property of<br>the individual TH message within<br>the BATCH_TH message.|long|No||**1451496660000**|No|
|singleTH/THmetadata/<br>flightState|This element contains the current<br>status of the flight as specified by<br>SFDPS.|string|No|**“Proposed|Active|Landed|Cancelled|D**<br>**ropped”**|**“Proposed”**|No|
|singleTH/THmetadata/<br>flightStateActiveOrPro<br>posed|This element specifies whether the<br>current status of the flight as<br>specified by SFDPS is active or<br>proposed.|boolean|No|**“true|false”**<br>**Default: “true”**|**“true”**|No|
|singleTH/THmetadata/<br>fdpsGufi|The SFDPS GUFI is an identifier on<br>every message that positively<br>identifies what flight the message is<br>for.  It represents apropertyof the|string|No||**us.fdps.2016-01-**<br>**06T16:47:54Z.000/20/400**|No|

252

NAS-JMSDD-4309-001 Rev C July 10, 2018

||individual TH message within the<br>BATCH_TH message.||||||
|---|---|---|---|---|---|---|
|singleTH/THmetadata/<br>eramGufi_316aFPId|Contains the eramGufi flight plan<br>identifier from the SFDPS system,<br>the unique flight plan identifier.  It<br>represents a property of the<br>individual TH message within the<br>BATCH_TH message.|T_eramGufi|No|**"[A-Z]{2}\d{5}[1-7]\d{2}"**|**KU60474400**|No|
|singleTH/THmetadata/<br>eramGufi_316aDT|Contains the date and time<br>representation of the eramGufi<br>flight plan.  It represents a property<br>of the individual TH message within<br>the BATCH_TH message.|T_eramGufiDT|No|**"\d{4}-\d{2}-**<br>**\d{2}T\d{2}:\d{2}:\d{2}Z/[A-Za-z0-9/]+"**|**2016-01-**<br>**06T16:47:54Z/000/20/400**|No|
|singleTH/THmetadata/<br>uuidGufi|This element specifies a unique<br>identifier for a flight that conforms<br>to the Universal Unique Identifier<br>standard and conforms to the GUFI<br>requirements of FIXM 3.0.  It<br>represents a property of the<br>individual TH message within the<br>BATCH_TH message.|string|No||**18561ed7-74ed-4748-bae9-**<br>**9e74b406c730**|No|
|singleTH/THmetadata/<br>flightPlanSeqNo|Contains the sequence number for<br>each flight plan.  It represents a<br>property of the individual TH<br>message within the BATCH_TH<br>message.|integer|No||**4**|No|
|singleTH/TH/sourceId_<br>00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where the first<br>6 digits are the UTC time<br>(23:59:35 UTC) and the last 4<br>digits are sequence number<br>of the message (9001).|Yes|
|singleTH/TH/sourceTi<br>me_00e1|This element specifies the time<br>component of the previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents 23:59:35<br>UTC|Yes|

253

NAS-JMSDD-4309-001 Rev C July 10, 2018

|singleTH/TH/sourceSeq<br>No_00e2|This element specifies the message<br>sequence number component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|---|---|---|---|---|---|---|
|singleTH/TH/flightId_0<br>2a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|singleTH/TH/computer<br>Id_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**, as<br>specified by the pattern above.|**020**|Yes|
|singleTH/TH/sspId_167<br>a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|
|singleTH/TH/groundSp<br>eed_05b|This element contains the aircraft<br>ground speed in knots.|string|No|**"\d{3}"**<br>The format is three digits.<br>If the aircraft ground speed is not<br>available, this element contains three<br>zeroes.|**357**<br>Aircraft ground speed is 357<br>knots.<br>**000**<br>Indicates that the aircraft<br>ground speed is missing.|Yes|
|singleTH/TH/assignedA<br>lt_08a|Assigned altitude or flight level<br>expressed in hundreds of feet.<br>Only one of the altitude elements<br>assignedAlt_08a, assignedAlt_08b,<br>assignedAlt_08c, assignedAlt_08d,<br>assignedAlt_08e, assignedAlt_08f,<br>assignedAlt_08g, assignedAlt_08h<br>may be included in the message.|string|No|**“(\d{2,3}) | VFR”**<br>The format consists of either two to<br>three digits, or the constant string**VFR**.<br>Three digits are required for ARTS III,<br>thus a leading zero needs to be used<br>when necessary.|Assigned altitude of 34,000<br>feet:<br>**340**<br>Assigned altitude 9,000 feet<br>ARTS III:<br>**090**|No|
|singleTH/TH/assignedA<br>lt_08b|Fixed value of**OTP**which indicates<br>VFR-ON-Top. It specifies that the<br>aircraft is flying above the clouds in<br>VFR conditions.<br>It may only be specified if none of<br>the other assignedAtl_08 elements<br>is included in the message.|string|No|**“OTP”**|Fixed value of**OTP.**|No|

254

NAS-JMSDD-4309-001 Rev C July 10, 2018

|singleTH/TH/assignedA<br>lt_08c|VFR-ON-Top with altitude. It<br>represents an IFR flight operating<br>above the clouds in VFR conditions<br>at the specified assigned altitude.<br>It may only be specified if none of<br>the other assignedAtl_08 elements<br>is included in the message.|string|No<br>“**OTP/\d{2,3}**”<br>The format is the constant string**OTP**/<br>followed by two to three digits that<br>represent the assigned altitude in<br>hundreds of feet.|Aircraft flying VFR-ON-Top<br>at 25,000 feet:<br>**OTP/250**|No|
|---|---|---|---|---|---|
|singleTH/TH/assignedA<br>lt_08d|The assigned block of altitudes for<br>the flight to fly at.<br>It may only be specified if none of<br>the other assignedAtl_08 elements<br>is included in the message.|string|No<br>**"\d{2,3}B\d{2,3}"**<br>The format is two to three digits,<br>followed by the letter**B**, followed by<br>two to three digits. The leading and<br>trailing two to three digits define the<br>block of altitudes in hundreds of feet for<br>the flight to fly at. The lowest altitude<br>must be listed first.|Assigned altitude block of<br>8,000 feet to 14,000 feet:<br>**80B140**|No|
|singleTH/TH/assignedA<br>lt_08e|Element used for IFR flights<br>operating above a specified<br>altitude.<br>It may only be specified if none of<br>the other assignedAtl_08 elements<br>is included in the message.|string|No<br>**“ABV/\d{2,3}"**<br>The format consists of the string**ABV/**<br>followed by two to three digits that<br>represent the altitude in hundreds of<br>feet above which the flight is flying.|Aircraft is flying above<br>60,000 feet.<br>**ABV/600**|No|
|singleTH/TH/assignedA<br>lt_08f|Assigned Altitude/FIX/Altitude<br>element specifies the altitudes to<br>and from a fix for the flight to fly at.<br>It may only be specified if none of<br>the other assignedAtl_08 elements<br>is included in the message.|<br>string|No<br>**"(\d{2,3}/[A-Z0-9]{2,5}/\d{2,3})|**<br>**(\d{2,3}/[A-Z0-9]{2,5}\d{6}/\d{2,3}) |**<br>**(\d{2,3}/\d{4}[A-Z]?/\d{4,5}[A-**<br>**Z]?/\d{2,3})"**<br>The altitudes are specified in hundreds<br>of feet in a two to three digit format.<br>The fix is specified using the same<br>format as the coordination fix element<br>“coordFix_06a”.<br>The fix cannot be the departure or<br>arrival point.|**240/DAL350010/220**<br>Flight flies at altitude 24,000<br>feet to the fix radial distance<br>fix and then descend to<br>altitude 22,000 feet.|No|
|singleTH/TH/assignedA<br>lt_08g|It is used to specify that the flight is<br>flying Visual Flight Rules (VFR). It<br>can only have the value**VFR**.<br>It may only be specified if none of<br>the other assignedAtl_08 elements<br>is included in the message.|string|No<br>**“VFR”**|The string**VFR.**|No|

255

NAS-JMSDD-4309-001 Rev C July 10, 2018

|singleTH/TH/assignedA<br>lt_08h|It is used to specify that the flight is<br>flying VFR at a specified altitude.<br>It may only be specified if none of<br>the other assignedAtl_08 elements<br>is included in the message.|string|No|**“VFR/\d{2,3}"**<br>The format consists of the string**VFR/**<br>followed by two to three digits that<br>represent an altitude in hundreds of<br>feet.|**VFR/75**<br>The aircraft is flying VFR at<br>7,500 feet.|No|
|---|---|---|---|---|---|---|
|singleTH/TH/reportedA<br>lt_54a|The element is used to specify the<br>reported altitude. For aircraft with<br>operative Mode C capability, this<br>element contains the Mode C<br>altitude. For aircraft without Mode<br>C capability or with non-operative<br>Mode C capability, this element may<br>contain the controller reported<br>altitude. If there is no Mode C or<br>controller reported altitude, or the<br>reported altitude is negative, this<br>element contains “0” or "000" or is<br>optional.|string|No|**"\d{1,3}"**<br>The format consists of one to three<br>digits that represent the reported<br>aircraft altitude in hundreds of feet.<br>Leading zeros may be inserted for<br>altitudes of less than 3 digits.|**310**<br>The aircraft reported<br>altitude is 31,000 feet.|No<br>It may<br>be<br>absent<br>only if<br>eleme<br>nt<br>_report_<br>_edAlt__<br>_54b_<br>=**N**|
|singleTH/TH/reportedA<br>lt_54b|This field is the reported altitude B4<br>indicator. The ERAM controllers’ full<br>data block used for tracking an<br>aircraft has a special indicator for<br>the B4 character of the full data<br>block.|string|No|**“[ABCFNTVX^v+-/]”**<br>The format of this element is one<br>character as follows:<br>A - Reported altitude (controller<br>entered) equals single assigned altitude.<br>B - Beacon reported altitude is in<br>conformance or controller entered<br>reported altitude is in the block for an<br>aircraft which has been assigned an<br>altitude block (B1 to B3 - low altitude<br>limit of block and C1 to C3=high altitude<br>limit of block).<br>C - Beacon reported altitude is within<br>Altitude Conformance Limits feet.<br>F - Reported altitude (controller entered)<br>equals first altitude or (beacon reported)<br>is within Altitude Conformance Limits of<br>first altitude when assigned altitude is<br>(d)dd/fix/(d)dd and the first altitude is<br>displayed in Field B.<br>N - No beacon reported altitude has|**B**|Yes|

256

NAS-JMSDD-4309-001 Rev C July 10, 2018

||||been received for the aircraft; no<br>controller entered reported altitude<br>exists for the aircraft; or the aircraft’s<br>rate of change is questionable and<br>Computed Rate of Change is being used<br>to make further conformance checks.<br>T - Interim altitude is currently being<br>displayed in the assigned altitude field<br>(B1 through B3).<br>V - Beacon reported or controller<br>entered reported altitude, when no<br>assigned altitude exists for the aircraft.<br>X - Beacon reported altitude becomes<br>disestablished. (C1-C3 also contains `X'<br>character.)<br>^ - Beacon reported or controller<br>entered reported altitude is below<br>assigned altitude when flight is climbing<br>v - Beacon reported or controller<br>entered reported altitude is above<br>assigned altitude when flight is<br>descending<br>+ - Beacon reported altitude exceeds<br>upper conformance limit for an aircraft<br>which has reached it assigned altitude or<br>the controller entered reported altitude<br>exceeds the assigned altitude for a non-<br>Mode C aircraft which has previously<br>been reported at the assigned altitude.<br>- - Beacon reported altitude is less than<br>lower conformance limit for an aircraft<br>which has reached its assigned altitude<br>or the controller entered reported<br>altitude is less than the assigned altitude<br>for a non-Mode C aircraft which has<br>previously been reported at the assigned<br>altitude.<br>/ - Flight type is `OTP' or `VFR’|
|---|---|---|---|
|singleTH/TH/reportedA<br>lt_54c|The element specifies the reported<br>altitude C4 indicator.|string|No<br>**“[#X]”**<br>**#**<br>No|

257

NAS-JMSDD-4309-001 Rev C July 10, 2018

||The ERAM controllers full data block<br>used for tracking an aircraft has a<br>special indicator for the C4<br>character of the full data block as<br>follows: If the aircraft is not<br>responding with the Mode C<br>altitude, the controller entered<br>reported altitude is displayed in<br>_reportedAlt_54c_with a pound sign<br>(#) or X in position C4 whenever (1)<br>the controller entered reported<br>altitude does not equal the assigned<br>altitude or is not within the assigned<br>altitude block, (2) no assigned<br>altitude has been entered, or (3) the<br>assigned altitude is VFR, VFR/(d)dd,<br>OTP, or OTP/(d)dd. In either case for<br>a Mode C reported altitude or a<br>controller reported altitude, when<br>an interim altitude is displayed in<br>_reportedAlt_54b_<br>the B4 character position contains<br>the letter “T” and the reported<br>altitude, or either the lower or<br>upper altitude of an assigned block<br>altitude is displayed in<br>_reportedAlt_54c_. In the case where<br>a controller entered reported<br>altitude exists, a pound sign (#) or X<br>is displayed in the C4 position.||||
|---|---|---|---|---|
|singleTH/TH/controllin<br>gFacility_138a|This element specifies the facility<br>that is controlling the flight.|string|No<br>**“LLL”**<br>The format consists of three letters.<br>The value is 3 blank characters if<br>identification of the controlling facility is<br>not available.|ZCH<br>No|
|singleTH/TH/controllin<br>gSector_138b|This element specifies the<br>controlling ARTS position or the<br>controlling ERAM ARTCC sector<br>number. The Controlling Sector is<br>the sector/position that is<br>controllingthe flight. The value is 00|string|No<br>**“\d[A-Z0-9]”**<br>The format is one digit followed by one<br>alphanumeric.|1W<br>No|

258

NAS-JMSDD-4309-001 Rev C July 10, 2018

||if identification of the controlling<br>sector is not available.||||||
|---|---|---|---|---|---|---|
|singleTH/TH/receivingF<br>acility_139a|This element specifies the facility<br>that is receiving the flight.|string|No|**“[A-Z]{3}”**<br>The format is three letters.|AIA|No|
|singleTH/TH/receivingS<br>ector_139b|This element specifies the receiving<br>ARTS position or the receiving ERAM<br>ARTCC sector number. The receiving<br>sector is the sector/position that is<br>receiving the flight. The value is 00 if<br>identification of the receiving sector<br>is not available.|string|No|**“[0-9][A-Z0-9]”**<br>The format is one digit followed by one<br>alphanumeric.|1W|No|
|singleTH/TH/trackPosit<br>ion_23d|This element specifies the track<br>position form ERAM to ATM-IPOP.|string|No|**"\d{6}[A-Z]/\d{7}[A-Z]"**<br>It is a latitude/longitude pair, separated<br>by a virgule. For latitude, the first two<br>digits are degrees, the second two are<br>minutes, and the last two are seconds.<br>The letter can be N or S. For the<br>longitude, the first three digits are<br>degrees, the second two are minutes,<br>and the last two are seconds. The letter<br>can be E or W.|393106N/0842535W|Yes|
|singleTH/TH/trackVelo<br>city_23e|This element specifies the velocity in<br>nautical miles per hour.|string|No|**"[+\-]\d\d{0,3}/[+\-SH]\d\d{0,3}"**<br>Minimum length = 5<br>Maximum length = 11<br>It has an X and a Y component separated<br>by a virgule. Either component can be<br>preceded by either a + or – sign,<br>followed by one to three digits. The<br>second component can be preceded by<br>an S or an H, for speed only (NM/hr), or<br>heading only (degrees), respectively.|+46/-355<br>-0/S439|Yes|
|singleTH/TH/coastIndic<br>ator_153a|This element specifies an action<br>indicator. It has only one possible<br>value, C for Coast.|string|No|**“C”**|**C**|No|
|singleTH/TH/timeOfTra<br>ckData_170a|This element specifies the date and<br>time the track data was stored.|dateTime|No|**dateTime**|**2014-06-20T20:17:52**|No|
|singleTH/TH/targetPosi|This element specifies the ERAM|string|No|**"\d{6}[A-Z]/\d{7}[A-Z]"**|393106N/0842535W|No|

259

NAS-JMSDD-4309-001 Rev C July 10, 2018

|singleTH/TH/tion_171a|radar target position, in<br>latitude/longitude format, as<br>described in message number.|||Length = 16<br>It is a latitude/longitude pair, separated<br>by a virgule.|||
|---|---|---|---|---|---|---|
|singleTH/TH/targetAlt_<br>172a|This element specifies the Mode C<br>Target altitude (corrected for<br>barometric pressure) in hundreds of<br>feet.|string|No|**"\d{3}“**<br>The format is three digits, with leading<br>zeroes required. If the target altitude is<br>negative, targetAlt_172a is**000**.|**290**<br>**000**|No|
|singleTH/TH/targetAltI<br>nvalid_172b|If the element_targetAlt_172a_is not<br>valid, this field is set to**INV**, for<br>invalid Mode C altitude.|string|No|**“INV”**|**INV**|No|
|singleTH/TH/timeOfTar<br>getData_173a|This element specifies the date and<br>time of the correlated target.|dateTime|No|**dateTime**|**2014-06-20T20:17:50**|No|

260

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.51 Batch Track Information [BATCH_TH] - Diagram**

261

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.52 Batch Track Information Message in FIXM Format [BATCH_TH_FIXM] – Data Elements**

The following elements of the BATCH_TH message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

- reportedAlt_54b

- reportedAlt_54c

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@name<br>flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@value|FDPS_Seque<br>nceNo|Sequence number assigned by SFDPS<br>to each message it receives from<br>HADDS. The attribute_name_includes<br>the constant string"MSG_SEQ_NO",<br>and the attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|@name="MSG_S<br>EQ_NO"<br>@value="686041<br>6"|Yes|
|flight/departure/@departu<br>rePoint|FDPS_Origin/<br>departurePoi<br>nt_26a|Attribute used to specify the first<br>point or other initial entity where<br>the air traffic control/management<br>system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arrivalPoint|FDPS_DestId<br>/destination<br>_27a|The final point or other final entity<br>where the air traffic<br>control/management system route<br>terminates.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**|No|

262

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
||||||Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**3500N/04000W**||
|flight/operator/operatingO<br>rganization/organization/<br>@name|FDPS_Flight<br>Operator/OP<br>RIndicator_9<br>18f|Attribute used to specify the full<br>official name of the State,<br>Organization, Authority, aircraft<br>operating agency, handling agency<br>engaged in or offering to engage in<br>aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/flightIdentification/<br>@aircraftIdentification|flightId_02a|Name used by Air Traffic Services<br>units to identify and communicate<br>with an aircraft.|fb:FlightIdentifierT<br>ype|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/@system|propSourceS<br>ystem|This attribute indicates which SFDPS<br>system generated the message.|fb:ProvenanceSyst<br>emType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTim<br>e|This attribute conatins the time at<br>which the message was received by<br>SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028<br>Z|Yes|
|flight/@centre|center|This attribute specifies the code of<br>the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCen<br>treType|No|xs:string|ZAU|Yes|
|flight/arrival/runwayPositi<br>onAndTime/runwayTime/[<br>estimated|actual]/@time|arrivalTime|This attribute specifies the proposed<br>or the actual time of arrival at<br>destination, set according to the<br>flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/departure/runwayPo<br>sitionAndTime/runwayTim<br>e/[actual|estimated]/@tim<br>e|departureTi<br>me|This element specifies the proposed<br>or actual departure time, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|

263

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
|flight/flightStatus/@fdpsFli<br>ghtStatus|flightState|This attribute contains the current<br>status of the flight as specified by<br>SFDPS.|nas:SfdpsFlightSta<br>tusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETED<br>|CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@name<br>flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@value|fdpsGufi|The name value pair specifies the<br>SFDPS GUFI, an identifier on every<br>message that positively identifies<br>what flight the message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-z0-<br>9/]+"|name="FDPS_GU<br>FI"<br>value="us.fdps.2<br>015-12-<br>18T16:59:10Z.00<br>0/14/100"/>|Yes|
|flight/flightPlan/@identifie<br>r|eramGufi_31<br>6a|This attribute specifies the unique<br>flight plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@name<br>flight/supplementalData/a<br>dditionalFlightInformation/<br>nameValue/@value||The flight supplemental data is used<br>to indicate that a flight message is a<br>test message, by setting the attribute<br>_name_to “**SIMULATED_FLIGHT**” and<br>the attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLI**<br>**GHT”**<br>@value =**“true”**|No|
|flight/departure/@departu<br>rePoint|FDPS_Origin/<br>departurePoi<br>nt_26a|Attribute used to specify the first<br>point or other initial entity where<br>the air traffic control/management<br>system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|

264

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
|flight/arrival/@arrivalPoint|FDPS_DestId<br>/destination<br>_27a|The final point or other final entity<br>where the air traffic<br>control/management system route<br>terminates.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/operator/operatingO<br>rganization/organization/<br>@name|FDPS_Flight<br>Operator/OP<br>RIndicator_9<br>18f|Attribute used to specify the full<br>official name of the State,<br>Organization, Authority, aircraft<br>operating agency, handling agency<br>engaged in or offering to engage in<br>aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/flightIdentification/<br>@aircraftIdentification|FDPS_FlightI<br>d/flightId_02<br>a|Name used by Air Traffic Services<br>units to identify and communicate<br>with an aircraft.|fb:FlightIdentifierT<br>ype|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/flightIdentification/<br>@computerId|computerId_<br>02d|A unique identification assigned by<br>ERAM to each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/<br>@siteSpecificPlanId|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by Instrument Flight<br>Procedures Automation (IFPA) to<br>uniquely identify a flight plan in each<br>ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/enRoute/position/ac<br>tualSpeed/surveillance|groundSpeed<br>_05b|This element contains the measured<br>horizontal speed of the aircraft<br>relative to a fixed point on the<br>ground for flights being tracked by|ff:GroundSpeedTy<br>pe|Yes|**xs:double**<br>The Groundspeed type represents<br>any ground speed measurement,<br>in metric or imperial, as specified|**357**<br>uom=KNOTS<br>Aircraft ground<br>speed is 357|Yes|

265

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
|||surveillance or satellite.|||by the "_uom_" attribute.|knots.||
|flight/enRoute/position/ac<br>tualSpeed/surveillance/@u<br>om|groundSpeed<br>_05b|Attribute of groundspeed indicating<br>units of ground speed<br>measurement.|ff:GroundSpeedM<br>easureType|No|**“KILOMETRES_PER_HOUR|KNOTS**<br>**”**|**KNOTS**|Yes|
|flight/enRoute/position/@<br>reportSource|groundSpeed<br>_05b|The source of the current position<br>report information.|fb:ProvenanceSour<br>ceType|No|**“SURVEILLANCE”**|**SURVEILLANCE**|No|
|flight/assignedAltitude/sim<br>ple<br>flight/assignedAltitude/sim<br>ple/@uom<br>flight/assignedAltitude/sim<br>ple/@ref|assignedAlt_<br>08a|Simple altitude: single measurement<br>above reference point. It represents<br>the only NAS altitude that maps<br>directly to the core ICAO altitude<br>types.<br>Only one of the altitude elements<br>_simple_,_vfrOnTop_,_vfrOnTopPlus_,<br>_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.|assignedAltitude/si<br>mple:<br>nas:SimpleAltitude<br>Type<br>uom:<br>ff:AltitudeMeasure<br>Type<br>ref:<br>ff:AltitudeReferenc<br>eType|Yes|**“xs:double”**<br>_@uom_:<br>“**FEET|METERS**”<br>_@ref_:<br>**“MEAN_SEA_LEVEL|**<br>**FLIGHT_LEVEL”**|Assigned altitude<br>of 34,000 feet:<br>**34000**<br>_Uom_:<br>**FEET**<br>_Ref_:<br>**MEAN_SEA_LEV**<br>**EL**|<br>No|
|flight/assignedAltitude/vfr<br>OnTop|assignedAlt_<br>08b|The presence of this element<br>indicates VFR-ON-Top. It specifies<br>that the aircraft is flying above the<br>clouds in VFR conditions.<br>Only one of the altitude elements<br>_simple_,_vfrOnTop_,_vfrOnTopPlus_,<br>_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.|Nas:VfrOnTopAltit<br>udeType|Yes|Empty element.||No|
|flight/assignedAltitude/vfr<br>OnTopPlus<br>flight/assignedAltitude/vfr<br>OnTopPlus/@uom|assignedAlt_<br>08c|VFR-ON-Top with altitude. It<br>represents an Instrument Flight<br>Rules (IFR) flight operating above<br>the clouds in VFR conditions at the<br>specified assigned altitude.<br>Only one of the altitude elements<br>_simple_, _vfrOnTop_, _vfrOnTopPlus_,|nas:VfrOnTopPlus<br>AltitudeType<br>uom:<br>ff:AltitudeMeasure<br>Type|No|**“xs:double”**<br>uom:<br>**“FEET|METRES”**|Aircraft flying<br>VFR-ON-Top at<br>25,000 feet:<br>**25000**<br>_uom_:**FEET**|No|

266

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
|||_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.||||||
|flight/assignedAltitude/blo<br>ck/above<br>flight/assignedAltitude/blo<br>ck/above/@uom|assignedAlt_<br>08d|The bottom level of the assigned<br>block of altitudes for the flight to fly<br>at.<br>Only one of the altitude elements<br>_simple_,_vfrOnTop_,_vfrOnTopPlus_,<br>_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.|ff:AltitudeType<br>uom:<br>ff:AltitudeMeasure<br>Type|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**|_above:_<br>**8000**<br>_uom:_<br>**FEET**|No|
|flight/assignedAltitude/blo<br>ck/below<br>flight/assignedAltitude/blo<br>ck/below/@uom|assignedAlt_<br>08d|The top level of the assigned block<br>of altitudes for the flight to fly at.<br>Only one of the altitude elements<br>_simple_,_vfrOnTop_,_vfrOnTopPlus_,<br>_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.|ff:AltitudeType<br>uom:<br>ff:AltitudeMeasure<br>Type|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**|_below:_<br>**14000**<br>_uom:_<br>**FEET**|No|
|flight/assignedAltitude/abo<br>ve<br>flight/assignedAltitude/abo<br>ve/@uom|assignedAlt_<br>08e|Element used for IFR flights<br>operating above a specified altitude.<br>Only one of the altitude elements<br>_simple_,_vfrOnTop_,_vfrOnTopPlus_,<br>_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.|nas:AboveAltitude<br>Type<br>uom:<br>ff:AltitudeMeasure<br>Type|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**|Aircraft is flying<br>above 60,000<br>feet:<br>**60000**<br>**uom:**<br>**FEET**|No|
|flight/assignedAltitude/altF<br>ixAlt/point|assignedAlt_<br>08f|_assignedAltitude/altFixAlt_element is<br>defined as an altitude prior to a<br>specified fix, the specified fix itself,<br>and altitude post specified fix. The<br>element_altFixAlt/point_defines the<br>specified fix associated with the<br>altitude.<br>The fix cannot be the departure or<br>arrival point.<br>Only one of the altitude elements<br>_simple_,_vfrOnTop_,_vfrOnTopPlus_,<br>_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.|fb:SignificantPoint<br>Type (abstract<br>type)<br>_fb:FixPointType/_<br>_ff:GeographicalLoc_<br>_ationType/_<br>_fb:RelativePointTy_<br>_pe_|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0|**MDG**|No|

267

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
||||||maxInclusive<br>=360|||
|flight/assignedAltitude/altF<br>ixAlt/pre<br>flight/assignedAltitude/altF<br>ixAlt/pre/@uom|assignedAlt_<br>08f|_assignedAltitude/altFixAlt_element is<br>defined as an altitude prior to a<br>specified fix, the specified fix itself,<br>and altitude post specified fix. The<br>element_altFixAlt/pre_defines the<br>altitude before the specified fix.<br>Only one of the altitude elements<br>_simple_,_vfrOnTop_,_vfrOnTopPlus_,<br>_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.|ff:AltitudeType<br>uom:<br>ff:AltitudeMeasure<br>Type|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**|**24000**<br>**uom:**<br>**FEET**|No.|
|flight/assignedAltitude/altF<br>ixAlt/post<br>flight/assignedAltitude/altF<br>ixAlt/post/@uom|assignedAlt_<br>08f|_assignedAltitude/altFixAlt_element is<br>defined as an altitude prior to a<br>specified fix, the specified fix itself,<br>and altitude post specified fix. The<br>element_altFixAlt/pre_defines the<br>altitude after the specified fix.<br>Only one of the altitude elements<br>_simple_,_vfrOnTop_,_vfrOnTopPlus_,<br>_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.|ff:AltitudeType<br>uom:<br>ff:AltitudeMeasure<br>Type|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**|**22000**<br>**uom:**<br>**FEET**|No.|
|flight/assignedAltitude/vfr|assignedAlt_<br>08g|Its presence in the message specifies<br>that the flight is flying Visual Flight<br>Rules (VFR).<br>Only one of the altitude elements<br>_simple_,_vfrOnTop_,_vfrOnTopPlus_,<br>_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.|nas:VfrAltitudeTyp<br>e|Yes|**Empty element**||No|
|flight/assignedAltitude/vfr<br>Plus<br>flight/assignedAltitude/vfr<br>Plus/@uom|assignedAlt_<br>08h|It is used to specify that the flight is<br>flying VFR at a specified altitude.<br>Only one of the altitude elements<br>_simple_,_vfrOnTop_,_vfrOnTopPlus_,<br>_block_,_above_,_altFixAlt_,_vfr_,_vfrPlus_<br>may be included in the message.|nas:VfrPlusAltitude<br>Type<br>uom:<br>ff:AltitudeMeasure<br>Type|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**|The aircraft is<br>flying VFR at<br>7,500 feet:<br>**7500**<br>uom:<br>**FEET**|No|

268

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
|flight/enRoute/position/alt<br>itude<br>flight/enRoute/position/alt<br>itude/@uom|reportedAlt_<br>54a|The element is used to specify the<br>reported altitude. For aircraft with<br>operative Mode C capability, this<br>element contains the Mode C<br>altitude. For aircraft without Mode C<br>capability or with non-operative<br>Mode C capability, this element may<br>contain the controller reported<br>altitude.|ff:AltitudeType|Yes|**xs:double**<br>**@uom:**<br>**“FEET|METRES”**|**31000**<br>**FEET**<br>The aircraft<br>reported altitude<br>is 31,000 feet.|No|
|flight/controllingUnit/@uni<br>tIdentifier|controllingFa<br>cility_138a|This element specifies the identifier<br>of the Air Traffic Control unit in<br>control of the aircraft.|ff:AtcUnitNameTy<br>pe|No|**“([A-Z]{4})|([A-Za-z0-9]{1, })”**|ZCH|No|
|flight/controllingUnit/@sec<br>torIdentifier|controllingSe<br>ctor_138b|This element specifies the identifier<br>of the Air Traffic Control sector in<br>control of the aircraft.|fb:FreeStringType|No|**“\d[A-Z0-9]”**<br>The format is one digit followed by<br>one alphanumeric.|1W|No|
|flight/enRoute/boundaryCr<br>ossings/handoff/receiving<br>Unit/@unitIdentifier|receivingFaci<br>lity_139a|This element specifies the Air Traffic<br>Control unit receiving control of the<br>aircraft as a result of a handoff.|ff:AtcUnitNameTy<br>pe|No|**“([A-Z]{4})|([A-Za-z0-9]{1, })”**|AIA|No|
|flight/enRoute/boundaryCr<br>ossings/handoff/receiving<br>Unit/@sectorIdentifier|receivingSect<br>or_139b|This element specifies the ATC sector<br>receiving control of the aircraft as a<br>result of a handoff.|fb:FreeStringType|No|**“[0-9][A-Z0-9]”**<br>The format is one digit followed by<br>one alphanumeric.|1W|No|
|flight/enRoute/position/po<br>sition/location/pos|trackPosition<br>_23d|This element specifies the actual<br>location of an active flight as<br>reported by surveillance, for a flight<br>tracked by radar, or from the<br>position part of a pilot progress<br>report, for an oceanic flight or a<br>flight operating in a non-radar<br>airspace.|_ff:GeographicalLoc_<br>_ationType_|Yes|List of two**xs:double**: latitude<br>followed by longitude:<br>**"\d{6}[A-Z] \d{7}[A-Z]"**<br>For latitude, the first two digits are<br>degrees, the second two are<br>minutes, and the last two are<br>seconds. For the longitude, the<br>first three digits are degrees, the<br>second two are minutes, and the<br>last two are seconds.|393106 0842535|Yes|
|flight/enRoute/position/po<br>sition/location/@srsName|trackPosition<br>_23d|This attribute specifies the name of<br>the coordinate reference system|xs:string|No|fixed=**"urn:ogc:def:crs:EPSG::4326**<br>**"**|urn:ogc:def:crs:E<br>PSG::4326|Yes|

269

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
|||(CRS) that defines the semantics of<br>the lat/long pair<br>_flight/enRoute/position/position/@p_<br>_os_according to the ISO6709<br>standard. FIXM uses only<br>"urn:ogc:def:crs:EPSG::4326".||||||
|flight/enRoute/position/tra<br>ckVelocity/x|trackVelocity<br>_23e|This element specifies the velocity of<br>the aircraft along the X axis.<br>NOTE<br>Certain values for x/y velocity can<br>indicate this is only a (directionless)<br>speed or only a heading.|ff:AirspeedInIasOr<br>MachType|Yes|xs:double|46<br>uom=”KNOTS”|Yes|
|flight/enRoute/position/tra<br>ckVelocity/x/@uom|trackVelocity<br>_23e|Attribute of the element<br>_trackVelocity/x_indicating<br>measurement in metric, imperial, or<br>Mach units.|ff:AirspeedMeasur<br>eType|No|**“KILOMETRES_PER_HOUR|KNOTS**<br>**|MACH”**|KNOTS|Yes|
|flight/enRoute/position/tra<br>ckVelocity/y|trackVelocity<br>_23e|This element specifies the velocity of<br>the aircraft along the Y-axis.<br>NOTE<br>Certain values for x/y velocity can<br>indicate this is only a (directionless)<br>speed or only a heading.|ff:AirspeedInIasOr<br>MachType|Yes|**xs:double**<br>It can be preceded by the<br>character “S” or “H”, for speed<br>only or heading only, respectively.|S439<br>uom=”KNOTS”|Yes|
|flight/enRoute/position/tra<br>ckVelocity/y/@uom|trackVelocity<br>_23e|Attribute of the element<br>_trackVelocity/y_indicating<br>measurement in metric, imperial, or<br>Mach units.|ff:AirspeedMeasur<br>eType|No|**“KILOMETRES_PER_HOUR|KNOTS**<br>**|MACH”**|KNOTS|Yes|
|flight/enRoute/position/ac<br>tualSpeed/surveillance|trackVelocity<br>_23e|The measured horizontal speed of<br>the aircraft relative to a fixed point<br>on the ground for flights being<br>tracked by surveillance or satellite.|ff:GroundspeedTy<br>pe|Yes|**xs:double**|500<br>uom=”KNOTS”|No|
|flight/enRoute/position/ac<br>tualSpeed/surveillance/@u<br>om|trackVelocity<br>_23e|Attribute of the element<br>_actualSpeed/surveillance_indicating<br>units ofground speed measurement.|ff:GroundspeedMe<br>asureType|No|**“KILOMETRES_PER_HOUR|KNOTS**<br>**”**|KNOTS|Yes|

270

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
|flight/enRoute/position/tra<br>ck|trackVelocity<br>_23e|The direction the aircraft is flying<br>over the ground relative to the true<br>north. It is the heading of the aircraft<br>as impacted by the wind.|fb:DirectionType|Yes|**xs:double**<br>**minInclusive=0**<br>**maxInclusive=360**|40|Yes|
|flight/enRoute/position/tra<br>ck/@uom|trackVelocity<br>_23e|This element indicates angle units of<br>measure.|ff:AngleMeasureTy<br>pe|No|**“DEGREES”**|**DEGREES**|Yes|
|flight/enRoute/position/@<br>coastIndicator|coastIndicat<br>or_153a|This element contains an indicator<br>the aircraft was unexpectedly not<br>detected by radar (after a period of<br>tracking).|Nas:NasCoastIndic<br>atorType|No|**“COASTING”**|**COASTING**|No|
|flight/enRoute/position/@<br>positionTime|timeOfTrack<br>Data_170a|This element specifies the time<br>associated with the current position<br>of an active flight, from the radar<br>surveillance report or the pilot<br>report.|ff:TimeType|No|xs:dateTime|**2014-06-**<br>**20T20:17:52**|No|
|flight/enRoute/position/tar<br>getPosition/pos|targetPositio<br>n_171a|This element specifies theaircraft<br>target position as a<br>latitude/longitude pair, as reported<br>by one raw radar return.|ff:GeographicLocat<br>ionType|Yes|List of doubles that contain the<br>latitude and longitude of the<br>location, in order of latitude first,<br>then longitude:<br>**"\d{6}[A-Z] \d{7}[A-Z]"**|393106 0842535|No|
|flight/enRoute/position/tar<br>getPosition/@srsName|targetPositio<br>n_171a|This element names the coordinate<br>reference system (CRS) for the<br>element_targetPosition_that defines<br>the semantics of the lat/long pair<br>according to the ISO6709 standard.<br>FIXM uses only<br>"urn:ogc:def:crs:EPSG::4326".|xs:string|No|"urn:ogc:def:crs:EPSG::4326"|urn:ogc:def:crs:E<br>PSG::4326|Yes|
|flight/enRoute/position/tar<br>getAltitude|targetAlt_17<br>2a|This element specifies the Mode C<br>Target altitude corrected for<br>barometricpressure. Suspected|Nas:NasPositionAlt<br>itudeType|Yes|xs:double||No|

271

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BATCH_TH_FIXM]**|**Name**<br>**[BATCH_TH]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required**<br>**?**|
|---|---|---|---|---|---|---|---|
|||invalid altitudes are marked with the<br>_@invalid_attribute.||||||
|flight/enRoute/position/tar<br>getAltitude/@uom|targetAlt_17<br>2a|A required altitude measure unit.|ff:AltitudeMeasure<br>Type|No|**“FEET|METRES”**|**FEET**|Yes|
|flight/enRoute/position/tar<br>getAltitude/@invalid|targetAltInva<br>lid_172b|Indicates whether the value of the<br>element_targetAltitude_is invalid.|Nas:InvalidIndicato<br>rType|No|**“INVALID”**|**INVALID**|No|
|flight/enRoute/position/@<br>targetPositionTime|timeOfTarge<br>tData_173a|This element specifies the time<br>associated with the raw radar return.|ff:TimeType|No|**xs:dateTime**|**2014-06-**<br>**20T20:17:50**|No|

##### **5.5.1.53 Drop Track Information [RH] – Data Elements**

|**Element Name**<br>**[RH]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed by<br>a four-digit sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and the<br>last four digits, represent the message<br>sequence number in the range [0000-9999].|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number<br>of the message<br>(9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:_hh_<br>stands for the 2-digit-hour in the range 00-<br>23,_mm_stands for the 2-digit minutes in the<br>range 00-59, and_ss_stands for the 2-digit<br>seconds in the range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|

272

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[RH]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceSeqNo_00e<br>2|This element specifies the<br>message sequence number<br>component of the sourceId_00e<br>element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|"([0-9][A-HJ-NP-Z0-9]{2})|<br>([0-9]{2}[A-HJ-NP-Z0-9])"<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**, as specified<br>by the pattern above.|**020**|Yes|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each<br>ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|

273

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.54 Drop Track Information [RH] - Diagram**

##### **5.5.1.55 Drop Track Information Message in FIXM Format [RH_FIXM] – Data Elements**

The following elements of the RH message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

|**Name**<br>**[RH_FIXM]**|**Name**<br>**[RH]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/a<br>dditionalFlightInformation<br>/nameValue/@name<br>flight/supplementalData/a<br>dditionalFlightInformation<br>/nameValue/@value|FDPS_Sequenc<br>eNo|Sequence number assigned by SFDPS to<br>each message it receives from HADDS. The<br>attribute_name_includes the constant string<br>"MSG_SEQ_NO", and the attribute_value_<br>contains the sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name=”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|@name="M<br>SG_SEQ_NO<br>"<br>@value="68<br>60416"|Yes|
|flight/departure/@depart<br>urePoint|FDPS_Origin/de<br>parturePoint_2<br>6a|Attribute used to specify the first point or<br>other initial entity where the air traffic<br>control/management system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**|No|

274

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[RH_FIXM]**|**Name**<br>**[RH]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
||||||**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-**<br>**Z]?)”**<br>Any of the standard ways<br>to represent a fix can be<br>used for this element (fix<br>name, lat/long, or fix-<br>radial-distance), including<br>the standard airport<br>designators.|**ATOKA3000**<br>**40**<br>**3500N/0400**<br>**0W**||
|flight/arrival/@arrivalPoint|<br>destination_27<br>a|The final point or other final entity where<br>the air traffic control/management system<br>route terminates.|fb:FreeTextType|No|xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-**<br>**Z]?)”**<br>Any of the standard ways<br>to represent a fix can be<br>used for this element (fix<br>name, lat/long, or fix-<br>radial-distance), including<br>the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA3000**<br>**40**<br>**3500N/0400**<br>**0W**|No|
|flight/operator/operating<br>Organization/organization<br>/@name|FDPS_FlightOp<br>erator/OPRIndi<br>cator_918f|Attribute used to specify the full official<br>name of the State, Organization,<br>Authority, aircraft operating agency,<br>handling agency engaged in or offering to<br>engage in aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/@system|propSourceSyst<br>em|This attribute indicates which SFDPS<br>system generated the message.|fb:ProvenanceSystemType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTime|This attribute conatins the time at which<br>the message was received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02<br>.028Z|Yes|
|flight/@centre|center|This attribute specifies the code of the|fb:ProvenanceCentreType|No|xs:string|ZAU|Yes|

275

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[RH_FIXM]**|**Name**<br>**[RH]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|||ARTCC (or<br>FIR) that produced the data.||||||
|flight/arrival/runwayPositi<br>onAndTime/runwayTime/[<br>estimated|actual]/@time|arrivalTime|This attribute specifies the proposed or the<br>actual time of arrival at destination, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/departure/runwayP<br>ositionAndTime/runwayTi<br>me/[actual|estimated]/@t<br>ime|departureTime|This element specifies the proposed or<br>actual departure time, set according to the<br>flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/flightStatus/@fdpsFl<br>ightStatus|flightState|This attribute contains the current status<br>of the flight as specified by SFDPS.|nas:SfdpsFlightStatusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COM<br>PLETED|CANCELLED|DROP<br>PED”|ACTIVE|Yes|
|flight/supplementalData/a<br>dditionalFlightInformation<br>/nameValue/@name<br>flight/supplementalData/a<br>dditionalFlightInformation<br>/nameValue/@value|fdpsGufi|The name value pair specifies the SFDPS<br>GUFI, an identifier on every message that<br>positively identifies what flight the<br>message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[<br>A-Za-z0-9/]+"|name="FDP<br>S_GUFI"<br>value="us.fd<br>ps.2015-12-<br>18T16:59:10<br>Z.000/14/10<br>0"/>|Yes|
|flight/flightPlan/@identifie<br>r|eramGufi_316a|This attribute specifies the unique flight<br>plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU6837810<br>0"|No|
|flight/gufi|uuidGufi|This element contains a reference that<br>uniquely identifies a flight and that is<br>independent of any particular system. This<br>reference conforms to the Universal<br>Unique Identifier standard.|fb:GloballyFlightIdentifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-<br>F]{4}\-4[0-9a-fA-F]{3}\-<br>[89aAbB][0-9a-fA-F]{3}\-[0-<br>9a-fA-F]{12}"|4aaf92be-<br>ac0a-4dba-<br>998f-<br>9e56f5d450<br>b6|Yes|

276

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[RH_FIXM]**|**Name**<br>**[RH]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|flight/flightIdentification/<br>@aircraftIdentification|flightId_02a|Name used by Air Traffic Services units to<br>identify and communicate with an aircraft.|fb:FlightIdentifierType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/a<br>dditionalFlightInformation<br>/nameValue/@name<br>flight/supplementalData/a<br>dditionalFlightInformation<br>/nameValue/@value||The flight supplemental data is used to<br>indicate that a flight message is a test<br>message, by setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the attribute<br>_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1,**<br>**maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATE**<br>**D_FLIGHT”**<br>@value =<br>**“true”**|No|
|flight/flightIdentification/<br>@computerId|computerId_02<br>d|A unique identification assigned by ERAM<br>to each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a<br>digit, followed by two<br>alphanumeric characters<br>with the exception of the<br>letters**I**and**O**, such as<br>_ddd, ddL, dLd, dLL_.|<br>**020**|No|
|flight/flightIdentification/<br>@siteSpecificPlanId|sspId_167a|Site Specific Plan Identifier. It is assigned<br>by Instrument Flight Procedures<br>Automation (IFPA) to uniquely identify a<br>flight plan in each ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|

##### **5.5.1.56 Interim Altitude Information [LH] – Data Elements**

|**Element Name**<br>**[LH]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source|string|No|**“\d{10}”**|**2359359001**, where|Yes|

277

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[LH]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|||Ten digits, of which the first 6 digits represent<br>the UTC time (_hhmmss_) and the last four digits,<br>represent the message sequence number in<br>the range [0000-9999].|the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number<br>of the message<br>(9001).||
|sourceTime_00e1|This element specifies the time<br>component of the previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:_hh_<br>stands for the 2-digit-hour in the range 00-23,<br>_mm_stands for the 2-digit minutes in the range<br>00-59, and_ss_stands for the 2-digit seconds in<br>the range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e<br>2|This element specifies the message<br>sequence number component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-9999].|**9001**|Yes|
|interimAlt_76a|This element specifies the letter D<br>that is used to delete the interim<br>altitude stored by ATM-IPOP.<br>The message has to include either<br>this element or the element<br>_interimAlt_76b._|string|No|**“D”**|**D**|Yes, if element<br>_interimAlt_76b_<br>is not included<br>in the message|
|interimAlt_76b|This element specifies the interim<br>altitude for the flight in hundreds of<br>feet.<br>The message has to include either<br>this element or the element<br>_interimAlt_76a._|string|No|**"\d{1,3}"**<br>The format is one to three digits, in the range 0<br>to 999.|**240**<br>Aircraft interim<br>altitude of 24,000<br>feet.|Yes, if element<br>_interimAlt_76a_<br>is not included<br>in the message|
|flightId_02a|Aircraft ID, or flight ID (also called Call<br>Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character followed<br>by one to six alphanumeric characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,followed bytwo|**020**|Yes|

278

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[LH]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||alphanumeric characters with the exception of<br>the letters**I**and**O**, as specified by the pattern<br>above.|||
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned byIFPA to uniquely identify<br>a flight plan in each ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|

##### **5.5.1.57 Interim Altitude Information [LH] - Diagram**

##### **5.5.1.58 Interim Altitude Information Message in FIXM Format [LH_FIXM] – Data Elements**

The following elements of the LH message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

279

NAS-JMSDD-4309-001 Rev C July 10, 2018

###### • sourceSeqNo_00e2

|**Name**<br>**[LH_FIXM]**|**Name**<br>**[LH]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Require**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@name<br>flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@value|FDPS_Seq<br>uenceNo|Sequence number assigned by<br>SFDPS to each message it<br>receives from HADDS. The<br>attribute_name_includes the<br>constant string<br>"MSG_SEQ_NO", and the<br>attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive value="999999999"|@name="MSG_SEQ_NO"<br>@value="6860416"|Yes|
|flight/departure/@d<br>eparturePoint|FDPS_Orig<br>in/depart<br>urePoint_<br>26a|Attribute used to specify the<br>first point or other initial<br>entity where the air traffic<br>control/management system<br>route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arriv<br>alPoint|FDPS_Des<br>tId/destin<br>ation_27a|The final point or other final<br>entity where the air traffic<br>control/management system<br>route terminates.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/operator/oper<br>atingOrganization/or<br>ganization/@name|FDPS_Flig<br>htOperato<br>r/OPRIndi|Attribute used to specify the<br>full official name of the State,<br>Organization, Authority,|ff:TextNameTyp<br>e|No|xs:string|UAL|No|

280

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[LH_FIXM]**|**Name**<br>**[LH]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Require**<br>**d?**|
|---|---|---|---|---|---|---|---|
||cator_918<br>f|aircraft operating agency,<br>handling agency engaged in or<br>offering to engage in aircraft<br>operation.||||||
|flight/@system|propSourc<br>eSystem|This attribute indicates which<br>SFDPS system generated the<br>message.|fb:ProvenanceS<br>ystemType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvd<br>Time|This attribute conatins the time<br>at which the message was<br>received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the<br>code of the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceC<br>entreType|No|xs:string|`ZAU`|Yes|
|flight/arrival/runway<br>PositionAndTime/ru<br>nwayTime/estimate<br>d/@time|arrivalTim<br>e|This attribute specifies the<br>proposed or the actual time of<br>arrival at destination, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/departure/run<br>wayPositionAndTim<br>e/runwayTime/actu<br>al/@time|departure<br>Time|This element specifies the<br>proposed or actual departure<br>time, set according to the flight<br>state.|ff:TimeType|No|xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/flightStatus/@<br>fdpsFlightStatus|flightState|This attribute contains the<br>current status of the flight as<br>specified by SFDPS.|nas:SfdpsFlightS<br>tatusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETED|<br>CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@name<br>flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@value|fdpsGufi|The name value pair specifies<br>the SFDPS GUFI, an identifier<br>on every message that<br>positively identifies what flight<br>the message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-z0-<br>9/]+"|name="FDPS_GUFI"<br>value="us.fdps.2015-12-<br>18T16:59:10Z.000/14/100<br>"/>|Yes|

281

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[LH_FIXM]**|**Name**<br>**[LH]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Require**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/flightPlan/@id<br>entifier|eramGufi_<br>316a|This attribute specifies the<br>unique flight plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|This element contains a<br>reference that uniquely<br>identifies a flight and that is<br>independent of any particular<br>system. This reference<br>conforms to the Universal<br>Unique Identifier standard.|fb:GloballyFlight<br>IdentifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-4[0-<br>9a-fA-F]{3}\-[89aAbB][0-9a-fA-<br>F]{3}\-[0-9a-fA-F]{12}"|4aaf92be-ac0a-4dba-<br>998f-9e56f5d450b6|Yes|
|flight/interimAltitud<br>e|interimAlt<br>_76a<br>interimAlt<br>_76b|This element specifies the<br>interim altitude the flight is<br>cleared to maintain different<br>from that in the flight plan.<br>This element is set to a NULL<br>value when the message is<br>used to indicate that a<br>previously received interim<br>altitude needs to be deleted.|nas:SimpleAltitu<br>deType|Yes|xs:double<br>or NULL value:<br>xsi:nil=”true”|Aircraft interim altitude of<br>24,000 feet:<br>**240000**<br>uom=**FEET**|Yes|
|flight/interimAltitud<br>e/@uom|interimAlt<br>_76a<br>interimAlt<br>_76b|The attribute_uom_specifies the<br>unit of measure for the<br>_interimAltitude_element:<br>FEET/METRES.|ff:AltitudeMeas<br>ureType|No|**“FEET|METRES”**|**FEET**|Yes|
|flight/flightIdentifica<br>tion/@aircraftIdentif<br>ication|flightId_0<br>2a|Name used by Air Traffic<br>Services units to identify and<br>communicate with an aircraft.|fb:FlightIdentifi<br>erType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@name<br>flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@value||The flight supplemental data is<br>used to indicate that a flight<br>message is a test message, by<br>setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the<br>attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|No|

282

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[LH_FIXM]**|**Name**<br>**[LH]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Require**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/flightIdentifica<br>tion/@computerId|computerI<br>d_02d|A unique identification<br>assigned by ERAM to each<br>flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentifica<br>tion/@siteSpecificPl<br>anId|sspId_167<br>a|Site Specific Plan Identifier. It<br>is assigned by Instrument<br>Flight Procedures Automation<br>(IFPA) to uniquely identify a<br>flight plan in each ERAM<br>facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|

##### **5.5.1.59 ARTS Flow Control Track/Full Data Block Information [HZ] – Data Elements**

|**Element Name**<br>**[HZ]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC time<br>followed by a four-digit sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits represent<br>the UTC time (_hhmmss_) and the last four digits,<br>represent the message sequence number in the<br>range [0000-9999].|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of<br>the message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:_hh_<br>stands for the 2-digit-hour in the range 00-23,<br>_mm_stands for the 2-digit minutes in the range<br>00-59, and_ss_stands for the 2-digit seconds in<br>the range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|

283

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HZ]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-9999].|**9001**|Yes|
|addresseeARTS_00<br>d|This element contains the ARTS facility<br>identification to which ERAM is to relay<br>the message.|string|No|**"[A-Z]{1,3}"**|**NNN**|Yes|
|addresserARTS_00<br>a|This element contains the ARTS facility<br>identification from which ERAM is to relay<br>the message.|string|No|**"[A-Z]{1,3}"**|**MMM**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called Call<br>Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character followed by<br>one to six alphanumeric characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification (Computer<br>ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by two<br>alphanumeric characters with the exception of<br>the letters**I**and**O**, as specified by the pattern<br>above.|**020**|Yes|
|sspId_167a|Site Specific Plan Identifier. It is assigned<br>by IFPA to uniquely identify a flight plan in<br>each ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|
|groundSpeed_05b|This element contains the aircraft ground<br>speed in knots.|string|No|**"\d{3}"**<br>The format is three digits.<br>If the aircraft ground speed is not available, this<br>element contains three zeroes.|**357**<br>Aircraft ground speed<br>is 357 knots.<br>**000**<br>Indicates that the<br>aircraft ground speed<br>is missing.|Yes|
|assignedAlt_08a|Assigned altitude or flight level expressed<br>in hundreds of feet.<br>It may only be specified if none of the<br>other altitude elements (assignedAlt_08a,<br>assignedAlt_08c, interimAlt_76bT,<br>assignedAlt_08d, reportedAlt_54aC) is|string|No|**“(\d{2,3}) | VFR”**<br>The format consists of either two to three<br>digits, or the constant string**VFR**. Three digits<br>are required for ARTS III, thus a leading zero<br>needs to be used when necessary.|Assigned altitude of<br>34,000 feet:<br>**340**<br>Assigned altitude<br>9,000 feet ARTS III:<br>**090**|No|

284

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HZ]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||included in the message.||||||
|assignedAlt_08c|VFR-ON-Top with altitude. It represents<br>an IFR flight operating above the clouds in<br>VFR conditions at the specified assigned<br>altitude.<br>It may only be specified if none of the<br>other altitude elements (assignedAlt_08a,<br>assignedAlt_08c, interimAlt_76bT,<br>assignedAlt_08d, reportedAlt_54aC) is<br>included in the message.|string|No|“**OTP/\d{2,3}**”<br>The format is the constant string**OTP**/ followed<br>by two to three digits that represent the<br>assigned altitude in hundreds of feet.|Aircraft flying VFR-<br>ON-Top at 25,000<br>feet:<br>**OTP/250**|No|
|interimAlt_76bT|This element specifies the interim altitude<br>for the flight in hundreds of feet<br>It may only be specified if none of the<br>other altitude elements (assignedAlt_08a,<br>assignedAlt_08c, interimAlt_76bT,<br>assignedAlt_08d, reportedAlt_54aC) is<br>included in the message.|string|No|**"\d{1,3}T"**<br>One to three digits in the range 0 – 999.|**240**|No|
|assignedAlt_08d|The assigned block of altitudes for the<br>flight to fly at.<br>It may only be specified if none of the<br>other altitude elements (assignedAlt_08a,<br>assignedAlt_08c, interimAlt_76bT,<br>assignedAlt_08d, reportedAlt_54aC) is<br>included in the message.|string|No|**"\d{2,3}B\d{2,3}"**<br>The format is two to three digits, followed by<br>the letter**B**, followed by two to three digits.<br>The leading and trailing two to three digits<br>define the block of altitudes in hundreds of feet<br>for the flight to fly at. The lowest altitude must<br>be listed first.|Assigned altitude<br>block of 8,000 feet to<br>14,000 feet:<br>**80B140**|No|
|reportedAlt_54aC|This element contains the reported Mode<br>C altitude.<br>It may only be specified if none of the<br>other altitude elements (assignedAlt_08a,<br>assignedAlt_08c, interimAlt_76bT,<br>assignedAlt_08d, reportedAlt_54aC) is<br>included in the message.|string|No|**"\d{3}C"**<br>Three digits followed by the letter C. The digits<br>represent the aircraft altitude in hundreds of<br>feet. Leading zeroes have to be inserted when<br>necessary.<br>If there is no Mode C or the reported altitude is<br>negative, this element contains "000".|**090C**<br>Mode C altitude of<br>9,000 feet.|No|
|trackPosition_23d|This element specifies the track position<br>form ERAM to ATM-IPOP.|string|No|**"\d{6}[A-Z]/\d{7}[A-Z]"**<br>It is a latitude/longitude pair, separated by a<br>virgule. For latitude, the first two digits are<br>degrees,the second two are minutes,and the|393106N/0842535W|Yes|

285

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HZ]**|**Element Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||last two are seconds. The letter can be N or S.<br>For the longitude, the first three digits are<br>degrees, the second two are minutes, and the<br>last two are seconds. The letter can be E or W.|||

286

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.60 ARTS Flow Control Track/Full Data Block Information [HZ] - Diagram**

##### **5.5.1.61 ARTS Flow Control Track/Full Data Block Information [HZ_FIXM] – Data Elements**

The following elements of the HZ message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

- addresseeARTS_00d

287

NAS-JMSDD-4309-001 Rev C July 10, 2018

###### • addresserARTS_00a

|**Name**<br>**[HZ_FIXM]**|**Name**<br>**[HZ]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/add<br>itionalFlightInformation/nam<br>eValue/@name<br>flight/supplementalData/add<br>itionalFlightInformation/nam<br>eValue/@value|FDPS_Se<br>quenceN<br>o|Sequence number assigned by SFDPS to<br>each message it receives from HADDS. The<br>attribute_name_includes the constant string<br>"MSG_SEQ_NO", and the attribute_value_<br>contains the sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|@name="MSG_SE<br>Q_NO"<br>@value="6860416<br>"|Yes|
|flight/departure/@departure<br>Point|FDPS_Ori<br>gin/depa<br>rturePoin<br>t_26a|Attribute used to specify the first point or<br>other initial entity where the air traffic<br>control/management system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used<br>for this element (fix name,<br>lat/long, or fix-radial-<br>distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arrivalPoint|destinati<br>on_27a|The final point or other final entity where<br>the air traffic control/management system<br>route terminates.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used<br>for this element (fix name,<br>lat/long, or fix-radial-<br>distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/operator/operatingOrg<br>anization/organization/@na<br>me|FDPS_Flig<br>htOperat<br>or/OPRIn<br>dicator_9<br>18f|Attribute used to specify the full official<br>name of the State, Organization,<br>Authority, aircraft operating agency,<br>handling agency engaged in or offering to<br>engage in aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|

288

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HZ_FIXM]**|**Name**<br>**[HZ]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|flight/@system<br><br>|propSour<br>ceSystem|<br>This attribute indicates which SFDPS<br>system generated the message.|fb:ProvenanceSyste<br>mType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp<br><br>|propRcvd<br>Time|This attribute conatins the time at which<br>the message was received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre<br>|center|This attribute specifies the code of the<br>ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCentr<br>eType|No|xs:string|`ZAU`|Yes|
|flight/arrival/runwayPosition<br>AndTime/runwayTime/[estim<br>ated|actual]/@time<br><br>|arrivalTi<br>me|This attribute specifies the proposed or the<br>actual time of arrival at destination, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/departure/runwayPosit<br>ionAndTime/runwayTime/[ac<br>tual|estimated]/@time<br><br>|departur<br>eTime|This element specifies the proposed or<br>actual departure time, set according to the<br>flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/flightStatus/@fdpsFlig<br>htStatus<br><br>|flightStat<br>e|This attribute contains the current status<br>of the flight as specified by SFDPS.|nas:SfdpsFlightStatu<br>sType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLE<br>TED|CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/add<br>itionalFlightInformation/nam<br>eValue/@name<br>flight/supplementalData/add<br>itionalFlightInformation/nam<br>eValue/@value<br>|fdpsGufi|The name value pair specifies the SFDPS<br>GUFI, an identifier on every message that<br>positively identifies what flight the<br>message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-<br>Za-z0-9/]+"|name="FDPS_GUFI<br>"<br>value="us.fdps.201<br>5-12-<br>18T16:59:10Z.000/<br>14/100"/>|Yes|
|flight/flightPlan/@identifier<br><br>|eramGufi<br>_316a|This attribute specifies the unique flight<br>plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi<br>|uuidGufi|<sup>This element contains a reference that</sup><br>uniquely identifies a flight and that is<br>independent of any particular system. This|fb:GloballyFlightIde<br>ntifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-|4aaf92be-ac0a-<br>4dba-998f-|Yes|

289

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HZ_FIXM]**|**Name**<br>**[HZ]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|||reference conforms to the Universal<br>Unique Identifier standard.|||F]{4}\-4[0-9a-fA-F]{3}\-<br>[89aAbB][0-9a-fA-F]{3}\-[0-<br>9a-fA-F]{12}"|9e56f5d450b6||
|flight/flightIdentification/@ai<br>rcraftIdentification|flightId_0<br>2a|Name used by Air Traffic Services units to<br>identify and communicate with an aircraft.|fb:FlightIdentifierTy<br>pe|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/add<br>itionalFlightInformation/nam<br>eValue/@name<br>flight/supplementalData/add<br>itionalFlightInformation/nam<br>eValue/@value|flightId_0<br>2a|The flight supplemental data is used to<br>indicate that a flight message is a test<br>message, by setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the attribute<br>_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1,**<br>**maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLIG**<br>**HT”**<br>@value =**“true”**|No|
|flight/flightIdentification/@c<br>omputerId|compute<br>rId_02d|A unique identification assigned by ERAM<br>to each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two<br>alphanumeric characters with<br>the exception of the letters**I**<br>and**O**, such as_ddd, ddL, dLd,_<br>_dLL_.|**020**|No|
|flight/flightIdentification/@si<br>teSpecificPlanId|sspId_16<br>7a|Site Specific Plan Identifier. It is assigned<br>by Instrument Flight Procedures<br>Automation (IFPA) to uniquely identify a<br>flight plan in each ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|

290

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HZ_FIXM]**|**Name**<br>**[HZ]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|flight/enRoute/position/actu<br>alSpeed/surveillance|groundSp<br>eed_05b|This element contains the measured<br>horizontal speed of the aircraft relative to<br>a fixed point on the ground for flights<br>being tracked by surveillance or satellite.|ff:GroundSpeedType|Yes|**xs:double**<br>The Groundspeed type<br>represents any ground speed<br>measurement, in metric or<br>imperial, as specified by the<br>"_uom_" attribute.|**357**<br>uom=KNOTS<br>Aircraft ground<br>speed is 357 knots.|Yes|
|flight/enRoute/position/actu<br>alSpeed/surveillance/@uom|groundSp<br>eed_05b|Attribute of groundspeed indicating units<br>of ground speed measurement.|ff:GroundSpeedMea<br>sureType|No|**“KILOMETRES_PER_HOUR|K**<br>**NOTS”**|**KNOTS**|Yes|
|flight/enRoute/position/@re<br>portSource|groundSp<br>eed_05b|The source of the current position report<br>information.|fb:ProvenanceSourc<br>eType|No|**“SURVEILLANCE”**|**SURVEILLANCE**|No|
|flight/assignedAltitude/simpl<br>e|assigned<br>Alt_08a|Simple altitude: single measurement<br>above reference point. It represents the<br>only NAS altitude that maps directly to the<br>core ICAO altitude types.<br>Only one of the altitude elements_simple_,<br>_vfrOnTop_,_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be included in the<br>message.|nas:SimpleAltitudeT<br>ype|Yes|**“xs:double”**|Assigned altitude<br>of 34,000 feet:<br>**34000**<br>_uom_:<br>**FEET**<br>_Ref_:<br>**MEAN_SEA_LEVEL**|No|
|flight/assignedAltitude/simpl<br>e/@uom|assigned<br>Alt_08a||ff:AltitudeMeasureT<br>ype|No|“**FEET|METERS**”|**FEET**|Yes|
|flight/assignedAltitude/simpl<br>e/@ref|assigned<br>Alt_08a||ff:AltitudeReference<br>Type|No|**“MEAN_SEA_LEVEL|**<br>**FLIGHT_LEVEL”**|**MEAN_SEA_LEVEL**|Yes|
|flight/assignedAltitude/vfrOn<br>TopPlus|assigned<br>Alt_08c|VFR-ON-Top with altitude. It represents an<br>Instrument Flight Rules (IFR) flight<br>operating above the clouds in VFR<br>conditions at the specified assigned<br>altitude.<br>Only one of the altitude elements_simple_,<br>_vfrOnTop_, _vfrOnTopPlus_, _block_, _above_,|nas:VfrOnTopPlusAlt<br>itudeType|No|**“xs:double”**<br>uom:|Aircraft flying VFR-<br>ON-Top at 25,000<br>feet:<br>**25000**<br>_uom_:**FEET**|No|

291

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HZ_FIXM]**|**Name**<br>**[HZ]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|||_altFixAlt_,_vfr_,_vfrPlus_may be included in the<br>message.||||||
|flight/assignedAltitude/vfrOn<br>TopPlus/@uom|assigned<br>Alt_08c|This attribute specifies the altitude<br>measure unit for the element<br>_assignedAltitude/vfrOnTopPlus_.|ff:AltitudeMeasureT<br>ype|No|**“FEET|METRES”**|**FEET**|Yes|
|flight/interimAltitude|interimAl<br>t_76bT|This element specifies the interim altitude<br>the flight is cleared to maintain different<br>from that in the flight plan.|nas:SimpleAltitudeT<br>ype|Yes|xs:double|interimAltitude of<br>240,000 feet:<br>**240000**<br>uom=**FEET**|No|
|flight/interimAltitude/@uom|interimAl<br>t_76bT|This attribute specifies the unit of measure<br>for the_interimAltitude_element:<br>FEET/METRES.|_ff:AltitudeMeasureT_<br>_ype_|No|**“FEET|METRES”**|**FEET**|Yes|
|flight/assignedAltitude/block<br>/above|assigned<br>Alt_08d|The bottom level of the assigned block of<br>altitudes for the flight to fly at.<br>Only one of the altitude elements_simple_,<br>_vfrOnTop_,_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be included in the<br>message.|ff:AltitudeType|Yes|**"xs:double"**<br>uom:|**8000**<br>_uom:_<br>**FEET**|No|
|flight/assignedAltitude/block<br>/above/@uom|assigned<br>Alt_08d|This attribute specifies the unit of measure<br>for the_assignedAltitude/block/above_<br>element.|ff:AltitudeMeasureT<br>ype|No|**“FEET|METRES”**|**FEET**|Yes|
|flight/assignedAltitude/block<br>/below|assigned<br>Alt_08d|The top level of the assigned block of<br>altitudes for the flight to fly at.<br>Only one of the altitude elements_simple_,<br>_vfrOnTop_,_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be included in the<br>message.|ff:AltitudeType|Yes|**"xs:double"**|**14000**<br>_uom:_**FEET**|No|
|flight/assignedAltitude/block<br>/below/@uom|assigned<br>Alt_08d|This attribute specifies the unit of measure<br>for the_assignedAltitude/block/below_<br>element.|ff:AltitudeMeasureT<br>ype|No|**“FEET|METRES”**|**FEET**|Yes|

292

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HZ_FIXM]**|**Name**<br>**[HZ]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|flight/enRoute/position/altit<br>ude|reported<br>Alt_54aC|This element contains the reported Mode<br>C altitude.<br>It may only be specified if none of the<br>other altitude elements (assignedAltitude,<br>interimAltitude) is included in the<br>message.|ff:AltitudeType|Yes|**xs:double**|**31000**<br>**FEET**<br>The aircraft<br>reported altitude<br>is 31,000 feet.|No|
|flight/enRoute/position/altit<br>ude/@uom|reported<br>Alt_54aC|This attribute specifies the altitude<br>measure unit for the element<br>_flight/enRoute/position/altitude_.|ff:AltitudeMeasureT<br>ype|No|**“FEET|METRES”**|**FEET**|Yes|
|flight/enRoute/position/posit<br>ion/location/pos|trackPosi<br>tion_23d|This element specifies the actual location<br>of an active flight as reported by<br>surveillance, for a flight tracked by radar,<br>or from the position part of a pilot progress<br>report, for an oceanic flight or a flight<br>operating in a non-radar airspace.|_ff:GeographicalLocat_<br>_ionType_|Yes|List of two**xs:double**: latitude<br>followed by longitude:<br>**"\d{6}[A-Z] \d{7}[A-Z]"**<br>For latitude, the first two<br>digits are degrees, the second<br>two are minutes, and the last<br>two are seconds. For the<br>longitude, the first three<br>digits are degrees, the second<br>two are minutes, and the last<br>two are seconds.|393106 0842535|Yes|
|flight/enRoute/position/posit<br>ion/location/@srsName|trackPosi<br>tion_23d|This attribute specifies the name of the<br>coordinate reference system (CRS) that<br>defines the semantics of the lat/long pair<br>_flight/enRoute/position/position/@pos_<br>according to the ISO6709 standard. FIXM<br>uses only "urn:ogc:def:crs:EPSG::4326".|xs:string|No|fixed=**"urn:ogc:def:crs:EPSG::**<br>**4326"**|urn:ogc:def:crs:EP<br>SG::4326|Yes|

293

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.62 Beacon Code Reassignment [BA] – Data Elements**

|**Element Name**<br>**[BA]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed by<br>a four-digit sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and the<br>last four digits, represent the message<br>sequence number in the range [0000-9999].|**2359359001**, where the first<br>6 digits are the UTC time<br>(23:59:35 UTC) and the last<br>4 digits are sequence<br>number of the message<br>(9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:_hh_<br>stands for the 2-digit-hour in the range 00-<br>23,_mm_stands for the 2-digit minutes in the<br>range 00-59, and_ss_stands for the 2-digit<br>seconds in the range 00-59.|**23_59_35**<br>that represents 23:59:35<br>UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the sourceId_00e<br>element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character followed<br>by one to six alphanumeric characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by two<br>alphanumeric characters with the exception<br>of the letters**I**and**O**, as specified by the<br>pattern above.|**020**|No|
|eramGufi_316a|GUFI that uniquely identifies<br>each flight in the system.|string|No|**"[A-Z]{2}\d{5}[1-7]\d{2}"**<br>This element includes<br>10 alphanumeric characters:<br>-ICAO country code (one letter);<br>-en-route facility ID (one letter);<br>-time in seconds  of current day (five digits in<br>the range 00000-86400);|**KB5980017**|No|

294

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[BA]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||-sequence number (two digits).|||
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each<br>ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|
|beaconCode_04a|Beacon code.|string|No|**"[0-7]{4}"**<br>The element includes four octal digits (i.e. 0-<br>7). When the last two digits of the four digits<br>are zero, the beacon code is a non-discrete<br>code.<br>A discrete code is any code not ending in 00.|Non-discrete VFR code:<br> **2101**|Yes|
|departurePoint_26<br>a|It is used to specify the point at<br>which to start processing the<br>flight plan route as follows: the<br>departure airport or the airfile<br>point.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a fix<br>can be used for this element (fix name,<br>lat/long, or fix-radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|destination_27a|It is used to specify the point at<br>which to end processing the<br>flight plan route.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a fix<br>can be used for this element (fix name,<br>lat/long, or fix-radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|

295

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.63 Beacon Code Reassignment [BA] - Diagram**

##### **5.5.1.64 Beacon Code Reassignment Message in FIXM Format [BA_FIXM] – Data Elements**

The following elements of the BA message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

296

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BA_FIXM]**|**Name**<br>**[BA]**|**Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@name<br>flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@value|FDPS_Sequenc<br>eNo|Sequence number assigned by<br>SFDPS to each message it receives<br>from HADDS. The attribute_name_<br>includes the constant string<br>"MSG_SEQ_NO", and the<br>attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|@name="MSG_SEQ_N<br>O"<br>@value="6860416"|Yes|
|flight/operator/oper<br>atingOrganization/or<br>ganization/@name|FDPS_FlightOp<br>erator/OPRInd<br>icator_918f|Attribute used to specify the full<br>official name of the State,<br>Organization, Authority, aircraft<br>operating agency, handling<br>agency engaged in or offering to<br>engage in aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/@system|propSourceSys<br>tem|This attribute indicates which<br>SFDPS system generated the<br>message.|fb:ProvenanceSystemType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTime|This attribute conatins the time at<br>which the message was received<br>by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the code<br>of the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCentreType|No|xs:string|`ZAU`|Yes|
|flight/arrival/runway<br>PositionAndTime/ru<br>nwayTime/[estimate<br>d|actual]/@time|arrivalTime|This attribute specifies the<br>proposed or the actual time of<br>arrival at destination, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/departure/run<br>wayPositionAndTim<br>e/runwayTime/[actu<br>al|estimated]/@tim<br>e|departureTime|This element specifies the<br>proposed or actual departure<br>time, set according to the flight<br>state.|ff:TimeType|No|xs:dateTime|2014-06-20T20:17:52|Yes|

297

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BA_FIXM]**|**Name**<br>**[BA]**|**Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|flight/flightStatus/@<br>fdpsFlightStatus|flightState|This attribute contains the<br>current status of the flight as<br>specified by SFDPS.|nas:SfdpsFlightStatusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLET<br>ED|CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@name<br>flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@value|fdpsGufi|The name value pair specifies the<br>SFDPS GUFI, an identifier on<br>every message that positively<br>identifies what flight the message<br>is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-<br>z0-9/]+"|name="FDPS_GUFI"<br>value="us.fdps.2015-12-<br>18T16:59:10Z.000/14/1<br>00"/>|Yes|
|flight/flightPlan/@id<br>entifier|eramGufi_316<br>a|This attribute specifies the unique<br>flight plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|This element contains a reference<br>that uniquely identifies a flight<br>and that is independent of any<br>particular system. This reference<br>conforms to the Universal Unique<br>Identifier standard.|fb:GloballyFlightIdentifierT<br>ype||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-<br>4[0-9a-fA-F]{3}\-[89aAbB][0-9a-<br>fA-F]{3}\-[0-9a-fA-F]{12}"|4aaf92be-ac0a-4dba-<br>998f-9e56f5d450b6|Yes|
|flight/flightIdentifica<br>tion/@aircraftIdentif<br>ication|flightId_02a|Name used by Air Traffic Services<br>units to identify and<br>communicate with an aircraft.|fb:FlightIdentifierType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@name<br>flight/supplemental<br>Data/additionalFligh<br>tInformation/nameV<br>alue/@value||The flight supplemental data is<br>used to indicate that a flight<br>message is a test message, by<br>setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the<br>attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>fb:FreeTextType|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT”**|@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|No|

298

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BA_FIXM]**|**Name**<br>**[BA]**|**Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
||||||@value =**“true”**|||
|flight/flightIdentifica<br>tion/@computerId|computerId_0<br>2d|A unique identification assigned<br>by ERAM to each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception<br>of the letters**I**and**O**, such as<br>_ddd, ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentifica<br>tion/@siteSpecificPl<br>anId|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by Instrument Flight<br>Procedures Automation (IFPA) to<br>uniquely identify a flight plan in<br>each ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/enRoute/beac<br>onCodeAssignment/<br>currentBeaconCode|beaconCode_0<br>4a|Current assigned beacon code.|fb:BeaconCodeType|No|"[0-7]{4}"<br>The element includes four<br>octal digits (i.e. 0-7). When the<br>last two digits of the four-digits<br>are zero, the beacon code is a<br>non-discrete code.<br>A discrete code is any code not<br>ending in 00.|Non-discrete VFR code:<br> **2101**|Yes|
|flight/departure/@d<br>eparturePoint|departurePoin<br>t_26a|It is used to specify the first point<br>or other initial entity where the<br>air traffic control/management<br>system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name,<br>lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|flight/arrival/@arriv<br>alPoint|destination_27|The final point or other final<br>entitywhere the air traffic|fb:FreeTextType|No|**xs:string**|**AB**|Yes|

299

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[BA_FIXM]**|**Name**<br>**[BA]**|**Definition**|**Type**|**Com**<br>**plex?**|**Format/Permissible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
||a|control/management system<br>route terminates.|||minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name,<br>lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**||

##### **5.5.1.65 Beacon Code Restricted [RE] – Data Elements**

|**Element Name**<br>**[RE]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC time<br>followed by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where<br>the first 6 digits are the<br>UTC time (23:59:35<br>UTC) and the last 4<br>digits are sequence<br>number of the message<br>(9001).|<br>Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of the|string|No|**“\d{4}”**<br>Four-digit number in the range[0000-|**9001**|Yes|

300

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[RE]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||sourceId_00e element.|||9999].|||
|flightId_02a|Aircraft ID, or flight ID (also called Call<br>Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**, as<br>specified by the pattern above.|**020**|No|
|eramGufi_316a|GUFI that uniquely identifies each<br>flight in the system.|string|No|**"[A-Z]{2}\d{5}[1-7]\d{2}"**<br>This element includes<br>10 alphanumeric characters:<br>-ICAO country code (one letter);<br>-en-route facility ID (one letter);<br>-time in seconds  of current day (five<br>digits in the range 00000-86400);<br>-sequence number (two digits).|**KB5980017**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely identify<br>a flight plan in each ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|
|beaconCode_04a|Beacon code.|string|No|**"[0-7]{4}"**<br>The element includes four octal digits<br>(i.e. 0-7). When the last two digits of the<br>four digits are zero, the beacon code is a<br>non-discrete code.<br>A discrete code is any code not ending<br>in 00.|Non-discrete VFR code:<br> **2101**|<br>Yes|
|departurePoint_26a|It is used to specify the point at which<br>to start processing the flight plan<br>route as follows: the departure<br>airport or the airfile point.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a<br>fix can be used for this element(fix|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**|Yes|

301

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[RE]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||name, lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**ATOKA300040**<br>**3500N/04000W**||
|destination_27a|This element is used to specify the<br>point at which to end processing the<br>flight plan route.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a<br>fix can be used for this element (fix<br>name, lat/long, or fix-radial-distance),<br>including the standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|restrictedBeaconCode_04a<br>R|This element is used to specify the<br>restricted beacon code.|string|No|**"[0-7]{4}"**<br>The element includes four octal digits<br>(i.e. 0-7). When the last two digits of the<br>four digits are zero, the beacon code is a<br>non-discrete code.<br>A discrete code is any code not ending<br>in 00.|2101|Yes|

302

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.66 Beacon Code Restricted [RE] - Diagram**

##### **5.5.1.67 Beacon Code Restricted Message in FIXM Format [RE_FIXM] – Data Elements**

The following elements of the RE message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

303

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[RE_FIXM]**|**Name**<br>**[RE]**|**Definition**|**Type**|Com<br>plex?|Format/Permissible Values|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData<br>/additionalFlightInforma<br>tion/nameValue/@name<br>flight/supplementalData<br>/additionalFlightInforma<br>tion/nameValue/@value|FDPS_Seq<br>uenceNo|Sequence number assigned by SFDPS to each<br>message it receives from HADDS. The attribute<br>_name_includes the constant string<br>"MSG_SEQ_NO", and the attribute_value_<br>contains the sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive value="999999999"|@name="MSG_SEQ_<br>NO"<br>@value="6860416"|Yes|
|flight/operator/operatin<br>gOrganization/organizati<br>on/@name|FDPS_Flig<br>htOperat<br>or/OPRIn<br>dicator_9<br>18f|Attribute used to specify the full official name<br>of the State, Organization, Authority, aircraft<br>operating agency, handling agency engaged in<br>or offering to engage in aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/@system|propSourc<br>eSystem|This attribute indicates which SFDPS system<br>generated the message.|fb:ProvenanceSyst<br>emType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvd<br>Time|This attribute conatins the time at which the<br>message was received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the code of the ARTCC<br>(or<br>FIR) that produced the data.|fb:ProvenanceCen<br>treType|No|xs:string|`ZAU`|Yes|
|flight/arrival/runwayPosi<br>tionAndTime/runwayTim<br>e/[estimated|actual]/@t<br>ime|arrivalTim<br>e|This attribute specifies the proposed or the<br>actual time of arrival at destination, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/departure/runway<br>PositionAndTime/runwa<br>yTime/[actual|estimated<br>]/@time|departure<br>Time|This element specifies the proposed or actual<br>departure time, set according to the flight<br>state.|ff:TimeType|No|xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/flightStatus/@fdps<br>FlightStatus|flightState|This attribute contains the current status of<br>the flight as specified by SFDPS.|nas:SfdpsFlightSta<br>tusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETED|C<br>ANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData|fdpsGufi|The name value pair specifies the SFDPS GUFI,|fb:FreeTextType|No|xs:string|name="FDPS_GUFI"|Yes|

304

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[RE_FIXM]**|**Name**<br>**[RE]**|**Definition**|**Type**|Com<br>plex?|Format/Permissible Values|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|/additionalFlightInforma<br>tion/nameValue/@name<br>flight/supplementalData<br>/additionalFlightInforma<br>tion/nameValue/@value||an identifier on every message that positively<br>identifies what flight the message is for.|||@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-z0-<br>9/]+"|value="us.fdps.2015-<br>12-<br>18T16:59:10Z.000/14/<br>100"/>||
|flight/flightPlan/@identi<br>fier|eramGufi<br>_316a|This attribute specifies the unique flight plan<br>identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|This element contains a reference that<br>uniquely identifies a flight and that is<br>independent of any particular system. This<br>reference conforms to the Universal Unique<br>Identifier standard.|fb:GloballyFlightId<br>entifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-4[0-<br>9a-fA-F]{3}\-[89aAbB][0-9a-fA-F]{3}\-<br>[0-9a-fA-F]{12}"|4aaf92be-ac0a-4dba-<br>998f-9e56f5d450b6|Yes|
|flight/flightIdentification<br>/@aircraftIdentification|flightId_0<br>2a|Name used by Air Traffic Services units to<br>identify and communicate with an aircraft.|fb:FlightIdentifierT<br>ype|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData<br>/additionalFlightInforma<br>tion/nameValue/@name<br>flight/supplementalData<br>/additionalFlightInforma<br>tion/nameValue/@value|flightId_0<br>2a|The flight supplemental data is used to<br>indicate that a flight message is a test<br>message, by setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the attribute_value_<br>to “**true**”.|@_name:_<br>_@value_:<br>fb:FreeTextType|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|No|
|flight/flightIdentification<br>/@computerId|computerI<br>d_02d|A unique identification assigned by ERAM to<br>each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of the<br>letters**I**and**O**, such as_ddd, ddL, dLd,_<br>_dLL_.|**020**|No|
|flight/flightIdentification<br>/@siteSpecificPlanId|sspId_167<br>a|Site Specific Plan Identifier. It is assigned by<br>Instrument Flight Procedures Automation|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|

305

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[RE_FIXM]**|**Name**<br>**[RE]**|**Definition**|**Type**|Com<br>plex?|Format/Permissible Values|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||(IFPA) to uniquely identify a flight plan in each<br>ERAM facility.||||||
|flight/enRoute/beaconC<br>odeAssignment/currentB<br>eaconCode|beaconCo<br>de_04a|Current assigned beacon code.|fb:BeaconCodeTyp<br>e|No|"[0-7]{4}"<br>The element includes four octal<br>digits (i.e. 0-7). When the last two<br>digits of the four-digits are zero, the<br>beacon code is a non-discrete code.<br>A discrete code is any code not<br>ending in 00.|Non-discrete VFR<br>code:<br> **2101**|Yes|
|flight/departure/@depar<br>turePoint|departure<br>Point_26a|<br>It is used to specify the first point or other<br>initial entity where the air traffic<br>control/management system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|flight/arrival/@arrivalPoi<br>nt|destinatio<br>n_27a|The final point or other final entity where the<br>air traffic control/management system route<br>terminates.|fb:FreeTextType|No|**xs:string**<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|Yes|
|flight/enRoute/beaconC<br>odeAssignment/previous<br>BeaconCode|restricted<br>BeaconCo<br>de_04aR|The Secondary Surveillance Radar (SSR) mode<br>and code the flight was transponding before<br>the current SSR mode and code.|fb:BeaconCodeTyp<br>e|Yes|**"[0-7]{4}"**<br>The element includes four octal<br>digits (i.e. 0-7). When the last two<br>digits of the four digits are zero, the<br>beacon code is a non-discrete code.<br>A discrete code is anycode not|2101|Yes|

306

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**|**Name**|**Definition**|**Type**|Com|Format/Permissible Values|**Example**|**Requ**|
|---|---|---|---|---|---|---|---|
|**[RE_FIXM]**|**[RE]**|||plex?|||**ired?**|
||||||ending in 00.|||

##### **5.5.1.68 FDB Fourth Line Information [HF] – Data Elements**

|**Element Name**<br>**[HF]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC time<br>followed by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where the<br>first 6 digits are the UTC<br>time (23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of the<br>message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents 23:59:35<br>UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called Call<br>Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O.**|**020**|Yes|

307

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HF]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely identify<br>a flight plan in each ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|
|FDB4thLineHeading_155<br>a|This element is used to display the<br>heading of the aircraft issued by the<br>controller. Its format is one to four<br>alphanumeric characters. Samples:<br>075, H075.|string|No|**“[A-Z0-9]{1,4}”**|**075**<br>**H075**|No|
|FDB4thLineSpeed_155b|This element is used to display the<br>speed of the aircraft issued by the<br>controller.|string|No|**"[A-Z0-9+-\.]{1,4}"**<br>Minimum length = 1 character<br>Maximum length = 4 characters.|280+<br>S260<br>M83+<br>.75-|No|
|FDB4thLineText_155c|This element is used to display free-<br>form text issued by the controller.|string|No|**"[A-Z0-9+-=\*/_;\.,\|^v]{1,8}"**<br>The allowed characters are the<br>alphanumeric characters, −, +, =, *, /,<br>underscore (_), semicolon (;), period (.),<br>and comma (,). No leading or embedded<br>spaces are allowed.<br>It can be one to eight characters long.|-BUFFI<br>NOBBL<br>BLVNS|No|

308

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.69 FDB Fourth Line Information [HF] - Diagram**

##### **5.5.1.70 FDB Forth Line Message in FIXM Format [HF_FIXM] – Data Elements**

The following elements of the HF message in Simple XML format are not translated in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

|**Name**<br>**[HF_FIXM]**|**Name**<br>**[HF]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|flight/supplemental<br>Data/additionalFlight<br>Information/nameVa<br>lue/@name<br>flight/supplemental<br>Data/additionalFlight<br>F<br>o|DPS_SequenceN<br>|Sequence number assigned by SFDPS to<br>each message it receives from HADDS.<br>The attribute_name_includes the constant<br>string "MSG_SEQ_NO", and the attribute<br>_value_contains the sequence number<br>value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive|@name="MSG_SEQ<br>_NO"<br>@value="6860416"|Yes|

309

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HF_FIXM]**|**Name**<br>**[HF]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|Information/nameVa<br>lue/@value|||||value="999999999"|||
|flight/departure/@d<br>eparturePoint|FDPS_Origin/dep<br>arturePoint_26a|Attribute used to specify the first point or<br>other initial entity where the air traffic<br>control/management system route<br>starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arriv<br>alPoint|destination_27a|The final point or other final entity where<br>the air traffic control/management<br>system route terminates.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/operator/oper<br>atingOrganization/or<br>ganization/@name|FDPS_FlightOpera<br>tor/OPRIndicator<br>_918f|Attribute used to specify the full official<br>name of the State, Organization,<br>Authority, aircraft operating agency,<br>handling agency engaged in or offering to<br>engage in aircraft operation.|ff:TextNameTyp<br>e|No|xs:string|UAL|No|
|flight/@system|propSourceSyste<br>m|This attribute indicates which SFDPS<br>system generated the message.|fb:ProvenanceS<br>ystemType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTime|This attribute conatins the time at which<br>the message was received by SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the code of the<br>ARTCC (or|fb:ProvenanceC<br>entreType|No|xs:string|`ZAU`|Yes|

310

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HF_FIXM]**|**Name**<br>**[HF]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|||FIR) that produced the data.||||||
|flight/arrival/runway<br>PositionAndTime/ru<br>nwayTime/[estimate<br>d|actual]/@time|arrivalTime|This attribute specifies the proposed or<br>the actual time of arrival at destination,<br>set according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/departure/run<br>wayPositionAndTime<br>/runwayTime/[actual<br>|estimated]/@time|departureTime|This element specifies the proposed or<br>actual departure time, set according to<br>the flight state.|ff:TimeType|No|xs:dateTime|2014-06-<br>20T20:17:52|Yes|
|flight/flightStatus/@<br>fdpsFlightStatus|flightState|This attribute contains the current status<br>of the flight as specified by SFDPS.|nas:SfdpsFlightS<br>tatusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETED<br>|CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplemental<br>Data/additionalFlight<br>Information/nameVa<br>lue/@name<br>flight/supplemental<br>Data/additionalFlight<br>Information/nameVa<br>lue/@value|fdpsGufi|The name value pair specifies the SFDPS<br>GUFI, an identifier on every message that<br>positively identifies what flight the<br>message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-z0-<br>9/]+"|name="FDPS_GUFI"<br>value="us.fdps.2015<br>-12-<br>18T16:59:10Z.000/1<br>4/100"/>|Yes|
|flight/flightPlan/@id<br>entifier|eramGufi_316a|This attribute specifies the unique flight<br>plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|This element contains a reference that<br>uniquely identifies a flight and that is<br>independent of any particular system.<br>This reference conforms to the Universal<br>Unique Identifier standard.|fb:GloballyFlight<br>IdentifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-<br>4[0-9a-fA-F]{3}\-[89aAbB][0-9a-<br>fA-F]{3}\-[0-9a-fA-F]{12}"|4aaf92be-ac0a-<br>4dba-998f-<br>9e56f5d450b6|Yes|
|flight/flightIdentifica|flightId_02a|Name used by Air Traffic Services units to|fb:FlightIdentifi|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|

311

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HF_FIXM]**<br>**Name**<br>**[HF]**|**Definition**|**Type**|**Complex**<br>**?**|**Format/Permissible Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|
|tion/@aircraftIdentif<br>ication|identify and communicate with an<br>aircraft.|erType|||||
|flight/supplemental<br>Data/additionalFlight<br>Information/nameVa<br>lue/@name<br>flight/supplemental<br>Data/additionalFlight<br>Information/nameVa<br>lue/@value|The flight supplemental data is used to<br>indicate that a flight message is a test<br>message, by setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the attribute<br>_value_to “**true**”.|@_name:_<br>_@value_:<br>fb:FreeTextType|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLIGH**<br>**T”**<br>@value =**“true”**|No|
|flight/flightIdentifica<br>tion/@computerId<br>computerId_02d|A unique identification assigned by ERAM<br>to each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentifica<br>tion/@siteSpecificPl<br>anId<br>sspId_167a|Site Specific Plan Identifier. It is assigned<br>by Instrument Flight Procedures<br>Automation (IFPA) to uniquely identify a<br>flight plan in each ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/enRoute/clear<br>ed/@clearanceHeadi<br>ng<br>FDB4thLineHeadi<br>ng_155a|This element contains the En-Route<br>Controller Clearance heading as entered<br>by the controller in the fourth line in Full<br>Data Block.|fb:FreeTextType|No|**“[A-Z0-9]{1,4}”**|**075**<br>**H075**|No|
|flight/enRoute/clear<br>ed/@clearanceSpee<br>d<br>FDB4thLineSpeed<br>_155b|This element contains the En-Route<br>Controller Clearance speed as entered by<br>the controller in the fourth line in Full<br>Data Block.|fb:FreeTextType|No|**"[A-Z0-9+-\.]{1,4}"**|280+<br>S260<br>M83+<br>.75-|No|
|flight/enRoute/clear<br>ed/@clearanceText<br>FDB4thLineText_<br>155c|This element contains the free-from text<br>as entered by the En-Route Controller, to<br>be associated with the Clearance in the<br>fourth line in Full Data Block.|fb:FreeTextType|No|**"[A-Z0-9+-=\*/_;\.,\|^v]{1,8}"**|-BUFFI<br>NOBBL<br>BLVNS|No|

312

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.71 Point Out Information [HT] – Data Elements**

|**Element Name**<br>**[HT]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where the<br>first 6 digits are the UTC<br>time (23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of the<br>message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents 23:59:35<br>UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of<br>the sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O.**|**020**|Yes|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|

313

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HT]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceSectorRouting_134<br>b|This element contains the entering<br>sector number for a Point Out<br>action_HT_message for ATM-IPOP.|string|No|**“\d{2}”**<br>Two digits in the range 00 – 99.|**50**|Yes|
|targetSector_16g|This element contains an adjacent<br>center sector number for that<br>center or an internal ERAM sector<br>number.|string|No|**"[A-Z]?[0-9]{2}"**<br>The format is an optional letter to<br>specify the center, followed by two<br>digits to specify the sector.|M45<br>80|Yes|

##### **5.5.1.72 Point Out Information [HT] - Diagram**

##### **5.5.1.73 Point Out Information Message in FIXM Format [HT_FIXM] – Data Elements**

The following elements of the HT message in Simple XML format are not translated in the FIXM format of the message:

314

NAS-JMSDD-4309-001 Rev C July 10, 2018

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

|**Name**<br>**[HT_FIXM]**|**Name**<br>**[HT]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|flight/supplementalData/ad<br>ditionalFlightInformation/na<br>meValue/@name<br>flight/supplementalData/ad<br>ditionalFlightInformation/na<br>meValue/@value|FDPS_Seque<br>nceNo|Sequence number assigned by SFDPS to<br>each message it receives from HADDS. The<br>attribute name includes the constant string<br>"MSG_SEQ_NO", and the attribute value<br>contains the sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No<br>@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive value="999999999"|@name="MSG_SEQ_NO<br>"<br>@value="6860416"|Yes|
|flight/departure/@departur<br>ePoint|FDPS_Origin<br>/departureP<br>oint_26a|Attribute used to specify the first point or<br>other initial entity where the air traffic<br>control/management system route starts.|fb:FreeTextType|No<br>xs:string<br>minLength=2, maxLength=12<br>"([A-Z0-9]{2,5}) |<br>([A-Z0-9]{2,5}\d{6}) |<br>(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance), including the<br>standard airport designators.|AB<br>DFW<br>KDFW<br>SHP090015<br>ATOKA300040<br>3500N/04000W|No|
|flight/arrival/@arrivalPoint|FDPS_DestId<br>/destination<br>_27a|The final point or other final entity where<br>the air traffic control/management system<br>route terminates.|fb:FreeTextType|No<br>xs:string<br>minLength=2, maxLength=12<br>"([A-Z0-9]{2,5}) |<br>([A-Z0-9]{2,5}\d{6}) |<br>(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”<br>Any of the standard ways to<br>represent a fix can be used for this<br>element (fix name, lat/long, or fix-<br>radial-distance), including the<br>standard airport designators.|AB<br>DFW<br>KDFW<br>SHP090015<br>ATOKA300040<br>3500N/04000W|No|
|flight/operator/operatingOr<br>ganization/organization/@n<br>ame|FDPS_Flight<br>Operator/O<br>PRIndicator|Attribute used to specify the full official<br>name of the State, Organization,<br>Authority,aircraft operatingagency,|ff:TextNameType|No<br>xs:string|UAL|No|

315

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HT_FIXM]**|**Name**<br>**[HT]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
||_918f|handling agency engaged in or offering uto<br>engage in aircraft operation.|||||
|flight/@system|propSourceS<br>ystem|This attribute indicates which SFDPS<br>system generated the message.|fb:Provenan<br>ceSystemTy<br>pe|No<br>xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTi<br>me|This attribute conatins the time at which<br>the message was received by SFDPS.|ff:TimeType|No<br>xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the code of the<br>ARTCC (or<br>FIR) that produced the data.|fb:Provenan<br>ceCentreTyp<br>e|No<br>xs:string|`ZAU`|Yes|
|flight/arrival/runwayPosition<br>AndTime/runwayTime/[esti<br>mated|actual]/@time|arrivalTime|This attribute specifies the proposed or the<br>actual time of arrival at destination, set<br>according to the flight state.|ff:TimeType|No<br>xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/departure/runwayPosi<br>tionAndTime/runwayTime/[<br>actual|estimated]/@time|departureTi<br>me|This element specifies the proposed or<br>actual departure time, set according to the<br>flight state.|ff:TimeType|No<br>xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/flightStatus/@fdpsFlig<br>htStatus|flightState|This attribute contains the current status<br>of the flight as specified by SFDPS.|nas:SfdpsFlight<br>StatusType|Yes<br>xs:string<br>“PROPOSED|ACTIVE|COMPLETED|C<br>ANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/ad<br>ditionalFlightInformation/na<br>meValue/@name<br>flight/supplementalData/ad<br>ditionalFlightInformation/na<br>meValue/@value|fdpsGufi|The name value pair specifies the SFDPS<br>GUFI, an identifier on every message that<br>positively identifies what flight the<br>message is for.|fb:FreeTextTyp<br>e|No<br>xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-z0-<br>9/]+"|name="FDPS_GUFI"<br>value="us.fdps.2015-12-<br>18T16:59:10Z.000/14/10<br>0"/>|Yes|
|flight/flightPlan/@identifier|eramGufi_3<br>16a|This attribute specifies the unique flight<br>plan identifier.|fb:FreeTextTyp<br>e|No<br>xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|

316

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HT_FIXM]**|**Name**<br>**[HT]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|
|flight/gufi|uuidGufi|This element contains a reference that<br>uniquely identifies a flight and that is<br>independent of any particular system. This<br>reference conforms to the Universal<br>Unique Identifier standard.|fb:GloballyFligh<br>tIdentifierType|xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-4[0-<br>9a-fA-F]{3}\-[89aAbB][0-9a-fA-F]{3}\-<br>[0-9a-fA-F]{12}"|4aaf92be-ac0a-4dba-<br>998f-9e56f5d450b6|Yes|
|flight/flightIdentification/@a<br>ircraftIdentification|flightId_02a|Name used by Air Traffic Services units to<br>identify and communicate with an aircraft.|fb:FlightIdentifier<br>Type|No<br>"[A-Z0-9]{7}"|AAL20|Yes|
|flight/supplementalData/ad<br>ditionalFlightInformation/na<br>meValue/@name<br>flight/supplementalData/ad<br>ditionalFlightInformation/na<br>meValue/@value|flightId_02a|The flight supplemental data is used to<br>indicate that a flight message is a test<br>message, by setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the attribute<br>_value_to “**true**”.|@_name:_<br>_@value_:<br>_fb:FreeTextType_|No<br>_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|No|
|flight/flightIdentification/@c<br>omputerId|computerId<br>_02d|A unique identification assigned by ERAM<br>to each flight plan.|fb:FreeTextType|No<br>"([0-9][A-HJ-NP-Z0-9]{2})|<br>([0-9]{2}[A-HJ-NP-Z0-9])"<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of the<br>letters I and O, such as ddd, ddL, dLd,<br>dLL.|020|No|
|flight/flightIdentification/@s<br>iteSpecificPlanId|sspId_167a|Site Specific Plan Identifier. It is assigned<br>by Instrument Flight Procedures<br>Automation (IFPA) to uniquely identify a<br>flight plan in each ERAM facility.|fb:CountType|No<br>"\d{1,4}"<br>One to four-digits.|24|No|
|flight/enRoute/pointout/ori<br>ginatingUnit/@unitIdentifier|sourceSecto<br>rRouting_13<br>4b|This element contains the identifier of the<br>Air Traffic Control unit originating the Point<br>Out.|ff:AtcUnitNameT<br>ype|No<br>“([A-Z]{4})|([A-Za-z0-9]{1, })”|ZCH|No|
|flight/enRoute/pointout/ori<br>ginatingUnit/@sectorIdentifi|sourceSecto<br>rRouting_13|This element contains the entering sector<br>number for a Point Out action.|fb:FreeStringType|No<br>“\d[A-Z0-9]”<br>The format is one digit followed by|1W|No|

317

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[HT_FIXM]**|**Name**<br>**[HT]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissible Values**||**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|er|4b|||one alphanumeric.||||
|flight/enRoute/pointout/rec<br>eivingUnit/@unitIdentifier|targetSector<br>_16g|This element contains an adjacent center<br>sector number for that center or an<br>internal ERAM sector number.|ff:AtcUnitNameT<br>ype|No<br>“([A-Z]{4})|([A-Za-z0-9]{1, })”|ZCH||No|
|flight/enRoute/pointout/rec<br>eivingUnit/@sectorIdentifier|targetSector<br>_16g|This element contains the sector number<br>of an adjacent sector receiving the point<br>out.|fb:FreeStringType|No<br>“\d[A-Z0-9]”|1W||No|

##### **5.5.1.74 Inbound Point Out Information [PT] – Data Elements**

|**Element Name**<br>**[PT]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where the<br>first 6 digits are the UTC<br>time (23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of the<br>message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents 23:59:35<br>UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of<br>the sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|

318

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[PT]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**||**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**||Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O.**|**020**||Yes|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**||No|
|controllingFacility_138<br>a|This element contains the facility<br>that is controlling the flight.|string|No|**“[A-Z]{3}”**<br>The format consists of three letters.<br>Value is three blank characters if<br>identification of the controlling facility is<br>not available.|ZCH||Yes|
|controllingSector_138<br>b|This element contains the<br>controlling ARTS position or the<br>controlling ERAM ARTCC sector<br>number. The Controlling Sector is<br>the sector/position that is<br>controlling the flight. The value is<br>00 if identification of the<br>controlling sector is not available.|string|No|**“\d[A-Z0-9]”**<br>The format is one digit followed by one<br>alphanumeric.|1W||Yes|
|receivingFacility_139a|This element contains the facility<br>that is receiving the flight.|string|No|**“[A-Z]{3}”**<br>The format is three letters.<br>Value is three blank characters if<br>identification of the controlling facility is<br>not available.|AIA||Yes|
|receivingSector_139b|This element contains the receiving<br>ERAM ARTCC sector number in the<br>_PT_message. The receiving sector is<br>the sector/position that is receiving|string|No|**“[0-9]{2}”**<br>The format consists of two digits.|74||Yes|

319

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[PT]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||the flight. The value is 00 if<br>identification of the receiving<br>sector is not available.<br>_Note_: When used in the TH or OH<br>messages, this element contains<br>the receiving ERAM ARTCC sector<br>number, or the ARTS IIII<br>Receiving Position.||||||

##### **5.5.1.75 Inbound Point Out Information [PT] - Diagram**

##### **5.5.1.76 Inbound Point Out Information Message in FIXM [PT_FIXM] – Data Elements**

- The following elements of the PT message in Simple XML format are not translated in the FIXM format of the message: • sourceId_00e

320

NAS-JMSDD-4309-001 Rev C July 10, 2018

- sourceTime_00e1

- sourceSeqNo_00e2

|**Name**<br>**[PT_FIXM]**|**Name**<br>**[PT]**|**Element Definition**|**Type**|**Co**<br>**mp**<br>**lex**<br>**?**<br>**Format/Permissible**<br>**Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|
|flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@name<br>flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@value|FDPS_SequenceNo|Sequence number assigned by<br>SFDPS to each message it<br>receives from HADDS. The<br>attribute_name_includes the<br>constant string<br>"MSG_SEQ_NO", and the<br>attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No<br>@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeIntege<br>r<br>xs:maxInclusive<br>value="999999999"|@name="MSG_SEQ_N<br>O"<br>@value="6860416"|Yes|
|flight/departure/@departurePoi<br>nt|FDPS_Origin/departur<br>ePoint_26a|Attribute used to specify the<br>first point or other initial<br>entity where the air traffic<br>control/management system<br>route starts.|fb:FreeTextType|No<br>xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-**<br>**Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard<br>ways to represent a<br>fix can be used for<br>this element (fix<br>name, lat/long, or fix-<br>radial-distance),<br>including the<br>standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arrivalPoint|FDPS_DestId/destinati<br>on_27a|The final point or other final<br>entity where the air traffic<br>control/management system<br>route terminates.|fb:FreeTextType|No<br>xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-**|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|

321

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**|**Name**|**Element Definition**|**Type**|**Co**<br>**Format/Permissible**<br>|**Example**|**Req**<br>|
|---|---|---|---|---|---|---|
|**[PT_FIXM]**|**[PT]**|||**mp**<br>**lex**<br>**?**<br>**Values**||**uire**<br>**d?**|
|||||**Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard<br>ways to represent a<br>fix can be used for<br>this element (fix<br>name, lat/long, or fix-<br>radial-distance),<br>including the<br>standard airport<br>designators.|||
|flight/operator/operatingOrganiz<br>ation/organization/@name<br><br>|FDPS_FlightOperator/<br>OPRIndicator_918f|Attribute used to specify the<br>full official name of the State,<br>Organization, Authority,<br>aircraft operating agency,<br>handling agency engaged in or<br>offering to engage in aircraft<br>operation.|ff:TextNameType|No<br>xs:string|UAL|No|
|flight/@system<br>|propSourceSystem|This attribute indicates which<br>SFDPS system generated the<br>message.|fb:ProvenanceSyste<br>mType|No<br>xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp<br>|propRcvdTime|This attribute conatins the<br>time at which the message was<br>received by SFDPS.|ff:TimeType|No<br>xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre<br>|center|This attribute specifies the<br>code of the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCentr<br>eType|No<br>xs:string|`ZAU`|Yes|
|flight/arrival/runwayPositionAnd<br>Time/runwayTime/[estimated|a<br>ctual]/@time<br>|arrivalTime|This attribute specifies the<br>proposed or the actual time of<br>arrival at destination, set<br>according to the flight state.|ff:TimeType|No<br>xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/departure/runwayPosition<br>AndTime/runwayTime/[actual|e<br>stimated]/@time<br>|departureTime|This element specifies the<br>proposed or actual departure<br>time,set accordingto the|ff:TimeType|No<br>xs:dateTime|2014-06-20T20:17:52|Yes|

322

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[PT_FIXM]**|**Name**<br>**[PT]**|**Element Definition**|**Type**|**Co**<br>**mp**<br>**lex**<br>**?**<br>**Format/Permissible**<br>**Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|
|||flight state.|||||
|flight/flightStatus/@fdpsFlightSt<br>atus|flightState|This attribute contains the<br>current status of the flight as<br>specified by SFDPS.|nas:SfdpsFlightStatu<br>sType|Yes xs:string<br>“PROPOSED|ACTIVE|<br>COMPLETED|CANCEL<br>LED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@name<br>flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@value|fdpsGufi|The name value pair specifies<br>the SFDPS GUFI, an identifier<br>on every message that<br>positively identifies what flight<br>the message is for.|fb:FreeTextType|No<br>xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-<br>\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2<br>}Z\.[A-Za-z0-9/]+"|name="FDPS_GUFI"<br>value="us.fdps.2015-<br>12-<br>18T16:59:10Z.000/14/1<br>00"/>|Yes|
|flight/flightPlan/@identifier|eramGufi_316a|This attribute specifies the<br>unique flight plan identifier.|fb:FreeTextType|No<br>xs:string<br>"[A-Z]{2}\d{5}[1-<br>7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|This element contains a<br>reference that uniquely<br>identifies a flight and that is<br>independent of any particular<br>system. This reference<br>conforms to the Universal<br>Unique Identifier standard.|fb:GloballyFlightIden<br>tifierType|xs:string<br>"[0-9a-fA-F]{8}\-[0-<br>9a-fA-F]{4}\-4[0-9a-<br>fA-F]{3}\-[89aAbB][0-<br>9a-fA-F]{3}\-[0-9a-fA-<br>F]{12}"|4aaf92be-ac0a-4dba-<br>998f-9e56f5d450b6|Yes|
|flight/flightIdentification/@aircr<br>aftIdentification|flightId_02a|Name used by Air Traffic<br>Services units to identify and<br>communicate with an aircraft.|fb:FlightIdentifierTy<br>pe|No<br>**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additio<br>nalFlightInformation/nameValue<br>/@name<br>flight/supplementalData/additio<br>nalFlightInformation/nameValue||The flight supplemental data is<br>used to indicate that a flight<br>message is a test message, by<br>setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the|@_name:_<br>_@value_:<br>fb:FreeTextType|No<br>_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**|@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|No|

323

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**|**Name**|**Element Definition**|**Type**|**Co**<br>**Format/Permissible**<br>|**Example**|**Req**<br>|
|---|---|---|---|---|---|---|
|**[PT_FIXM]**|**[PT]**|||**mp**<br>**lex**<br>**?**<br>**Values**||**uire**<br>**d?**|
|/@value||attribute_value_to “**true**”.||**minLength=1,**<br>**maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT**<br>**”**<br>@value =**“true”**|||
|flight/flightIdentification/@com<br>puterId|computerId_02d|A unique identification<br>assigned by ERAM to each<br>flight plan.|fb:FreeTextType|No<br>**"([0-9][A-HJ-NP-Z0-**<br>**9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-**<br>**9])"**<br>The element includes<br>a digit, followed by<br>two alphanumeric<br>characters with the<br>exception of the<br>letters**I**and**O**, such<br>as_ddd, ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/@siteS<br>pecificPlanId|sspId_167a|Site Specific Plan Identifier. It<br>is assigned by Instrument<br>Flight Procedures Automation<br>(IFPA) to uniquely identify a<br>flight plan in each ERAM<br>facility.|fb:CountType|No<br>**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/controllingUnit/@unitIden<br>tifier|controllingFacility_138<br>a|This element specifies the<br>identifier of the Air Traffic<br>Control unit in control of the<br>aircraft.|ff:AtcUnitNameType|No<br>**“([A-Z]{4})|([A-Za-z0-**<br>**9]{1, })”**|ZCH|No|
|flight/controllingUnit/@sectorId<br>entifier|controllingSector_138<br>b|This element specifies sector<br>number of the Air Traffic<br>Control sector in control of the<br>aircraft.|fb:FreeStringType|No<br>**“\d[A-Z0-9]”**<br>The format is one<br>digit followed by one<br>alphanumeric.|1W|No|
|flight/enRoute/boundaryCrossin<br>gs/handoff/receivingUnit/@unitI|receivingFacility_139a|This element specifies the Air<br>Traffic Control unit receiving|ff:AtcUnitNameType|No<br>**“([A-Z]{4})|([A-Za-z0-**<br>**9]{****_1,_ })”**|AIA|No|

324

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[PT_FIXM]**|**Name**<br>**[PT]**|**Element Definition**|**Type**|**Co**<br>**mp**<br>**lex**<br>**?**<br>**Format/Permissible**<br>**Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|
|dentifier||control of the aircraft as a<br>result of a handoff.|||||
|flight/enRoute/boundaryCrossin<br>gs/handoff/receivingUnit/@sect<br>orIdentifier|receivingSector_139b|This element specifies the ATC<br>sector receiving control of the<br>aircraft as a result of a<br>handoff.|fb:FreeStringType|No<br>**“[0-9][A-Z0-9]”**<br>The format is one<br>digit followed by one<br>alphanumeric.|1W|No|

##### **5.5.1.77 Handoff Status [OH] – Data Elements**

|**Element Name**<br>**[OH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where the<br>first 6 digits are the UTC<br>time (23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of the<br>message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents 23:59:35<br>UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character|**AAL20**|Yes|

325

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[OH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||followed by one to six alphanumeric<br>characters.|||
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**, as<br>specified by the pattern above.|**020**|Yes|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely identify<br>a flight plan in each ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|
|controllingFacility_138a|This element contains the facility<br>that is controlling the flight.|string|No|**“[A-Z]{3}”**<br>The format consists of three letters.<br>Value is three blank characters if<br>identification of the controlling facility is<br>not available.|ZCH|No|
|controllingSector_138b|This element contains the controlling<br>ARTS position or the controlling<br>ERAM ARTCC sector number. The<br>Controlling Sector is the<br>sector/position that is controlling the<br>flight. The value is 00 if identification<br>of the controlling sector is not<br>available.|string|No|**“\d[A-Z0-9]”**<br>The format is one digit followed by one<br>alphanumeric.|1W|Yes|
|receivingFacility_139a|This element contains the facility<br>that is receiving the flight.|string|No|**“[A-Z]{3}”**<br>The format is three letters.<br>Value is three blank characters if<br>identification of the controlling facility is<br>not available.|AIA|No|
|receivingSector_139b|This element contains the ARTS IIII<br>Receiving Position, or the receiving<br>ERAM ARTCC sector number.<br>The value is 00 if the identification of<br>the receiving sector is not available.|string|No|**“[0-9][A-Z0-9]”**<br>The format is one digit followed by one<br>alphanumeric character.|Facility position in<br>Houston ARTS:<br>IN<br>The receiving ERAM<br>ARTCC sector number:|Yes|

326

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[OH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||||||**74**||
|acceptingFacility_334a|This element contains the accepting<br>facility identifier. The accepting<br>facility is the facility receiving the<br>flight when the handoff was<br>initiated. Data in this field indicates<br>that a handoff is accepted.|string|No|**“[A-Z]{3}”**<br>The format consists of three letters.|ZCA|No|
|acceptingSector_335a|This element contains the accepting<br>sector data. The accepting sector is<br>the receiving sector/position that<br>accepts the flight in handoff status.<br>Element_acceptingSector_335a_is<br>the same as element<br>_receivingSector_139b_.|string|No|**“[0-9][A-Z0-9]”**<br>The format is one digit followed by one<br>alphanumeric character.<br>|1B<br>49|No|
|handoffEventIndicator_336<br>a|This element contains the handoff<br>event indicator. The possible values<br>and their meanings are:<br>I – initiation<br>A – acceptance<br>R – retraction<br>T – take control<br>U – update<br>F – failure|string|No|**“[IARTUF]”**<br>One of the letters above.|I<br>A|Yes|

327

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.78 Handoff Status [OH] – Diagram**

##### **5.5.1.79 Handoff Status Message in FIXM Format [OH_FIXM] – Data Elements**

The following elements of the HV message in Simple XML format are not used in the FIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

328

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[OH_FIXM]**|**Name**<br>**[OH]**|**Definition**|**Type**|**Comp**<br>**lex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalD<br>ata/additionalFlightIn<br>formation/nameValue<br>/@name<br>flight/supplementalD<br>ata/additionalFlightIn<br>formation/nameValue<br>/@value|FDPS_SequenceN<br>o|Sequence number assigned by SFDPS<br>to each message it receives from<br>HADDS. The attribute_name_includes<br>the constant string"MSG_SEQ_NO",<br>and the attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|@name="MSG_SEQ_NO"<br>@value="6860416"|Yes|
|flight/departure/@de<br>parturePoint|FDPS_Origin/dep<br>arturePoint_26a|Attribute used to specify the first<br>point or other initial entity where the<br>air traffic control/management<br>system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-**<br>**Z]?)”**<br>Any of the standard<br>ways to represent a fix<br>can be used for this<br>element (fix name,<br>lat/long, or fix-radial-<br>distance), including the<br>standard airport<br>designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|
|flight/arrival/@arrival<br>Point|FDPS_DestId/dest<br>ination_27a|The final point or other final entity<br>where the air traffic<br>control/management system route<br>terminates.|fb:FreeTextType|No|xs:string<br>minLength=2,<br>maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-**<br>**Z]?)”**<br>Any of the standard<br>ways to represent a fix<br>can be used for this<br>element (fix name,<br>lat/long, or fix-radial-<br>distance),includingthe|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300040**<br>**3500N/04000W**|No|

329

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[OH_FIXM]**|**Name**<br>**[OH]**|**Definition**|**Type**|**Comp**<br>**lex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
||||||standard airport<br>designators.|||
|flight/operator/opera<br>tingOrganization/orga<br>nization/@name|FDPS_FlightOpera<br>tor/OPRIndicator<br>_918f|Attribute used to specify the full<br>official name of the State,<br>Organization, Authority, aircraft<br>operating agency, handling agency<br>engaged in or offering to engage in<br>aircraft operation.|ff:TextNameType|No|xs:string|UAL|No|
|flight/@system|propSourceSyste<br>m|This attribute indicates which SFDPS<br>system generated the message.|fb:ProvenanceSystem<br>Type|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdTime|This attribute conatins the time at<br>which the message was received by<br>SFDPS.|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:02.028Z|Yes|
|flight/@centre|center|This attribute specifies the code of the<br>ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCentreT<br>ype|No|xs:string|`ZAU`|Yes|
|flight/arrival/runwayP<br>ositionAndTime/runw<br>ayTime/[estimated|a<br>ctual]/@time|arrivalTime|This attribute specifies the proposed<br>or the actual time of arrival at<br>destination, set according to the flight<br>state.|ff:TimeType|No|xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/departure/runw<br>ayPositionAndTime/r<br>unwayTime/[actual|e<br>stimated]/@time|departureTime|This element specifies the proposed<br>or actual departure time, set<br>according to the flight state.|ff:TimeType|No|xs:dateTime|2014-06-20T20:17:52|Yes|
|flight/flightStatus/@f<br>dpsFlightStatus|flightState|This attribute contains the current<br>status of the flight as specified by<br>SFDPS.|nas:SfdpsFlightStatusT<br>ype|Yes|xs:string<br>“PROPOSED|ACTIVE|CO<br>MPLETED|CANCELLED|<br>DROPPED”|ACTIVE|Yes|
|flight/supplementalD<br>ata/additionalFlightIn<br>formation/nameValue|fdpsGufi|The name value pair specifies the<br>SFDPS GUFI, an identifier on every<br>message that positively identifies|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"|name="FDPS_GUFI"<br>value="us.fdps.2015-12-<br>18T16:59:10Z.000/14/100|Yes|

330

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[OH_FIXM]**|**Name**<br>**[OH]**|**Definition**|**Type**|**Comp**<br>**lex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|/@name<br>flight/supplementalD<br>ata/additionalFlightIn<br>formation/nameValue<br>/@value||what flight the message is for.|||@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z<br>\.[A-Za-z0-9/]+"|"/>||
|flight/flightPlan/@ide<br>ntifier|eramGufi_316a|This attribute specifies the unique<br>flight plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378100"|No|
|flight/gufi|uuidGufi|This element contains a reference that<br>uniquely identifies a flight and that is<br>independent of any particular system.<br>This reference conforms to the<br>Universal Unique Identifier standard.|fb:GloballyFlightIdenti<br>fierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-<br>fA-F]{4}\-4[0-9a-fA-<br>F]{3}\-[89aAbB][0-9a-fA-<br>F]{3}\-[0-9a-fA-F]{12}"|4aaf92be-ac0a-4dba-<br>998f-9e56f5d450b6|Yes|
|flight/flightIdentificati<br>on/@aircraftIdentific<br>ation|flightId_02a|Name used by Air Traffic Services<br>units to identify and communicate<br>with an aircraft.|fb:FlightIdentifierType|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalD<br>ata/additionalFlightIn<br>formation/nameValue<br>/@name<br>flight/supplementalD<br>ata/additionalFlightIn<br>formation/nameValue<br>/@value||The flight supplemental data is used<br>to indicate that a flight message is a<br>test message, by setting the attribute<br>_name_to “**SIMULATED_FLIGHT**” and<br>the attribute_value_to “**true**”.|@_name:_<br>_@value_:<br>fb:FreeTextType|No|_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>_@value:_<br>**xs:string**<br>**minLength=1,**<br>**maxLength=100**<br>@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|@name =<br>**“SIMULATED_FLIGHT”**<br>@value =**“true”**|No|
|flight/flightIdentificati<br>on/@computerId|computerId_02d|A unique identification assigned by<br>ERAM to each flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-**<br>**9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-**<br>**9])"**<br>The element includes a<br>digit,followed bytwo|**020**|No|

331

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[OH_FIXM]**|**Name**<br>**[OH]**|**Definition**|**Type**|**Comp**<br>**lex?**|**Format/Permissible**<br>**Values**||**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|---|
||||||alphanumeric<br>characters with the<br>exception of the letters<br>**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.||||
|flight/flightIdentificati<br>on/@siteSpecificPlanI<br>d|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by Instrument Flight<br>Procedures Automation (IFPA) to<br>uniquely identify a flight plan in each<br>ERAM facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**||No|
|flight/controllingUnit/<br>@unitIdentifier|controllingFacility<br>_138a|This element specifies the identifier of<br>the Air Traffic Control unit in control<br>of the aircraft.|ff:AtcUnitNameType|No|**“([A-Z]{4})|([A-Za-z0-**<br>**9]{1, })”**|ZCH||No|
|flight/controllingUnit/<br>@sectorIdentifier|controllingSector<br>_138b|This element specifies sector number<br>of the Air Traffic Control sector in<br>control of the aircraft.|fb:FreeStringType|No|**“\d[A-Z0-9]”**<br>The format is one digit<br>followed by one<br>alphanumeric.|1W||No|
|flight/enRoute/bound<br>aryCrossings/handoff/<br>receivingUnit/@unitId<br>entifier|receivingFacility_<br>139a|This element specifies the Air Traffic<br>Control unit receiving control of the<br>aircraft as a result of a handoff.|ff:AtcUnitNameType|No|**“([A-Z]{4})|([A-Za-z0-**<br>**9]{1,})”**|AIA||No|
|flight/enRoute/bound<br>aryCrossings/handoff/<br>receivingUnit/@secto<br>rIdentifier|receivingSector_1<br>39b|This element specifies the ATC sector<br>receiving control of the aircraft as a<br>result of a handoff.|fb:FreeStringType|No|**“[0-9][A-Z0-9]”**<br>The format is one digit<br>followed by one<br>alphanumeric.|1W||No|
|flight/enRoute/bound<br>aryCrossings/handoff/<br>acceptingUnit/@unitI<br>dentifier|acceptingFacility_<br>334a|This element contains the accepting<br>facility identifier. The accepting facility<br>is the facility receiving the flight when<br>the handoff was initiated. Data in this<br>field indicates that a handoff is<br>accepted.|ff:AtcUnitNameType|No|**“([A-Z]{4})|([A-Za-z0-**<br>**9]{1, })”**|ZCH||No|
|flight/enRoute/bound<br>aryCrossings/handoff/<br>acceptingUnit/@sect|acceptingSector_<br>335a|This element contains the accepting<br>sector data. The accepting sector is<br>the receivingsector that accepts the|fb:FreeStringType|No|**“[0-9][A-Z0-9]”**|1B<br>49||No|

332

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[OH_FIXM]**|**Name**<br>**[OH]**|**Definition**|**Type**|**Comp**<br>**lex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|orIdentifier||flight in handoff status.||||||
|flight/enRoute/bound<br>aryCrossings/handoff/<br>@event|handoffEventIndi<br>cator_336a|This element contains the handoff<br>status.|nas:NasHandoffEventT<br>ype|No|**“INITIATION|ACCEPTAN**<br>**CE|RETRACTION|TAKE_**<br>**CONTROL|UPDATE|FAI**<br>**LURE”**|**ACCEPTANCE**|Yes|

##### **5.5.1.80 Flight Plan Reconstitution [DBRTFPI] – Data Elements**

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|computerId_02d|ERAM Computer Identification (Computer<br>ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by two<br>alphanumeric characters with the exception of<br>the letters**I**and**O**, such as_ddd, ddL, dLd, dLL_.|**020**|No|
|flightId_02a|Aircraft ID, or flight ID (also called Call<br>Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character followed<br>by one to six alphanumeric characters.|**AAL20**|Yes|
|eramGufi_316a|GUFI that uniquely identifies each flight in<br>the system.|string|No|**"[A-Z]{2}\d{5}[1-7]\d{2}"**<br>This element includes<br>10 alphanumeric characters:<br>-ICAO country code (one letter);<br>-en-route facility ID (one letter);<br>-time in seconds  of current day (five digits in<br>the range 00000-86400);<br>-sequence number (two digits).|**KB5980017**|No|
|sspId_167a|Site Specific Plan Identifier. It is assigned<br>by IFPA to uniquely identify a flight plan in<br>each ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|

333

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|numberOfAircraft_03a|This element includes the number of<br>aircraft for the flight followed optionally by<br>the Special Aircraft Indicator.|string|No|**"\d{0,2}[A-Z]?"**<br>The element consists of zero to two digits<br>optionally followed by one uppercase letter to<br>represent the Special Aircraft Indicator. The<br>indicator can also appear on its own (without<br>the leading digits).|**3H**<br>The<br>number of<br>aircraft is 3<br>and the<br>special<br>aircraft<br>indicator is<br>**H**for Heavy<br>Jet.|<br>No|
|typeOfAircraft_03c|Type of aircraft.|string|No|**"[A-Z][A-Z0-9]{1,3}"**<br>The element consists of one letter followed by<br>one to three alphanumeric characters.|**B747**|Yes|
|airborneEquip_03e|Airborne equipment qualifier. It consists of<br>one alphanumeric character.|string|No|**"[A-Z]"**<br>The element consists of one alphanumeric<br>character, that can have one of the following<br>values:<br>**A**- Transponder with no Mode C<br>**B**- Transponder with Mode C<br>**E**– FMS with DME/DME and IRU position<br>updating<br>**G**– GNSS, including GPS or WAAS, with en-<br>route and terminal capability<br>**X**– No transponder<br>**W**- RVSM|**E**|No|
|beaconCode_04a|Beacon code.<br>**_Note_**: As of SFDPS 1.3.1, if the flightState<br>element has a value of ‘Canceled’ or<br>‘Proposed’, this element is only present in<br>the version of a message with<br>FDPS_Restricted=’R’|string|No|**"[0-7]{4}"**<br>The element includes four octal digits (i.e. 0-<br>7). When the last two digits of the four digits<br>are zero, the beacon code is a non-discrete<br>code.<br>A discrete code is any code not ending in 00.|Non-<br>discrete<br>VFR code:<br> **2101**|No|
|trueAirSpeed_05a|True airspeed expressed in knots.|string|No|**"\d{2,4}"**<br>The format is two to four digits, in the range<br>01 – 3700 knots.|**540**<br>Aircraft<br>true|Yes, if<br>neither<br>machSpeed_|

334

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||Aircraft speed is required to be specified by<br>using one of the three possible elements:<br>trueAirSpeed_05a, machSpeed_05c or<br>classifiedSpeed_05d.|airspeed is<br>54,000<br>knots.|05c nor<br>classifiedSpe<br>ed_05d are<br>included in<br>the message.|
|machSpeed_05c|Mach speed.|string|No|**“M\d{3}”**<br>The letter**M**followed by three digits. The<br>maximum value is M500.|The speed<br>0.85 Mach<br>is<br>represente<br>d as**M085**.|Yes, if<br>neither<br>trueAirSpeed<br>_05a nor<br>classifiedSpe<br>ed_05dare<br>included in<br>the message.|
|classifiedSpeed_05d|Adapted classified speed. It is not printed<br>on flight strips.|string|No|**“SC”**|This<br>element<br>may only<br>include the<br>string<br>character<br>**SC**.|Yes, if<br>neither<br>trueAirSpeed<br>_05a nor<br>machSpeed_<br>05c are<br>included in<br>the message.|
|coordFix_06a|The Coordination fix represents the<br>starting point to begin processing the<br>flight plan route from one of the following<br>points: the departure airport, the airfile fix<br>or the adjacent center inbound<br>coordination fix. For ARTS III flight plans<br>the coordination fix Field 06 is used as the<br>inbound coordination fix or the outbound<br>coordination fix or, for an ARTS internal<br>flight, it can be the departure or<br>destination airport.|string|No|**“([A-Z0-9]{2,5})|**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)|**<br>**([A-Z0-9]{3,4}}"**<br>This element can have one of the following<br>formats:<br>Two to five alphanumeric characters for a fix<br>name.<br>The fix name as above followed by six digits,<br>for a fix radial distance.<br>Four digits followed by an optional alphabetic<br>character, followed by a virgule (‘/’), followed<br>by four to five digits followed by an optional<br>alphanumeric character for a lat/long.<br>Three to four alphanumeric characters for|**AB**<br>**DFW**<br>**KDFW**<br>**AB200010**<br>**SHP090015**<br>**ATOKA300**<br>**040**<br>**3500/0400**<br>**0**<br>**3500N/040**<br>**00W**|Yes|

335

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||aLOCID.|||
|coordStatusTime_07d|Coordination time that represents the<br>starting time in hours and minutes at the<br>coordination fix.|string|No|**"((A|D|E|P|F)[0-1][0-9][0-5][0-9) |**<br>**((A|D|E|P|F)2[0-3][0-5][0-9])”**<br>The element includes one letter (possible<br>values are**A**,**D, E**,**P**, or**F**) followed by four<br>digits that represent time as_hhmm_.|**P1020**|Yes|
|coordStatus_07d1|The coordStatus field is the single letter**A**,<br>**D**,**E**,**F**, or**P**, as described for element<br>coordStatusTime_07d.|string|No|**“(A|D|E|P|F)”**|**F**|Yes|
|coordTime_07d2|Starting time at the coordination fix.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:5**<br>**2**|Yes|
|delayTime_07e|Delay time in expressed in minutes.|string|No|**“\d{3}”**<br>Three digits.|**030**|No|
|departureTime_243n|This element specifies the reported<br>(actual) departure time.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:5**<br>**2**|No|
|proposedDepartureTime<br>_2431|This element specifies the proposed<br>departure time.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:5**<br>**2**|No|
|estDepartureClearanceTi<br>me_2432|This element specifies the EDCT.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:27:5**<br>**2**|No|
|arrivalTime_28b|This element specifies the reported<br>(actual) arrival time.|dateTime|No|**dateTime**|**2014-06-**<br>**20T22:27:5**<br>**2**|No|
|assignedAlt_08a|Assigned altitude or flight level expressed<br>in hundreds of feet.<br>Onlyone of the altitude elements|string|No|**“(\d{2,3}) | VFR”**<br>The format consists of either two to three<br>digits,or the constant string **VFR**. Three digits|Assigned<br>altitude of<br>34,000|No|

336

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||assignedAlt_08a, assignedAlt_08b,<br>assignedAlt_08c, assignedAlt_08d,<br>assignedAlt_08e, assignedAlt_08f,<br>assignedAlt_08g, assignedAlt_08h may be<br>included in the message.|||are required for ARTS III, thus a leading zero<br>needs to be used when necessary.|feet:<br>**340**<br>Assigned<br>altitude<br>9,000 feet<br>ARTS III:<br>**090**||
|assignedAlt_08b|Fixed value of**OTP**which indicates VFR-<br>ON-Top. It specifies that the aircraft is<br>flying above the clouds in VFR conditions.|string|No|**“OTP”**|**OTP**|No|
|assignedAlt_08c|VFR-ON-Top with altitude. It represents an<br>IFR flight operating above the clouds in<br>VFR conditions at the specified assigned<br>altitude.|string|No|“**OTP/\d{2,3}**”<br>The format is the constant string**OTP**/<br>followed by two to three digits that represent<br>the assigned altitude in hundreds of feet.|Aircraft<br>flying VFR-<br>ON-Top at<br>25,000<br>feet:<br>**OTP/250**|No|
|assignedAlt_08d|The assigned block of altitudes for the<br>flight to fly at.|string|No|**"\d{2,3}B\d{2,3}"**<br>The format is two to three digits, followed by<br>the letter**B**, followed by two to three digits.<br>The leading and trailing two to three digits<br>define the block of altitudes in hundreds of<br>feet for the flight to fly at. The lowest altitude<br>must be listed first.|Assigned<br>altitude<br>block of<br>8,000 feet<br>to 14,000<br>feet:<br>**80B140**|No|
|assignedAlt_08e|Element used for IFR flights operating<br>above a specified altitude.|string|No|**“ABV/\d{2,3}"**<br>The format consists of the string**ABV/**<br>followed by two to three digits that represent<br>the altitude in hundreds of feet above which<br>the flight is flying.|Aircraft is<br>flying<br>above<br>60,000<br>feet.<br>**ABV/600**|No|
|assignedAlt_08f|Assigned Altitude/FIX/Altitude element<br>specifies the altitudes to and from a fix for<br>the flight to fly at.|string|No|**"(\d{2,3}/[A-Z0-9]{2,5}/\d{2,3})|**<br>**(\d{2,3}/[A-Z0-9]{2,5}\d{6}/\d{2,3}) |**<br>**(\d{2,3}/\d{4}[A-Z]?/\d{4,5}[A-Z]?/\d{2,3})"**<br>The altitudes are specified in hundreds of feet|**240/DAL35**<br>**0010/220**<br>Flight flies<br>at altitude|No|

337

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||in a two to three digit format. The fix is<br>specified using the same format as the<br>coordination fix element “coordFix_06a”.<br>The fix cannot be the departure or arrival<br>point.|24,000 feet<br>to the fix<br>radial<br>distance fix<br>and then<br>descend to<br>altitude<br>22,000<br>feet.||
|assignedAlt_08g|It is used to specify that the flight is flying<br>Visual Flight Rules (VFR). It can only have<br>the value**VFR**.|string|No|**“VFR”**|**VFR.**|No|
|assignedAlt_08h|It is used to specify that the flight is flying<br>VFR at a specified altitude.|string|No|**“VFR/\d{2,3}"**<br>The format consists of the string**VFR/**<br>followed by two to three digits that represent<br>an altitude in hundreds of feet.|**VFR/75**<br>The aircraft<br>is flying<br>VFR at<br>7,500 feet.|No|
|requestedAlt_09a|The element is used to specify requested<br>altitude or flight level in hundreds of feet.<br>Only one of the seven requested altitude<br>elements (requestedAlt_09a to<br>requestedAlt_08g) may be included in a<br>proposed flight message.|string|No|**“\d{2,3}"**<br>The format consists of two to three digits.<br>ARTS III requires three characters, with a<br>leading**0**when required (such as 090).|**340**<br>Aircraft is<br>requesting<br>to fly at<br>34,000 feet<br>altitude.|No|
|requestedAlt_09b|The element Requested Altitude format<br>OTP represents an IFR flight requesting to<br>operate above the clouds in VFR<br>conditions.<br>OTP stands for VFR-ON-Top.|string|No|**“OTP”**|The<br>element<br>has a fixed<br>value of<br>**OTP**.|No|
|requestedAlt_09c|The element “Requested Altitude format<br>OTP with altitude” represents a flight<br>requesting to operate VFR-ON-Top at the<br>requested altitude.<br>numberOfAircraft_03a.|string|No|**“OTP/\d{2,3}"**<br>The format consists of the string**OTP/**<br>followed by two to three digits that represent<br>the requested altitude in hundreds of feet.<br>ERAM onlysends ARTS III the requested|**OTP/250**<br>Flight is<br>requesting<br>to fly VFR-<br>ON-Top at|No|

338

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||altitude with a format of three digits  (leading<br>zeroes used when necessary, as in 090) and<br>places a special altitude indicator (**U**if Heavy<br>Jet) in element numberOfAircraft_03a.|25,000<br>feet.||
|requestedAlt_09d|Element used for an IFR flight requesting<br>to operate above a specified altitude.|string|No|“ABV/\d{2,3}"<br>The format consists of the string**ABV/**<br>followed by two to three digits that represent<br>the requested altitude in hundreds of feet.|**ABV/600**|No|
|requestedAlt_09e|Element used to specify a requested block<br>of altitudes or flight levels for the flight to<br>fly at. The altitudes are specified in<br>hundreds of feet.|string|No|**"\d{2,3}B\d{2,3}"**<br>The format consists of two to three digits for<br>the lowest altitude, followed by the letter**B**,<br>followed by two to three digits for the highest<br>altitude.|**250B260**<br>Flight is<br>requesting<br>to fly inside<br>an altitude<br>block<br>between<br>25,000 feet<br>and<br>260,000<br>feet.|No|
|requestedAlt_09f|This element is used when the aircraft is<br>requesting to fly VFR.|string|No|**“VFR”**<br>It can only include the fixed string “VFR”.<br>ERAM sends ARTS III the three characters and<br>also places a special altitude indicator**V**(not a<br>Heavy Jet) or**W**(if a Heavy Jet) in element<br>numberOfAircraft_03a.||No|
|requestedAlt_09g|The element used to represent a flight<br>requesting to fly VFR at a specified<br>altitude.|string|No|**“VFR/\d{2,3}"**<br>The format consists of the constant string<br>**VFR/**followed by two to three digits that<br>specify the requested altitude in hundreds of<br>feet.|**VFR/35**<br>Aircraft is<br>requesting<br>to fly VFR<br>at 3,500<br>feet|No|
|flightPlanRoute_10a|It specifies the trajectory followed by the<br>airplane from the departure point to the<br>arrival point, based on the fixes and routes<br>along that trajectory.|string|No|**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-9+\./]*\.[A-Z0-**<br>**9+/\*]{2,12}_?(/\d{4})?"**<br>The element format consists of a string that<br>includes fixes and routes along the trajectory<br>flown by the airplane. The fixes and routes are|OKC.V14S.T<br>UL.TUL090.<br>.FYV270.FY<br>V|Yes|

339

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||specified using the FIX.ROUTE.FIX format,<br>where either element can be implied, such as<br>FIX..FIX, or ROUTE..ROUTE.|||
|departurePoint_26a|It is used to specify the point at which to<br>start processing the flight plan route as<br>follows: the departure airport or the airfile<br>point.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a fix<br>can be used for this element (fix name,<br>lat/long, or fix-radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300**<br>**040**<br>**3500N/040**<br>**00W**|Yes|
|destination_27a|It is used to specify the point at which to<br>end processing the flight plan route.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to represent a fix<br>can be used for this element (fix name,<br>lat/long, or fix-radial-distance), including the<br>standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP090015**<br>**ATOKA300**<br>**040**<br>**3500N/040**<br>**00W**|Yes|
|ETE_2439|This element specifies the estimated time<br>en route (ETE).|duration|No||PT2H30M|No|
|ETA_28a|This element specifies the estimated time<br>of arrival at the flight plan destination.|dateTime|No|**dateTime**|**2014-06-**<br>**20T22:27:5**<br>**2**|No|
|remarks_11c|Flight plan remarks text.|string|No|**The string is from 1 to 400 characters in**<br>**length.**<br>It has an attribute called_remarktype_with the<br>possible values of interfacility or intrafacility.|**OAIR EVAC**<br>**AMG/N048**<br>**2F290**<br>**SQT/N0479**<br>**F310 JOL+**|No|
|holdDataFix_21a|This element specifies the position location<br>for the flight to hold along the filed route<br>of flight. If the message does not include|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**|**AB**<br>**KDFW**<br>**SHP090015**|No|

340

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||the optional_holdDataTime_21d_<br>element, the flight goes into an<br>indefinite hold status when the flight<br>arrives at the hold fix.|||Any of the valid fix formats can be used,<br>as described for_coordFix_06a_element.|**3500N/040**<br>**00W**||
|holdDataTime_21d|This element specifies the time the flight<br>can expect further clearance at the holding<br>location specified in the element<br>_holdDataFix_21a_. This element can only be<br>included in the HH messages if the element<br>_holdDataFix_21a_is also included.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:5**<br>**2**|No|
|progressReportFix_18a|This element specifies the position location<br>report of the flight along the filed route of<br>flight.|string|No|**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>It uses the standard fix formats, as specified<br>for the element_coordFix_06a_`.`|**AB**<br>**KDFW**<br>**SHP090015**|No|
|progressReportTime_18<br>d|This element specifies the time of the flight<br>arriving at the fix specified in element<br>_progressReportFix_18a_, above.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:5**<br>**2**|No|
|departureAutoRouteInhi<br>bitIndicator_244g|This element specifies whether the<br>departure route from the departure airport<br>is inhibited or not.|string|No|**“*”**|*****|No|
|destinationAutoRouteIn<br>hibitIndicator_244h|This element specifies whether the arrival<br>route to the arrival airport is inhibited or<br>not.|string|No|**“*”**|*****|No|
|interimAlt_76b|This element specifies the interim altitude<br>for the flight in hundreds of feet.|string|No|**"\d{1,3}"**<br>The format is one to three digits, in the range 0<br>to 999.|**240**<br>Aircraft<br>interim<br>altitude of<br>24,000<br>feet.|No|
|AARFld10_142e|This element includes the AAR preferential|string|No|**"[A-Z0-9\./]{4,97}"**|**./.BLEUZ.R**|No|

341

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||route in Field 10 format.<br>**Either this element or the element**<br>_AARNonFld10_142f_may be included in the<br>message.|||Field 10 format.|**YTHM3.**||
|AARNonFld10_142f|This element includes the AAR preferential<br>route in non-Field 10 format.<br>**Either this element or the element**<br>_AARFld10_142e_may be included in the<br>message.|string|No|**"[A-Z0-9\./\+&#x20;]{4,97}"**<br>A “+” delimiter precedes and follows the non-<br>Field10 elements.|**.J25.CRP+LI**<br>**SSE6+**<br>Notice the<br>non-<br>Field10<br>substring<br>that is<br>enclosed<br>between<br>“+”<br>characters.|No|
|ADRFld10_142c|Adapted ADR preferential route in Field 10<br>format.<br>**Either this element or the element**<br>_ADRNonFld10_142d_may be included in the<br>message.|string|No|**"[A-Z0-9\./\*]{4,84}"**<br>Field 10 format.|**.ALAMO6.**<br>**HENLY.J13**<br>**1.FUZ.J105.**|No|
|ADRNonFld10_142d|Adapted ADR preferential route in non-<br>Field 10 format.<br>**Either this element or the element**<br>_ADRFld10_142c_may be included in the<br>message.|string|No|**"[A-Z0-9\./\+&#x20;-]{4,84}"**<br>A “+” delimiter precedes and follows the non-<br>Field10 elements.|**+RV**<br>**J25+CRP.LI**<br>**SSE6**<br>Notice the<br>non-<br>Field10<br>substring<br>that is<br>enclosed<br>between<br>“+”<br>characters.|No|
|ADARFld10_142a|This element contains the adapted ADAR<br>preferential route in Field 10 format. The|string|No|**"[A-Z0-9\./]{4,44}"**<br>Field 10 format.|.PSX2.PSX.<br>V20.CRP.|No|

342

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||Preferential Route Alphanumerics are used<br>to control the flow and separation of traffic<br>departing and arriving at designated<br>airports. An ADAR has the complete<br>preferential routing from the departure<br>airport to the arrival airport.<br>**Either this element or the element**<br>_ADARNonFld10_142b_may be included in<br>the message.||||||
|ADARNonFld10_142b|This element contains the adapted ADAR<br>preferential route in non-Field 10 format. If<br>required for the flight and if the element<br>ADARFld10_142a is not included in the<br>message, the FH message contains this<br>element for the ADAR adapted route.<br>**Either this element or the element**<br>_ADARFld10_142a_may be included in the<br>message.|string|No|**"[A-Z0-9\./\+&#x20;]{4,44}"**<br>A “+” delimiter will precede and follow the<br>non-Field10 elements.|+LISSE6+<br>+TS1<br>MEM270<br>LIT050+|No|
|AARId_141c|If required for the flight, this element<br>specifies the AAR adapted arrival route<br>name.|string|No|**“\d{5}”**|PA001|No|
|ADRId_141b|If required for the flight, the Adapted<br>Route indicator format specifies the ADR<br>adapted departure route name.|string|No|**“\d{5}”**|PD001|No|
|ADARId_141a|If required for the flight, this element<br>specifies the ADAR departure arrival route<br>name.|string|No|**“\d{5}”**<br>The format consists of five alphanumeric<br>characters.|DA001|No|
|FPA_143a0|FPA containing the first postable fix (1<sup>st</sup>)|string|No|**“\d{4}”**|7601|No|
|FPA_143a1|FPA containing the first postable fix (2<sup>nd</sup>)|string|No|**“\d{4}”**|7601|No|
|FPA_143a2|FPA containing the first postable fix (3<sup>rd</sup>)|string|No|**“\d{4}”**|7601|No|
|FPA_143a3|FPA containing the first postable fix (4<sup>th</sup>)|string|No|**“\d{4}”**|7601|No|

343

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|FAV_143b0|The element specifies the FAV number<br>containing the first fix where the route<br>alteration occurs due to an AAR<br>application.|string|No|**“\d{4}”**<br>The format is four digits.|7601|No|
|FAV_143b1|The element specifies the FAV number<br>containing the second fix where the route<br>alteration occurs due to an AAR<br>application.|string|No|**“\d{4}”**<br>The format is four digits.|7601|No|
|FAV_143b2|The element specifies the FAV number<br>containing the third fix where the route<br>alteration occurs due to an AAR<br>application.|string|No|**“\d{4}”**<br>The format is four digits.|7601|No|
|FAV_143b3|The element specifies the FAV number<br>containing the fourth fix where the route<br>alteration occurs due to an AAR<br>application.|string|No|**“\d{4}”**<br>The format is four digits.|7601|No|
|timeBtw1stAndLastConv<br>ertedRouteFix_2449|The element specifies the time interval<br>between the first and last converted route<br>fix.|duration|No||PT30M<br>**The above**<br>**value**<br>**specifies a**<br>**period of**<br>**30 minutes**|No|
|flightRules_908a|This element specifies the flight rules as<br>one character as follows:<br>**I**= IFR<br>**V**= VFR<br>**Y**= IFR First<br>**Z**= VFR First|string|No|**“[IVYZ]”**<br>If**Y**or**Z**is used, the point or points at which a<br>change of flight rules is planned should be<br>shown in the route.|V|No|
|typeOfFlight_908b|This element specifies the type of flight<br>specified using one of the following<br>characters:<br>**S**= Scheduled air transport<br>**N**= Non-scheduled air transport<br>**G**= General Aviation<br>**M**= Military|string|No|**“[SNGMO]”**|N|No|

344

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||**O**= Other flights||||||
|wakeTurbulenceCat_909<br>c|This element specifies the wake<br>turbulence category as heavy, medium or<br>light.|string|No|**“[HML]”**<br>, where:<br>**H**= Heavy<br>**M**= Medium<br>**L =**Light|H<br>M<br>L|No|
|comNavApproachEquip_<br>910a|Airborne Equipment Qualifier: Radio<br>Communication, Navigation, and Approach<br>AID Equipment.|string|No|**"([A-M,O-Z]{1,25}) | N"**<br>This element has one required plus 24 optional<br>letters. The 25 possible letters are the letters**A**<br>through**Z**and each letter can only be used<br>once. If the letter**N**is present, it must be the<br>only letter present.|SCHJ<br>See ICAO<br>4444 for<br>the<br>complete<br>list of<br>characters.|No|
|survEquip_910b|This element represents the ICAO airborne<br>equipment qualifier.|string|No|**"[NACXPIS][D]?"**<br>The format consists of up to two letters. The<br>first letter must be one of the SSR equipment<br>letters and the second letter, if used, must be<br>the ADS capability letter**“D”**.<br>The valid values for the first letter and their<br>significance are:<br>**N**: Nil<br>**A**: Transponder Mode A<br>**C**: Transponder Mode A and C<br>**X**: Transponder Mode S without both aircraft ID<br>and pressure-altitude transmission<br>**P**: Transponder Mode S, with pressure-altitude<br>transmission but aircraft ID transmission<br>**I**: Transponder Mode S with aircraft ID<br>transmission but no pressure-altitude<br>transmission<br>**S**: Transponder Mode S with both pressure-<br>altitude and aircraft ID transmission<br>**D**: ADS capability|**SSR**<br>**equipment**<br>**as Mode S**<br>**with ADS**<br>**capability:**<br>SD|No|

345

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|altAero_916c|This element contains Alternate Arrival<br>Point(s) or Aerodrome(s), if any. More<br>than one alternate arrival points of<br>aerodromes may be specified.|string|No|**"([A-Z]{4}&#x20;?[A-Z]{0,4}) |**<br>**([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?) |**<br>**([A-Z0-9]{3,4})”**<br>The aerodrome is specified using the 4-letter<br>ICAO name or ZZZZ if no ICAO location indicator<br>has been allocated.<br>The arrival point format has to be one of the fix<br>formats described above (see coordFix_06a).<br>If two or more alternatives are included, they<br>may have any of the valid formats and they<br>have to be separated by blanks.|EBBR EDDL|No|
|FDB4thLineHeading_155<br>a|This element is used to display the heading<br>of the aircraft issued by the controller. Its<br>format is one to four alphanumeric<br>characters. Samples: 075, H075.|string|No|**“[A-Z0-9]{1,4}”**|**075**<br>**H075**|No|
|FDB4thLineSpeed_155b|This element is used to display the speed<br>of the aircraft issued by the controller.|string|No|**"[A-Z0-9+-\.]{1,4}"**<br>Minimum length = 1 character<br>Maximum length = 4 characters.|280+<br>S260<br>M83+<br>.75-|No|
|FDB4thLineText_155c|This element is used to display free-form<br>text issued by the controller.|string|No|**"[A-Z0-9+-=\*/_;\.,\|^v]{1,8}"**<br>The allowed characters are the alphanumeric<br>characters, −, +, =, *, /, underscore (_),<br>semicolon (;), period (.), and comma (,). No<br>leading or embedded spaces are allowed.<br>It can be one to eight characters long.|-BUFFI<br>NOBBL<br>BLVNS|No|
|externalBeaconCode_04<br>b|This element specifies the external<br>beacon. It contains the requested beacon<br>code when the flight plan is inbound from<br>an adjacent Center or an adjacent Non-U.S.<br>Automated Facility, the requested beacon<br>code is different from the assigned beacon<br>code,and the aircraft is not established on|string|No|**"[0-7]{4}"**<br>It has the same format as element<br>beaconCode_04a.|**3434**|No|

346

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||the assigned beacon code. Then, if the<br>facility is adapted to receive Field (04b),<br>Field 04b is transmitted.<br>**_Note_:** As of SFDPS 1.3.1, if the flightState<br>element has a value of ‘Canceled’ or<br>‘Proposed’, this element is only present in<br>the version of a message with<br>FDPS_Restricted=’R’||||||
|localIntendedRoute_10b|The Local Intended Route element contains<br>the flight plan route that is coordinated to<br>penetrated facilities. It consists of the flight<br>plan route with any expected-to-be-<br>applied-by-the-controlling-center ADRs,<br>ADARs or AARs already applied. It is<br>intended for the clients that wish to know<br>the expected state of the flight plan when<br>the current facility releases control of the<br>flight. Element localIntendedRoute_10b<br>contains the filed route (field 10a) merged<br>with any locally applicable adapted routes<br>(preferential routes, transition fixes and A-<br>line fixes). Optional Field 10b is sent to<br>ATM-IPOP, when Field 10b is not the same<br>as Field 10a.|string|No|**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-9+\./]*\.[A-Z0-**<br>**9+/\*]{2,12}_?(/\d{4})?"**<br>Minimum length = 3<br>Maximum length = 1000||No|
|timeRouteValues_2461|This element contains the time of the route<br>values.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:5**<br>**2**|No|
|fixTimes|This element specifies the fix and<br>calculated time of arrival at each fix that<br>describes the aircraft’s ERAM converted<br>route of flight.||Yes|Sequence of the elements_fixTime_68c,_<br>fix_68c1, and_crossingTime_68c2_.<br>It can be included between zero and 326<br>times.||No|
|fixTime_68c|This element contains a fix and the<br>expected time of arrival at the fix in hours<br>and minutes.|string|No|**"([A-Z0-9]{2,5}/\d{4}) |**<br>**([A-Z0-9]{2,5}\d{6}/\d{4}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?/\d{4}) "**|**LFT/1800**<br>**JIMIE0040**<br>**34/1320**|No|

347

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||The format consists of a valid representation<br>of a fix (see element coordFix_06a in the FH<br>message table), followed by a virgule, and<br>followed by time in_hhmm_format.<br>Minimum length = 7<br>Maximum length = 17|||
|fix_68c1|This element specifies the fix component<br>of the element_fixTime_68c_.|string|No|**“([A-Z0-9]{2,5})|**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)|**<br>**([A-Z0-9]{3,4}}"**<br>The format consists of a valid representation<br>of a fix (see element coordFix_06a in the FH<br>message table).|**KDFW**<br>**3500N/040**<br>**00W**|No|
|crossingTime_68c2|This element specifies the time<br>component of the element_fixTime_68c_.|dateTime|No|The format is_dateTime_, and not_hhmm_as it is<br>in the_fixTime_68c_element.|**2014-06-**<br>**20T20:17:5**<br>**2**|No|
|adjacentCenterRouting|It groups the elements<br>_outputRouting_253a_and_FAV_29d_.||Yes|It can be included between zero and 25 times.||No|
|outputRouting_253a|This element indicates the destination of<br>the output message.|string|No|**"[A-Z+]{1,3}"**||Required in<br>the element<br>_adjacentCent_<br>_erRouting_.|
|FAV_29d|This element provides the FAV Airspace<br>Assignment number.|string|No|**"\d{4}"**<br>The format consists in four digits, with leading<br>zeroes as needed.|0053<br>2509|No|
|ICAOStoredFormat_918a|This element may only have the value<br>zero, to indicate that none of the Other<br>Information elements (with suffixes 918b<br>– 918x) is present in the message.|string|No|**“0”**|0|No|
|EETIndicator_918b|This element specifies Significant Points or<br>FIR Boundary designators and<br>accumulated estimated elapsed times to|string|No|Freeform text up to a total of 3,000 characters.<br>The element consists of one or more<br>Significant Points with appended estimated|<br>KZNY0046<br>HUBE0213|No|

348

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||such points or boundaries, when so<br>prescribed on the basis of regional air<br>navigation agreements, or by the<br>appropriate ATS authority.<br>EET stands for Estimated Elapsed Time.|||flying time from departure in_hhmm_format<br>with a blank separating each occurrence of<br>Significant Point and time.|||
|RIFIndicator_918c|This element specifies the route to a<br>revised destination aerodrome, followed<br>by the aerodrome location code. The<br>revised route is subject to re-clearance in<br>flight. RIF stands for Revised in Flight.|string|No|Free-form string of up to 3000 characters.<br>The destination aerodrome has to be specified<br>using the four-letter ICAO location code.|DTA HEC<br>KLAX|No|
|REGIndicator_918d|This element specifies Aircraft Registration<br>(tail number), if different from the aircraft<br>identification specified in element flightId-<br>_02a.|string|No|Free-form string of up to 3000 characters.|N5258E|No|
|SELIndicator_918e|This element specifies the SELCAL code.<br>SELCAL is a selective-calling radio system<br>that alerts aircraft crew to incoming radio<br>communications.|string|No|Free-form string of up to 3000 characters.|ACHA<br>BRLM|No|
|OPRIndicator_918f|This field specifies the Aircraft Operator, if<br>not obvious from the aircraft identification<br>in_flightId_02a_.|string|No|Free-form string of up to 3000 characters.|UAL|No|
|STSIndicator_918g|This element specifies the Reason for<br>Special Handling by ATS, such as hospital<br>aircraft.|string|No|Free-form string of up to 3000 characters.<br>The following are the only valid special<br>handling indicators:<br>**ALTRV**<br>**ATFMX**<br>**FFR**<br>**FLTCK**<br>**HAZMAT**<br>**HEAD**<br>**HOSP**|ALTRV|No|

349

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||**HUM**<br>**MARSA**<br>**MEDEVAC**<br>**NONRVSM**<br>**SAR**<br>**STATE**<br>**NONRNP10**<br>**NO NRPN10**<br>**PROTECTED**<br>**CARGO**<br>**CARGO FLT**|||
|TYPIndicator_918h|Type(s) of Aircraft, preceded if necessary<br>by number of aircraft, if ZZZZ is specified<br>in the element numberOfAircraft_03a.|string|No|Free-form string of up to 3000 characters.|**CESNA140**|No|
|PERIndicator_918i||string|No|Single valid letter specified in PAN-OPS 8168<br>Volume 1:<br>A – Indicated airspeed (IAS) less than 169 km/h<br>(91kt)<br>B – IAS between 169 km/h (91kt) and 224<br>km/h (121 kt)<br>C – IAS between 224 km/h (121 kt) and 261<br>km/h ( 141 kt)<br>D – IAS between 261 km/h ( 141 kt) and 307<br>km/h (166 kt)<br>E - IAS between 307 km/h (166 kt) and 391<br>km/h (211 kt)<br>H - Helicopters|C|No|
|COMIndicator_918j|This element contains Communication<br>Equipment Data. It is used for additional<br>Communication Equipment on board not<br>specified in the flightPlanRoute_10a<br>element.|string|No|Free-form string of up to 3000 characters.|**HF ONLY**<br>**TCAS**|No|

350

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|DATIndicator_918k|This element specifies data related to data<br>link capability.|string|No|Free-form string of up to 3000 characters.<br>Valid values are:<br>S – satellite data link<br>H – HF data link<br>V – VHF data link<br>M – SSR Mode S data link<br>One or more of the valid letters may be<br>specified in this element.|SV|No|
|NAVIndicator_918l|This element contains Navigation<br>Equipment Data. It is used for additional<br>Navigation Equipment not specified in the<br>flightPlanRoute_10a element.|string|No|Free-form string of up to 3000 characters.|**ADF ONLY**|No|
|DEPIndicator_918m|This element contains the name of the<br>Departure Aerodrome if ZZZZ is specified<br>in Field 13, or the ICAO four-letter location<br>indicator of the location of the ATS unit<br>from which supplementary flight plan data<br>can be obtained, if AFIL is specified in Field<br>13 (flight plan was filed by an active flight).<br>Note: Field 13 does not appear in FH, AH,<br>and HU messages.|string|No|Free-form string of up to 3000 characters.|**NORTON**<br>**FIELD**|No|
|DESTIndicator_918n|This element includes the name of the<br>destination aerodrome.|string|No|Free-form string of up to 3000 characters.|**MILLSPAW**<br>**FARM**|No|
|ALTNIndicator_918o|This element includes the name of the<br>alternate destination aerodrome(s).|string|No|Free-form string of up to 3000 characters.|**MILLSPAW**<br>**FARM**|No|
|RALTIndicator_918p|This element contains the en-route<br>alternate aerodrome(s).|string|No|Free-form string of up to 3000 characters.|**JP RANCH**|No|
|CODEIndicator_918q|This element specifies the aircraft<br>Controller-Pilot Data Link Communications<br>(CPDLC) address.|string|No|Free-form string of up to 3000 characters.|45FA16|No|
|RACEIndicator_918r|This element specifies the requested<br>altitude and speed en route.|string|No|Free-form string of up to 3000 characters.|**KRAFT/M0**<br>**80F380**|No|
|SURIndicator_918s|This element specifies the surveillance<br>applications or capabilities not specified in|string|No|Free-form string of up to 3000 characters.|**282B**|No|

351

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||localIntendedRoute_10b.||||||
|DLEIndicator_918t|This element specifies significant en route<br>delay or holding point(s), followed by<br>length of delay. It is new in ICAO 2012.|string|No|Free-form string of up to 3000 characters.<br>The length of delay is specified in the format<br>_hhmm_.|**MDG0030**|No|
|TALTIndicator_918u|This element specifies the take-off<br>alternate aerodrome.|string|No|Free-form string of up to 3000 characters.<br>Valid formats include aerodrome name or any<br>of the fix formats (i.e., lat/long, fix-radial-<br>distance, or name).|KRAFT<br>FARM|No|
|DOFIndicator_918v|This element specifies the date of flight.|string|No|**“\d{6}”**<br>Six-digit date in the format_yymmdd_.|140617|No|
|ORGNIndicator_918w|This element specifies the originator’s<br>eight-letter AFTN address or other<br>appropriate contact details, in cases where<br>the originator of the flight plan may not be<br>readily identified, as required by the<br>appropriate ATS authority.|string|No|**Eight-letter character string.**|**LEBBYNYX**|No|
|PBNIndicator_918x|This element specifies the RNAV or RNP<br>capability. PBN stands for Performance<br>Based Navigation.|string|No|Up to eight two-character specifications may<br>be included, for a total of 16 characters. RNAV<br>and RNP capabilities are two-characters each,<br>as follows.<br>RNAV specifications:<br>A1**RNAV10 (RNP 10)**<br>B**1 RNAV 5 all permitted sensors**<br>B2**RNAV 5 GNSS**<br>B3**RNAV 5 DME/DME**<br>B4**RNAV 5 VOR/DME**<br>B5**RNAV 5 INS or IRS**<br>B6**RNAV 5 LORANC**<br>C1**RNAV 2 all permitted sensors**<br>C2**RNAV 2 GNSS**<br>C3**RNAV 2 DME/DME**<br>C4**RNAV 2 DME/DME/IRU**<br>D1**RNAV 1 all permitted sensors**|B1O1|No|

352

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||D2**RNAV 1 GNSS**<br>D3**RNAV 1 DME/DME**<br>D4**RNAV 1 DME/DME/IRU**_RNP_specifications:<br>**L1**RNP 4<br>**O1**Basic RNP 1 all permitted sensors<br>**O2**Basic RNP 1 GNSS<br>**O3**Basic RNP 1 DME/DME<br>**O4**Basic RNP 1 DME/DME/IRU<br>**S1**RNP APCH<br>**S2**RNP APCH with BAR-VNAV<br>**T1**RNP AR APCH with RF (special authorization<br>required)<br>**T2**RNP AR APCH without RF (special<br>authorization required)|||
|ICAO1stAdaptedField18_<br>999a|Elements having the suffix of__999a_<br>through__999y_contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO2ndAdaptedField18<br>_999b|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO3rdAdaptedField18<br>_999c|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO4thAdaptedField18<br>_999d|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,|string|No|Free-form string of up to 3000 characters.||No|

353

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.||||||
|ICAO5thAdaptedField18<br>_999e|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO6thAdaptedField18<br>_999f|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO7thAdaptedField18<br>_999g|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO8thAdaptedField18<br>_999h|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO9thAdaptedField18<br>_999i|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO10thAdaptedField1<br>8_999j|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable,usinga Field Reference|string|No|Free-form string of up to 3000 characters.||No|

354

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||Number of 999, with elements_a_through_y_.||||||
|ICAO11thAdaptedField1<br>8_999k|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO12thAdaptedField1<br>8_999l|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO13thAdaptedField1<br>8_999m|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO14thAdaptedField1<br>8_999n|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO15thAdaptedField1<br>8_999o|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO16thAdaptedField1<br>8_999p|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|

355

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|ICAO17thAdaptedField1<br>8_999q|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO18thAdaptedField1<br>8_999r|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO19thAdaptedField1<br>8_999s|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO20thAdaptedField1<br>8_999t|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO21stAdaptedField18<br>_999u|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO22ndAdaptedField1<br>8_999v|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|

356

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|ICAO23rdAdaptedField1<br>8_999w|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO24thAdaptedField1<br>8_999x|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|ICAO25thAdaptedField1<br>8_999y|Elements having the suffix of _999a<br>through _999y contain the data that is<br>present for the optionally adapted element<br>918 indicators that are transmitted to CMS,<br>when applicable, using a Field Reference<br>Number of 999, with elements_a_through_y_.|string|No|Free-form string of up to 3000 characters.||No|
|lastSeqNo_245a|The ERAM sequence number of the last<br>message received for a flight. Sequence<br>number is part of field 00.|integer|No|||Yes|
|lastFltMsgRcvd_245b|This element specifies the time the last<br>message was received for a flight.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:5**<br>**2**|Yes|
|RNVArrival_925a|This element specifies the RNAV accuracy<br>value for the arrival phase of the flight<br>expressed in hundredths (.01) nm.|string|No|**"\d{4}"**<br>The valid range is [0001-9999]. If the value is 0<br>then the field is not included.|**Accuracy**<br>**of 0.3 nm:**<br>0030|No|
|RNVEnroute_925b|This element specifies the RNAV accuracy<br>value for the en route phase of the flight<br>expressed in hundredths (.01) nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the value<br>is 0 then the field is not included.|**Accuracy**<br>**of 0.1 nm:**<br>0010|No|
|RNVOceanic_925c|This element specifies the RNAV accuracy<br>value for the oceanic phase of the flight<br>expressed in hundredths (.01) nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the value<br>is 0 then the field is not included.|**Accuracy**<br>**of 0.1 nm:**<br>0010|No|

357

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|RNVDeparture_925d|This element specifies the RNAV accuracy<br>value for the departure phase of the flight<br>expressed in hundredths (.01) nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the value<br>is 0 then the field is not included.|**Accuracy**<br>**of 0.1 nm:**<br>0010|No|
|RNVSpare1_925e|This is a spare element.|string|No|**"\d{4}"**||No|
|RNVSpare2_925f|This is a spare element.|string|No|**"\d{4}"**||No|
|tentativeFlightPlanIndica<br>tor_2459|This element indicates whether the flight<br>plan data is from a tentative flight plan or<br>not.|string|No|**“*”**|*|No|
|RNPArrival_925g|This element specifies the RNP accuracy<br>value for the arrival phase of the flight<br>expressed in hundredths (.01) nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the value<br>is 0 then the field is not included.|**Accuracy**<br>**of 0.3 nm:**<br>0030|No|
|RNPEnroute_925h|This element specifies the RNP accuracy<br>value for the en route phase of the flight<br>expressed in hundredths (.01) nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the value<br>is 0 then the field is not included.|**Accuracy**<br>**of 0.3 nm:**<br>0030|No|
|RNPOceanic_925i|This element specifies the RNP accuracy<br>value for the oceanic phase of the flight<br>expressed in hundredths (.01) nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the value<br>is 0 then the field is not included.|**Accuracy**<br>**of 0.3 nm:**<br>0030|No|
|RNPDeparture_925j|This element specifies the RNP accuracy<br>value for the departure phase of the flight<br>expressed in hundredths (.01) nm.|string|No|**"\d{4}"**<br>The allowable range is 0001-9999. If the value<br>is 0 then the field is not included.|**Accuracy**<br>**of 0.3 nm:**<br>0030|No|
|RNPSpare1_925k|This is a spare element.|string|No|**"\d{4}"**||No|
|RNPSpare2_925l|This is a spare element.|string|No|**"\d{4}"**||No|

358

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|cancellationIndicator_92<br>b|This optional element includes a<br>cancellation indicator.|string|No|**“C”**<br>The letter C is the only valid value.|C|No|
|ATCIntendedRoute_10c|The ATC Intended Route element contains<br>the current cleared flight plan route with<br>any unacknowledged auto routes already<br>applied. The ATC Intended Route includes<br>to-be-applied AARs that are not to be<br>notified in the current center. It is intended<br>for clients that wish to know the currently<br>expected route of the flight across<br>contiguous ERAM airspace. Field 10c<br>contains the filed route (field 10a) merged<br>with any adapted routes (preferential<br>routes, transition fixes and A-line fixes).<br>Optional Field 10c is sent to ATM-IPOP,<br>when parameter Merged ATC Intended<br>Route Switch (MARS) is ON and if either<br>one of the following is true:<br>If Field 10b exists and Field 10c is not the<br>same as Field 10b<br>If Field 10b does not exist and Field 10c is<br>not the same as Field 10a.|string|No|**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-9+\./]*\.[A-Z0-**<br>**9+/\*]{2,12}_?(/\d{4})?"**<br>Minimum length = 3<br>Maximum length = 1000|**JFK.J42.TX**<br>**K.STAR1.D**<br>**FW**|No|
|flightPlanRouteRevNo_2<br>468|This optional element specifies the flight<br>plan route revision number.|string|no|**"[0-9]"**|7|No|
|reconReportedAlt_2460|If the flight is active, this field contains the<br>reported altitude from the last track<br>messge received for the flight.|String|No|**"\d{1,3}"**<br>One to three digits in the range 0 – 999.|240|No|
|clearanceRoute_2469||string|no|**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-9+\./]*\.[A-Z0-**<br>**9+/\*]{2,12}_?(/\d{4})?"**<br>Minimum length = 3<br>Maximum length = 1000||No|
|comNavApproachEquipI<br>CAO2012_910c|This element is the ICOA 2012 version of<br>the element_comNavApproachEquip_910a_.|string|No|**"[A-Z][A-Z0-9]{0,63}"**<br>The valid values are:<br>N – No equipment is carried,or equipment is|ADE3RV|No|

359

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||unserviceable<br>S – Standard equipment is carried and is<br>serviceable<br>A – GBAS landing system<br>B – LPV (APV with SBAS)<br>C – LORAN C<br>D – DME<br>E1 – FMC WPR ACARS<br>E2 – D-FIS ACARS<br>E3 – PDC ACARS<br>F – ADF<br>G – GNSS<br>H – HF RTF<br>I – Inertial Navigation<br>J1 – CPDLC ATN VDL Mode 2<br>J2 – CPDLC FANS 1/A HDFL<br>J3 - CPDLC FANS 1/A VDL Mode A<br>J4 - CPDLC FANS 1/A VDL Mode 2<br>J5 - CPDLC FANS 1/A SATCOM (INMARSAT)<br>**J6**- CPDLC FANS 1/A SATCOM (MTSAT)<br>J7 - CPDLC FANS 1/A SATCOM (Iridium)<br>K – MLS<br>L – ILS<br>M1 – ATC RTF SATCOM (INMARSAT)<br>M2 - ATC RTF SATCOM (MTSAT)<br>M3 – ATC RTF (Iridium)<br>O – VOR<br>P1-P9 – Reserved for RCP<br>R – PBN approved<br>T – TACAN<br>U – UHF RTF<br>V – VHF RTF<br>W – RVSM approved|||

360

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||X – MNPS approved<br>Y – VHF with 8.33 kHz spacing capacity<br>Z – Other equipment carried|||
|survEquipICAO2012_910<br>d|This element is the ICAO 2012 equivalent<br>of the_element survEquip_910b_.|string|No|**“N|A|C|(C?[BDEGHILPSUVX][BDEGHILPSUVX**<br>**12]*)"**<br>Minimum element length=1<br>Maximum element length=20<br>The valid values are the following:<br>N – No surveillance equipment or equipment<br>unserviceable<br>A – Transponder Mode A<br>C – Transponder Mode A and C<br>E – Transponder – Mode S, including aircraft<br>identification, pressure-altitude and extended<br>squitter (ADS-B) capability<br>H – Transponder – Mode S, including aircraft<br>identification, pressure-altitude and enhanced<br>surveillance capability<br>I - Transponder – Mode S, including aircraft<br>identification, but no pressure-altitude<br>capability<br>L – Transponder – Mode S, including aircraft<br>identification, pressure-altitude, extended<br>squitter (ADS-B) and enhanced surveillance<br>capability<br>P – Transponder – Mode S, including pressure-<br>altitude, but no aircraft identification<br>S – Transponder – Mode S, including both<br>pressure-altitude and aircraft identification<br>capability<br>X – Transponder - Mode S with neither aircraft<br>identification nor pressure-altitude capability<br>B1 – ADS-B with dedicated 1090 mHz ADS-B<br>“out” capability<br>B2 – ADS-B with dedicated 1090 mHz ADS-B|HB2U2V2G<br>1|No|

361

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTFPI]**|**Element Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||“out” and “in” capability<br>U1 - ADS-B “out” capability using UAT<br>U2 - ADS-B “out” AND “IN” capability using<br>UAT<br>V1 - ADS-B “out” capability using VDL Mode 4<br>V2 - ADS-B “out” and “in” capability using VDL<br>Mode 4<br>D1 – ADS-C with FANS 1/A capabilities<br>G1 - ADS-C with ATN capabilities|||

362

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.81 Flight Plan Reconstitution [DBRTFPI] – Diagram**

363

NAS-JMSDD-4309-001 Rev C July 10, 2018

364

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.1.82 Flight Plan Reconstitution Message in FIXM Format [DBRTFPI_FIXM] – Data Elements**

The following elements of the DBRTFPI message in Simple XML format are not translated in the FIXM format of the message (DBRTRPI_FIXM):

- coordStatusTime_07d

- FPA_143a0

- FPA_143a1

- FPA_143a2

365

NAS-JMSDD-4309-001 Rev C July 10, 2018

- FPA_143a3

- comNavApproachEquip_910a

- survEquip_910b

- timeRouteValues_2461

- fixTimes

- fixTime_68c

- adjacentCenterRouting

- outputRouting_253a

- FAV_29d

- ICAOStoredFormat_918a

- RACEIndicator_918r

- DOFIndicator_918v

- lastSeqNo_245a

- lastFltMsgRcvd_245b

- tentativeFlightPlanIndicator_2459

- flightPlanRouteRevNo_2468

- clearanceRoute_2469

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/supplementalData/additional<br>FlightInformation/nameValue/@na<br>me<br>flight/supplementalData/additional<br>FlightInformation/nameValue/@val<br>ue|FDPS_Seq<br>uenceNo|Sequence number assigned by<br>SFDPS to each message it<br>receives from HADDS. The<br>attribute_name_includes the<br>constant string<br>"MSG_SEQ_NO", and the<br>attribute_value_contains the<br>sequence number value.|@name:<br>@value:<br>fb:FreeTextType|No|@name:<br>”MSG_SEQ_NO”<br>@value:<br>xs:nonNegativeInteger<br>xs:maxInclusive<br>value="999999999"|@name="<br>MSG_SEQ<br>_NO"<br>@value="<br>6860416"|Yes|
|flight/@system|propSourc<br>eSystem|This attribute indicates which<br>SFDPS system generated the<br>message.|fb:ProvenanceSys<br>temType|No|xs:string<br>maxLength=128|ATL|Yes|
|flight/@timestamp|propRcvdT<br>ime|This attribute conatins the<br>time at which the message was|ff:TimeType|No|xs:dateTime|2015-12-<br>18T22:19:|Yes|

366

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||received by SFDPS.||||02.028Z||
|flight/@centre|center|This attribute specifies the<br>code of the ARTCC (or<br>FIR) that produced the data.|fb:ProvenanceCe<br>ntreType|No|xs:string|`ZAU`|Yes|
|flight/flightStatus/@fdpsFlightStatu<br>s|flightState|This attribute contains the<br>current status of the flight as<br>specified by SFDPS.|nas:SfdpsFlightSt<br>atusType|Yes|xs:string<br>“PROPOSED|ACTIVE|COMPLETE<br>D|CANCELLED|DROPPED”|ACTIVE|Yes|
|flight/supplementalData/additional<br>FlightInformation/nameValue/@na<br>me<br>flight/supplementalData/additional<br>FlightInformation/nameValue/@val<br>ue|fdpsGufi|The name value pair specifies<br>the SFDPS GUFI, an identifier<br>on every message that<br>positively identifies what flight<br>the message is for.|fb:FreeTextType|No|xs:string<br>@name:<br>"FDPS_GUFI"<br>@value:<br>"us\.fdps\.\d{4}-\d{2}-<br>\d{2}T\d{2}:\d{2}:\d{2}Z\.[A-Za-<br>z0-9/]+"|name="F<br>DPS_GUFI<br>"<br>value="us<br>.fdps.201<br>5-12-<br>18T16:59:<br>10Z.000/1<br>4/100"/>|Yes|
|flight/flightPlan/@identifier|eramGufi_<br>316a|This attribute specifies the<br>unique flight plan identifier.|fb:FreeTextType|No|xs:string<br>"[A-Z]{2}\d{5}[1-7]\d{2}"|"KU68378<br>100"|No|
|flight/gufi|uuidGufi|This element contains a<br>reference that uniquely<br>identifies a flight and that is<br>independent of any particular<br>system. This reference<br>conforms to the Universal<br>Unique Identifier standard.|fb:GloballyFlightI<br>dentifierType||xs:string<br>"[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-<br>4[0-9a-fA-F]{3}\-[89aAbB][0-9a-<br>fA-F]{3}\-[0-9a-fA-F]{12}"|4aaf92be-<br>ac0a-<br>4dba-<br>998f-<br>9e56f5d4<br>50b6|Yes|
|flight/flightIdentification/@aircraftI<br>dentification|flightId_02<br>a|Name used by Air Traffic<br>Services units to identify and<br>communicate with an aircraft.|fb:FlightIdentifier<br>Type|No|**"[A-Z0-9]{7}"**|**AAL20**|Yes|
|flight/supplementalData/additional<br>FlightInformation/nameValue/@na|flightId_02<br>a|The flight supplemental data is<br>used to indicate that a flight|@_name:_<br>_@value_:|No|Format:<br>_@name:_|@name =<br>**“SIMULA**|No|
|me<br>flight/supplementalData/additional<br>FlightInformation/nameValue/@val||message is a test message, by<br>setting the attribute_name_to<br>“**SIMULATED_FLIGHT**” and the|_fb:FreeTextType_||**“[A-Z0-9_]{1,20}”**<br>_@value:_|**TED_FLIG**<br>**HT”**<br>@value =||

367

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|ue||attribute_value_to “**true**”.|||**xs:string**<br>**minLength=1, maxLength=100**<br>Permissible values:<br>@name =**“SIMULATED_FLIGHT”**<br>@value =**“true”**|**“true”**||
|flight/flightIdentification/@comput<br>erId|computerI<br>d_02d|A unique identification<br>assigned by ERAM to each<br>flight plan.|fb:FreeTextType|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, such as_ddd,_<br>_ddL, dLd, dLL_.|**020**|No|
|flight/flightIdentification/@siteSpec<br>ificPlanId|sspId_167<br>a|Site Specific Plan Identifier. It<br>is assigned by Instrument<br>Flight Procedures Automation<br>(IFPA) to uniquely identify a<br>flight plan in each ERAM<br>facility.|fb:CountType|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|flight/aircraftDescription/@aircraft<br>Quantity|numberOf<br>Aircraft_0<br>3a|This element includes the<br>number of aircraft for the<br>flight.|fb:countType|No|**"\d{0,2}"**<br>The element consists of zero to<br>two digits.|**3**|No|
|flight/aircraftDescription/@tfmsSp<br>ecialAircraftQualifier|numberOf<br>Aircraft_0<br>3a- Special<br>Aircraft<br>Indicator|<br>This element includes the<br>Special Aircraft Indicator. It<br>indicates the flight is a heavy<br>jet, B757 or, if not present, a<br>large jet and if the flight is<br>either equipped or not with<br>TCAS. This indicator is used for<br>output purposes such as strip<br>printing and message transfers<br>to other facilities such as<br>Automated Radar Terminal<br>System (ARTS).<br>NOTE<br>TFMS Special AircraftQualifier|nas:NasSpecialAir<br>craftQualifierTyp<br>e|No|**“HEAVY_JET|TCAS|B757|HEAVY**<br>**_JET_AND_TCAS”**<br>**“HEAVY_JET”**=Capable of<br>takeoff weights of 300,000<br>pounds or more<br>**“TCAS”**=Traffic collision<br>avoidance system or traffic<br>alert and collision avoidance<br>system<br>**“B757”**=Controllers are<br>required to apply the special<br>wake turbulence separation<br>criteria for the Boeing 757.<br>**“HEAVY_JET_AND_TCAS”**=<br>Capable of takeoff weights of|**HEAVY_JE**<br>**T**|No|

368

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||is a bad fit to Special Aircraft<br>Indicator but no other fields<br>seem to fit.|||300,000 pounds or more and<br>traffic collision avoidance<br>system.|||
|flight/aircraftDescription/aircraftTy<br>pe/icaoModelIdentifier|typeOfAirc<br>raft_03c|The ICAO code of the aircraft<br>type.|fb:IcaoAircraftIde<br>ntifierType|No|**"[A-Z][A-Z0-9]{1,3}"**<br>The element consists of one<br>letter followed by one to three<br>alphanumeric characters.|**B747**|Yes|

369

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/aircraftDescription/@equipm<br>entQualifier|airborneEq<br>uip_03e|Airborne equipment qualifier.<br>A value assigned to the<br>aircraft, based on its<br>navigational equipment,<br>whether or not it has a<br>transponder, and if it has a<br>transponder, whether the<br>transponder supports Mode C.|nas:NasAirborneE<br>quipmentQualifie<br>rType|No|**" [ ABCDGHILMNPSTUVWXYZ]"**<br>The element consists of one<br>alphanumeric character, that can<br>have one of the following values:<br>•<br>“X”= No RVSM, No<br>DME, No transponder<br>•<br>“T”= No RVSM, No<br>DME, Transponder with<br>no mode C<br>•<br>“U”= No RVSM, No<br>DME: Transponder with<br>mode C<br>•<br>“D”= DME: No<br>transponder<br>•<br>“B”= DME:<br>Transponder with no<br>mode C<br>•<br>“A”= DME:<br>Transponder with<br>mode<br>•<br>“M”= TACAN ONLY: No<br>transponder<br>•<br>“N”= TACAN ONLY:<br>Transponder with no<br>mode C<br>•<br>“P”= TACAN ONLY:<br>Transponder with<br>mode C<br>•<br>“C”= “Y”=<br>LORAN,VORDME,INS,R<br>NAV: No transponder<br>•<br>“I”=<br>LORAN,VORDME,INSRN<br>AV: Transponder with<br>mode C<br>•<br>“H”= RVSM, Failed<br>transponder or Failed|**E**|No|

370

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||||||Mode C capability<br>•<br>“S=ADVANCED RNAV,<br>TRANSPONDER, MODE<br>C: FMS with DMEDME<br>position updating<br>•<br>“G”= ADVANCED RNAV,<br>TRANSPONDER, MODE<br>C: Global Navigation<br>Satellite System<br>(GNSS), including GPS<br>or Wide Area<br>Augmentation System<br>(WAAS), with enroute<br>and terminal capability<br>•<br>“V”= ADVANCED RNAV,<br>TRANSPONDER, MODE<br>C: Required<br>Navigational<br>Performance (RNP).<br>The aircraft meets the<br>RNP type prescribed for<br>the route segments,<br>routes and/or area<br>concerned.<br>•<br>“Z”= REDUCED<br>VERTICAL SEPARATION<br>MINIMUM (RVSM): E<br>with RVSM<br>• “L”= REDUCED<br>VERTICAL<br>SEPARATION<br>MINIMUM<br>(RVSM): G with<br>RVSM<br>• “W”= REDUCED<br>VERTICAL<br>SEPARATION<br>MINIMUM|||

371

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||||||(RVSM): RVSM|||
|flight/enRoute/beaconCodeAssign<br>ment/currentBeaconCode|beaconCo<br>de_04a|Current assigned beacon code.<br>**_Note_: **As of SFDPS R1.3.1, if<br>the<br>flight/flightStatus/@fdpsFlight<br>Status attribute has a value of<br>‘CANCELED or ‘PROPOSED,<br>this element is only present in<br>the version of a message with<br>FDPS_Restricted=’R’|fb:BeaconCodeTy<br>pe|No|"[0-7]{4}"<br>The element includes four octal<br>digits (i.e. 0-7). When the last<br>two digits of the four-digits are<br>zero, the beacon code is a non-<br>discrete code.<br>A discrete code is any code not<br>ending in 00.|Non-<br>discrete<br>VFR code:<br> **2101**|Yes|
|flight/requestedAirspeed/nasAirspe<br>ed<br>flight/requestedAirspeed/@uom|trueAirSpe<br>ed_05a<br>machSpee<br>d_05c|The aircraft speed expressed in<br>either true airspeed or mach.|nasAirspeed:<br>ff:<br>TrueAirSpeedOr<br>MachType<br>uom:<br>ff:AirspeedMeasu<br>reType|No|nasAirspeed:<br>**“xs:double”**<br>uom:<br>**“KILOMETERS_PER_HOUR|KNOT**<br>**S|MACH”**<br>This element is required if<br>requestedAirspeed/classifed not<br>included in the message.|nasAirspe<br>ed:<br>**540**<br>uom:<br>**KNOTS**|Yes|
|flight/requestedAirspeed/classified|classifiedS<br>peed_05d|Classified Speed Indicator. It<br>indicates that the speed for<br>this flight is classified and is<br>not to be recorded.|nas:ClassifiedSpe<br>edIndicatorType|No|**“CLASSIFIED”**<br>This element is required if<br>requestedAirspeed/nasAirspeed<br>not included in the message.|**CLASSIFIE**<br>**D**|Yes|
|flight/coordination/coordinationFix<br>/@fix|coordFix_0<br>6a|The fix to be used in<br>conjunction with the<br>CoordinationTime so<br>processing for this flight can<br>be synchronized for the next<br>sector/facility. It coordinates<br>the flight plan with the aircraft<br>position.|fb:SignificantPoin<br>tType (abstract<br>type)<br>_fb:FixPointType/_<br>_ff:GeographicalLo_<br>_cationType/_<br>_fb:RelativePointT_<br>_ype_|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>**-**_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:|**KBOS**|Yes|

372

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||||||_fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|||
|flight/coordination/@coordination<br>TimeHandling|coordStatu<br>s_07d1|The indicator for the type of<br>Coordination Time.|nas:Coordination<br>TimeType|No|**“(P|D|E|A)”**<br>**“P”**= Proposed flight plan.<br>**“D”**= Aircraft has departed from<br>the departure airport.<br>**“E”**= Active aircraft.<br>**“A”**= Aircraft arrived at the<br>destination airport.|**P**|Yes|
|flight/coordination/@coordination<br>Time|coordTime<br>_07d2|Coordination Time: the time to<br>be used in conjunction with<br>the Coordination Fix so<br>processing for this flight can be<br>synchronized for the next<br>sector/facility.|ff:TimeType|No|**xs:dateTime**|**2015-06-**<br>**20T20:17:**<br>**52**|Yes|
|flight/coordination/@delayTimeTo<br>Absorb|delayTime<br>_07e|Delay time to absorb:<br>indicates the amount of time<br>that needs to be absorbed<br>during the flight. It is<br>corrective action for meeting<br>the goal of Estimated<br>Departure Clearance Time<br>(EDCT), when the flight is<br>already active and needs to<br>arrive later than originally<br>planned.|ff:DurationTime|No|**xs:duration**|**PT30M**|No|
|flight/departure/runwayPositionAn<br>dTime/runwayTime/actual/@time|departure<br>Time_243<br>n|This element specifies the<br>actual departure time in UTC.|ff:TimeType|No|**xs:dateTime**|**2014-06-**<br>**20T20:17:**<br>**52**|No|
|flight/departure/runwayPositionAn<br>dTime/runwayTime/estimated/@ti|proposedD<br>epartureTi|This element specifies the<br>proposed departure time.|ff:TimeType|No|**xs:dateTime**|**2014-06-**<br>**20T20:17:**|No|

373

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|me|me_2431|||||**52**||
|flight/departure/runwayPositionAn<br>dTime/runwayTime/controlled/@ti<br>me|estDepart<br>ureClearan<br>ceTime_24<br>32|This element specifies the<br>EDCT.|ff:TimeType|No|**xs:dateTime**|**2014-06-**<br>**20T20:27:**<br>**52**|No|
|flight/arrival/runwayPositionAndTi<br>me/runwayTime/actual/@time|arrivalTim<br>e_28b|This element specifies the<br>actual arrival time.|ff:TimeType|No|**xs:dateTime**|**2014-06-**<br>**20T22:27:**<br>**52**|No|
|flight/assignedAltitude/simple<br>flight/assignedAltitude/simple/@uo<br>m|assignedAl<br>t_08a|Simple altitude: single<br>measurement above<br>reference point. It represents<br>the only NAS altitude that<br>maps directly to the core ICAO<br>altitude types.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.<br>The attribute_uom_specifies<br>the altitude unit of<br>measurement.|nas:SimpleAltitud<br>eType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**“xs:double”**<br>**@uom:**<br>“**FEET|METERS**”|Assigned<br>altitude<br>of 34,000<br>feet:<br>**34000**<br>_Uom_:<br>**FEET**|No|
|flight/assignedAltitude/vfrOnTop|assignedAl<br>t_08b|The presence of this element<br>indicates VFR-ON-Top. It<br>specifies that the aircraft is<br>flying above the clouds in VFR<br>conditions.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|Nas:VfrOnTopAlti<br>tudeType|Yes|Empty element.||No|

374

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/assignedAltitude/vfrOnTopPl<br>us<br>flight/assignedAltitude/vfrOnTopPl<br>us/@uom|assignedAl<br>t_08c|VFR-ON-Top with altitude. It<br>represents an Instrument<br>Flight Rules (IFR) flight<br>operating above the clouds in<br>VFR conditions at the specified<br>assigned altitude.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|nas:VfrOnTopPlus<br>AltitudeType<br>@uom:<br>ff:AltitudeMeasur<br>eType|No|**“xs:double”**<br>@uom:<br>**“FEET|METRES”**|Aircraft<br>flying<br>VFR-ON-<br>Top at<br>25,000<br>feet:<br>**25000**<br>_uom_:<br>**FEET**|No|
|flight/assignedAltitude/block/abov<br>e<br>flight/assignedAltitude/block/abov<br>e/@uom|assignedAl<br>t_08d|The bottom level of the<br>assigned block of altitudes for<br>the flight to fly at.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|ff:AltitudeType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**"xs:double"**<br>**@**uom:<br>**“FEET|METRES**|_above:_<br>**8000**<br>_uom:_<br>**FEET**|No|
|flight/assignedAltitude/block/belo<br>w<br>flight/assignedAltitude/block/belo<br>w/@uom|assignedAl<br>t_08d|The top level of the assigned<br>block of altitudes for the flight<br>to fly at.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|ff:AltitudeType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|_below:_<br>**14000**<br>_uom:_<br>**FEET**|No|
|flight/assignedAltitude/above<br>flight/assignedAltitude/above/@uo<br>m|assignedAl<br>t_08e|Element used for IFR flights<br>operating above a specified<br>altitude.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|nas:AboveAltitud<br>eType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|Aircraft is<br>flying<br>above<br>60,000<br>feet:<br>**60000**<br>**uom:**<br>**FEET**|No|

375

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/assignedAltitude/altFixAlt/poi<br>nt|assignedAl<br>t_08f|_assignedAltitude/altFixAlt_<br>element is defined as an<br>altitude prior to a specified fix,<br>the specified fix itself, and<br>altitude post specified fix. The<br>element_altFixAlt/point_<br>defines the specified fix<br>associated with the altitude.<br>The fix cannot be the<br>departure or arrival point.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|fb:SignificantPoin<br>tType (abstract<br>type)<br>_fb:FixPointType/_<br>_ff:GeographicalLo_<br>_cationType/_<br>_fb:RelativePointT_<br>_ype_|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|**MDG**|No|
|flight/assignedAltitude/altFixAlt/pr<br>e<br>flight/assignedAltitude/altFixAlt/pr<br>e/@uom|assignedAl<br>t_08f|_assignedAltitude/altFixAlt_<br>element is defined as an<br>altitude prior to a specified fix,<br>the specified fix itself, and<br>altitude post specified fix. The<br>element_altFixAlt/pre_defines<br>the altitude before the<br>specified fix.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|ff:AltitudeType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|**240000**<br>**uom:**<br>**FEET**|No|
|flight/assignedAltitude/altFixAlt/po<br>st<br>flight/assignedAltitude/altFixAlt/po<br>st/@uom|assignedAl<br>t_08f|_assignedAltitude/altFixAlt_<br>element is defined as an<br>altitude prior to a specified fix,<br>the specified fix itself, and<br>altitude post specified fix. The<br>element_altFixAlt/pre_defines<br>the altitude after the specified|ff:AltitudeType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|**22000**<br>**uom:**<br>**FEET**|No|

376

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||fix.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.||||||
|flight/assignedAltitude/vfr|assignedAl<br>t_08g|Its presence in the message<br>specifies that the flight is<br>flying Visual Flight Rules (VFR).<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|<br>nas:VfrAltitudeTy<br>pe|Yes|**Empty element**||No|
|flight/assignedAltitude/vfrPlus<br>flight/assignedAltitude/vfrPlus/@u<br>om|assignedAl<br>t_08h|It is used to specify that the<br>flight is flying VFR at a<br>specified altitude.<br>Only one of the altitude<br>elements_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|nas:VfrPlusAltitu<br>deType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|The<br>aircraft is<br>flying VFR<br>at 7,500<br>feet:<br>**7500**<br>uom:<br>**FEET**|No|
|flight/requestedAltitude/simple<br>flight/requestedAltitude/simple/@<br>uom|requested<br>Alt_09a|The element is used to specify<br>requested altitude. Only one<br>of the seven requested<br>altitude elements may be<br>included in a proposed flight<br>message.<br>Only one of the<br>requestedAltitude elements<br>_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|nas:SimpleAltitud<br>eType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**“xs:double”**<br>@uom:<br>“**FEET|METRES**”|Aircraft is<br>requestin<br>g to fly at<br>34,000<br>feet<br>altitude:<br>**34000**|No|
|flight/requestedAltitude/vfrOnTop|requested<br>Alt_09b|This element specifies an IFR<br>flight requesting to operate|nas:VfrOnTopAlti<br>tudeType|Yes|Empty element.|The<br>presence|No|

377

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||above the clouds in VFR<br>conditions.<br>Only one of the<br>requestedAltitude elements<br>_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.||||of this<br>empty<br>element<br>indicates<br>VFR-ON-<br>Top.||
|flight/requestedAltitude/vfrOnTopP<br>lus<br>flight/requestedAltitude/vfrOnTopP<br>lus/@uom|requested<br>Alt_09c|VFR-ON-Top with altitude. It<br>represents an Instrument<br>Flight Rules (IFR) flight<br>requesting to operate above<br>the clouds in VFR conditions at<br>the specified altitude.<br>Only one of the<br>requestedAltitude elements<br>_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|nas:VfrOnTopPlus<br>AltitudeType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**“xs:double”**<br>@uom:<br>**“FEET|METRES”**|Aircraft<br>requestin<br>g to fly<br>VFR-ON-<br>Top at<br>25,000<br>feet:<br>**25000**<br>uom:**feet**|No|
|flight/requestedAltitude/above<br>flight/requestedAltitude/above/@u<br>om|requested<br>Alt_09d|Element used for IFR flights<br>requesting to operate above a<br>specified altitude.<br>Only one of the<br>requestedAltitude elements<br>_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|nas:AboveAltitud<br>eType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|Aircraft is<br>requestin<br>g to fly<br>above<br>60,000<br>feet:<br>**60000**<br>**uom:**<br>**FEET**|No|
|flight/requestedAltitude/block/abo<br>ve<br>flight/requestedAltitude/block/abo<br>ve/@uom|requested<br>Alt_09e|The bottom level of the<br>requested block of altitudes<br>for the flight to fly at.<br>Only one of the<br>requestedAltitude elements<br>_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_, _block_, _above_,|ff:AltitudeType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|_above:_<br>**8000**<br>_uom:_<br>**FEET**|No|

378

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.||||||
|flight/requestedAltitude/block/belo<br>w<br>flight/requestedAltitude/block/belo<br>w/@uom|requested<br>Alt_09e|The top level of the requested<br>block of altitudes for the flight<br>to fly at.<br>Only one of the<br>requestedAltitude elements<br>_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|ff:AltitudeType<br>@uom:<br>ff:AltitudeMeasur<br>eType|Yes|**"xs:double"**<br>@uom:<br>**“FEET|METRES”**|_below:_<br>**14000**<br>_uom:_<br>**FEET**|No|
|flight/requestedAltitude/vfr|requested<br>Alt_09f|Its presence in the message<br>specifies that the flight is<br>requesting to fly Visual Flight<br>Rules (VFR).<br>Only one of the<br>requestedAltitude elements<br>_simple_,_vfrOnTop_,<br>_vfrOnTopPlus_,_block_,_above_,<br>_altFixAlt_,_vfr_,_vfrPlus_may be<br>included in the message.|nas:VfrAltitudeTy<br>pe|Yes|Empty element||No|
|flight/requestedAltitude/vfrPlus<br>flight/requestedAltitude/vfrPlus/@<br>uom|requested<br>Alt_09g|The element used to<br>represent a flight requesting<br>to fly VFR at a specified<br>altitude.|nas:VfrPlusAltitu<br>deType|Yes|**"xs:double"**<br>uom:<br>**“FEET|METRES”**|The<br>aircraft is<br>requestin<br>g to fly<br>VFR at<br>7,500<br>feet:<br>**7500**<br>uom:<br>**feet**|No|
|flight/agreed/route/@nasRouteTex<br>t|flightPlanR<br>oute_10a|This attribute specifies the<br>trajectory followed by the<br>airplane from the departure<br>point to the arrival point,<br>based on the fixes and routes|fb:FreeTextType|No|**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-**<br>**9+\./]*\.[A-Z0-**<br>**9+/\*]{2,12}_?(/\d{4})?"**<br>The element format consists of a<br>string that includes fixes and|OKC.V14S<br>.TUL.TUL0<br>90..FYV27<br>0.FYV|Yes|

379

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||along that trajectory.|||routes along the trajectory flown<br>by the airplane. The fixes and<br>routes are specified using the<br>FIX.ROUTE.FIX format, where<br>either element can be implied,<br>such as FIX..FIX, or<br>ROUTE..ROUTE.|||
|flight/departure/@departurePoint|departure<br>Point_26a|This attribute is used to<br>specify the first point or other<br>initial entity where the air<br>traffic control/management<br>system route starts.|fb:FreeTextType|No|xs:string<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP09001**<br>**5**<br>**ATOKA30**<br>**0040**<br>**3500N/04**<br>**000W**|Yes|
|flight/arrival/@arrivalPoint|destinatio<br>n_27a|The final point or other final<br>entity where the air traffic<br>control/management system<br>route terminates.|fb:FreeTextType|No|**xs:string**<br>minLength=2, maxLength=12<br>**"([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?)”**<br>Any of the standard ways to<br>represent a fix can be used for<br>this element (fix name, lat/long,<br>or fix-radial-distance), including<br>the standard airport designators.|**AB**<br>**DFW**<br>**KDFW**<br>**SHP09001**<br>**5**<br>**ATOKA30**<br>**0040**<br>**3500N/04**<br>**000W**|Yes|
|flight/agreed/route/@flightDuratio<br>n|ETE_2439|The total estimated time en<br>route (ETE), from the<br>departure (runway) to the<br>arrival at the destination<br>(runway).  For an airfile flight,<br>this is the total estimated time<br>en route, from the route start<br>point to the arrival at the<br>destination(runway).|ff:DurationType|No|xs:duration|**PT2H30M**<br>The<br>above<br>value<br>specifies<br>an ETE of<br>2 hours<br>and 30|No|

380

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||||||minutes.||
|flight/arrival/runwayPositionAndTi<br>me/runwayTime/estimated/@time|ETA_28a|This attribute specifies the<br>most reliable estimated time<br>when the aircraft will touch<br>down on the runway at the<br>flight plan destination.|ff:TimeType|No|xs:dateTime|**2014-06-**<br>**20T22:27:**<br>**52**|No|
|flight/flightPlan/@flightPlanRemark<br>s|remarks_1<br>1c|This attribute contains the NAS<br>Flight Plan Field 11 remarks<br>processed by the Traffic Flow<br>Management System (TFMS)<br>and used for TFM purposes.|fb:FreeTextType|No|The string is from 1 to 4,096<br>characters in length.|**OAIR**<br>**EVAC**<br>**AMG/N0**<br>**482F290**<br>**SQT/N04**<br>**79F310**<br>**JOL+**|No|
|flight/agreed/route/holdFix|holdDataFi<br>x_21a|This element specifies the<br>position location for the flight<br>to hold along the filed route of<br>flight. The attribute<br>flight/status/@airborneHold is<br>set to “**AIRBORNE_HOLD**”<br>when the element<br>flight/agreed/route/holdFix is<br>included.|fb:SignificantPoin<br>tType (abstract<br>type)<br>_fb:FixPointType/_<br>_ff:GeographicalLo_<br>_cationType/_<br>_fb:RelativePointT_<br>_ype_|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|**KBOS**<br>flight/stat<br>us/@airb<br>orneHold<br>is always<br>set to<br>“**AIRBOR**<br>**NE_HOLD**<br>” if<br>holdFix<br>specified.|No|
|flight/status/@airborneHold|holdDataFi<br>x_21a|This attribute specifies<br>whether or not the aircraft is<br>in an airborne hold.|fx:AirborneHoldIn<br>dicatorType|No|**“AIRBORNE_HOLD”**<br>If the aircraft is in an airborne<br>hold, the holdFix element is<br>included in the message and the<br>attribute airboneHold is set<br>to“**AIRBORNE_HOLD**”.|**“AIRBOR**<br>**NE_HOLD**<br>**”**|No|

381

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/enRoute/expectedFurtherCle<br>aranceTime/@time|holdDataTi<br>me_21d|This attribute specifies the<br>time the flight can expect<br>further clearance at the<br>holding location specified in<br>the element<br>flight/agreed/route/holdFix.<br>This element can only be<br>included in the HH_FIXM<br>messages if the element<br>flight/agreed/route/holdFix is<br>also included.|ff:TimeType|No|xs:dateTime|**2014-06-**<br>**20T20:17:**<br>**52**|No|
|flight/enRoute/position/position|progressR<br>eportFix_1<br>8a|This element specifies the<br>position location report of the<br>flight along the filed route of<br>flight and associated data of<br>the aircraft.|fb:SignificantPoin<br>tType (abstract<br>type)<br>_fb:FixPointType/_<br>_ff:GeographicalLo_<br>_cationType/_<br>_fb:RelativePointT_<br>_ype_|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|**KBOS**|Yes|
|flight/enRoute/position/@position<br>Time|progressR<br>eportTime<br>_18d|This attribute specifies the<br>time associated with the<br>current position of an active<br>flight from the radar<br>surveillance report or progress<br>report. The current position is<br>specified in the element<br>_flight/enRoute/position/positio_<br>_n_,above.|ff:TimeType|No|xs:dateTime|**2014-10-**<br>**31T22:30:**<br>**00**|Yes|

382

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/agreed/route/@inhibitAdapt<br>edDepRoutes|departure<br>AutoRoute<br>InhibitIndi<br>cator_244<br>g|This attribute specifies<br>whether the adapted<br>departure routes from the<br>departure airport are inhibited<br>for use for the route of the<br>flight.|nas:InhibitAdapte<br>dDepRoutesIndic<br>atorType|No|**“INHIBIT_ADAPTED_DEPARTURE**<br>**_ROUTES”**|**INHIBIT_**<br>**ADAPTED**<br>**_DEPART**<br>**URE_ROU**<br>**TES**|No|
|flight/agreed/route/@inhibitAdapt<br>edArrRoutes|destinatio<br>nAutoRout<br>eInhibitInd<br>icator_244<br>h|This attribute specifies<br>whether the adapted arrival<br>routes are inhibited for use for<br>the route of the flight.|nas:InhibitAdapte<br>dArrRoutesIndica<br>torType|No|**“INHIBIT_ADAPTED_ARRIVAL_R**<br>**OUTES”**|**INHIBIT_**<br>**ADAPTED**<br>**_**<br>**ARRIVAL**<br>**_ROUTES**|No|
|flight/interimAltitude|interimAlt<br>_76bT|This element specifies the<br>interim altitude the flight is<br>cleared to maintain different<br>from that in the flight plan.|nas:SimpleAltitud<br>eType|Yes|xs:double|interimAlt<br>itude of<br>240,000<br>feet:<br>**240000**<br>uom=**FEE**<br>**T**|No|
|flight/interimAltitude/@uom|interimAlt<br>_76bT|This attribute specifies the unit<br>of measure for the<br>_interimAltitude_element:<br>FEET/METRES.|_ff:AltitudeMeasur_<br>_eType_|No|**“FEET|METRES”**|**FEET**|Yes|
|flight/agreed/route/nasadaptedArri<br>valRoute/@nasRouteAlphanumeric|AARFld10_<br>142e<br>AARNonFl<br>d10_142f|This element includes the<br>Adapted Arrival Route (AAR)<br>preferential route in Field 10<br>or non-Field 10 formats.|fb:FreeTextType|No|**"([A-Z0-9\./]{4,97}) |**<br>**([A-Z0-9\./\+&#x20;]{4,97})"**<br>Field 10 format:<br>**"[A-Z0-9\./]{4,97}"**<br>Non-Field 10 format:<br>**"[A-Z0-9\./\+&#x20;]{4,97}"**<br>A “+” delimiter precedes and<br>follows the non-Field10<br>elements.|Field 10<br>format:<br>**./.BLEUZ.**<br>**RYTHM3.**<br>Non-Field<br>10<br>format:<br>**.J25.CRP+**<br>**LISSE6+**<br>Notice<br>the non-<br>Field10<br>substring<br>that is|No|

383

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||||||enclosed<br>between<br>“+”<br>character<br>s.||
|flight/agreed/route/adaptedDepart<br>ureRoute/@nasRouteAlphanumeric|ADRFld10_<br>142c<br>ADRNonFl<br>d10_142d|Adapted Departure Route<br>(ADR) preferential route in<br>Field 10 or non-Field 10<br>format.|fb:FreeTextType|No|**"([A-Z0-9\./\*]{4,84}) |**<br>**([A-Z0-9\./\+&#x20;-]{4,84})"**<br>Field 10 format:<br>**"([A-Z0-9\./\*]{4,84}”**<br>Non-Field 10 format:<br>**"[A-Z0-9\./\+&#x20;-]{4,84}"**<br>A “+” delimiter precedes and<br>follows the non-Field10<br>elements.|Field 10<br>format:<br>**.ALAMO6**<br>**.HENLY.J1**<br>**31.FUZ.J1**<br>**05.**<br>Non-Field<br>10<br>format:<br>**+RV**<br>**J25+CRP.L**<br>**ISSE6**|No|
|flight/agreed/route/adaptedArrival<br>DepartureRoute/@nasRouteAlphan<br>umeric|ADARFld1<br>0_142a<br>ADARNonF<br>ld10_142b|<br>This element contains the<br>adapted ADAR preferential<br>route in Field 10 or non-Field<br>10 formats. The Preferential<br>Route Alphanumeric are used<br>to control the flow and<br>separation of traffic departing<br>and arriving at designated<br>airports. An ADAR has the<br>complete preferential routing<br>from the departure airport to<br>the arrival airport.|fb:FreeTextType|No|**"([A-Z0-9\./]{4,44})|([A-Z0-**<br>**9\./\+&#x20;]{4,44})"**<br>The Field10 format is:<br>**"[A-Z0-9\./]{4,44}”**<br>The non-Field10 format is:<br>**"[A-Z0-9\./\+&#x20;]{4,44}"**<br>A “+” delimiter precedes and<br>follows the non-Field10<br>elements.|Field10<br>format:<br>SX2.PSX.V<br>20.CRP<br>Non-<br>Field10<br>format:<br>+LISSE6+<br>+TS1<br>MEM270<br>LIT050+|No|
|flight/agreed/route/nasadaptedArri<br>valRoute/@nasRouteIdentifier|AARId_141<br>c|If required for the flight, this<br>element specifies the Adapted<br>Arrival Route (AAR) identifier,<br>used to internally identify it.|fb:FreeTextType|No|**[A-Z0-9/\-\?\(\)\.,=\+ ]{5}"**<br>The format consists of five<br>characters.|PA001|No|
|flight/agreed/route/adaptedDepart<br>ureRoute/@nasRouteIdentifier|ADRId_14<br>1b|If required for the flight, this<br>element specifies the Adapted<br>Departure Route (ADR)|fb:FreeTextType|No|**[A-Z0-9/\-\?\(\)\.,=\+ ]{5}"**<br>The format consists of five<br>characters.|PD001|No|

384

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||identifier, used to internally<br>identify it.||||||
|flight/agreed/route/adaptedArrival<br>DepartureRoute/@nasRouteIdentifi<br>er|ADARId_1<br>41a|If required for the flight, this<br>element specifies the Adapted<br>Departure Arrival Route<br>(ADAR)/ Adapted Departure<br>Route (ADR)/ Adapted Arrival<br>Route (AAR) identifier, used to<br>internally identify an adapted<br>departure/ arrival/ departure<br>arrival route.|fb:FreeTextType|No|**[A-Z0-9/\-\?\(\)\.,=\+ ]{5}"**<br>The format consists of five<br>characters.|DA001|No|
|flight/agreed/route/nasadaptedArri<br>valRoute/nasFavNumber|FAV_143b<br>0<br>FAV_143b<br>1<br>FAV_143b<br>2<br>FAV_143b<br>3|This element includes a list of<br>Fixed Airspace Volume (FAV)<br>numbers for the FAVs<br>containing the first four<br>Adapted Arrival Route (AAR)<br>fixes.|list<br>itemType=”fb:Fre<br>eTextType”|No|**“\d{4}([ ]\d{4}){0,3}”**|7601<br>7602|No|
|flight/agree/route/@initialFlightRul<br>es|flightRules<br>_908a|The regulation, or<br>combination of regulations,<br>that governs all aspects of<br>operations under which the<br>pilot plans to fly.|fb:FlightRulesTyp<br>e|No|**“IFR|VFR”**|**IFR**|No|
|flight/@flightType|typeOfFlig<br>ht_908b|This element contains an<br>indication of the rule under<br>which an air traffic controller<br>provides categorical handling<br>of a flight.|fx:TypeOfFlightTy<br>pe|No|**“MILITARY|GENERAL|NON_SCH**<br>**EDULED| SCHEDULED|OTHER”**|**SCHEDUL**<br>**ED**|No|
|flight/aircraftDescription/@wakeTu<br>rbulence|wakeTurb<br>ulenceCat<br>_909c|This element specifies the<br>ICAO classification of the<br>aircraft wake turbulence,<br>based on the maximum<br>certified take off mass.|fx:WakeTurbulen<br>ceCategoryType|No|**“[JHML]”**<br>, where:<br>**J**= Super Heavy<br>**H**= Heavy<br>**M**= Medium<br>**L**= Light|H|No|

385

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/arrival/arrivalAerodromeAlter<br>nate/@code<br>or<br>flight/arrival/arrivalAerodromeAlter<br>nate/point<br>flight/arrival/arrivalAerodromeAlter<br>nate/@name|altAero_9<br>16c or<br>ALTNIndic<br>ator_918o|ICAO designator or the name<br>of an alternate aerodrome to<br>which an aircraft may proceed,<br>should it become either<br>impossible or inadvisable to<br>land at the original destination<br>aerodrome or an alternate<br>destination location. More<br>than one alternate arrival<br>aerodromes may be specified<br>for a flight.|_arrivalAerodrome_<br>_Alternate_is of<br>abstract type:<br>_fb:AerodromeRef_<br>_erenceType_<br>that can<br>instantiate as:<br>_ff:IcaoAerodrome_<br>_ReferenceType_<br> if the aerodrome<br>has an ICAO<br>designator, or:<br>_fb:UnlistedRefere_<br>_nceType,_<br>otherwise.<br>Type of<br>_arrivalAerodrome_<br>_Alternate/@code_<br>:<br>_ff:IcaoAerodrome_<br>_ReferenceType_<br>Type of<br>_arrivalAerodrome_<br>_/point:_<br>_fb:SignificantPoin_<br>_tType_(abstract<br>type that can<br>instantiate as:<br>_fb:FixPointType/_<br>_ff:GeographicalLo_<br>_cationType/_<br>_fb:RelativePointT_<br>_ype_)<br>Type of<br>_arrivalAerodrome_<br>_Alternate/@nam_|Yes|The aerodrome is specified using<br>its 4-letter ICAO name if it has<br>one.  If no ICAO location indicator<br>has been allocated, the<br>aerodrome is identified by its<br>name ("Dallas Fort Worth") or a<br>3-character IATA Alternate<br>Identifier ("DFW") and a<br>significant point consisting of one<br>of the following data:<br>•<br>geographic location (<br>latitude and longitude),<br>or<br>•<br>location of a fix<br>specified by name, or<br>•<br>fix/radial/distance<br>(FRD).<br>If the aerodrome has an ICAO<br>designator, the attribute_@code_<br>includes the ICAO code according<br>to the format:<br> **“[A-Z]{4}”**<br>Otherwise, if no ICAO location has<br>been allocated, the unlisted<br>aerodrome is identified by its<br>name (optionally) plus a<br>significant point according to the<br>following format:<br>_-arrivalAerodrome/@name_:<br>**xs:string**<br>-for _arrivalAerodrome/point_<br>there are three ways to specify<br>the significant point_:_<br>_1)_location of  fix<br>specified by name_(_type<br>f_b:FixPointType)_:<br> **“[A-Z0-9]{2,5}” **|<br>_@code_:<br>**KDFW**<br>_@name_:<br>**MILLSPA**<br>**W FARM**<br>_point/@fi_<br>_x:_<br>**HBZ**<br>_point/dist_<br>_ance_<br>(_@uom_<br>**NAUTICA**<br>**L_MILES):**<br>**10.0**<br>_point/radi_<br>_al_(_@uom_<br>**DEGREES**)<br>:<br>**236.0**|<br>No|

386

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||||_e_:<br>_fb:AerodromeNa_<br>_meType_||_2)_geographic location<br>specified by latitude and<br>longitude<br>_(ff:GeographicalLocationType):_<br>- list of two**xs:double**<br>(latitude followed by longitude)<br>3) fix-radial-distance<br>(_fb:RelativePointType):_<br>(a) fix:<br> **“[A-Z0-9]{2,5}”**<br>(b) distance<br>(_ff:DistanceType_):<br> **xs:double**<br>(c) radial<br>(_fb:DirectionType_):<br> **xs:double**<br> minInclusive =<br>0<br>maxInclusive<br>=360|||
|flight/enRoute/cleared/@clearance<br>Heading|FDB4thLin<br>eHeading_<br>155a|This element contains the En-<br>Route Controller Clearance<br>heading as entered by the<br>controller in the fourth line in<br>Full Data Block.|fb:FreeTextType|No|**“[A-Z0-9]{1,4}”**|**075**<br>**H075**|No|
|flight/enRoute/cleared/@clearance<br>Speed|FDB4thLin<br>eSpeed_1<br>55b|This element contains the En-<br>Route Controller Clearance<br>speed as entered by the<br>controller in the fourth line in<br>Full Data Block.|fb:FreeTextType|No|**"[A-Z0-9+-\.]{1,4}"**|280+<br>S260<br>M83+<br>.75-|No|
|flight/enRoute/cleared/@clearance<br>Text|FDB4thLin<br>eText_155<br>c|This element contains the free-<br>from text as entered by the En-<br>Route Controller, to be<br>associated with the Clearance<br>in the fourth line in Full Data<br>Block.|fb:FreeTextType|No|**"[A-Z0-9+-=\*/_;\.,\|^v]{1,8}"**|-BUFFI<br>NOBBL<br>BLVNS|No|

387

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/enRoute/beaconCodeAssign<br>ment/reassignedBeaconCode|externalBe<br>aconCode<br>_04b|Reassigned beacon code.<br>Identifies the downstream unit<br>that assigned the next beacon<br>code, in the case the beacon<br>code was already in use by<br>another flight at the<br>downstream unit.<br>**_Note_: **As of SFDPS R1.3.1, if<br>the<br>flight/flightStatus/@fdpsFlight<br>Status attribute has a value of<br>‘CANCELED or ‘PROPOSED,<br>this element is only present in<br>the version of a message with<br>FDPS_Restricted=’R’|fb:BeaconCodeTy<br>pe|No|**"[0-7]{4}"**<br>It has the same format as<br>currentBeaconCode.|**3434**|No|
|flight/agreed/route/@localIntende<br>dRoute|localInten<br>dedRoute_<br>10b|The Local Intended Route<br>attribute contains the flight<br>plan route that is coordinated<br>to penetrated facilities. It<br>consists of the flight plan route<br>merged with any expected-to-<br>be-applied-by-the-controlling-<br>center Adapted Departure<br>Routes (ADRs), Adapted<br>Departure Arrival Routes<br>(ADARs) or Adapted Arrival<br>Routes (AARs). It is intended<br>for the clients that wish to<br>know the expected state of the<br>flight plan when the current<br>facility releases control of the<br>flight. The attribute<br>localIntendedRoute contains<br>the filed route<br>(flight/agreed/route/@nasRou<br>teText)merged with any|_fb:FreeTextType_|No|**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-**<br>**9+\./]*\.[A-Z0-**<br>**9+/\*]{2,12}_?(/\d{4})?"**<br>Minimum length = 3<br>Maximum length = 4096||No|

388

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||locally applicable adapted<br>routes (preferential routes,<br>transition fixes and A-line<br>fixes). Optional<br>localIntendedRoute is sent to<br>ATM-IPOP, when the<br>localIntendedRoute is not the<br>same as filed route<br>(flight/agreed/route/@nasRou<br>teText).||||||
|flight/agreed/route/expandedRout<br>e/routePoint/point|fix_68c1|A route may contain an<br>optional expanded route that<br>consists of an ordered list of<br>expanded route points.<br>The expanded route<br>represents the expansion of<br>the route into a list of points<br>which describe the aircraft’s<br>expected 2D path from the<br>departure aerodrome to the<br>arrival aerodrome.<br>This element specifies a single<br>point that is part of the<br>aircraft’s expanded route of<br>flight.|fb:SignificantPoin<br>tType (abstract<br>type)<br>_fb:FixPointType/_<br>_ff:GeographicalLo_<br>_cationType/_<br>_fb:RelativePointT_<br>_ype_|Yes|-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|**KDFW**|No|
|flight/agreed/route/expandedRout<br>e/routePoint/@estimatedTime|crossingTi<br>me_68c2|This element specifies the<br>estimated time over the<br>expanded route point.|ff:TimeType|No|xs:dateTime|**2014-06-**<br>**20T20:17:**<br>**52**|No|
|flight/agreed/route/estimatedElaps<br>edTime/location<br>flight/agreed/route/estimatedElaps<br>edTime/@elapsedTime|EETIndicat<br>or_918b|This element specifies the<br>estimated amount of time<br>from takeoff to reach a<br>significant point or Flight<br>Information Region (FIR)<br>boundary along the route of|_location_:<br>fx:ElapsedTimeLo<br>cationType<br>_@elapsedTime_:|fx:El<br>aps<br>edT<br>ime<br>Loc<br>atio|The_location_associated with the<br>elapsed time can be_longitude_,<br>_significant point_or_region_(Flight<br>Information Region (FIR)<br>boundary):<br>-_longitude_:|location:<br>**KZNY**<br>@elapsed<br>Time:<br>**PT1H46M**|No|

389

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||the flight.|ff:DurationType|nTy<br>pe<br>(lon<br>gitu<br>de/<br>poi<br>nt/r<br>egi<br>on)<br>:<br>_Yes_<br>ff:D<br>urat<br>ion<br>Typ<br>e:<br>_No_|**xs:double**<br>-_point_:<br>- fb:FixPointType<br> **“[A-Z0-9]{2,5}”**<br>- ff:GeographicalLocationType<br>List of two**xs:double**<br>(latitude followed by longitude)<br>- fb:RelativePointType<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br>ff:DistanceType<br> **xs:double**<br>- radial:<br>fb:DirectionType<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360<br> -_region_:<br> **xs:string**<br>_@elapsedTime:_<br>**xs:duration**|||
|flight/routeToRevisedDestination/r<br>oute/@routeText|RIFIndicat<br>or_918c|This attribute specifies the<br>ICAO route text of a route to a<br>revised destination<br>aerodrome. The route text is<br>as depicted from the flight<br>plan.|fb:FreeTextType|No|Free-form string of up to 4,096<br>characters.<br>The destination aerodrome has to<br>be specified using the four-letter<br>ICAO location code.|**DTA HEC**<br>**KLAX**|No|
|flight/aircraftDescription/@registra<br>tion|REGIndicat<br>or_918d|A unique, alphanumeric string<br>that identifies a civil aircraft<br>and consists of the Aircraft<br>Nationality or Common Mark<br>and an additional<br>alphanumeric string assigned<br>by the state of registry or<br>common mark registering|fx:AircraftRegistr<br>ationType|No|**“[A-Z0-9]{1,7}”**<br>Up to 4,096 characters.|**N5258E**|No|

390

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||authority.||||||
|flight/aircraftDescription/capabiliti<br>es/communication/@selectiveCalli<br>ngCode|SELIndicat<br>or_918e|This attribute specifies the<br>Selective Calling (SELCAL)<br>Code that consists of two 2-<br>letter pairs. SELCAL is a<br>selective-calling radio system<br>that alerts aircraft crew to<br>incoming radio<br>communications. It acts as a<br>paging system for an ATS unit<br>to establish voice<br>communications with the pilot<br>of an aircraft.|fx:SelectiveCodeT<br>ype|No|**“[A-HJ-MP-S]{4}”**|**ACHA**<br>**BRLM**|No|
|flight/operator/operatingOrganizati<br>on/organization/@name|OPRIndicat<br>or_918f|This attribute specifies the full<br>official name of the State,<br>Organization, Authority,<br>aircraft operating agency,<br>handling agency engaged in or<br>offering to engage in aircraft<br>operation.|ff:TextNameType|No|xs:string<br>NOTE<br>Always map to organization.|UAL|No|
|flight/specialHandling|STSIndicat<br>or_918g|This element specifies the<br>special handling reason: a<br>property of the flight that<br>requires ATS units to give it<br>special consideration, such as<br>hospital aircraft.|fx:SpecialHandlin<br>gCodeType|No|The following are the only valid<br>special handling indicators:<br>**“ALTRV|ATFMX|FFR|FLTCK|HAZ**<br>**MAT|HEAD|HOSP|HUM|MARS**<br>**A|MEDEVAC|NONRVSM|SAR|S**<br>**TATE”**<br>NOTE<br>There could be multiple entries.|**ALTRV**|No|
|flight/aircraftDescription/aircraftTy<br>pe/otherModelData|TYPIndicat<br>or_918h|Other, non-ICAO,<br>identification of the aircraft.|fb:FreeTextType|No|Free-form string of up to 4,096<br>characters.|**CESNA14**<br>**0**|No|
|flight/aircraftDescription/@aircraft<br>Performance|PERIndicat<br>or_918i|A coded category assigned to<br>the aircraft based on a speed<br>directly proportional to its stall<br>speed, which functions as a<br>standardized basis for relating|fx:AircraftPerfor<br>manceCategoryT<br>ype|No|Single valid letter specified in<br>PAN-OPS 8168 Volume 1:<br>**“[ABCDEH]”**<br>where:|**C**|No|

391

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||aircraft maneuverability to<br>specific instrument approach<br>procedures.|||**A**– Indicated airspeed (IAS) less<br>than 169 km/h (91kt)<br>**B**– IAS between 169 km/h (91kt)<br>and 224 km/h (121 kt)<br>**C**– IAS between 224 km/h (121<br>kt) and 261 km/h ( 141 kt)<br>**D**– IAS between 261 km/h ( 141<br>kt) and 307 km/h (166 kt)<br>**E**- IAS between 307 km/h (166 kt)<br>and 391 km/h (211 kt)<br>**H**- Helicopters|||
|flight/aircraftDescription/capabiliti<br>es/communication/@otherCommu<br>nicationCapabilities|COMIndica<br>tor_918j|This element contains<br>additional Communication<br>Equipment available on<br>aircraft not specified in the<br>route/@nasRouteText<br>attribute.|fb:FreeTextType|No|Free-form string of up to 4,096<br>characters.|**HF ONLY**<br>**TCAS**|No|
|flight/aircraftDescription/capabiliti<br>es/communication/@otherDataLin<br>kCapabilities|DATIndicat<br>or_918k|This element specifies data<br>link capabilities available on<br>the aircraft.|fb:FreeTextType|No|**“[SHVM]{1,4}”**<br>Free-form string of up to 4,096<br>characters.<br>where:<br>**S**– satellite data link<br>**H**– HF data link<br>**V**– VHF data link<br>**M**– SSR Mode S data link<br>One or more of the valid letters<br>may be specified in this element.|**SV**|No|
|flight/aircraftDescription/capabiliti<br>es/navigation/@otherNavigationCa<br>pabilities|NAVIndica<br>tor_918l|This element contains<br>Navigation Equipment Data. It<br>is used for additional<br>Navigation Equipment<br>available on board of aircraft<br>not specified in the<br>route/@nasRouteText<br>attribute.|string|No|Free-form string of up to 4,096<br>characters.|**ADF ONLY**|<br>No|

392

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/departure/departureAerodro<br>me/@name<br>flight/departure/departureAerodro<br>me/point|DEPIndicat<br>or_918m|This element contains the<br>name of the unlisted<br>aerodrome from which the<br>flight departs.<br>If the departure aerodrome<br>has an ICAO designator, it is<br>stored in the attribute<br>flight/departure/@departure<br>Point, as suggested in 19.|Abstract type:<br>_fb:AerodromeRef_<br>_erenceType_<br>that instantiates<br>as:<br>_fb:UnlistedRefere_<br>_nceType_<br>Type of<br>_departureAerodr_<br>_omeAlternate/@_<br>_name_:<br>_fb:AerodromeNa_<br>_meType_<br>Type of<br>_departureAerodr_<br>_ome/point:_<br>_fb:SignificantPoin_<br>_tType_(abstract<br>type that can<br>instantiate as:<br>_fb:FixPointType/_<br>_ff:GeographicalLo_<br>_cationType/_<br>_fb:RelativePointT_<br>_ype_)|Yes|The unlisted aerodrome is<br>identified by its name (optionally)<br>plus a significant point according<br>to the following format:<br>_-departureAerodrome/@name_:<br>**xs:string**<br>-for _departurelAerodrome/point_<br>there are three ways to specify<br>the significant point_:_<br>_1)_location of  fix<br>specified by name_(_type<br>f_b:FixPointType)_:<br> **“[A-Z0-9]{2,5}”**<br>_2)_geographic location<br>specified by latitude and<br>longitude<br>_(ff:GeographicalLocationType):_<br>- list of two**xs:double**<br>(latitude followed by longitude)<br>3) fix-radial-distance<br>(_fb:RelativePointType):_<br>(a) fix:<br> **“[A-Z0-9]{2,5}”**<br> (b) distance<br>(_ff:DistanceType_):<br> **xs:double**<br>(c) radial<br>(_fb:DirectionType_):<br> **xs:double**<br> minInclusive =<br>0<br>maxInclusive<br>=360|_@name_:<br>**MILLSPA**<br>**W FARM**<br>_point/@fi_<br>_x:_<br>**HBZ**<br>_point/dist_<br>_ance_<br>(_@uom_<br>**NAUTICA**<br>**L_MILES):**<br>**10.0**<br>_point/radi_<br>_al_(_@uom_<br>**DEGREES**)<br>:<br>**236.0**|<br>No|
|flight/arrival/arrivalAerodrome/@n<br>ame<br>flight/arrival/arrivalAerodrome/poi<br>nt|DESTIndica<br>tor_918n|This element includes the<br>name and location of the<br>unlisted aerodrome at which<br>the flight is scheduled to<br>arrive.|Abstract type:<br>_fb:AerodromeRef_<br>_erenceType_<br>that instantiates|Yes|The unlisted aerodrome is<br>identified by its name (optionally)<br>plus a significant point according<br>to the following format:<br>_-arrivalAerodrome/@name_:|_@name_:<br>**MILLSPA**<br>**W FARM**<br>_point/@fi_|No|

393

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||If the arrival aerodrome has<br>an ICAO designator, it is<br>stored in the attribute<br>flight/arrival/@arrivalPoint, as<br>suggested in 19.|as:<br>_fb:UnlistedRefere_<br>_nceType_<br>Type of<br>_arrivalAerodrome_<br>_Alternate/@nam_<br>_e_:<br>_fb:AerodromeNa_<br>_meType_<br>Type of<br>_arrivalAerodrome_<br>_/point:_<br>_fb:SignificantPoin_<br>_tType_(abstract<br>type that can<br>instantiate as:<br>_fb:FixPointType/_<br>_ff:GeographicalLo_<br>_cationType/_<br>_fb:RelativePointT_<br>_ype_)||**xs:string**<br>-for _arrivalAerodrome/point_<br>there are three ways to specify<br>the significant point_:_<br>_1)_location of  fix<br>specified by name_(_type<br>f_b:FixPointType)_:<br> **“[A-Z0-9]{2,5}”**<br>_2)_geographic location<br>specified by latitude and<br>longitude<br>_(ff:GeographicalLocationType):_<br>- list of two**xs:double**<br>(latitude followed by longitude)<br>3) fix-radial-distance<br>(_fb:RelativePointType):_<br>(a) fix:<br> **“[A-Z0-9]{2,5}”**<br> (b) distance<br>(_ff:DistanceType_):<br> **xs:double**<br>(c) radial<br>(_fb:DirectionType_):<br> **xs:double**<br> minInclusive =<br>0<br>maxInclusive<br>=360|_x:_<br>**HBZ**<br>_point/dist_<br>_ance_<br>(_@uom_<br>**NAUTICA**<br>**L_MILES):**<br>**10.0**<br>_point/radi_<br>_al_(_@uom_<br>**DEGREES**)<br>:<br>**236.0**||
|flight/enRoute/alternateAerodrom<br>e|RALTIndica<br>tor_918p|This element identifies an En<br>Route Alternate Aerodrome to<br>which a flight could be<br>diverted while en route, if<br>needed. Multiple alternate<br>aerodromes may be specified.|Abstract type:<br>_fb:AerodromeRef_<br>_erenceType_that<br>instantiates as:<br>_ff:IcaoAerodrome_<br>_ReferenceType_<br>if the aerodrome<br>has an ICAO<br>designator, or as:|Yes|The aerodrome may be identified<br>by:<br>- ICAO code:<br>_alternateAerodrome/@code_:<br> **“[A-Z]{4}”**, or:<br>- name ("Dallas Fort Worth") or<br>3-character IATA Alternate<br>Identifier (such as "DFW”) plus<br>significant point, for an unlisted<br>aerodrome_, _accordingto the|<br>**KDFW**<br>or:<br>_@name_:<br>**MILLSPA**<br>**W FARM**<br>_point/@fi_<br>_x:_<br>**HBZ**<br>_point/dist_|No|

394

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||||_fb:UnlistedRefere_<br>_nceType_<br>otherwise.<br>_@code:_<br>_ff:IcaoAerodrome_<br>_ReferenceType_)<br>_@name_:<br>AerodromeName<br>Type<br>_point:_<br>_fb:SignificantPoin_<br>_tType_(abstract<br>type that can<br>instantiate as:<br>_fb:FixPointType/_<br>_ff:GeographicalLo_<br>_cationType/_<br>_fb:RelativePointT_<br>_ype_)||following format:<br>_-alternateAerodrome/@name_:<br>**xs:string**<br>-for _alternateAerodrome/point_<br>there are three ways to specify<br>the significant point_:_<br>_1)_location of  fix<br>specified by name_(_type<br>f_b:FixPointType)_:<br> **“[A-Z0-9]{2,5}”**<br>_2)_geographic location<br>specified by latitude and<br>longitude<br>_(ff:GeographicalLocationType):_<br>- list of two**xs:double**<br>(latitude followed by longitude)<br>3) fix-radial-distance<br>(_fb:RelativePointType):_<br>(a)_point/@fix_:<br> **“[A-Z0-9]{2,5}”**<br> (b)_point/distance_<br>(_ff:DistanceType_):<br> **xs:double**<br>(c)_point/radial_<br>(_fb:DirectionType_):<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|_ance_<br>(_@uom_<br>**NAUTICA**<br>**L_MILES):**<br>**10.0**<br>_point/radi_<br>_al_(_@uom_<br>**DEGREES**)<br>:<br>**236.0**||
|flight/aircraftDescription/@aircraft<br>Address|CODEIndic<br>ator_918q|A code that enables the<br>exchange of text-based<br>messages between suitably<br>equipped Air Traffic Service<br>(ATS) ground systems and<br>aircraft cockpit displays (the<br>aircraft Controller-Pilot Data<br>Link Communications (CPDLC)<br>address).|fx:AircraftAddres<br>sType|No|**“[0-9A-F]{6}”**|**45FA16**|No|

395

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|flight/aircraftDescription/capabiliti<br>es/surveillance/@otherSurveillance<br>Capabilities<br>SURIndicator_918s|SURIndicat<br>or_918s|This element specifies the<br>surveillance applications or<br>capabilities not specified in the<br>attribute<br>_flight/agreed/route/@localInte_<br>_ndedRoute_.|fb:FreeTextType|No|Free-form string of up to 4096<br>characters.|**282B**|No|
|flight/agreed/route/segment/route<br>Point/point<br>flight/agreed/route/segment/@del<br>ayAtPoint|DLEIndicat<br>or_918t|The element_routePoint/point_<br>specifies a single point along<br>the flight route.<br>The attribute<br>routePoint/@_delayAtPoint_<br>specifies the length of time the<br>flight is expected to be delayed<br>at this specific point en route.|_point_Type:<br>fb:SignificantPoin<br>tType (abstract<br>type)<br>_fb:FixPointType/_<br>_ff:GeographicalLo_<br>_cationType/_<br>_fb:RelativePointT_<br>_ype_<br>_@delayAtPoint_<br>_Type_:<br>ff:DurationType|Sign<br>ifica<br>ntP<br>oint<br>Typ<br>e<br>:Yes<br>Dur<br>atio<br>nTy<br>pe:<br>No|_point:_<br>-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360<br>_@delayAtPoint_:<br>xs:duration|Example<br>for_point:_<br>**MDG**<br>Example<br>for<br>_delayAtPo_<br>_int:_<br>**PT46M**|No|
|flight/departure/takeoffAlternateA<br>erodrome|TALTIndica<br>tor_918u|This element specifies an<br>alternate aerodrome at which<br>an aircraft can land, should it<br>become necessary shortly<br>after takeoff, and it is not<br>possible to land at the<br>departure aerodrome.<br>Multiple alternate takeoff<br>aerodromes may be specified.|fb:AerodromeRef<br>erenceType<br>ff:IcaoAerodrome<br>ReferenceType or<br>fb:UnlistedRefere<br>nceType|Yes|The aerodrome may be identified<br>by:<br>- its ICAO code ("KDFW")<br>(_ff:IcaoAerodromeReferenceType_)<br>in the attribute<br>_takeoffAlternateAerodrome/@co_<br>_de,_where the format is:<br> **“[A-Z]{4}”**<br>- its name ("Dallas Fort Worth")<br>or 3-character IATA Alternate<br>Identifier(such as "DFW”)|**KDFW**|No|

396

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||||||_takeoffAlternateAerodrome/@na_<br>_me_(optional) and a significant<br>point<br>_takeoffAlternateAerodrome/poin_<br>_t,_for an unlisted aerodrome<br>(_fb:UnlistedReferenceType_).<br>Format for<br>_takeoffAlternateAerodrome/@na_<br>_me:_<br>**xs:string**<br>Format for<br>_takeoffAlternateAerodrome_<br>_/point_:<br>-_fb:FixPointType_<br> **“[A-Z0-9]{2,5}”**<br>-_ff:GeographicalLocationType_<br>List of two**xs:double**<br>(latitude followed by longitude)<br>-_fb:RelativePointType_<br>- fix:<br> **“[A-Z0-9]{2,5}”**<br>- distance:<br> _ff:DistanceType_<br> **xs:double**<br>- radial:<br> _fb:DirectionType_<br> **xs:double**<br> minInclusive = 0<br>maxInclusive<br>=360|||
|flight/originator/aftnAddress<br>flight/originator/flightOriginator|ORGNIndic<br>ator_918w|<br>This element contains<br>information about the flight<br>originator that initiated the<br>flight. It specifies the<br>originator’s eight-letter<br>Aeronautical Fixed<br>Telecommunication Network<br>(AFTN)station address or|Type of<br>_originator/aftnAd_<br>_dress_:<br>fb:AftnAddressTy<br>pe<br>Type of<br>_originator/flight_|No|For_aftnAddress:_<br>**“[A-Z]{8}”**<br>For _flightOriginator:_<br>Free-form string of up to 4096<br>characters.|**LEBBYNY**<br>**X**|No|

397

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||other appropriate contact<br>details, in cases where the<br>originator of the flight plan<br>may not be readily identified,<br>as required by the appropriate<br>ATS authority.|_Originator_:<br>fb:FreeTextType|||||
|flight/aircraftDescription/capabiliti<br>es/navigation/performanceBasedC<br>ode|PBNIndicat<br>or_918x|This element specifies acoded<br>category denoting which<br>Required Navigation<br>Performance (RNP) and Area<br>Navigation (RNAV)<br>requirements can be met by<br>the aircraft while operating in<br>the context of a particular<br>airspace when supported by<br>the appropriate navigation<br>infrastructure.|fx:PerformanceB<br>asedCodeType|No|**“A1|B[1-6]|C[1-4]|D[1-**<br>**4]|L1|O[1-4]|S[1-2]|T[1-2]”**<br>_RNAV_and_RNP_capabilities are<br>two-characters each, as follows:<br>_RNAV_specifications:<br>**A1**RNAV10 (RNP 10)<br>**B1**RNAV 5 all permitted sensors<br>**B2**RNAV 5 GNSS<br>**B3**RNAV 5 DME/DME<br>**B4**RNAV 5 VOR/DME<br>**B5**RNAV 5 INS or IRS<br>**B6**RNAV 5 LORANC<br>**C1**RNAV 2 all permitted sensors<br>**C2**RNAV 2 GNSS<br>**C3**RNAV 2 DME/DME<br>**C4**RNAV 2 DME/DME/IRU<br>**D1**RNAV 1 all permitted sensors<br>**D2**RNAV 1 GNSS<br>**D3**RNAV 1 DME/DME<br>**D4**RNAV 1 DME/DME/IRU<br>_RNP_specifications:<br>**L1**RNP 4<br>**O1**Basic RNP 1 all permitted<br>sensors<br>**O2**Basic RNP 1 GNSS<br>**O3**Basic RNP 1 DME/DME<br>**O4**Basic RNP 1 DME/DME/IRU|**B1O1**|No|

398

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||||||**S1**RNP APCH<br>**S2**RNP APCH with BAR-VNAV<br>**T1**RNP AR APCH with RF (special<br>authorization required)<br>**T2**RNP AR APCH without RF<br>(special authorization required)|||
|flight/supplementalData/additional<br>FlightInformation/nameValue/@na<br>me<br>flight/supplementalData/additional<br>FlightInformation/nameValue/@val<br>ue|ICAO1stAd<br>aptedField<br>18_999a<br>ICAO1stAd<br>aptedField<br>18_999b<br>ICAO1stAd<br>aptedField<br>18_999c<br>ICAO1stAd<br>aptedField<br>18_999d<br>ICAO1stAd<br>aptedField<br>18_999e<br>ICAO1stAd<br>aptedField<br>18_999f<br>ICAO1stAd<br>aptedField<br>18_999g<br>ICAO1stAd<br>aptedField<br>18_999h<br>ICAO1stAd<br>aptedField<br>18_999i<br>ICAO1stAd<br>aptedField<br>18_999j|Additional information about a<br>flight that does not fall into<br>other predefined category. The<br>information is expressed in<br>key-value pairs. The element<br>consists of an identification<br>tag/indicator and the relevant<br>value.<br>**NOTE**<br>There are 25 fields that could<br>be stored under the element<br>_additionalFlightInformation_<br>but only 10 slots allowed in<br>FIXM.  Additionally, SFDPS is<br>planning on using some of<br>these slots for storing a<br>number SFDPS specific items<br>that did not seem to be a good<br>choice for addition in the FIXM<br>U.S. Extension.  Data analysis<br>has shown no more than five<br>of these adapted field 18<br>entries tend to appear in the<br>actual data feed but this is a<br>definite risk if more begin to<br>show up.|Type of<br>_additionalFlightIn_<br>_formation_is a list<br>of up to 10 name-<br>value pairs:<br>_fb:NameValueList_<br>_Type_<br>Type of<br>_nameValue_:<br>_fb:NameValuePai_<br>_rType_<br>Type for attribute<br>_name_:<br>_fb:FreeTextType_<br>Type for attribute<br>_value_:<br>_fb:FreeTextType_|No|Format for_@name:_<br>**“[A-Z0-9_]{1,20}”**<br>Format for_@value:_<br>**xs:string**<br>**minLength=1, maxLength=100**||No|

399

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||ICAO1stAd<br>aptedField<br>18_999k<br>ICAO1stAd<br>aptedField<br>18_999l<br>ICAO1stAd<br>aptedField<br>18_999m<br>ICAO1stAd<br>aptedField<br>18_999n<br>ICAO1stAd<br>aptedField<br>18_999o<br>ICAO1stAd<br>aptedField<br>18_999p<br>ICAO1stAd<br>aptedField<br>18_999q<br>ICAO1stAd<br>aptedField<br>18_999r<br>ICAO1stAd<br>aptedField<br>18_999s<br>ICAO1stAd<br>aptedField<br>18_999t<br>ICAO1stAd<br>aptedField<br>18_999u<br>ICAO1stAd|||||||
||aptedField<br>18_999v|||||||

400

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||ICAO1stAd<br>aptedField<br>18_999w<br>ICAO1stAd<br>aptedField<br>18_999x<br>ICAO1stAd<br>aptedField<br>18_999y|||||||
|flight/aircraftDescription/accuracy/<br>cmsFieldType|RNVArrival<br>_925a<br>…→_925f<br>RNPArrival<br>_925g …<br>→<br>RNP…_925<br>l|<br>This element specifies the<br>flight's navigation accuracy<br>value for the phase of flight,<br>specified in the Performance-<br>Based Navigation Phase,<br>included in the attribute<br>_@phase_, and for the<br>Performance-Based Navigation<br>Category specified in the<br>attribute_@type_.|nas:CmsAccuracy<br>Type|No|**xs:double**|Accuracy<br>of 0.3 nm:<br>0.3<br>cmsFieldT<br>ype/@uo<br>m =<br>“NAUTICA<br>L_MILES”|No|
|flight/aircraftDescription/accuracy/<br>cmsFieldType/@type|RNVArrival<br>_925a<br>…→_925f<br>RNPArrival<br>_925g …<br>→<br>RNP…_925<br>l|<br>This element specifies the<br>Performance-Based Navigation<br>Category that indicates<br>whether the accuracy measure<br>in Performance-Based<br>Navigation Accuracy is<br>measuring Area Navigation<br>(RNAV) or Required Navigation<br>Performance(RNP).|nas:CmsAccuracy<br>TypeType|No|**“RNV|RNP”**|**RNV**|No|
|flight/aircraftDescription/accuracy/<br>cmsFieldType/@phaseflight/aircraf<br>tDescription/accuracy/cmsFieldTyp<br>e/@uom|RNVArrival<br>_925a<br>…→_925f<br>RNPArrival<br>_925g …<br>→<br>RNP…_925<br>l|<br>This element specifies the<br>Performance-Based Navigation<br>Phasethat indicates the phase<br>of flight for which navigation<br>performance is being<br>recorded.|nas:NasPerforma<br>nceBasedNavigat<br>ionPhaseType||”**DEPARTURE|ARRIVAL|ENROUT**<br>**E|OCEANIC|SPARE_1|SPARE_2**”|**DEPARTU**<br>**RE**|No|
|flight/aircraftDescription/accuracy/<br>cmsFieldType/@uom|<br>RNVArrival<br>_925a|This element specifies the|ff:DistanceMeasu|No|**“KILOMETERS|NAUTICAL_MILES**|**NAUTICA**|Yes|

401

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||…→_925f<br>RNPArrival<br>_925g …<br>→<br>RNP…_925<br>l|units of measure for distance.|reType||**|MILES”**|**L_MILES**||
|flight/enRoute/position/altitude|reconRepo<br>rtedAlt_24<br>60|This element specifies the<br>reported altitude that is the<br>latest valid Mode C altitude<br>received from an aircraft or<br>the latest reported altitude<br>received from a pilot.|ff:AltitudeType|Yes|xs:double|24000<br>@uom=FE<br>ET|No|
|flight/enRoute/position/altitude/@<br>uom|reconRepo<br>rtedAlt_24<br>60|This element specifies the unit<br>of measure for altitude.|ff:AltitudeMeasu<br>reType|No|**“FEET|METRES”**|FEET|Yes|
|flight/departure/runwayPositionAn<br>dTime/runwayTime/controlled|cancellatio<br>nIndicator<br>_92b|This optional element is<br>included to indicate a<br>cancellation.|Element value set<br>to NULL:<br>xsi:nill=”true”|No|**NULL**||No|
|flight/agreed/route/@atcIntended<br>Route|ATCIntend<br>edRoute_1<br>0c|The current cleared flight plan<br>route with any<br>unacknowledged auto routes<br>(preferential routes, transition<br>fixes and A-line fixes) already<br>applied.|fb:FreeTextType|No|**"[A-Z0-9+/\*]{2,12}_?\.[A-Z0-**<br>**9+\./]*\.[A-Z0-**<br>**9+/\*]{2,12}_?(/\d{4})?"**<br>Minimum length = 3<br>Maximum length = 1000|**JFK.J42.T**<br>**XK.STAR1**<br>**.DFW**|No|
|flight/aircraftDescription/capabiliti<br>es/@standardCapabilities|comNavAp<br>proachEqu<br>ipICAO201<br>2_910c|If present,this element<br>indicates that aircraft has the<br>"standard" capabilities for the<br>flight.|fx:StandardCapa<br>bilitiesIndicatorT<br>ype|No|**restriction of xs:string**<br>**“STANDARD”**|**STANDAR**<br>**D**|No|
|flight/aircraftDescription/capabiliti<br>es/communication/communication<br>Code|comNavAp<br>proachEqu<br>ipICAO201<br>2_910c|This element describes the<br>aircraft communication code.|fx:Communicatio<br>nCodeType|No|**“E[1-3]|H|M[1-3]|P[1-9]|[UVY]”**<br>Where:<br>E1 – FMC WPR ACARS<br>E2 – D-FIS ACARS<br>E3 – PDC ACARS<br>H – HF RTF<br>M1 – ATC RTF SATCOM|<br>E1|No|

402

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|<br>**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||||||(INMARSAT)<br>M2 - ATC RTF SATCOM (MTSAT)<br>M3 – ATC RTF (Iridium)<br>P1-P9 – Reserved for RCP<br>U – UHF RTF<br>V – VHF RTF<br>Y – VHF with 8.33 kHz spacing<br>capacity|||
|flight/aircraftDescription/capabiliti<br>es/communication/dataLinkCod|comNavAp<br>proachEqu<br>ipICAO201<br>2_910c|This element specifies Data<br>Link Communication<br>Capabilities that consist in<br>serviceable equipment and<br>capabilities available on the<br>aircraft at the time of flight<br>that may be used to<br>communicate data to and from<br>the aircraft.|fx:DataLinkCodeT<br>ype|No|**“J[1-7]”**<br>Where:<br>J1 – CPDLC ATN VDL Mode 2<br>J2 – CPDLC FANS 1/A HDFL<br>J3 - CPDLC FANS 1/A VDL Mode A<br>J4 - CPDLC FANS 1/A VDL Mode 2<br>J5 - CPDLC FANS 1/A SATCOM<br>(INMARSAT)<br>J6 - CPDLC FANS 1/A SATCOM<br>(MTSAT)<br>J7 - CPDLC FANS 1/A SATCOM<br>(Iridium)|J2|No|
|flight/aircraftDescription/capabiliti<br>es/navigation/navigationCode|comNavAp<br>proachEqu<br>ipICAO201<br>2_910c|This element describes the<br>aircraft navigation code.|fx:NavigationCod<br>eType|No|**“[ABCDFGIKLOTWX]”**<br>Where:<br>**A**– GBAS landing system<br>**B**– LPV (APV with SBAS)<br>**C**– LORAN C<br>**D**– DME<br>**F**– ADF<br>**G**– GNSS<br>**I**– Inertial Navigation<br>**K**– MLS<br>**O**– VOR<br>**T**– TACAN<br>**W**– RVSM approved|A|No|

403

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||||||**X**– MNPS approved|||
|flight/aircraftDescription/capabiliti<br>es/surveillance/surveillanceCode|survEquipI<br>CAO2012_<br>910d|This elementdescribes the<br>aircraft surveillance code.|fx:SurveillanceCo<br>deType|No|**“[ACEHILPSX]|[BUV][12]|D1|G1**<br>**"**<br>where:<br>**A**– Transponder Mode A<br>**C**– Transponder Mode A and C<br>**E**– Transponder – Mode S,<br>including aircraft identification,<br>pressure-altitude and extended<br>squitter (ADS-B) capability<br>**H**– Transponder – Mode S,<br>including aircraft identification,<br>pressure-altitude and enhanced<br>surveillance capability<br>**I**- Transponder – Mode S,<br>including aircraft identification,<br>but no pressure-altitude<br>capability<br>**L**– Transponder – Mode S,<br>including aircraft identification,<br>pressure-altitude, extended<br>squitter (ADS-B) and enhanced<br>surveillance capability<br>**P**– Transponder – Mode S,<br>including pressure-altitude, but<br>no aircraft identification<br>**S**– Transponder – Mode S,<br>including both pressure-altitude<br>and aircraft identification<br>capability<br>**X**– Transponder - Mode S with<br>neither aircraft identification nor<br>pressure-altitude capability<br>**B1**– ADS-B with dedicated 1090<br>mHz ADS-B “out” capability<br>**B2**– ADS-B with dedicated 1090|HB2U2V2<br>G|No|

404

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[DBRTFPI_FIXM]**|**Name**<br>**[DBRTFPI]**|**Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible Values**|**Example**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
||||||mHz ADS-B “out” and “in”<br>capability<br>**U1**- ADS-B “out” capability using<br>UAT<br>**U2**- ADS-B “out” AND “IN”<br>capability using UAT<br>**V1**- ADS-B “out” capability using<br>VDL Mode 4<br>**V2**- ADS-B “out” and “in”<br>capability using VDL Mode 4<br>**D1**– ADS-C with FANS 1/A<br>capabilities<br>**G1**- ADS-C with ATN capabilities|||

#### **5.5.2 Airspace Data Publication Service Data Elements and Diagrams**

##### **5.5.2.1 ERADP Service: targetNamespace**

The targetNamespace that applies to all messages in the Airspace Data Publication Service is: **us:gov:dot:faa:atm:enroute:entities:flightdata**

##### **5.5.2.2 Sector Assignment Status [SH] – Data Elements**

|**Element Name**<br>**[SH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed<br>by a four-digit sequence|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are|Yes|

405

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[SH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||number.|||message sequence number in the range<br>[0000-9999].|sequence number of<br>the message (9001).||
|sourceTime_00e1|This element specifies the<br>time component of the<br>previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|sector|This element is used to group<br>the following elements:<br>sector_29a,**n**oFAV_29c, and<br>FAVAssignments, The<br>element FAVAssignments is<br>used to group, between one<br>and 437 FAV_29d elements.<br>Each sector element can<br>include one sector_29a<br>element, followed by either a<br>noFAV_29c element or a<br>FAVAssignments element.|T_airspaceA<br>ssignment|Yes|This element can appear from one to<br>one hundred times.||Yes|
|tracon|This element is used to group<br>the following elements:<br>tracon_29g,<br>traconNoFAV_29h,<br>traconFAVAssignments,  Each<br>tracon element can include<br>one tracon_29g element,<br>followed by either a<br>traconNoFAV_29h element or<br>a traconFAVAssignments<br>element.|T_traconAss<br>ignment|Yes|The tracon element can appear from<br>zero to one hundred times.||No|
|sector_29a|This element provides the|string|No|**“\d{2}”**|53|Yes|

406

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[SH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||sector number, for which the<br>following FAV data applies.|||The format consists of two digits, with<br>leading zeroes as needed.|**09**||
|noFAV_29c|When this element is present<br>in the message, it indicates<br>that there is no FAV<br>assignment for this sector.<br>Either this element or the<br>element FAVAssignments<br>must be present in a<br>message.|string|No|**“-“**<br>Only one valid value, “-“(a dash).|**-**|No|
|FAVAssignments|This element groups the<br>following_FAV_29d_elements.<br>There can be from one to 437<br>FAV_29d elements in each<br>FAVAssignments element.<br>Either this element or<br>noFAV_29c must be present<br>in the element_tracon_.||Yes|||No|
|FAV_29d|This element provides the<br>FAV Airspace Assignment<br>number|string|No|**"\d{4}"**<br>The format consists of four digits, with<br>leading zeroes as needed.|0053<br>2509|No|
|tracon_29g|This element provides the<br>tracon identifier, for which<br>the following FAV data<br>applies.|string|No|**"[A-Z0-9]{3}"**|PIP|No|
|traconNoFAV_29h|When this element is<br>included in the message, it<br>indicates that there is no FAV<br>assignment for this sector. If<br>this field appears,<br>_FAVAssignments_element is<br>not be included in the<br>message.|string|No|**“-“**<br>It has only one allowed value, - (a dash).|**-**|No|
|traconFAVAssignments|This element groups the<br>following_traconFAV_29i_<br>elements. There can be from||Yes|||No|

407

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[SH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||one to 437_traconFAV_29i_<br>elements in each<br>_traconFAVAssignments_<br>element.<br>If this element appears in the<br>message, element<br>_traconNoFAV_29h_is not<br>included in the message.||||||
|traconFAV_29i|This element provides the<br>FAV Airspace Assignment<br>number.|string|No|**“\d{4}”**<br>The format consists of four digits.<br>Leading zeroes are included when<br>necessary.|0053<br>2509|No|

408

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.2.3 Sector Assignment Status [SH] - Diagram**

##### **5.5.2.4 Sector Assignment Status Message in AIXM Format [SH_AIXM] – Data Elements**

The following elements of the SH message in Simple XML format are not used in the AIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

- sector

- tracon

- noFAV_29c

- FAVAssignments

409

NAS-JMSDD-4309-001 Rev C July 10, 2018

- tracon_29g

- traconNoFAV_29h

- traconFAVAssignments

- traconFAV_29i

|**Element Name**<br>**[SH_AIXM]**|**Eleme**<br>**nt**<br>**Name**<br>**[SH]**|<br>**Element Definition**|**Type**|**Com**<br>**plex**<br>**?**|**Format/Per**<br>**missible**<br>**Values**|**Example**|**Re**<br>**qui**<br>**red**<br>**?**|
|---|---|---|---|---|---|---|---|
|AIXMBasicMessage/hasMember/<br>Airspace/timeSlice/AirspaceTime<br>Slice/aixm:interpretation||Property indicating how the time<br>slice is to be interpreted.|string|No|“SNAPSHOT”|“SNAPSHOT”|Yes|
|AIXMBasicMessage/hasMember/<br>Airspace/timeSlice/AirspaceTime<br>Slice/type||A coded list of values that indicates<br>a type of airspace.|aixm:CodeAirspaceType|Yes|“SECTOR”|“SECTOR”|Yes|
|AIXMBasicMessage/hasMember/<br>Airspace/timeSlice/AirspaceTime<br>Slice/designator<br><br>|sector<br>_29a|This element provides the sector<br>number, for which the FAV data<br>applies.|aixm:CodeAirspaceDesignatorType|Yes|**“\d{2}”**|53<br>09|Yes|
|AIXMBasicMessage/hasMember/<br>extension/SectorAssignmentStat<br>usExtension/FAVNumber<br><br>|FAV_2<br>9d|This element provides the FAV<br>Airspace Assignment number, or a<br>code (a dash character) that<br>indicates that there is no FAV<br>assignment for this sector.|aixm:TextNameType|No|**"\d{4}|\-"**<br>There may<br>be up to 437<br>FAV<br>numbers for<br>each sector<br>defined.|**7801**<br>**“-“**|Yes|

##### **5.5.2.5 Route Status [HR] – Data Elements**

|**Element Name**<br>**[HR]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed<br>by a four-digit sequence|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_)<br>and the last four digits,represent|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and|Yes|

410

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HR]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||number.|||the message sequence number in<br>the range [0000-9999].|the last 4 digits are<br>sequence number of<br>the message (9001).||
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_<br>stands for the 2-digit minutes in<br>the range 00-59, and_ss_stands for<br>the 2-digit seconds in the range 00-<br>59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|routeStatus|This element groups the<br>following two elements,<br>routeStatusElements_135a<br>and actionIndicator_36a.|T_routeSt<br>atus|Yes|This element can be repeated from<br>one to 281 times.||Yes|
|routeStatusElements_135a|This element contains the<br>adapted route status<br>elements. The adapted names<br>are Standard Instrument<br>Departures (SID), Standard<br>Terminal Arrival Routes (STAR),<br>Adapted Arrival Routes (AAR),<br>Adapted Departure Routes<br>(ADR) and Adapted Departure<br>and Arrival Routes (ADAR) that<br>are active when initialization<br>begins.|string|No|**"[A-Z0-9]{2,6}"**<br>The format is two to six<br>alphanumeric characters.|SD001|Yes|
|actionIndicator_36a|This element shows the status<br>of the route elements in<br>element_actionIndicator_36a_.|string|No|**“(ON)|(OFF)”**<br>It can have one of two possible<br>values: ON or OFF.|**ON**<br>**OFF**|Yes|

411

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.2.6 Route Status [HR] - Diagram**

##### **5.5.2.7 Route Status Message in AIXM Format [HR_AIXM] – Data Elements**

The following elements of the HV message in Simple XML format are not used in the AIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

|**Element Name**<br>**[HR_AIXM]**|**Element**<br>**Name**<br>**[HR]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Exampl**<br>**e**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|AIXMBasicMessage/hasMember|routeStat<br>us|This element contains the RouteSegment with the<br>route name and the route status specified.|message:BasicMessageMemberAI<br>XMPropertyType|Yes|maxOccurs=”unboun<br>ded”||Yes|
|AIXMBasicMessage/hasMember/R<br>outeSegment/gml:name|routeStat<br>usEleme<br>nts_135a|This element contains the adapted route names.<br>The adapted names are Standard Instrument<br>Departures (SID), Standard Terminal Arrival Routes<br>(STAR), Adapted Arrival Routes (AAR), Adapted<br>Departure Routes(ADR)and Adapted Departure|gml:CodeType|Yes|**"[A-Z0-9]{2,6}"**<br>The format is two to<br>six alphanumeric<br>characters.|SD001|Yes|

412

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HR_AIXM]**|**Element**<br>**Name**<br>**[HR]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Exampl**<br>**e**|**Requ**<br>**ired?**|
|---|---|---|---|---|---|---|---|
|||and Arrival Routes (ADAR) that are active when<br>initialization begins.||||||
|AIXMBasicMessage/hasMember/R<br>outeSegment/timeSlice/RouteSeg<br>mentTimeSlice[interpretation=”SN<br>APSHOT”]/availability/RouteAvaila<br>bility/status|actionInd<br>icator_36<br>a|This element shows the availability status of the<br>route segment element.|aixm:CodeRouteAvailabilityType|Yes|**“(OPEN)|(CLSD)”**|**OPEN**|Yes|

##### **5.5.2.8 Route Status Message in AIXM Format [HR_AIXM] – Diagram**

413

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.2.9 Special Activities Airspace (SAA) [SU] – Data Elements**

|**Element Name**<br>**[SU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed<br>by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of<br>the message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|saaId_161a|This element specifies the ID<br>for the special activities<br>airspace|string|No|**“[A-Z0-9]{1,10}”**<br>It consists of one to ten alphanumeric<br>characters.|SHPT38ALPHA<br>Specifies: SHP Air<br>Force BASE training<br>area “Alpha” for<br>T38s.|Yes|
|saaActivationType_162a|This element provides the<br>status of the SAA area.|string|No|**“(ON)|(OFF)|(SCHED)”**<br>There are three possible values: ON<br>(area is active), OFF (area is not active),<br>SCHED (area activation is controlled by<br>schedule).|**ON**<br>**OFF**<br>**SCHED**|Yes|
|saaAltRange|This element groups together<br>the following two elements:<br>saaLowAlt_165a and<br>saaHighAlt_165b.|group|Yes|Either this element or _saaSchedule_may<br>appear in a message.||No|
|saaLowAlt_165a|This element contains the|integer|No|Integer in the range -2000 – 100000.|**5000**|No|

414

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[SU]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||lower limit of the altitude<br>range for the SAA, expressed<br>in feet.||||||
|saaHighAlt_165b|This element contains the<br>higher limit of the altitude<br>range for the SAA, expressed<br>in feet.|integer|No|Integer in the range -2000 – 100000.|**30000**|No|
|saaSchedule|This element groups together<br>the following elements:<br>_saaScheduleId_166a,_<br>_saaScheduleType_163a,_<br>_saaSchedActivationTime_164a,_<br>_saaSchedDeactivationTime_16_<br>_4b,_and_saaAltRange._|group|Yes|Either this element or _saaAltRange_may<br>appear in a message.<br>This element may appear between zero<br>and 14 times in the SU message.||No|
|saaScheduleId_166a|This element contains the SAA<br>schedule ID followed by a<br>sequence number.|string|No|**"[A-Z]{3}\d{10}"**<br>The format is three letters followed by<br>ten digits.|SHP0000000016|Yes|
|saaScheduleType_163a|This element contains the SAA<br>schedule type. The Schedule<br>Type describes whether the<br>activity is for the SAA is<br>Scheduled or Deleted.|string|No|**“S|D”**<br>The following formats are valid:<br>• “S” = scheduled<br>• “D” = deleted|**S**<br>**D**|Yes|
|saaSchedActivationTime_164a|This element contains the<br>dates and UTC times of an<br>activation period.|string|No|**"\d{6}"**<br>Date/time format_ddhhmm_, where:_dd_:<br>day of month,_hh_: UTC hour,_mm_: UTC<br>minute.|**302030**|No|
|saaSchedDeactivationTime_164<br>b|This element contains the<br>dates and UTC times of a<br>deactivation period.|string|No|**"\d{6}"**<br>Date/time format_ddhhmm_, where:_dd_:<br>day of month,_hh_: UTC hour,_mm_: UTC<br>minute.|**302330**|No|

415

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.2.10 Special Activities Airspace (SAA) [SU] – Diagram**

##### **5.5.2.11 Special Activities Airspace (SAA) in AIXM Format [SU_AIXM] – Data Elements**

The following elements of the HV message in Simple XML format are not used in the AIXM format of the message:

- sourceId_00e

- sourceTime_00e1

- sourceSeqNo_00e2

416

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[SU_AIXM]**|**Name**<br>**[SU]**|<br>**Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/aix<br>m:interpretation||Property indicating how the time slice is<br>to be interpreted.|string|No|**“SNAPSHOT”**|**“SNAPSHOT”**|Yes|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/typ<br>e||This element contains a code indicating<br>the general structure or characteristics of<br>a particular airspace.It contains the code<br>“R” that indicates restricted area.<br>Restricted area is defined as airspace of<br>defined dimensions, above the land areas<br>or territorial waters of a state, within<br>which the flight of aircraft is restricted in<br>accordance with certain specified<br>conditions.|aixm:CodeAirspaceType|Yes|**“R”**|**“R”**|Yes|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/des<br>ignator|saaId_<br>161a|This element specifies the ID for the<br>special activities airspace. It consists in a<br>published sequence of characters<br>allowing the identification of the airspace.|aixm:CodeAirspaceDesigna<br>torType|Yes|**“[A-Z0-9]{1,10}”**<br>It consists of one to ten<br>alphanumeric characters.|**SHPT38ALPHA**<br>Specifies: SHP Air<br>Force BASE<br>training area<br>“Alpha” for T38s.|Yes|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/act<br>ivation/AirspaceActivation/status|saaActi<br>vation<br>Type_<br>162a|This element provides the status of the<br>SAA area.|aixm:CodeStatusAirspaceT<br>ype|Yes|**“(ACTIVE)|(**<br>**ACTIVE)|(AVBL_FOR_ACTI**<br>**VATION)”**<br>There are three possible<br>values:**ACTIVE**(area is<br>active),**ACTIVE**(area is not<br>active),<br>**AVBL_FOR_ACTIVATION**<br>(area activation is<br>controlled by schedule).|**AVBL_FOR_ACTI**<br>**VATION**|Yes|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/ge<br>ometryComponent/AirspaceGeometr<br>yComponent/the AirspaceVolume<br>/AirspaceVolume|saaAlt<br>Range|A defined volume in the air, described as<br>horizontal projection with vertical limits.<br>The element_AirspaceVolume_has sub<br>elements_AirspaceVolume/lowerLimit_and<br>_AirspaceVolume/upperLimit_.|aixm: AirspaceVolumeType|Yes|||No|

417

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[SU_AIXM]**|**Name**<br>**[SU]**|**Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/ge<br>ometryComponent/AirspaceGeometr<br>yComponent/the AirspaceVolume<br>/AirspaceVolume/lowerLimit|saaLo<br>wAlt_1<br>65a|This element contains the lower limit of<br>the altitude range for the SAA. The<br>attribute_uom_contains the unit of<br>measurement for this element.|aixm:ValDistanceVerticalTy<br>pe|Yes|Integer|**5000**<br>uom=**FT**|No|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/ge<br>ometryComponent/AirspaceGeometr<br>yComponent/the AirspaceVolume<br>/AirspaceVolume/lowerLimit/@uom||This attribute contains the unit of<br>measurement for vertical distance.|aixm:UomDistanceVertical<br>Type|No|“FT|M|FL|SM|OTHER”<br>where:<br>FT=feet<br>M=meters<br>FL=flight level in hundreds<br>of feet<br>SM=standard meters (tens<br>of meters)|**FT**|Yes|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/ge<br>ometryComponent/AirspaceGeometr<br>yComponent/the AirspaceVolume<br>/AirspaceVolume/upperLimit|saaHig<br>hAlt_1<br>65b|This element contains the higher limit of<br>the altitude range for the SAA. The<br>attribute_uom_contains the unit of<br>measurement for this element.|aixm:ValDistanceVerticalTy<br>pe|Yes|Integer|**30000**<br>uom=**FT**|No|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/ge<br>ometryComponent/AirspaceGeometr<br>yComponent/the AirspaceVolume<br>/AirspaceVolume/upperLimit/@uom||This attribute contains the unit of<br>measurement for vertical distance.|aixm:UomDistanceVertical<br>Type|No|“FT|M|FL|SM|OTHER”<br>Where:<br>FT=feet<br>M=meters<br>FL=flight level in hundreds<br>of feet<br>SM=standard meters (tens<br>of meters)|**FT**|Yes|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/ext<br>ension/SAAScheduleExtension|saaSch<br>edule|This element has the following sub<br>elements:<br>ID, type, activationDateTime, and<br>deactivationDateTime.|SAAScheduleExtensionTyp<br>e|Yes|||No|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/ext<br>ension/ SAAScheduleExtension/ID|saaSch<br>eduleI<br>d_166<br>a|This element contains the SAA schedule<br>ID followed by a sequence number.|aixm:TextNameType|No|**"[A-Z]{3}\d{10}"**|ZAB0000000016|No|

418

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Name**<br>**[SU_AIXM]**|**Name**<br>**[SU]**|<br>**Definition**|**Type**|**Compl**<br>**ex?**|**Format/Permissible**<br>**Values**|**Example**|**Requi**<br>**red?**|
|---|---|---|---|---|---|---|---|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/ext<br>ension/AbstractAirspaceExtension/SA<br>AScheduleExtension/type|saaSch<br>eduleT<br>ype_1<br>63a|This element contains the SAA schedule<br>type. The Schedule Type describes<br>whether the activity is for the SAA is<br>Scheduled or Deleted.|aixm:TextNameType|No|**“S|D”**<br>where:<br>• “S” = scheduled<br>• “D” = deleted|**S**|No|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/ext<br>ension/SAAScheduleExtension/activat<br>ionDateTime|saaSch<br>edActi<br>vation<br>Time_<br>164a|This element contains the dates and UTC<br>times of an activation period.|aixm:TextNameType|No|**"\d{6}"**<br>Date/time format<br>_ddhhmm_, where:_dd_: day<br>of month,_hh_: UTC hour,<br>_mm_: UTC minute.|**302030**|No|
|AIXMBasicMessage/hasMember/Airs<br>pace/timeSlice/AirspaceTimeSlice/ext<br>ension/SAAScheduleExtension/deacti<br>vationDateTime|saaSch<br>edDea<br>ctivati<br>onTim<br>e_164<br>b|This element contains the dates and UTC<br>times of a deactivation period.|aixm:TextNameType|No|**"\d{6}"**<br>Date/time format<br>_ddhhmm_, where:_dd_: day<br>of month,_hh_: UTC hour,<br>_mm_: UTC minute.|**302330**|No|

##### **5.5.2.12 Altimeter Setting [HA] – Data Elements**

|**Element Name**<br>**[HA]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed<br>by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_)<br>and the last four digits, represent the<br>message sequence number in the<br>range [0000-9999].|**2359359001**, where<br>the first 6 digits are<br>the UTC time<br>(23:59:35 UTC) and<br>the last 4 digits are<br>sequence number of<br>the message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_stands<br>for the 2-digit minutes in the range|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|

419

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HA]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||00-59, and_ss_stands for the 2-digit<br>seconds in the range 00-59.|||
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|observedTime_35a|This element represents the<br>time of the observed altimeter<br>setting.|dateTime|No||**2014-10-**<br>**25T17:20:00**|No|
|stationId_13_3|This element groups the<br>following two elements:<br>altimeterData_34a and<br>altimeterReportMissing_34b.|group|Yes|||Yes|
|altimeterData_34a|This element contains the<br>three digits of barometric<br>pressure.|string|No|**"\d{3}"**<br>An altimeter setting of 000-499<br>implies a value of 3000-3499, and a<br>setting of 500-999 implies a value of<br>2500-2999. The only possible range<br>of settings is 2500 to 3499. NOTE:<br>The leading digit 2 or 3 is not<br>reported.|**929 :**the altimeter is<br>2929<br>**011**: the altimeter is<br>3011|Yes|
|altimeterReportMissing_34b|This element indicates that the<br>altimeter data for the<br>associated reporting station is<br>missing. Either this element or<br>altimeterData_34a appears in<br>the HA message.|string|No|**“M”**<br>The only allowed value is M.|**M**|Yes|

420

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.2.13 Altimeter Setting [HA] – Diagram**

##### **5.5.2.14 Adapted Route Status Reconstitution [DBRTRI] – Data Elements**

|**Element Name**<br>**[DBRTRI]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|routeStatusElements_135a|This element specifies the<br>adapted route status elements.|string|No|**"[A-Z0-9]{2,6}"**<br>The adapted names are Standard<br>Instrument Departures (**SID**), Standard<br>Terminal Arrival Routes (**STAR**), Adapted<br>Arrival Routes (**AAR**), Adapted Departure<br>Routes (**ADR**) and Adapted Departure<br>and Arrival Routes (**ADAR**) that are<br>active when initialization begins.|SD001|Yes|
|actionIndicator_36a|This element specifies the<br>status of the route elements<br>specified in the element<br>_routeStatusElements_135a_.|string|No|**“(ON)|(OFF)”**<br>This element has two valid values: ON or<br>OFF.|**ON**<br>**OFF**|Yes|
|seqNoOfLastRouteStatusMsg_251c|This element specifies the<br>sequence number of the last<br>route message was received.|int|No||**171**|Yes|

421

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTRI]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|timeLastRouteStatusMsgRcvd_251d|This element specifies the time<br>the last route message was<br>received.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:52**|Yes|

##### **5.5.2.15 Adapted Route Status Reconstitution [DBRTRI] – Diagram**

##### **5.5.2.16 Adapted Route Status Reconstitution Message in AIXM Format [DBRTRI_AIXM] – Data Elements**

The following elements of the HV message in Simple XML format are not used in the AIXM format of the message:

- seqNoOfLastRouteStatusMsg_251c

- timeLastRouteStatusMsgRcvd_251d

422

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTRI_AIXM]**|**Element Name**<br>**[DBRTRI]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**<br>**Format/Permissib**<br>**le**|**Exam**<br>**ple**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|
|AIXMBasicMessage/hasMember/RouteS<br>egment/gml:name<br><br>|routeStatusElements<br>_135a|This element contains the adapted route<br>names. The adapted names are Standard<br>Instrument Departures (SID), Standard<br>Terminal Arrival Routes (STAR), Adapted<br>Arrival Routes (AAR), Adapted Departure<br>Routes (ADR) and Adapted Departure and<br>Arrival Routes (ADAR) that are active<br>when initialization begins.|gml:CodeType|Yes<br>**"[A-Z0-9]{2,6}"**<br>The format is two<br>to six<br>alphanumeric<br>characters.|SD001|Yes|
|AIXMBasicMessage/hasMember/RouteS<br>egment/timeSlice/RouteSegmentTimeSli<br>ce[interpretation=”SNAPSHOT”]/availabi<br>lity/RouteAvailability/status<br>|actionIndicator_36a|This element shows the availability status<br>of the route segment element.|aixm:CodeRouteAv<br>ailabilityType|Yes<br>**“(OPEN)|(CLSD)”**|**OPEN**|Yes|

##### **5.5.2.17 Altimeter Status Reconstitution [DBRTAI] – Data Elements**

|**Element Name**<br>**[DBRTAI]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|observedTime_35a|This element specifies the<br>altimeter data entrance time.|dateTime|No||**2014-06-20T20:17:52**|No|
|stationId_13_3|This element specifies the<br>altimeter reporting station<br>identifier.|string|No|**"[A-Z0-9]{2,5}"**|**H5B**|Yes|
|altimeterData_34a|This element specifies the<br>reported altimeter setting.<br>Either this element or the<br>element<br>_altimeterReportMissing_34b_<br>must be included in a DBRTI<br>element.|string|No|**"\d{3}"**<br>The format is three digits in the<br>range 2500 – 3499.<br>This element reports the three<br>least-significant digits of the<br>barometric pressure. The most<br>significant digit can only be 2 or<br>3, and is devised as follows. An<br>altimeter settingof 000-499|An altimeter setting of:<br>The altimeter setting of:<br>**929**<br>implies a barometric<br>pressure value of:<br>2929**.**<br>The altimeter setting of:<br>**011**|No|

423

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTAI]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||implies a value of 3000-3499,<br>and a setting of 500-999 implies<br>a value of 2500-2999. The only<br>possible range of settings is 2500<br>to<br>3499.<br>If the character**M**is entered, the<br>altimeter setting for the<br>associated reporting station is<br>missing and it is specified in the<br>element<br>altimeterReportMissing_34b.|implies a barometric<br>pressure value of:<br>3011.||
|altimeterReportMissing_34b|This element specifies that the<br>altimeter setting for the<br>associated reporting station is<br>missing.<br>Either this element or the<br>element<br>_altimeterReportMissing_34a_<br>must be included in a DBRTI<br>element.|string|No|**“M”**<br>The only valid value is the letter<br>M.|**M**|No|
|seqNoOfLastAltimeterMsg_246d|This element specifies the<br>sequence number of the last<br>altimeter message received.|int|No||**240**|Yes|
|timeLastAltimeterMsgRcvd_246e|This element specifies the time<br>of the last altimeter message<br>received.|dateTime|No|**dateTime**|**2014-06-20T20:17:52**|Yes|

424

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.2.18 Altimeter Status Reconstitution [DBRTAI] – Diagram**

##### **5.5.2.19 Sector Assignment Reconstitution [DBRTSI] – Data Elements**

||**Element Name**<br>**[DBRTSI]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible**<br>**Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|sector_29a||This element specifies the<br>sector assignment.|string|No|**“\d{2}”**|22|Yes|
|noFAV_29c||When this element is present in<br>the message, it indicates that<br>there is no FAV assignment for<br>this sector. Either this element<br>or the element FAVAssignments<br>has to be present in a message,<br>but not both.|string|No|**“-“**<br>Only one valid value, “-<br>“(a dash).|**-**|No|
|FAVAssignments||This element groups the<br>following_FAV_29d_elements.<br>There can be from one to 437<br>FAV_29d elements in each<br>FAVAssignments element.||Yes|||No|

425

NAS-JMSDD-4309-001 Rev C July 10, 2018

||**Element Name**<br>**[DBRTSI]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible**<br>**Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|||Either this element or the<br>element noFAV_29c has to be<br>present in a message, but not<br>both.||||||
|FAV_29d||This element provides the FAV<br>Airspace Assignment number.|string|No|**"\d{4}"**<br>The format consists in<br>four digits, with leading<br>zeroes as needed.|0053<br>2509|No|
|seqNoOfLastS|ectorAssignmentStatusMsg_250c|This element specifies the<br>sequence number of the last<br>sector assignment status<br>message received.|int|No|||Yes|
|timeLastSecto|rAssignmentStatusMsgRcvd_250d|This element specifies the time<br>of the last sector assignment<br>status message received.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:52**|Yes|

426

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.2.20 Sector Assignment Reconstitution [DBRTSI] – Diagram**

##### **5.5.2.21 Sector Assignment Reconstitution Message in AIXM Format [DBRTSI_AIXM] – Data Elements**

The following elements of the HV message in Simple XML format are not used in the AIXM format of the message:

- noFAV_29c

- FAVAssignments

- seqNoOfLastSectorAssignmentStatusMsg_250c

- timeLastSectorAssignmentStatusMsgRcvd_250d

|**Element Name**<br>**[DBRTSI_AIXM]**|**Element Name**<br>**[DBRTSI]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permi**<br>**ssible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|AIXMBasicMessage/hasMember/Airspace/timeSli<br>ce/AirspaceTimeSlice/designator|sector_29a|A published sequence of characters<br>allowing the identification of the<br>airspace.<br>This elementprovides the sector|aixm:CodeAirspace<br>DesignatorType|Yes|**“\d{2}”**|53|Yes|

427

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[DBRTSI_AIXM]**|**Element Name**<br>**[DBRTSI]**|**Element Definition**|**Type**|**Co**<br>**mpl**<br>**ex?**|**Format/Permi**<br>**ssible Values**|**Example**|**Req**<br>**uire**<br>**d?**|
|---|---|---|---|---|---|---|---|
|||number, for which the FAV data<br>applies.||||||
|AIXMBasicMessage/hasMember/Airspace/timeSli<br>ce/AirspaceTimeSlice/aixm:interpretation||Property indicating how the time slice<br>is to be interpreted.|aixm:TextNameTyp<br>e|No|“SNAPSHOT”|“SNAPSHOT<br>”|Yes|
|AIXMBasicMessage/hasMember/Airspace/timeSli<br>ce/AirspaceTimeSlice/type||A coded list of values that indicates a<br>type of airspace.|aixm:CodeAirspace<br>Type|Yes|“SECTOR”|“SECTOR”|Yes|
|AIXMBasicMessage/hasMember/extension/Sector<br>AssignmentStatusExtension/FAVNumber|FAV_29d|This element provides the FAV Airspace<br>Assignment number, or a code (a dash<br>character) that indicates that there is<br>no FAV assignment for this sector.|aixm:TextNameTyp<br>e|No|**"\d{4}|\-"**<br>There may be<br>up to 437 FAV<br>numbers for<br>each sector<br>defined.|**7801**<br>**“-“**|No|

428

NAS-JMSDD-4309-001 Rev C July 10, 2018

#### **5.5.3 Operational Data Publication Service Data Elements and Diagrams**

##### **5.5.3.1 ERODP Service: targetNamespace**

The targetNamespace that applies to all messages in the Operational Data Publication Service is: **us:gov:dot:faa:atm:enroute:entities:flightdata**

##### **5.5.3.2 Traffic Count Adjustment [AK] – Data Elements**

|**Element Name**<br>**[AK]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed<br>by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the<br>message sequence number in the range<br>[0000-9999].|2359359001,<br>where the first 6<br>digits are the UTC<br>time (23:59:35<br>UTC) and the last<br>4 digits are<br>sequence<br>number of the<br>message (9001).|Yes|
|sourceTime_00e1|This element specifies the<br>time component of the<br>previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format_hh_mm_ss_, where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|23_59_35<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|9001|Yes|

429

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[AK]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|AAL20|Yes|
|computerId_02d|ERAM Computer<br>Identification (Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit, followed by<br>two alphanumeric characters with the<br>exception of the letters**I**and**O**, as<br>specified by the pattern above.|020|Yes|
|sspId_167a|Site Specific Plan Identifier. It<br>is assigned by IFPA to<br>uniquely identify a flight plan<br>in each ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|24|No|
|trafficCountAdjustment_337a|This element provides the<br>traffic count adjustment data<br>for the AK message.|string|No|**"[A-Z]{4}[+-]\d{3}"**<br>where the first four characters must be<br>one of the following subcategory<br>contractions:<br>ACDD Air Carrier Domestic Departures<br>ATDD Air Taxi Domestic Departures<br>GADD General Aviation Domestic<br>Departures<br>MIDD Military Domestic Departures<br>ACDO Air Carrier Domestic Overs<br>ATDO Air Taxi Domestic Overs<br>GADO General Aviation Domestic Overs<br>MIDO Military Domestic Overs<br>ACOD Air Carrier Oceanic Departures<br>ATOD Air Taxi Oceanic Departures<br>GAOD General Aviation Oceanic<br>Departures<br>MIOD Military Oceanic Departures<br>ACOO Air Carrier Oceanic Overs<br>ATOO Air Taxi Oceanic Overs|ACDD+001<br>Add one air<br>carrier<br>domestic<br>departures|Yes|

430

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[AK]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||GAOO General Aviation Oceanic Overs<br>MIOO Military Oceanic Overs<br>VFRC VFR Traffic Count<br>The “+/-“ character specifies either<br>incrementation (plus) or decrementation<br>(minus) of the current count.<br>The last three digits specify the value to<br>be applied, in the range 001-999.<br>This element can be included in a<br>message from one to eight times.|||
|enteringFacilityId_332a|This element specifies the<br>facility identifier. Each ERAM<br>facility has a unique one<br>letter identifier.|string|No|**“[A-Z]”**<br>A single letter identifying the entering<br>facility.|F is the facility<br>identifier for the<br>Ft. Worth ERAM.<br>W is the facility<br>identifier for the<br>Washington<br>ERAM.|Yes|
|positionType_331a|This element specifies the<br>type of the entering position.|string|No|**“[R|D|A|S]”**<br>The position type is specified using a<br>single letter as follows:<br>R – R-position console<br>D – D-position console<br>A – A-position console<br>S – AT Specialist|R<br>D<br>A<br>S|Yes|
|sectorNumber_327a|This element specifies the<br>sector number. It is used<br>when the element<br>positionType_331a specifies<br>one of the letters R, D, or A.<br>Otherwise, the element<br>enteringPosition_330a is<br>used.|string|No|**"\d{2}"**<br>Either this element or<br>enteringPosition_330a can be included<br>in the AK element, but not both.|50|Yes, if elem.<br>enteringPosi<br>tion_330a is<br>not included<br>in the msg.|
|enteringPosition_330a|This element contains the<br>position number identifying<br>the entering position. It is<br>used when the element|string|No|**"[A-Z][1-9]"**<br>The position number must begin with a<br>letter, followed by a one digit identifier|G2|Yes, if elem.<br>sectorNumb<br>er_327a is<br>not included|

431

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[AK]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||positionType_331a contains<br>the letter S.|||in the range 1 to 9.<br>Either this element or<br>sectorNumber_327a can be included in<br>the AK element, but not both.||in the msg.|

432

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.3.3 Traffic Count Adjustment [AK] - Diagram**

##### **5.5.3.4 Instrument Approach Count Adjustment [AC] – Data Elements**

||**Element Name**<br>**[AC]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|---|
|sourceId_00e||This element specifies the<br>source identification that<br>includes a UTC time followed<br>by a four-digit sequence<br>number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6<br>digits represent the UTC time<br>(_hhmmss_) and the last four digits,<br>represent the message sequence<br>number in the range[0000-|**2359359001**<br>where the first 6<br>digits are the UTC<br>time (23:59:35 UTC)<br>and the last 4 digits<br>are the sequence|Yes|

433

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[AC]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||9999].|number of the<br>message (9001).||
|sourceTime_00e1|This element specifies the<br>time component of the<br>previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_<br>stands for the 2-digit minutes in<br>the range 00-59, and_ss_stands<br>for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also<br>called Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic<br>character followed by one to six<br>alphanumeric characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer<br>Identification (Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of<br>the letters**I**and**O**, as specified in<br>the pattern above.|**020**|Yes|
|sspId_167a|Site Specific Plan Identifier. It<br>is assigned by IFPA to<br>uniquely identify a flight plan<br>in each ERAM facility.|string|No|**"\d{1,4}"**<br>One to four digits.|**24**|No|
|stationId_13_3|This element specifies a<br>reporting airport.|string|No|**"[A-Z0-9]{2,5}"**<br>Two to five alphanumeric<br>characters.|**AUS**|Yes|
|actionIndicator_36h|This element shows the<br>status of the instrument|string|No|**“(AUTO)|(ON)|(OFF)”**<br>It can have one of the following|**AUTO**<br>**ON**|No|

434

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[AC]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||approach count.|||values:<br>**AUTO**— count instrument<br>approaches based on stored<br>weather<br>**ON**— count instrument<br>approaches regardless of stored<br>weather<br>**OFF**— do not count instrument<br>approaches<br>Either this field or the following<br>field,<br>_instrumentApproachCountAdjust_<br>_ment_338a_, can appear in<br>element AC, but not both.|**OFF**||
|instrumentApproachCountAdjustment_338a|This element specifies the<br>Instrument Approach Count<br>Adjustment Data used in the<br>AC element. It specifies the<br>data subcategory, the<br>adjustment type (increment<br>or decrement), and the value<br>to use in the adjustment of<br>that subcategory.|string|No|**“((AC)|(AT)|(GA)|(MI))[+-]\d{2}”**<br>The first two letters represent<br>the alphabetic subcategory<br>contraction as follows:<br>**AC**(air carrier)<br>**AT**(air taxi)<br>**GA**(general aviation)<br>**MI**(military)<br>The following character, + /-,<br>specifies the adjustment type:<br>increment or decrement.<br>The last two digits specify the<br>value to be applied to the<br>alphabetic subcategory in the<br>range 01 - 99.<br>There can be zero to four<br>occurrences of this element in<br>the AC element.<br>Either this element or<br>_actionIndicator_36h_can appear<br>in element AC, but not both.|**AC+03**<br>In this example an air<br>carrier count is<br>incremented by 3.|No|
|enteringFacilityId_332a|This element specifies the|string|No|**“[A-Z]”**|**F**is the facility|Yes|

435

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[AC]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||facility identifier. Each ERAM<br>facility has a unique one<br>letter identifier.|||A single letter identifying the<br>entering facility.|identifier for the Ft.<br>Worth ERAM.<br>**W**is the facility<br>identifier for the<br>Washington ERAM.||
|positionType_331a|This element specifies the<br>type of the entering position.|string|No|**“[R|D|A|S]”**<br>The position type is specified<br>using a single letter as follows:<br>R – R-position console<br>D – D-position console<br>A – A-position console<br>**S**– AT Specialist|**R**<br>**D**<br>**A**<br>**S**|Yes|
|sectorNumber_327a|This element specifies the<br>sector number. It is used<br>when the element<br>_positionType_331a_specifies<br>one of the letters R, D, or A.<br>Otherwise, the element<br>_enteringPosition_330a_is<br>used.|string|No|**"\d{2}"**<br>Either this element or<br>_enteringPosition_330a_can be<br>included in the AC element, but<br>not both.|**50**|Yes, if<br>elem.<br>_enteringPo_<br>_sition_330_<br>_a_is not<br>included in<br>the msg.|
|enteringPosition_330a|This element contains the<br>position number identifying<br>the entering position. It is<br>used when the element<br>_positionType_331a_contains<br>the letter**S.**|string|No|**"[A-Z][1-9]"**<br>The position number must begin<br>with a letter, followed by a one-<br>digit identifier in the range 1 to 9.<br>Either this element or<br>_sectorNumber_327a_can be<br>included in the AC element, but<br>not both.|**G2**|Yes, if<br>elem.<br>_sectorNum_<br>_ber_327a_<br>is not<br>included in<br>the msg.|

436

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.3.5 Instrument Approach Count Adjustment [AC] - Diagram**

##### **5.5.3.6 Sign In Sign Out [SY] – Data Elements**

|**Element Name**<br>**[SY]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed by<br>a four-digit sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6<br>digits represent the UTC time<br>(_hhmmss_) and the last four<br>digits, represent the message<br>sequence number in the range<br>[0000-9999].|**2359359001**<br>, where the first<br>6 digits are the<br>UTC time<br>(23:59:35 UTC)<br>and the last 4<br>digits represent|Yes|

437

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[SY]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||||||the sequence<br>number of the<br>message (9001).||
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_<br>where:_hh_stands for the 2-<br>digit-hour in the range 00-23,<br>_mm_stands for the 2-digit<br>minutes in the range 00-59, and<br>_ss_stands for the 2-digit seconds<br>in the range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>sequence number component<br>of the sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|controllerInitials_317a|This element specifies the<br>controller initials for a sign<br>in/sign out action.|string|No|**"[A-Z]{2}[A-Z0-9]?"**<br>The format is two letters<br>followed by an optional<br>alphanumeric character.|**PD**|Yes|
|nonOperationalUserInitials_318a|This element specifies the non-<br>operational user initials for a<br>sign in/sign out action.|string|No|**"[A-Z]{2}[A-Z0-9]?"**<br>The format is two letters<br>followed by an optional<br>alphanumeric character.|**LB**|No|
|crewNumber_319a|This element specifies the crew<br>number associated with the<br>user(s) at the time of a sign in or<br>sign out action.|string|No|**“\d”**<br>The format is a single digit.|**7**|No|
|areaNumber_320a|This element specifies the area<br>number in a sign in or sign out<br>action. The area number is an<br>adapted value correlating a<br>defined area to a sector, i.e.,<br>the target position for a sign<br>in/sign out action.|string|No|**“\d”**<br>The format is a single digit.|**5**|No|
|inOutIndicator_321a|This element specifies the type<br>of message in a sign in or sign<br>out action. The type can be|string|No|**“[IO]”**<br>The letter**I**or**O**.|**I**<br>**O**|Yes|

438

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[SY]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||either a sign in: I or sign out: O.||||||
|role_322a|This element specifies field<br>contains the task of the user in<br>a sign in or sign out action,<br>either an operational role: O or<br>a training role: T.|string|No|**“[OT]”**<br>Either the letter O or T.|**O**<br>**T**|Yes|
|tracker_323a|This element specifies the<br>responsibilities of the user in a<br>sign in or sign out action, either<br>handoff controller (Y) or not<br>handoff controller (N).|string|No|**“[YN]”**<br>Either the letter Y or N.|**Y**<br>**N**|Yes|
|signInTime_324a|This element specifies the date<br>and time for a sign in action.<br>Current system time is always<br>used for a sign in action except<br>for those initiated at the AT<br>Specialist Position, which may<br>optionally include date and time<br>as part of the sign in message.<br>When both element<br>_signInTime_324a_and<br>_signOutTime_325a_are included<br>in a sign in/sign out action, the<br>user is signed in and<br>automatically signed out at the<br>same position.|dateTime|No||**2014-06-**<br>**20T20:17:52**|No|
|signOutTime_325a|This field contains the date and<br>time for a sign out action.<br>Current system time is always<br>used for a sign out action except<br>for those initiated at the AT<br>Specialist Position, which may<br>optionally include date and time<br>as part of the sign out message.|dateTime|No|**dateTime**|**2014-06-**<br>**20T20:17:52**|No|
|localUTCOffset_329a|This element specifies the local<br>UTC time offset, i.e. the number<br>of hours, plus or minus, that|string|No|**“[+-]\d{2}”**<br>The format consists of a plus (+)<br>or minus(-)sign followed by|**-06**|Yes|

439

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[SY]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||local midnight occurs relative to<br>UTC midnight.|||two digits.|||
|position_326a|This element specifies the<br>target position, i.e., the position<br>where a sign in/sign out action<br>occurs. The position that a user<br>is attempting to sign into is<br>defined as the target position,<br>and is determined by either the<br>sector position that the<br>command is entered from (R-,<br>D-, or A-positions), or the sector<br>position contained in a SISO<br>message entered at the AT<br>Specialist position.|string|No|**“[RDAN]”**<br>The format is one letter, and<br>the allowed values are: R – R-<br>position console<br>D – D-position console<br>A – A-position console<br>N – Pseudo position|**R**<br>**D**<br>**A**<br>**N**|Yes|
|sectorNumber_327a|This element specifies a two-<br>digit sector number. When used<br>in a sign in/sign out action<br>designating an "N" position, the<br>sector number is not checked to<br>determine if it is adapted in the<br>center.|string|No|**"\d{2}"**<br>Either this element or<br>_enteringPosition_330a_can be<br>included in the AC element, but<br>not both.|**50**|Yes|
|recordingReason_328a|This element specifies the<br>reason for recording a sign-<br>in/sign-out action. The reason<br>for the action must be one of<br>the following:<br>0 - Sign In/Sign Out entered<br>from a Sector Position<br>1 - Sign In/Sign Out (less than<br>two time fields) entered from<br>an AT Specialist Position<br>2 - Sign Out due to a<br>resectorization<br>3 - Forced Sign Out due to<br>another Sign In<br>4 - Automatically Signed Back In|string|No|**“0-5”**<br>The format consists of one digit,<br>in the range 0 - 5.|**0**<br>**1**<br>**2**<br>**3**<br>**4**<br>**5**|No|

440

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[SY]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||5 - Sign In/Sign Out due to a<br>Sign In with two time fields<br>from an AT Specialist Position.||||||

441

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.3.7 Sign In Sign Out [SY] - Diagram**

442

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.3.8 Beacon code Utilization [UB] – Data Elements**

|**Element Name**<br>**[UB]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time<br>followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6<br>digits represent the UTC time<br>(_hhmmss_) and the last four digits,<br>represent the message sequence<br>number in the range [0000-9999].|**2359359001**<br>where the first<br>6 digits are the<br>UTC time<br>(23:59:35 UTC)<br>and the last 4<br>digits are the<br>sequence<br>number of the<br>message<br>(9001).|Yes|
|sourceTime_00e1|This element specifies the<br>time component of the<br>previous element,<br>sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_<br>stands for the 2-digit minutes in<br>the range 00-59, and_ss_stands for<br>the 2-digit seconds in the range<br>00-59.|**23_59_35**<br>that<br>represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the<br>sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|internalPrimarySecondaryAdaptedCodes_47a|This element specifies the<br>peak number of internal<br>primary and secondary<br>codes and the total<br>number of adapted codes.|string|No|**“\d{4}/\d{4}”**<br>The format is a four-digit number<br>followed by a virgule, followed by<br>another four-digit number.|**0020/0417**|Yes|
|internalTertiaryAdaptedCodes_47b|This element specifies the<br>peak number of internal<br>tertiary codes and the total<br>number of adapted codes.|string|No|**“\d{4}/\d{4}”**<br>The format is a four-digit number<br>followed by a virgule, followed by<br>another four-digit number.|**0000/0000**|Yes|
|externalPrimarySecondaryAdaptedCodes_47c|This element specifies the|string|No|**“\d{4}/\d{4}”**|**0020/0417**|Yes|

443

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[UB]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||peak number of external<br>primary and secondary<br>codes and the total<br>number of adapted codes.|||The format is a four-digit number<br>followed by a virgule, followed by<br>another four-digit number.|||
|externalTertiaryAdaptedCodes_47d|This element specifies the<br>peak number of external<br>tertiary codes and the total<br>number of adapted codes.|string|No|**“\d{4}/\d{4}”**<br>The format is a four-digit number<br>followed by a virgule, followed by<br>another four-digit number.|**0000/0000**|Yes|
|codeReassignments_47e|This element specifies the<br>number of code<br>reassignments since<br>midnight.|string|No|**“\d{4}”**<br>The format is a four-digit number<br>in the range of 0000 – 9999.|**0020**|Yes|

##### **5.5.3.9 Beacon code Utilization [UB] - Diagram**

444

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.3.10 Geographic Beacon Code Utilization [UG] – Data Elements**

|**Element Name**<br>**[UG]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_)<br>and the last four digits, represent the<br>message sequence number in the<br>range [0000-9999].|**2359359001**<br>where the first 6<br>digits are the<br>UTC time<br>(23:59:35 UTC)<br>and the last 4<br>digits are the<br>sequence<br>number of the<br>message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_stands<br>for the 2-digit minutes in the range<br>00-59, and_ss_stands for the 2-digit<br>seconds in the range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of<br>the sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|elapsedTime_50a|This element specifies the elapsed<br>time since the last report in<br>minutes.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-1440].|**1220**|Yes|
|region|This element groups the following<br>three elements:<br>_destinationRegionId_50b_,<br>_geoPrimaryAdaptedCodes_50c_, and<br>_geoSecondaryAdaptedCodes_50d_.|group|Yes|This element may be included<br>between one and fifty times in an UG<br>element.||Yes|
|destinationRegionId_50b|This element specifies the<br>destination region identifier.|string|No|**“\d{2}”**<br>Two digit string.||Yes|
|geoPrimaryAdaptedCodes_50c|This element specifies the peak<br>number of geographic primary<br>beacon codes and the total number|string|No|**“\d{4}/\d{4}”**<br>The format is a four-digit number|0045/0315|Yes|

445

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[UG]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||of adapted primary codes for the<br>region. Its format is a four-digit<br>number flowed by a virgule,<br>followed by another four-digit<br>number.|||followed by a virgule, followed by<br>another four-digit number.|||
|geoSecondaryAdaptedCodes_50d|This element specifies the peak<br>number of geographic secondary<br>beacon codes and the total number<br>of adapted secondary codes for the<br>region.|string|No|**“\d{4}/\d{4}”**<br>The format is a four-digit number<br>followed by a virgule, followed by<br>another four-digit number.|0045/0315|Yes|

##### **5.5.3.11 Geographic Beacon Code Utilization [UG] - Diagram**

446

NAS-JMSDD-4309-001 Rev C July 10, 2018

#### **5.5.4 General Information Publication Service Data Elements and Diagram**

##### **5.5.4.1 ERGMP Service: targetNamespace**

The targetNamespace that applies to all messages in the General Information Publication Service is: **us:gov:dot:faa:atm:enroute:entities:flightdata**

##### **5.5.4.2 General Information [GH] – Data Elements**

|**Element Name**<br>**[GH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the<br>source identification that<br>includes a UTC time followed by<br>a four-digit sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_) and<br>the last four digits, represent the<br>message sequence number in the range<br>[0000-9999].|**2359359001**<br>where the first 6<br>digits are the UTC<br>time (23:59:35 UTC)<br>and the last 4 digits<br>are the sequence<br>number of the<br>message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_where:<br>_hh_stands for the 2-digit-hour in the<br>range 00-23,_mm_stands for the 2-digit<br>minutes in the range 00-59, and_ss_<br>stands for the 2-digit seconds in the<br>range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the<br>message sequence number<br>component of the sourceId_00e<br>element.|string|No|**“\d{4}”**<br>Four-digit number in the range [0000-<br>9999].|**9001**|Yes|
|remarks_11c|This element specifies the text<br>message that is sent to a<br>specified position. The length is<br>limited by the input device (up|string|No|String of one to 400 characters.<br>It has an attribute called_remarktype_<br>with the possible values of interfacility<br>or intrafacility.||Yes|

447

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[GH]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
||to 300 characters). The General<br>Information (GH) element<br>provides general<br>information/free text remarks<br>to ATM client applications.<br>ERAM sends a GH message to a<br>specific ATM client application<br>or to all ATM client applications<br>via ATM IPOP, as indicated by<br>destination address routing. The<br>Center-TRACON Automation<br>System (CTAS) can input a GH<br>message to a position in the<br>ERAM facility.||||||

448

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.4.3 General Information [GH] - Diagram**

##### **5.5.4.4 Interim Altitude Status Information [HE] – Data Elements**

|**Element Name**<br>**[HE]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_)<br>and the last four digits, represent the<br>message sequence number in the<br>range [0000-9999].|**2359359001**<br>, where the first<br>6 digits are the<br>UTC time<br>(23:59:35 UTC)<br>and the last 4<br>digits are the<br>sequence<br>number of the<br>message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_stands<br>for the 2-digit minutes in the range<br>00-59,and_ss_stands for the 2-digit|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|

449

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HE]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||seconds in the range 00-59.|||
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of<br>the sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of the<br>letters**I**and**O.**|**020**|Yes|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|interimAlt_76b|The aircraft altitude in hundreds of<br>feet.|string|No|**"\d{1,3}"**<br>One to three-digits.|**240**|Yes|

450

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.4.5 Interim Altitude Status Information [HE] – Diagram**

##### **5.5.4.6 Hold Status Information [HO] – Data elements**

|**Element Name**<br>**[HO]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_)<br>and the last four digits, represent the<br>message sequence number in the<br>range [0000-9999].|**2359359001**<br>, where the first<br>6 digits are the<br>UTC time<br>(23:59:35 UTC)<br>and the last 4<br>digits are the<br>sequence<br>number of the<br>message (9001).|Yes|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_stands<br>for the 2-digit minutes in the range<br>00-59,and_ss_stands for the 2-digit|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|

451

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HO]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||seconds in the range 00-59.|||
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of<br>the sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of the<br>letters**I**and**O.**|**020**|Yes|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|holdDataFix_21a|Hold Fix. Specifies the position<br>location for the flight to Hold along<br>the filed route of the flight.|string|No|**"(([A-Z0-9]{2,5}) |**<br>**([A-Z0-9]{2,5}\d{6}) |**<br>**(\d{4}[A-Z]?/\d{4,5}[A-Z]?))”**|**TXK**<br>**OKC270015**<br>**3500N/94000W**|Yes|
|holdDataTime_21d|Hold Time. Specifies the time the<br>flight can expect further clearance<br>at the hold fix specified in element<br>holdDataFix_21a.|dateTime|No||**2014-10-**<br>**30T17:20:00**|No|

452

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.4.7 Hold Status Information [HO] – Diagram**

##### **5.5.4.8 ERAM Status Information [HS] – Data Elements**

|**Element Name**<br>**[HO]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source<br>identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|string|No|**“\d{10}”**<br>Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_)<br>and the last four digits, represent the<br>message sequence number in the<br>range [0000-9999].|**2359359001**<br>, where the first<br>6 digits are the<br>UTC time<br>(23:59:35 UTC)<br>and the last 4<br>digits are the<br>sequence<br>number of the<br>message (9001).|Yes|

453

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HO]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_stands<br>for the 2-digit minutes in the range<br>00-59, and_ss_stands for the 2-digit<br>seconds in the range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of<br>the sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|operationalNativeStatus_140a|Status Change Indicator ON2<br>operational.|string|No|**“[A-Z]{2}[A-Z0-9]”**<br>The permissible values are:<br>•<br>INA = inactive<br>•<br>ON2 = operational using<br>live inputs|**INA**<br>**ON2**|Yes|
|plannedShutdownStatus_140b|Shutdown Status Indicator|string|No|**“[A-Z]{3}”**<br>The permissible values are:<br>•<br>PSE = planned shutdown<br>entered; it requires the<br>elements<br>shutdownStartTime_32a<br>and<br>shutdownTerminateTime_<br>33a<br>•<br>PSA = planned shutdown<br>activated<br>•<br>PSN = planned shutdown<br>not active|**PSA**<br>**PSN**<br>**PSE**|Yes|
|switchOverStatus_140c|Status Change Indicator Channel<br>Switch|string|No|**“[A-Z]{3}”**<br>The permissible values are:<br>•<br>SSW = channel switch<br>•<br>SSO  = PAS/SAS switch<br>•<br>SSN = channel switch or|**SSW**<br>**SSO**<br>**SSN**|Yes|

454

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HO]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||PAS/SAS switch not in<br>effect|||
|meteringStatus_140d|TMAD Status Change Indicator.|string|No|**“[A-Z]{3}”**<br>The permissible values are:<br>•<br>DOF = parameter TMAD is<br>OFF<br>•<br>DON = parameter TMAD is<br>ON|**DOF**<br>**DON**|Yes|
|RVSMStatus_140e|RVSM Status Change Indicator|string|No|**“[A-Z]{2}”**<br>The permissible values are:<br>ON = parameter RVSM is ON<br>OFF = parameter RVSM is OFF|**ON**<br>**OFF**|Yes|
|IREEStatus_140f|IREE Status Change Indicator|string|No|**“[A-Z]{2}”**<br>The permissible values are:<br>•<br>ON = parameter IREE is ON<br>•<br>OFF = parameter IREE is<br>OFF|**ON**<br>**OFF**|No|
|IITSStatus_140g|IITS Status Change Indicator|string|No|**“[A-Z]{2}”**<br>The permissible values are:<br>•<br>ON = parameter IITS is ON<br>•<br>OFF = parameter IITS is OFF|**ON**<br>**OFF**|No|
|shutdownStartTime_32a|Shutdown Start Time|xs:time|No|Needed only when<br>plannedShutdownStatus_140b = PSE.|**09:30:00**|No|
|shutdownTerminateTime_33a|Shutdown Terminate Time|xs:time|No|Needed only when<br>plannedShutdownStatus_140b = PSE.|**10:30:00**|No|
|systemTypeId_168a|System Type Identification|string|No|**“[A-Z]{4}”**<br>Permissible value is “ERAM”|**ERAM**|No|
|CMSVersionNo_169a|CMS version number that will<br>contain the third through sixth<br>alphanumeric characters of the<br>ERAM national release name that is<br>in use at the local ERAM facility.|string|No|**“[0-9]{4}”**<br>Four digits.|**0012**|No|

455

NAS-JMSDD-4309-001 Rev C July 10, 2018

##### **5.5.4.9 ERAM Status Information [HS] – Diagram**

##### **5.5.4.10 Unsuccessful Transmission Information [UI] – Data Elements**

|**Element Name**<br>**[HO]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|sourceId_00e|This element specifies the source|string|No|**“\d{10}”**|**2359359001**|Yes|
||identification that includes a UTC<br>time followed by a four-digit<br>sequence number.|||Ten digits, of which the first 6 digits<br>represent the UTC time (_hhmmss_)<br>and the last four digits,represent the|where the first 6<br>digits are the<br>UTC time||

456

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**<br>**[HO]**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|||||message sequence number in the<br>range [0000-9999].|(23:59:35 UTC)<br>and the last 4<br>digits are the<br>sequence<br>number of the<br>message (9001).||
|sourceTime_00e1|This element specifies the time<br>component of the previous<br>element, sourceId_00e.|string|No|**“[0-2]\d_[0-5]\d_[0-5]\d”**<br>Time in the format _hh_mm_ss,_<br>where:_hh_stands for the 2-digit-<br>hour in the range 00-23,_mm_stands<br>for the 2-digit minutes in the range<br>00-59, and_ss_stands for the 2-digit<br>seconds in the range 00-59.|**23_59_35**<br>that represents<br>23:59:35 UTC|Yes|
|sourceSeqNo_00e2|This element specifies the message<br>sequence number component of<br>the sourceId_00e element.|string|No|**“\d{4}”**<br>Four-digit number in the range<br>[0000-9999].|**9001**|Yes|
|flightId_02a|Aircraft ID, or flight ID (also called<br>Call Sign).|string|No|**"\+?[A-Z][A-Z0-9]{1,6}"**<br>One uppercase alphabetic character<br>followed by one to six alphanumeric<br>characters.|**AAL20**|Yes|
|computerId_02d|ERAM Computer Identification<br>(Computer ID).|string|No|**"([0-9][A-HJ-NP-Z0-9]{2})|**<br>**([0-9]{2}[A-HJ-NP-Z0-9])"**<br>The element includes a digit,<br>followed by two alphanumeric<br>characters with the exception of the<br>letters**I**and**O.**|**020**|No|
|sspId_167a|Site Specific Plan Identifier. It is<br>assigned by IFPA to uniquely<br>identify a flight plan in each ERAM<br>facility.|string|No|**"\d{1,4}"**<br>One to four-digits.|**24**|No|
|outputRouting_16b|Adapted coordination indicator of<br>the facility to which transmission of<br>flight data is unsuccessful.|string|No|3-byte long string.|**AD+**|Yes|
|FAV_29d|FAV Airspace assignment.|string|No|**"\d{4}"**<br>Four digits.|**1700**|No|

457

NAS-JMSDD-4309-001 Rev C July 10, 2018

|**Element Name**|**Element Definition**|**Type**|**Complex?**|**Format/Permissible Values**|**Example**|**Required?**|
|---|---|---|---|---|---|---|
|**[HO]**|||||||

##### **5.5.4.11 Unsuccessful Transmission Informattion [UI] - Diagram**

458

NAS-JMSDD-4309-001 Rev C July 10, 2018

## **6. Service Implementation**

The JMS provider for SFDPS is ActiveMQ deployed on NEMS infrastructure. SFDPS publishes messages to a JMS queue established at NEMS. Client consumers will connect to a topic to receive data.

### **6.1 Bindings**

The NEMS ICD describes the bindings.

#### **6.1.1 ActiveMQ**

All SFPDS connections to NEMS are through ActiveMQ.

##### **6.1.1.1 Data format**

All data published to NEMS in SimpleXML format (reference 15). Data for flight messages that were received from the ARTCC controlling the flight are also published in FIXM format (reference 17). Data for airspace messages are also published in AIXM format (reference 17).

##### **6.1.1.2 Message protocol**

The message protocol is JMS.

##### **6.1.1.3 Transport protocol**

The transport protocol is Transmission Control Protocol (TCP).

### **6.2 End Points**

#### **6.2.1 End Point 1**

SFDPS consumers connect to NEMS using JMS to retrieve data from their subscribed topic(s). Additional details about the NEMS JMS interface may be obtained in the NEMS ICD (reference [14]).

459