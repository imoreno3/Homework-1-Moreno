"Homework 1"
=============
#Chapter 1
**1. Classify each of the following as a violation of confidentiality, of integrity, of availability, or of some combination thereof.**  
* **a. John copies Mary’s homework.**  
  - *Confidentiality*  
* **b. Paul crashes Linda’s system.**  
  - *Availability*  
* **c. Carol changes the amount of Angelo’s check from $100 to $1,000.**  
  - *Integrity*  
* **d. Gina forges Roger’s signature on a deed.**  
  - *Integrity*  
* **e. Rhonda registers the domain name “AddisonWesley.com” and refuses to let the publishing house buy or use that domain name.**  
  - *Availability*
  - *Integrity*
* **f. Jonah obtains Peter’s credit card number and has the credit card company cancel the card and replace it with another card bearing a different account number.**  
  - *Confidentiality*
  - *Integrity*
  - *Availability*
* **g. Henry spoofs Julie’s IP address to gain access to her computer.**  
  - *Integrity*  
  - *Confidentiality*  

**3. The aphorism “security through obscurity” suggests that hiding information provides some level of security. Give an example of a situation in which hiding information does not add appreciably to the security of a system. Then give an example of a situation in which it does.**  
  - *Hiding an algorithm that protects your password might not necessarily add apreciably to the security of the system becuase the algorithm can be found within the source code of the library.*  
  - *However, hiding the password field within a form will add apreciably to the system. This way only the rightful user will have access to the account.*

**7. For each of the following statements, give an example of a situation in which the statement is true.**  
* **a. Prevention is more important than detection and recovery.**  
 - *Preventing the accessibility of a bank account information*  
* **b. Detection is more important than prevention and recovery.**  
 - *Detecting when an email is spam or contains a virus*  
* **c. Recovery is more important than prevention and detection.**  
 - *Recovery for data centers (companies' backups)*  

**11. How do laws protecting privacy impact the ability of system administrators to monitor user activity?**  
- *Laws protecting user privacy can sometimes be an obstacle for administrators to do a good job. For example, if an user were to be leaking information to a competitor via email and the company's law does not allow admins to check for email confidential information. Then the user would get way with no problem. However, if the admin has access to read the information being transfer, this could be prevented.*  

#Chapter 2

**1. Consider a computer system with three users: Alice, Bob, and Cyndy. Alice owns the file alicerc, and Bob and Cyndy can read it. Cyndy can read and write the file bobrc, which Bob owns, but Alice can only read it. Only Cyndy can read and write the file cyndyrc, which she owns. Assume that the owner of each of these files can execute it.**  
* **a. Create the corresponding access control matrix.**  

|  | alicerc | bobrc | cyndyrc |
|:-----------:|:------------:|:------------:|:------------:|
| Alice | --xo | r--- | ---- |
| Bob | r--- | --xo | ---- |
| Cyndy | r--- | rw-- | rwxo |

* **b. Cyndy gives Alice permission to read cyndyrc, and Alice removes Bob’s ability to read alicerc. Show the new access control matrix.**  

|  | alicerc | bobrc | cyndyrc |
|:-----------:|:------------:|:------------:|:------------:|
| Alice | --xo | r--- | r--- |
| Bob | ---- | --xo | ---- |
| Cyndy | r--- | rw-- | rwxo |

**2. Consider the set of rights {read, write, execute, append, list, modify, own}.**  
* **a. Using the syntax in Section 2.3, write a command delete_all_rights (p, q, s). This command causes p to delete all rights the subject q has over an object s.**  
 - command delete_all_rights(p, q, s)  
      delete read from a[q, s];  
      delete write from a[q, s];  
      delete execute from a[q, s];  
      delete append from a[q, s];  
      delete list from a[q, s];  
      delete modify from a[q, s];  
      delete own from a[q, s];  
end

* **b. Modify your command so that the deletion can occur only if p has modify rights over s.**  
 - command delete_all_rights(p,q,s)  
    if modify in a[p,s] then  
    delete read in a[q,s]  
    delete write in a[q,s]  
    delete execute in a[q,s]  
    delete append in a[q,s]  
    delete list in a[q,s]  
    delete modify in a[q,s]  
    delete own in a[q,s]  
end  

* **c. Modify your command so that the deletion can occur only if p has modify rights over s and q does not have own rights over s.**  
 - command delete_all_rights(p,q,s)  
      create subject tmp  
      enter read in a[tmp,s]  
      if own in a[q,s] then  
          delete read from a[tmp,s]  
      if modify in a[p,s] and read in a[tmp,s] then  
          delete read in a[q,s]  
          delete write in a[q,s]  
          delete execute in a[q,s]  
          delete append in a[q,s]  
          delete list in a[q,s]  
          delete modify in a[q,s]  
          delete own in a[q,s]  
          destroy subject tmp  
end
