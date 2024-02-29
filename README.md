# IN THIS REPOSITORY
## MongoDB basic queries
1) Find all the information about each products 
   
   **Answer**: `>db.products.find()`
1) Find the product price which are between 400 to 800
 **Answer:**`>db.products.find({'product_price':{$gt:400,$lt:800}});`

1) Find the product price which are not between 400 to 
600
**Answer:**`db.products.find({'product_price':{$not:{$gt:400,$lt:600}}});`
1) List the four product which are greater than 500 in price
   **Answer:**`db.products.find({'product_price':{$gt:500}}).limit(4);`
2) Find the product name and product material of each products
   **Answer:**`>db.products.find({},{_id:0,'product_name':1,'product_material':1});`

3) 	Find the product with a row id of 10.
   **Answer:**`>db.products.find({'id':10});`
4) 	Find only the product name and product material.
   **Answer:**`>db.products.find({'id':8},{'product_name':1,'product_material':1});`
5)   Find all products which contain the value of soft in product material
   **Answer:**`>db.products.find({'product_material':'Soft'});`
6) Find products which contain product color indigo  and product price 492.00.
   **Answer:**`>db.products.find({$and:[{'product_color':'indigo'},{'product_price':492.00}]});`
7) 	Delete the products which product price value are same
   **Answer:**
   ```
   >db.products.aggregate([
              {$group:
                  {_id:'product_price',
                   duplicate:{$addToSet:'$_id'},
                  count:{$sum:1}
                  }
               },
               {$match:{count:{$gt:1}}
               }
               ]).forEach(function(doc)
                 {
                  db.product.deleteOne({_id:{$in:doc.duplicates}})
                });
```