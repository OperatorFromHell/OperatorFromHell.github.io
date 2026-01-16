# Exposed MongoDB Instances: A Threat Actor’s Goldmine?
![Image of a pirate.]({{ "/assets/images/pirate.png" | relative_url }})

-----

## Introduction
MongoDB? What is this? MongoDB is an open-source document-orientated NoSQL database management program. The software application is designed for scalability and large-scale data storage.

Yes, your guess is correct, threat actors love to target the instances with many publicly accessible.

This article will highlight a vulnerability disclosure I performed, finding exposed sensitive data from an organisation’s MongoDB database.

-----

## The Hunt Begins!
Threat actors can identify publicly accessible MongoDB instances in several ways. In this article, I will show the Shodan method.

The below Shodan query will display all successful requests to MongoDB databases; Allowing threat actors to identify exposed databases.

```javascript
 "Set-Cookie: mongo-express=" "200 OK"
```
The current results as of (22/10/24) are the following:

- 357 exposed instances.
- The top countries are the follow, Germany, the United States, China, France and Singapore.
- 284 of the exposed instances are operating on port 8081.
![Image of Shodan results.]({{ "/assets/images/mongo_shodan_results.webp" | relative_url }})

-----
## The Disclosure

**Please note, that impacted party was provided with a detailed report on the findings and has successfully fixed their instance being exposed.**

The impacted party operates within the logistics sector. The data found potentially could have been abused for third-party compromise.
![An expossed Mongo instance.]({{ "/assets/images/exposed_mongo_db.webp" | relative_url }})
<p align="center"><em>Exposed MongoDB instance.</em></p>

This is just one example of multiple of a vulnerability disclosure I have conducted with exposed MongoDB instances.

In one previous case, I found an organisation exposing clear text email addresses, passwords, credit card information and SSH keys.

-----
## How to fix?
Simply put, basic mitigation authentication practices would prevent a threat actor from accessing the instance. Please see the following [article](https://www.mongodb.com/docs/manual/tutorial/enable-authentication/) for steps.

-----
## Conclusion
Overall, exposed MongoDB instances can spell disaster for an organisation. The low skill required for a threat actor to access an exposed instance makes it popular amongst threat actors.

Thanks for your time!
