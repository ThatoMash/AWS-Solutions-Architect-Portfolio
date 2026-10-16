#  Introduction to Amazon DynamoDB – Music Library Lab

##  Overview

I completed the **Introduction to Amazon DynamoDB** lab where I worked with a fully managed NoSQL database service designed for fast and predictable performance. This lab helped me understand how DynamoDB stores data using tables, items, and attributes, and how it provides flexible schema design.

In this lab, I created a music library table, added items, modified data, queried items efficiently, and finally deleted the table.

---

##  What I Achieved

During this lab, I

* Created a DynamoDB table named **Music**
* Inserted multiple music records with flexible attributes
* Modified existing data
* Queried and scanned records
* Deleted the table after verification

---

##  Task Breakdown

###  Create a DynamoDB Table

I created a table called **Music** using:

* **Partition Key:** Artist (String)
* **Sort Key:** Song (String)

This allowed me to uniquely identify each music item.

 *Picture Placeholder – Create Table Screen*
 Launch A DynamoDB
 <img width="1364" height="563" alt="image" src="https://github.com/user-attachments/assets/f21230c7-70c1-4775-9b37-6f39f6f08bda" />

 Create a table

 <img width="1365" height="525" alt="image" src="https://github.com/user-attachments/assets/3a6db081-7b91-4847-b2a5-0de2de941111" />

  Table is Successfully created

<img width="1365" height="318" alt="image" src="https://github.com/user-attachments/assets/e6361645-bd8a-43eb-9c5e-e9cb533a778c" />


---

### ** Add Data to the Table**

I inserted multiple songs into the table, each with different attributes such as Album, Genre, Year, and LengthSeconds.

This demonstrated how DynamoDB supports flexible schemas where each item can contain different attributes.

 Create Items


 <img width="1365" height="544" alt="image" src="https://github.com/user-attachments/assets/a4178417-7dec-461c-bdd0-4f630cdd6bbe" />

 adding Data

 <img width="1361" height="388" alt="image" src="https://github.com/user-attachments/assets/967c373c-2ca8-4505-ae5e-0b0d2d9c6de3" />

Adding new attributes

<img width="1365" height="488" alt="image" src="https://github.com/user-attachments/assets/be47fa7c-b118-4423-8f76-c5e15ed57807" />

Data is Successfully added to the table

<img width="1351" height="570" alt="image" src="https://github.com/user-attachments/assets/2ebc697e-1483-4622-aa08-8d49e84a7560" />


---

### ** Modify an Existing Item**

I updated the **Year** for the song **Gangnam Style** from 2011 to 2012.

 *Picture Placeholder – Edit Item Screen*

 <img width="1365" height="578" alt="image" src="https://github.com/user-attachments/assets/1c93e3ad-185d-4b90-8d24-fd8e7029dd11" />

I updated the year from 2011 to 2012

 <img width="1356" height="536" alt="image" src="https://github.com/user-attachments/assets/386a61fa-6370-45bd-a774-2d25cc368196" />

---

### ** Query the Table**

I performed two types of lookups:

* **Query:** Fast, based on primary key (Artist + Song)
* **Scan:** Checked all items and filtered by Year

   Query Results*
<img width="1353" height="579" alt="image" src="https://github.com/user-attachments/assets/e9d92abf-28cc-4222-8d32-9ec76f37d522" />


 *Picture Placeholder – Scan Results*
 
<img width="1365" height="568" alt="image" src="https://github.com/user-attachments/assets/d21cbee1-92b9-49d6-a242-5372612da221" />

 
---

### ** Delete the Table**

Once done, I deleted the **Music** table to clean up all resources.

*Delete Table Confirmation*

Go to Update Setting

<img width="1355" height="276" alt="image" src="https://github.com/user-attachments/assets/8a133805-1503-4e6f-b698-e60afc930fcb" />

Delete Table

<img width="1359" height="578" alt="image" src="https://github.com/user-attachments/assets/81fa39a6-531e-46a0-b317-32c5aaa71b1e" />

Confirm deletion of the table

<img width="736" height="471" alt="image" src="https://github.com/user-attachments/assets/9f8aadb9-70dd-46d9-a7f5-6c89c8190586" />

Table has been successfully deleted.

<img width="1363" height="230" alt="image" src="https://github.com/user-attachments/assets/3ed3a6f3-6a69-4ac5-bfc5-129210a1d78c" />

---

##  Conclusion

By completing this DynamoDB lab, I strengthened my understanding of:

* NoSQL data modeling
* Partition and sort keys
* DynamoDB queries vs scans
* Table and item management in a serverless database

This hands-on experience helped me build confidence in using DynamoDB for real-world applications.

---



