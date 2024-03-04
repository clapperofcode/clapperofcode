import random

class Character:
    def __init__(self, name, hp, attack):
        self.name = name
        self.hp = hp
        self.attack = attack

    def take_damage(self, damage):
        self.hp -= damage

    def is_alive(self):
        return self.hp > 0

    def attack_enemy(self, enemy):
        damage = random.randint(0, self.attack)
        enemy.take_damage(damage)
        print(f"{self.name} attacks {enemy.name} for {damage} damage!")

class Enemy(Character):
    pass

class Player(Character):
    def __init__(self, name, hp, attack, gold=0):
        super().__init__(name, hp, attack)
        self.gold = gold

    def add_gold(self, amount):
        self.gold += amount

def combat(player, enemy):
    print(f"A wild {enemy.name} appears!")
    while player.is_alive() and enemy.is_alive():
        print(f"\n{player.name} HP: {player.hp} | {enemy.name} HP: {enemy.hp}")
        player.attack_enemy(enemy)
        if enemy.is_alive():
            enemy.attack_enemy(player)
    if player.is_alive():
        print(f"\nYou defeated the {enemy.name}!")
        player.add_gold(random.randint(10, 20))
        print(f"You gained {player.gold} gold.")
    else:
        print("\nYou were defeated!")

def main():
    print("Welcome to the RPG Game!")
    player_name = input("Enter your character's name: ")
    player = Player(player_name, 100, 20)

    while True:
        print("\n1. Explore")
        print("2. Check inventory")
        print("3. Quit")
        choice = input("Enter your choice: ")

        if choice == "1":
            enemy = Enemy("Goblin", 50, 10)
            combat(player, enemy)
        elif choice == "2":
            print(f"{player.name}'s Gold: {player.gold}")
        elif choice == "3":
            print("Thanks for playing!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
