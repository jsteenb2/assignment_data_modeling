# assignment\_data\_modeling

contributors: By [Johnny Steenbergen](https://github.com/jsteenb2) & [Adrian Mui](https://github.com/adrianmui)

##Description
This is an exercise in understanding how to model data. Understanding the way the data interacts with different tables and the web application itself is stressed.

#Basics

Basics #1

GOALS
----
Serve a site with classes that have their own lesson plans and details (possibly shared details like authors etc.)

Teacher wants to put out a class and serve it to students.  Each class will likely consist of many lessons and follow a path (lesson plan).

###Entities
1. Course
	* title:varchar
	* description:text

2. Lesson
	* title:varchar
	* description:text
	* course_id:int 


Basics #2

Goals
----
Obtain users information and expand to info like City, State, Country, Age and Gender

Should have just 1 profile.

###Entities
1. Profile
  * user_id:int
  * location_id:int
  * age:int
  * gender:varchar
2. User
  * username:varchar
  * email:varchar
3. Location
  * city:varchar
  * state:varchar
  * country:varchar

  
#Intermediate

Intermediate #1: hacker news

Goals
----
Have posts and show them, allow for comments, and show them, and keep order integrity.

###Entities
1. Post/Link
  * title:varchar
  * link:varchar
  * vote_score:int
2. Comment
  * post_id:int
  * comment_id:int
  * vote_score:int
  * description:text

How would we make sure a comment knows where in the heirarch it lives?
 -> Follow the post_id then go to comment_id which it would be nested under.  Find other comments in tat section and compare vote_score.
 
#Advanced

Advanced #1: amazon.com

Goals
----
Collect products,user, orders, shipments, and other data to create a package for the user. procured marketing.

###Entities
1. Product
	* name:varchar
	* description:text
	* price:int
	* sku:varchar
2. User
	* name:varchar
	* location_id:int
3. Order
   * order_num:varchar
   * user_id:int
   * payment_id:int
4. Location
	* address:varchar
	* city:varchar
	* state:varchar
	* country:varchar
5. Shipment
   * ship\_to\_location_id:int
   * ship\_from\_location_id:int
   * tracking_num:varchar
   * order_id:int
6. Item
	* product_id:int
	* quantity:int
	* order_id:int
7. Payment
	* name:varchar
	* location_id:int
	* payment_source_id:int
	  (create sources perhaps later)

**How can you handle the quantity of items in each order?** 
Simply create the item entity which holds product and quantity of it. The order has a one-to-many relationship with the item. The order_id will be a foreign key in the item entity.

**How do you know where an order has been shipped?**
Have a ship\_to attr in the shipment that corresponds to a location_id, which is the location that it is shipping too.

**Bonus: What happens to your historical data if a user opts to delete their account?** 
We lose users name, that's about all. Since payment has unique name attr independent of user.

**How might you handle this?**
See above ^
