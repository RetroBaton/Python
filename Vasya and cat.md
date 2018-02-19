import random

class House:

	def __init__(self):
		self.dirty = 0
		self.cat_bowl = 0
		
class Man:

	def __init__(self, name):
		self.name = name
		self.money = 100000
		self.mood = 50
		self.house = None

	def status(self):
		print('Я - {}, денег {}, настроение на {}'. format(self.name, self.money, self.mood))

	def buy_house(self, house):
		print('{} купил дом!!!'.format(self.name))
		self.money -=99990
		self.house = house
		self.mood +=30

	def go_work(self):
		print('{} пошел на работу'.format(self.name))
		self.mood -=30
		self.money +=50

	def play_wow(self):
		print('{} играл целый день'.format(self.name))
		self.mood +30

	def pick_up_cat(self, cat):
		print('{} подобрал кота!'.format(self.name))
		cat.house = self.house
		self.cat = cat

	def put_food(self):
		if self.house.cat_bowl > 50:
		    print('{} положил коту еды'.format(self.name))
		else:
			self.house.cat_bowl += 50
			self.money -=50
			print('{} положил коту еды'.format(self.name))

	def act(self):
		dice = random.randint(1, 6)
		if dice == 1:
			self.go_work()
		else:
			self.play_wow()


class Cat:

	def __init__(self, name):
		self.name = name
		self.mood = 10
		self.house = None
		self.fullness = 0
	
	def status(self):
		print('Я - {}, сытость {}, настроение на {}'.format(self.name, self.fullness, self.mood))

	def meow(self):
		print('МЯУУУУУУ!')

	def eat(self):
		if self.house is None:
			print('У кота нет дома... есть нечего')
			return
		if self.house.cat_bowl > 10:
			self.fullness +=10
			self.house.cat_bowl -=10
			self.mood += 10
			print('Я {}, поел еды'.format(self.name))
		else:
			print('Я {}, не хватает еды! МЯУ!'.format(self.name))

	def sleep(self):
		print('Я {}, спал весь день'.format(self.name))
		self.fullness -= 10
		self.mood -= 10

	def act(self):
		if self.fullness <= 0:
			print('Кот {} умер...'.format(self.name))
			return
		dice = random.randint(1, 6)
		if self.fullness < 20:
			self.eat()
		elif dice == 1:
			self.eat()
		else:
			self.sleep()


vasya = Man(name='Вася')
home = House()
vasya.buy_house(house=home)

murzik = Cat(name='murzik')
murzik.meow()
murzik.eat()
vasya.pick_up_cat(cat=murzik)
murzik.eat()
vasya.put_food()
murzik.eat()

for day in range(1, 11):
	print('---------------- день', day)
	vasya.act()
	murzik.act()
	vasya.status()
	murzik.status()


vasya.go_work()
vasya.status()

vasya.play_wow()
vasya.status()
