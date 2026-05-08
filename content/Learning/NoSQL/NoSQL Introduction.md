---
id: NoSQL Introduction
aliases: An Introduction to NoSQL Databases
tags:
  - NoSQL
  - db
  - uni
  - uom
author: S.Sunhaloo
date: 2025-03-28
status: Completed
---

>[!INFO] 
>The Lecture Slides for this file / note is called '[[Database Systems - Introduction to NoSQL.pdf]]'

## List of Contents

- [[#Types of Data]]
	- [[#Structured Data]]
	- [[#Unstructured Data]]
	- [[#Static Data]]
	- [[#Dynamic Data]]
- [[#Classification of Data]]
- [[#Scaling of Traditional Databases]]
	- [[#Vertically - Up]]
	- [[#Horizontally - Out]]
- [[#Data Sharding | Sharding of Data]]
- [[#NO ACID]]
	- [[#CAP Theorem]]
	- [[#Compromise, Compromise and Adapt]]

---

- [[#Actual Introduction to NoSQL]]
	- [[#Types of NoSQL Databases]]
		- [[#Document Stores / Document Databases]]
		- [[#Graph Databases]]
		- [[#Key-Value Stores]]
		- [[#Columnar Databases]]

---

>[!INFO] Resources
>- https://www.geeksforgeeks.org/what-is-structured-data/
>- https://www.geeksforgeeks.org/what-is-unstructured-data/
>- https://skillapp.co/blog/understanding-the-key-differences-static-data-vs-dynamic-data-explained/
>- https://www.freecodecamp.org/news/horizontal-vs-vertical-scaling-in-database/
>- https://en.wikipedia.org/wiki/Shard_(database_architecture)
>- https://aws.amazon.com/what-is/database-sharding/
>- https://en.wikipedia.org/wiki/CAP_theorem
>- https://www.geeksforgeeks.org/the-cap-theorem-in-dbms/
>- https://en.wikipedia.org/wiki/NoSQL
>- https://en.wikipedia.org/wiki/Document-oriented_database
>- https://en.wikipedia.org/wiki/Graph_database
>- https://www.geeksforgeeks.org/what-is-a-columnar-database/

# Types of Data

There are 4 main, general types of data ( *or information* ):

1. Structured Data
2. Unstructured Data
3. Dynamic Data
4. Static Data

Let's go ahead and start finding about each of these categories of data!

## Structured Data

>[!TIP] Think of Relational Databases!

**Structured Data** is a type of *data* that has been **designed** and **organised** in a specific way that makes it easy for *both* humans and machines to read.

Example of **Structured Data** might be a `Car` table in 'DealerShip' database; whereby each *car* has its own:

- Brand
- Model
- Year
- Mileage
- Engine Displacement

>[!TIP] Lecturer's Note
>- Has a **predefined model** which **organises** data into a form that is relatively easy to *store*, *process*, *retrieve* and *manage*.
>- Example of Structured Data $\rightarrow$ [[Database Systems - Relational Model | Relational Data]]

>[!INFO] Where Structured Data is Used?
>1. SQL Databases
>2. Spreadsheet Software
>3. Sensors ( *like physical sensors gathering data* )
>4. Network / Web Server Logs
>5. Medical Devices

### Characteristic Of Structured Data

1. Data conforms to a 'data model' and *structured* into rows and columns ( *basically tables* )
2. Well Organised $\Rightarrow$ *Definition*, *Format* and *Meaning* of data is **explicitly** known
3. Each *data item* in that cell / record has a **specific size** ( *think of creation of tables* )
4. **Data items** are '*Addressable*' $\Rightarrow$ Easy to Analyse

### Advantages - Disadvantages of Structured Data

>[!NOTE] Advantages of Structured Data
>- Easy to Analyse, Understand and Use
>	- Because the conform to a **specific** / **predefined format**
>- Consistent ( *because the follow that fucking format $\uparrow$* )
>- *Storage* and *Retrieval* of data is **Efficient**
>- Enhanced Data Security
>	- Structured Data can be *controlled* by **Database's Security Protocol(s)**
>- Clear Lineage
>	- Easy to **modify** and **track** those changes

>[!NOTE] Disadvantages of Structured Data
>- Lack of Addition of New Data Types
>	- We are **locked** to the *predefined format*
>- Limited Complexity
>	- Complex data *structures* **cannot** be easily implemented $\Rightarrow$ Limited by [[Entity Relationship Diagram ( ERD ) and Relationships | Relationships]]
>- Lack of Additional Context and Information ( *or Description* )
>	- Making it **difficult** to understand *meaning* and *significance* of said data
>- **Expensive** to keep *maintenance* of Structured Data
>- Missing / Incomplete Data could be *present* ( *get it... 'Missing'... 'Present'* )

## Unstructured Data

>[!TIP] Think of Flat Files $\rightarrow$ Especially Audio, Text or Video Files

Its the complete **opposite** to *Structured Data* whereby it does **not** have any proper structure and just floats like *fleeting pages* on your desk!

>[!WARNING]
>When we saying that the *data* does not have a "*format*"... We are **not** referring to the *file extension* of that data.
>
>In the case of text files, it could be a normal text file or even a markdown files. For audio or video; it can be either `.mp3` or `.mp4` respectively
>
>We are saying that the contents **inside** those ( *storage* ) mediums are not structured in any way, shape or form.

### Characteristic of Unstructured Data

1. Lack of Format $\Rightarrow$ **Difficult** to *Categorise* and *Organise*
2. Variety of Data Types $\Rightarrow$ **Easy** to Store Variety of Data Types
3. Volume $\Rightarrow$ Makes up large percentage of data today
4. Contents can come from diverse sets of sources

### Advantages - Disadvantages of Unstructured Data

>[!NOTE] Advantages of Unstructured Data
>- No [[SQL Commands - Data Definition Language - Constraints | Constraints]]
>- Very **Portable** and **Scalable**
>- Can consists of *miscellaneous* data
>	- Heterogeneity of Data
>- Has a variety of *Business Intelligence* and *Analytics Application*

>[!NOTE] Disadvantages of Unstructured Data
>- **Difficult** to *Categorise*, *Organise*, *Store* Data
>- [[Database Indexing | Indexing]] is **Difficult** and **Error-Prone**
>	- Due to the **lack** of *structure*
>	- $\Rightarrow$ *Searching* is **not** very *accurate*
>- Ensuring *Data Security* is **Difficult**
>	- Due to "*ease of use*" or "*ease of availability*"
>	- Many normal people can look at contents without requiring specialised programs
>- Requires **lots** of *Storage Space*
>- Operations like `UPDATE`, `DELETE` are very difficult
>	- Because one place may be updated while another place was not

#### Solution for Storing Unstructured Data

- Can be **easily** converted to other types of *formats*
- Can be stored in [XML](https://en.wikipedia.org/wiki/XML) format

## Static Data

**Static Data** is a type of data that does **not** change over time and will mostly stay **unchanged** forever.

Its typically stored in a *Structure Format* $\uparrow$ and does **not** require constant modification. Additionally, they are mostly used to serve as a **record** for *past events* or *conditions*.

Example of Static Data could be $\downarrow$:

- Brand / Model of a Car
- Name Countries - Country Codes
- Archived / Historical Data

### Advantages - Disadvantages of Static Data

>[!NOTE] Advantages of Static Data
>- They are very **predictable**
>- **High Performance**
>	- As their *values* does **not** change $\Rightarrow$ Can be cached effectively
>- **Lower** Maintenance
>	- We don't need to modify it that much
>- **Simplified** *Security*
>	- **Easier** to *enforce* and *audit* security policies ( *as data is not modified often* )

>[!NOTE] Disadvantages of Static Data
>- **Inflexibility** of Data
>	- **Cannot** *adapt* to changes in Business Requirements / Rules
>	- Might lead of **outdated** information
>- **Limited** Scalability
>	- *Static Data* requires **manual** *updates* or *migrations*
>- Difficult to Extend
>	- Systems built around *Static Data* might get **disrupted** if we incorporate new data types
>- Redundancy ( *Well, I think it's self-explanatory* )

## Dynamic Data

Well, its the complete **opposite** of *Static Data* and this time; its going to get changed frequently!

Example are huge:

- Social Media
- Servers Logs
- Sensors Networks

### Advantages - Disadvantages of Dynamic Data

>[!NOTE] Advantages of Dynamic Data
>- Flexible
>	- Adapts to *changes in requirements* **quickly** and **without** major restructuring
>- Gets updated in real time
>	- **Essential** for *live data analytics*, *user interactions* and *monitoring systems*
>- Very Scalable
>	- Can **easily** accommodate growth and inclusion of other data types
>- Innovation Friendly
>	- **Encourages** for *experimentation* and *innovation*

>[!NOTE] Disadvantages of Dynamic Data
>- **Major Hit** on Performance
>	- Real-time processing of data will take a heavy toll on *system resource*
>- Maintenance Burden
>	- Keeping **track** of these types of data is a problem
>- Data Integrity Risks
>	- Ensuring *accuracy* and *consistency* of data is **more** *error-prone*

# Classification of Data

Data can be classified like so; Please study the image below $\downarrow$

![[NoSQL - Classification of Data.png]]

# Scaling of Traditional Databases

*Traditional* **Relational Database** can be scaled in 2 ways, namely:

1. Vertically ( *Up* )
2. Horizontally ( *Out* )

## Vertically - Up

Scaling "*vertically*" can be illustrated by the early days of [PayPal](https://en.wikipedia.org/wiki/PayPal), when [Elon Musk](https://en.wikipedia.org/wiki/Elon_Musk) used his personal computer as a server. At night, when traffic was low, he would repurpose that same computer to code the application. By day, he switched it back to hosting, handling the site’s user traffic.

**Scaling 'Vertically'** means that a person is going to **improve** the *performance* of that machine. Its like f Mr Elon upgraded his computer to improve its performance.

Therefore "*vertical*" scaling can be achieved using **hardware upgrades** by using things like *faster CPUs*, *more memory* or *larger storage*.

Nevertheless, all machines have their limits—only certain types of upgrades are possible, and further improvements may **not** be feasible. For example, in my computer, if I upgrade the CPU, the latest Intel processors available to me are from the 11th generation.

### Advantages - Disadvantages of Vertical Scaling

>[!NOTE] Advantages of Vertical Scaling
>- **No** need to upgrade to bigger *infrastructure*
>	- Using **same** computer is not going to required significant change in the building
>	- **No** need to install additional *cooling* / *power* in building
>- **Cost Efficient** ( *Hardware and Software* )
>	- No need to purchase another machine completely
>	- Using same ( *amount* ) of computers would require **no** additional software ( *to link them up* )
>- **Easy** to *implement* and *use*

>[!NOTE] Disadvantages of Vertical Scaling
>- **Limit** to upgrade $\Rightarrow$ Like I was saying above $\uparrow$
>- Hardware Costs are Big
>	- Companies don't use desktop computer ( *obviously* ) $\rightarrow$ Therefore, its costs more to upgrade
>- Reliance on Single Machine
>	- *Failure* in **system** can be be *catastrophic*
>- Still going to have to buy new machines as *requirements* **grows**.

## Horizontally - Out

Compared to *vertical scaling*... *Horizontal Scaling* means that instead of upgrading the machines / servers that we have... We are instead, going to **buy more** machines to be able to handle our *requirements*.

>*Because we have lots of cash to spare*!!!

### Advantages - Disadvantages of Horizontal Scaling

>[!NOTE] Advantages of Horizontal Scaling
>- **Decreases** load ( *spreads out resources* ) on *individual* servers
>- Offers **Flexible**, **Scaling Tools**
>- **Limitless Scaling**
>	- We can just keep adding more and more

>[!NOTE] Disadvantages of Horizontal Scaling
>- "**Bugs**" in *code* becomes more complex to debug and understand
>- License Fee
>	- Adding more and more *nodes* ( *servers* ) is going to required additional licenses
>- **Change** in *Infrastructure*
>	- Buildings will need to require **more** *power*, *cooling* and *space* ( *obviously* )

# Data Sharding

>[!INFO]
>I really recommend you to take a look at this link: https://aws.amazon.com/what-is/database-sharding/
>
>>I have also added this link in the '*Resources*' section above $\uparrow$
>

>[!TIP] Definition of '**Database Sharding**'
>Database **Sharding** is the processing of *large database* ( *like the actual database object* ) **across** multiple machines.
>
>"*Jobs*" are then going to be **splitted** across these difference machines ( *servers* ) as a **single** machine can process **smaller chunks** of *tasks* easier and faster compared to large amounts of information.
>
>>BTW "*Sharding*" basically means to **Split**!
>>Additionally, a "*Shard*" is **same** as a "*Chunk*".
>

"*Database Sharding*" is important as ( *if* ) application(s) continues to *grow*. This means that the number of users and the amount of data that is going to be stored is going to **massively increase**. Therefore, without "*shading*" the data, database will be *bottlenecked* by the amount of processes that the current machine(s) have.

Therefore, *splitting* the work across **multiple** database servers means that, again, *tasks* are going to be done much **faster** as it enables for **Parallel Processing**.

![[NoSQL - Data Sharding.png]]

>[!TIP]
><p align="center">Data Sharding :FasHandshakeSimple: Horizontal Scaling</p>

## Advantages - Disadvantages of Data Sharding

>[!NOTE] Advantages of Data Sharding
>- [[#Horizontally - Out | Horizontal Scalability]]
>	- Database *tasks* / *jobs* are **spreaded** out across multiple machines
>- **Improved** *Performance* and *Latency*
>	- Dividing large datasets into smaller, manageable chunks makes it **easier** for machines to *process*'
>- Efficient Resource Management
>	- Each individual machine ( *or server* ) does **not** receive a lot of *load*

>[!NOTE] Disadvantages of Data Sharding
>- **Increased** Complexity
>	- Managing and Debugging errors in code becomes difficult as we have a lot of servers
>- **Higher** Maintenance Costs
>	- *Well, I think you know the reason by now*!
>- Risk of Data Inconsistency
>	- **Without** proper *synchronisation*... Data becomes difficult to manage.

# NO ACID

>*No, not the chemical or the drug that people take*.

If you remember... Relational Databases and Database Transaction follows the '*ACID*' properties.

>You can find the note / file I am over at '[[Database Transactions - ACID]]'

But because the structure of NoSQL "*program*" ( *like actually, how do you call that*? ) are different; hence, this does **not** apply!

Therefore we have the '*CAP*' Theorem

## CAP Theorem

The '*CAP*' in *CAP Theorem* stands for $\downarrow$:

<p align="center">Consistency, Availability, Partition Tolerance</p>

>[!NOTE] Consistency
>- All ( *server* ) nodes inside a network should have the same *copies* of **replicated** data
>	- Each *client* should have the **same** view of the Data
>- Every read receives the **most recent** *write* / *error*
>
>>[!WARNING]
>>The 'Consistency' in **CAP Theorem** is <span style="color: red;">different</span> from the 'Consistency' of [[Database Transactions - ACID#Consistency | Consistency]]!
>>
>>Whereby here we are talking about how the *data* **appears** while in 'ACID' we talk above the **integrity** of that data.
>

>[!NOTE] Availability
>- Data Item is either *processed* successfully or *fails* and provides error message
>	- There needs to be a response **always** ( *even if failed* )
>- Each client can **always** *read* and *write* data

>[!NOTE] Partition Tolerance
>- Database operation can **still** continue to **operate** even if there is something *wrong* with ( *or in between the* ) network
>- Data **synchronisation** techniques are available
>	- Meaning when the network is back up $\rightarrow$ Data will be made available to other nodes

### Compromise, Compromise and Adapt

Compared to our lovely '*ACID*'; we **cannot** enforce *everything* in 'CAP'. We have to make a **selection** of *2*.

This means that in a Business, their database can only conform to '*Consistency*' and '*Availability*' while in another Business, their database can conform to '*Availability*' and '*Partition Tolerance*'.

>[!INFO] What is Best?
>
>>"*It Depends!!!*" Mrs Suddha
>
>**Not** all business and database are the *same*. It depends on what we are trying to do!
>
>Below $\downarrow$ you will find example of each *category* of where they are used.
>
>>[!INFO] Example of Systems
>>
>>| Consistency + Availability | Consistency + Partition Tolerance | Availability + Partition Tolerance |
>>| -------------------------- | --------------------------------- | ---------------------------------- |
>>| Bank's Financial System | Coordination - Configuration Management Systems | [YouTube](https://www.youtube.com/watch?v=dQw4w9WgXcQ), [Twitch](https://www.twitch.tv/directory/category/software-and-game-development) |

>[!WARNING]
>This does **not** mean that if a Business has chosen to go with '*Availability + Partition Tolerance*'; the database will be *inconsistent*. No! The database should still follow these rules but that Business surely know that the type of data that they are keeping don't "*become*" inconsistent.

# Actual Introduction to NoSQL

>[!TIP] 'NoSQL' Stands For
>1. No Relational
>2. No Relational Database Management System [[Database Management System ( DBMS ) | ( RDBMS )]]
>3. Not Only SQL
>
>>This does not that we are not going to be writing SQL any more.
>>Its actually the **opposite**!
>

This term of 'NoSQL' comes from the Internet and often known as the '*Big Data*' concept.

This is because compared to predefined format... The Internet is **Wild** ( *literally* )! This meant that we **cannot** simply use *Relational* database to structure this **unstructured** data and also that is really **massive** in size ( *that's what she said*! ).

## Types of NoSQL Databases

There are 4 main types of NoSQL databases, namely $\downarrow$:

1. Document Stored / Document Databases
2. Graph Databases
3. Key-Values Stores
4. Columnar Databases

>I really want to buy a, ( *takes deep breath* ), split, ortholinear, columnar, low profile mechanical keyboard.

### Document Stores / Document Databases

As the name suggest, this type of database is **stored** as *documents*. Yes! like the a text file, more specifically text file with format such as `.xml` or `.json`.

These *formats of files* are typically referred to as [Binary Large Objects ( BLOBs )](https://en.wikipedia.org/wiki/Object_storage)

In this case of *Document Stores*, they are mostly used for:

- [Content Management Systems](https://en.wikipedia.org/wiki/Content_management)
- Blogging Platforms
- Real Time Analytics
- E-Commerce Applications

Compared to traditional text file `.txt`; These above $\uparrow$ formats that I just mentioned can be **indexed**.
This means that we can **easily** *search* and *modify* the contents of these *document files*.

>In this case of [[MongoDB Data View | MongoDB]], We are going to be using [JSON](https://www.youtube.com/watch?v=_aHMfjk1YH8&t=298s) files.

#### Example of a JSON File

This is my part of my VS Code configuration... If you need to full thing or other any other configuration files that I have. Please visit 'https://github.com/Sunhaloo/dotfiles'

```json
{
	// other configuration above
	
    // vim keymapping
    // normal mode keymappings
    "vim.normalModeKeyBindingsNonRecursive": [
        // save and close
        {
            "before": ["leader", "q"],
            "commands":
                [
                        "workbench.action.files.save",
                        "workbench.action.closeActiveEditor"
                ]
        },
        // close without saving
        {
            "before": ["leader", "Q"],
            "commands": ["workbench.action.revertAndCloseActiveEditor"]
        },
        // open a new empty tab
        {
            "before": ["t", "e"],
            "commands": ["workbench.action.files.newUntitledFile"]

        },
		
	// other configuration below
}
```

>[!NOTE]
>[JSON](https://en.wikipedia.org/wiki/JSON) are **not** really a programming language or any thing sort of that. Instead, its just a simple file that holds **data** and that data change be modified and processed.

### Graph Databases

[Well, well, well](https://www.youtube.com/watch?v=XFagogEOZz8&t=15s)! As the name suggests... The data is *represented* as **vertices** / **nodes** and **edges** / **[[Entity Relationship Diagram ( ERD ) and Relationships | relationships]]**.

Similar to something like the *graph view* in Obsidian where we can link the individual files ( *or vertices* ) and we as you know; Obsidian makes a lot emphasis on its **linking** feature.

One of the most **important** ( *if not the most important* ) is going to be the **relationships** between each *nodes*.

>[!TIP]
>- **Entity** $\rightarrow$ **Node** / **Vertex**
>- **Relationship** $\rightarrow$ **Edge**

So **graphs** are considered as a *data structure* because it is a **data structure**. And this is how they are also implemented!

>One of the most popular Graph Database program is [Neo4j](https://neo4j.com/)

>[!TIP] Where are Graphs Used?
>In Social Media platforms like [Instagram](https://instagram.com), [Facebook](https://facebook.com), graph databases are used to provide friend suggestions.
>
>>Who are "*friends*" anyways?
>

### Key-Value Stores

Do you know what the fuck is a dictionary... Then you can use a fucking dictionary to find the meaning of '*dictionary*'.

They are the **simplest** forms of NoSQL databases. Whereby we have a **key** and a **value**.

>Its literally like an actual dictionary or dictionaries that are found in programming languages.

One thing is that Key-Value Stores / Databases does not have `JOIN`s or aggregate functions and mostly rely on **CRUD** operations.

Example of Programs that use Key-Value databases are going to be:

- [Amazon DynamoBD](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)

>[!TIP]
>- **Attribute** $\rightarrow$ **Key**
>- Each *Key* has a **Value**

### Columnar Databases

Similar to something like a table in Relational Database or like a Spreadsheet table. *Data* are stored in **rows** and **columns** but this time, we place lots of **emphasis** on the *columns*.

Nevertheless, the data is **not** stored as a single table... Instead, **columns** are grouped into *column families*.

Compared to Key-Value Database $\uparrow$, they have features like **aggregate** functions and they are very performant when it comes to functions like `SUM`, `AVG` and more.

Given this *table* below $\downarrow$:

| ID | Last Name | First Name |
| -- | --------- | ---------- |
| 1 | Senna | Ayrton |
| 2 | Hamilton | Lewis |
| 3 | Vettel | Sebastien |

This is how they are represented in **Columnar Databases**:

```console
1, 2, 3; Senna, Hamilton, Vettel; Ayrton, Lewis, Sebastien
```

Compared to the usual **Row Databases**:

```console
1, Senna, Ayrton; 2, Hamilton, Lewis; 3, Vettel, Sebastien
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/channel/UCMkQZsuW6eHMhdUObLPSpwg
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!