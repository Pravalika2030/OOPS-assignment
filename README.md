CODE:
import pandas as pd
import matplotlib.pyplot as plt
class House:
  def __init__(self, address, rent, bedrooms, bathrooms):
    self.address = address
    self.rent = rent
    self.bedrooms = bedrooms
    self.bathrooms= bathrooms
class User:
  def __init__(self, name):
    self.name = name
    self.purchases = []
  def purchase(self, house):
    self.purchases.append(house)
class App:
  def __init__(self):
    self.allhouses = pd.DataFrame(columns=['ID', 'Address', 'Rent', 'Bedrooms', 'Bathrooms'])
    self.purchasedhouses = pd.DataFrame(columns=['ID', 'Address', 'Rent', 'Bedrooms','Bathrooms'])
    self.availablehouses= pd.DataFrame(columns=['ID', 'Address', 'Rent', 'Bedrooms','Bathrooms'])
    self.users= pd.DataFrame(columns=['ID', 'Name'])
  def add_house(self, address, rent, bedrooms, bathrooms):
    newhouse_id = len(self.allhouses) + 1
    newhouse = pd.DataFrame([[newhouse_id, address, rent, bedrooms, bathrooms]],
    columns=['ID', 'Address', 'Rent', 'Bedrooms', 'Bathrooms'])
    self.allhouses = self.allhouses._append(newhouse, ignore_index=True)
    self.availablehouses = self.availablehouses._append(newhouse, ignore_index=True)
  def add_user(self, name):
    nuser_id = len(self.users) + 1
    nuser = pd.DataFrame([[nuser_id, name]], columns=['ID', 'Name'])
    self.users = self.users._append(nuser, ignore_index=True)
  def make_purchase(self, user_id, house_id):
    purchasedhouse = self.availablehouses[self.availablehouses['ID'] == house_id]
    self.purchasedhouses =self.purchasedhouses._append(purchasedhouse,ignore_index=True)
    self.availablehouses= self.availablehouses[self.availablehouses['ID'] != house_id]
    #newpurchase = pd.DataFrame([[user_id, house_id]], columns=['User_ID', 'House_ID'])
    #self.purchasedhouses= self.purchasedhouses._append(newpurchase, ignore_index=True)
  def purchased_houses(self):
    print("Purchased Houses:")
    print(self.purchasedhouses)
  def available_houses(self):
    print("Available Houses:")
    print(self.availablehouses)
  def rent_distribution(self):
    rents = self.allhouses['Rent']
    plt.hist(rents, bins=10, color='skyblue', edgecolor='black')
    plt.title('Rent Distribution')
    plt.xlabel('Rent (rupees)')
    plt.ylabel('Frequency')
    plt.show()
obj= App()
obj.add_house("gandipet cross road",25000,2,2)
obj.add_house("hitech city, road 2",30000,2,2)
obj.add_house("char minar road",8000,2,2)
obj.add_house("chandrayan gutta",10000,2,2)
print(" for selling house-1\n for creating account-2 \n for purchasing house-3\n for vewing
purchases in graph-4\n for getting lists of \n purchased houses - 5_1\n available houses -5-2\n
stop-6")
while True:
  n=input('enter the no. according to the instructions given')
  if n=='1':
    add=input("address = ")
    rent=int(input('rent = '))
    bt=input('no. of bathrooms')
    br=input('no. of bedrooms')
    obj.add_house(add,rent,bt,br)
  if n=='2':
     obj.add_user(input('name'))
  if n=='3':
     obj.make_purchase(int(input("user id")),int(input("houseid")))
  if n=='4':
     obj.rent_distribution()
  if n[0]=='5':
     if n[-1]=='1':
        obj.purchased_houses()
     if n[-1]=='2':
        obj.available_houses()
  if n=='6':
     break
