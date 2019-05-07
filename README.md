## Introduction
**If we can track down the use of our private data, we can protect it.**

Today, privacy is at the center of the debate on the consumer's use of technology. It has recently gained national attention with hearings from tech CEOs testifying in front of Congress. The hearings made it clear to legislators that not only has tech mishandled user privacy but that regulating it is difficult. These software companies have an unprecedented advantage over consumers when it comes to protecting sensitive consumer data. This is mainly due to complex privacy policies and the inability for government oversight to track down privacy breeches. From a governance perspective, it is unclear how to regulate matters of privacy especially at scale.
If, for example, a user's mobile number was shared amongst several companies, regulators and oversight committees would have an impossible time disseminating how such sensitive information got out and who was responsible. 
This is due primarily to the complex nature of not only software but the rules by which data is shared and transmitted to partners and associates. The sharing of data between entities is done by protocols knows as APIs.
APIs are foundational to modern networked computing. On a global scale, the most widely accepted apparatus utilized for the delivery and transport of data exchange is the JSON format - a  JavaScript object notation formatted as an array data type packaged for asynchronous delivery. There are many variants that utilize this transport mechanism. For example in healthcare, where data privacy is meant to retain the highest standards, derivatives of JSON include FHIR and HL-7.
For the purposes of simplification, we will focus on the vanilla "out of the box" version of JSON as it applies to API.
### Privacy vs. Security
There is a strong binding correlation between data security and data privacy but they mean different things.
Data security is fundamentally about security of data and who has authorization to access that data. Data privacy pertains to authorized access, concerning who has it and who defines it. Data security is a technical implementation of the policies set forth by data privacy. The trade-off between security and privacy is a balance between a person’s right to privacy and the counterbalance of how far data security is needed. 
It is with this differentiation that data security is much more clearly defined and most security measures are common amongst all organizations. For example, encryption is a security matter and has been standardized with common tools and methodology. Who gets to un-encrypt and de-crypt user data is a privacy issue and is left up to each organization to figure out.
There is no point in having more data security if people’s right to privacy will also be lost, in the process. These simple differences are significant because they have implications for privacy and security, which, in turn, have enormous consequences on business, politics, and society as a whole. 
### Obfuscation Problem
Software privacy policies have been relegated to users having to opt-in or opt-out of a feature or in most cases use of a software application or service all-together. The user is faced with the question 'What would you be willing to give to get in order to enter?'
Adding to its complexity are privacy policies. Legal ease with blanket clauses meant to protect a company as thinly veiled of compliance. Its these policies that often get called into question by consumer protection organizations and oversight committees. We currently have no mechanism to trace the validity of the claims put forth in these policies. GDPR was suppose to be that mechanism, but as it has demonstrated, it lacks real intelligence about how data is being moved around from system to system.

GDPR, in its current state, lacks specificity. Loosely consenting with the user that a web browser cookie may be used to track and share information doesn't even scratch the surface of solving privacy concerns. 'What specific data is being used?' and 'Whom is it being shared with?' are basic questions users, privacy advocates and oversight need to know the answer to. 
Once data is collected from the user, the next privacy vulnerability is data transport. This is a completely grey area for consumer privacy. Current laws limit disclosures of where the data is being shared with. Disclosure language such as "a 3rd party" is overly broad, but enough to shield software companies from litigation.*  
Let's hypothetically suppose that even if laws and legislation were enacted to disclose the names of 3rd parties, such as business associate agreements for public viewing, it would still leave the consumer in the dark. Does the named 3rd party get all of my data I shared when I signed up and used the application or service or only pieces of data?
### Removing Opacity
What one company deems as appropriate privacy policies may not be for its users. advocates or governance. There currently is no development methodology or framework to audit, trace, and ensure user privacy practices and validate an organizations safeguarding of user privacy. Tracing user data, at every node of contact, is the key to ensure the viability of privacy. The premise being introduced here is to ensure that all data tied to privacy policies can be flagged for auditing through the use of examining the transport of user data. There are some key advantages of tracking user data using this approach:
1) Developers can tag their API to provide full transparency with their stated privacy policies.
2) Users, advocates and oversight governance can become more efficient at examining an entity's privacy policy and standards
3) Intellectual property of software, such as source code and business logic, can remain protected during an open audit process.
4) Laws can be enforced, with less reliance on a software developer's disclosure.
5) Granular data control of what is allowable and fair use of data being shared

## A JSON notation for Privacy Object Protection — JSON-POP
The **JSON-POP** notation is designed to tag every data string, with a formatted privacy descriptor, as part of the standard JSON payload. This is done using commentary remarks which are enclosed in the payload and have no effect on code execution. JSON-POP executes asynchronously at run-time as the application accepting the JSON container ignores the POP commentary. However because it ties organically to every object, it can be traced back to its origins.

### POP consists of:
#### 1) Entity name
      Name or legal entity abbreviation of data collector
#### 2) Data category code
      Demographic, health, financial, confidential
#### 3) Share Rights
      Allowable shared use of data (Full, Timed limited, Pass-thru, None)

## Notation
1) ÞOÞ Object name for POP notation
2) [...] data type enclosure
3) -- listed entity add-ons

## Usage
As with any proposed documentation standard, JSON-POP relies on adherance that may be self-driven, market-driven or regulatory driven. The notation can be tracked for every API call made. As every organization shares user data, the JSON-POP notaion appends. JSON-POP is made up of its object identifier, the Entity- a developers name or organization's legal name, a Category which identifies the tyoe if data object, and Share Rights- the permission given by the developer to share the object. In the example below, the same user information is distributed three times. All three organizaztion are listed in the POP object. If the same data object were to be shared with other organizations, each of those organizations would be listed. This ensures traceabiity during the privacy review or auditing process.

## Protection
...
### Examples

      "ÞOÞ": "[ACME Corporation][Demographic][Full]--[ABC Inc.]--[ZZZ LLC]",

| Object | Entity           | Category  | Share Rights |
| ---- |:------------------:| -------------:| -------------:|
| ÞOÞ  | ACME Corp | Demographic | Full |
| ÞOÞ  | ABC Inc. | Demographic | Full |
| ÞOÞ  | ZZZ LLC | Demographic | None |

### Primary entity API request JSON object
```javascript
{
   "ÞOÞ": "[ACME Corporation][Demographic][Full]",
   "demographics": {
      "Primary": {
         "FirstName": "John",
         "LastName": "Doe",
         "UserList": {
            "UserEntry": {
               "ID": "JohnDoe12",
               "SortAs": "USR",
               "UserDef": {
                  "about": "I am a 23 year old student. My hobbies include Fortnight.",
                  "UserSeeAlso": ["GML", "XML"]
               },
               "UserSee": "markup"
            }
         }
      }
   }
}
```
### Secondary entity API request JSON object
```javascript
{
   "ÞOÞ": "[ACME Corporation][Demographic][Full]--[ABC Inc.]",
   "demographics": {
      "Primary": {
         "FirstName": "John",
         "LastName": "Doe"
      }
   }
}
```
### Tertiary entity API request JSON object
```javascript
{
   "ÞOÞ": "[ACME Corporation][Demographic][Full]--[ABC Inc.]--[ZZZ LLC]",
   "demographics": {
      "Primary": {
         "FirstName": "John",
         "LastName": "Doe"
      }
   }
}
```
## Development
The purpose of JSON-POP is to ensure traceability at every API share point. By doing so, every touch point ensures consistency and responsibility in the originator's data object. The JSON array itself can be built using any typed language. Formating is important so that an auditing system can cleanly read the object receipt that encapsulates the JSON-POP object.
