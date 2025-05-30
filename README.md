# mongodb_medium

## 1. Total Quantity of Products by Supplier:

aggregationAssignmentDB> db.products.aggregate([
...   {
...     $group: {
...       _id: "$supplier.name",
...       totalQuantity: { $sum: "$quantity" }
...     }
...   }
... ]);
...
[
  { _id: 'StyleCraft', totalQuantity: 120 },
  { _id: 'FashionHub', totalQuantity: 280 },
  { _id: 'ActiveLife', totalQuantity: 90 },
  { _id: 'SoundWave', totalQuantity: 60 },
  { _id: 'TechGlobe', totalQuantity: 60 },
  { _id: 'GadgetPro', totalQuantity: 125 },
  { _id: 'HomeBest', totalQuantity: 30 }
![Medium-1](https://github.com/user-attachments/assets/02d69613-32c3-4337-837f-f8a614ea89a7)


  ## 2. Average Price of Products per Tag:
aggregationAssignmentDB> db.products.aggregate([
...   { $unwind: "$tags" },
...   {
...     $group: {
...       _id: "$tags",
...       averagePrice: { $avg: "$price" }
...     }
...   },
...   {
...     $sort: { averagePrice: -1 }
...   }
... ]);
...
[
  { _id: 'work', averagePrice: 1200 },
  { _id: 'portable', averagePrice: 493 },
  { _id: 'computer', averagePrice: 433.3333333333333 },
  { _id: 'kitchen', averagePrice: 250 },
  { _id: 'coffee', averagePrice: 250 },
  { _id: 'appliance', averagePrice: 250 },
  { _id: 'gadget', averagePrice: 199 },
  { _id: 'wearable', averagePrice: 199 },
  { _id: 'audio', averagePrice: 80 },
  { _id: 'mechanical', averagePrice: 75 },
  { _id: 'denim', averagePrice: 60 },
  { _id: 'wireless', averagePrice: 52.5 },
  { _id: 'peripheral', averagePrice: 50 },
  { _id: 'fashion', averagePrice: 45 },
  { _id: 'leather', averagePrice: 45 },
  { _id: 'clothing', averagePrice: 40 },
  { _id: 'fitness', averagePrice: 30 },
  { _id: 'exercise', averagePrice: 30 },
  { _id: 'cotton', averagePrice: 20 },
  { _id: 'casual', averagePrice: 20 }
]

![Medium-2](https://github.com/user-attachments/assets/ec85b5bb-46e6-435b-addc-019d6baf94b3)

## 3. Products Added in February 2023:
aggregationAssignmentDB> db.products.aggregate([
...   {
...     $match: {
...       date_added: {
...         $gte: new Date("2023-02-01T00:00:00Z"),
...         $lt: new Date("2023-03-01T00:00:00Z")
...       }
...     }
...   },
...   {
...     $project: {
...       _id: 0,
...       name: 1,
...       category: 1,
...       formattedDateAdded: {
...         $dateToString: {
...           format: "%Y-%m-%d",
...           date: "$date_added"
...         }
...       }
...     }
...   }
... ]);
...
[
  {
    name: 'Wireless Mouse',
    category: 'Electronics',
    formattedDateAdded: '2023-02-01'
  },
  {
    name: 'Espresso Machine',
    category: 'Home Goods',
    formattedDateAdded: '2023-02-15'
  },
  {
    name: 'Bluetooth Speaker',
    category: 'Electronics',
    formattedDateAdded: '2023-02-25'
  }
]

![Medium_3](https://github.com/user-attachments/assets/3219c37a-ee52-4726-aab1-c16a31691d30)

