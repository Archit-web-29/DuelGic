# RECORD TIME OF BEATING THE GAME IS 9:28:98
import random, sys
import time
from colorama import Fore, Style

print(f"{Fore.BLUE}HOGWARTS III - THE LEGENDS")
print(f"{Fore.YELLOW}v.1.18.03. x.25. maj.8.03.25. err.absent. mal.present. up.past{Fore.RESET}")
print(f"{Fore.GREEN}Game is till date")
print(f"{Fore.RED}Malfunction Present - Zeus's Lightning Bolt Medallion{Fore.RESET}")
print()

def display_health_bar(label, current, maximum, bar_length=30):
    ratio = current / maximum if maximum > 0 else 0
    filled_length = int(round(ratio * bar_length))
    if ratio > 0.6:
        bar_color = Fore.GREEN
    elif ratio > 0.3:
        bar_color = Fore.YELLOW
    else:
        bar_color = Fore.RED
    bar = f"{bar_color}{'█' * filled_length}{Style.RESET_ALL}" + '░' * (bar_length - filled_length)
    percent = int(ratio * 100)
    print(f"{label}: [{bar}] {percent}% ({current}/{maximum})")

def display_shield_bar(label, current, maximum, bar_length=20):
    if maximum <= 0:
        return
    ratio = current / maximum
    filled_length = int(round(ratio * bar_length))
    bar = f"{Fore.BLUE}{'█' * filled_length}{Style.RESET_ALL}" + '░' * (bar_length - filled_length)
    percent = int(ratio * 100)
    print(f"{label} Shield: [{bar}] {percent}% ({current}/{maximum})")

def apply_damage(current_health, current_shield, damage):
    if current_shield > 0:
        if damage <= current_shield:
            current_shield -= damage
            damage = 0
        else:
            damage -= current_shield
            current_shield = 0
    current_health -= damage
    return current_health, current_shield

# Damage ranges for each spell (min, max)
spell_damage_ranges = {
    "1": (10, 15),
    "2": (0, 5),
    "3": (5, 10),
    "4": (10, 15),
    "5": (10, 15),
    "6": (5, 10),
    "7": (0, 1),
    "8": (5, 10),
    "9": (0, 0),
    "10": (0, 100),  # Avada Kedavra damage range
    "0": (0, 50),    # Secret spell from Medallion of Creation (input '0')
    "11": (1, 150),
    "999": (200, 200)  # Secret creator's limited spell
}

def choose_difficulty():
    print(f"{Fore.YELLOW}Choose Your Duel Difficulty:{Style.RESET_ALL}")
    print("1. Beginner (Neville Longbottom)")
    print("2. Medium (Draco Malfoy)")
    print("3. Easy (Harry Potter)")
    print("4. Skilled (Godric Gryffindor)")
    print("5. Enchantress (Morgana La Fey)")
    print("6. Dark Master (Salazar Slytherin)")
    print("7. Legendary (Gellert Grindelwald)")
    print("8. Grand Sorcerer (Albus Dumbledore)")
    print("9. Extreme (Lord Voldemort)")
    print("10. Mythical (Merlin Wyllt)")
    print(f"{Fore.RESET}11. {Fore.RED}HERO{Fore.RESET} ~ Eligibility Required - "f"{Fore.BLUE} HOGWARTS III - THE LEGENDS"f"{Fore.RESET}")
    print("12. "f"{Fore.RED}PRO{Fore.RESET} ~ Eligibility Required - "f"{Fore.BLUE} HOGWARTS III - THE LEGENDS"f"{Fore.RESET}")
    print("13. "f"{Fore.RED}Alfredo Casinido"f"{Fore.RESET} ~ Registry Password Required - "f"{Fore.BLUE} HOGWARTS IV - THE QUIESSCENCE UNCHARTED"f"{Fore.RESET}")
    print("14. "f"{Fore.RED}Calypso Scar"f"{Fore.RESET} ~ Registry Password Required - "f"{Fore.BLUE} HOGWARTS IV - THE QUIESSCENCE UNCHARTED"f"{Fore.RESET}")
    print("15. "f"{Fore.BLUE}Dr.Cronus Kane"f"{Fore.RESET} ~ Registry Password Required - "f"{Fore.BLUE} HOGWARTS V - THE RESISTORS"f"{Fore.RESET}")
    print("16. "f"{Fore.BLUE}Dr.Xeno Zylius"f"{Fore.RESET} ~ Registry Password Required - "f"{Fore.BLUE} HOGWARTS V - THE RESISTORS"f"{Fore.RESET}")
    print("17. "f"{Fore.YELLOW}Athena"f"{Fore.RESET} ~ Registry Password Required - "f"{Fore.BLUE} HOGWARTS VI - THE RISE AND FALL OF OLYMPUS"f"{Fore.RESET}")
    print()
    
    while True:
        choice = input("Enter a number (1-17) to select your difficulty level: ").strip()
        if choice not in [str(i) for i in range(1, 2812)]:
            print(f"{Fore.RED}Invalid choice, please select again.{Style.RESET_ALL}")
            continue
        level = int(choice)  # Use the chosen number as level
        if choice in ['7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17']:
            while True:
                player_name = input("Enter your name: ").strip()
                print()
                if player_name:
                    break
                print(f"{Fore.RED}Name cannot be empty!{Style.RESET_ALL}")
        else:
            player_name = "Player"
            
        if choice == '1':
            return player_name, "Neville Longbottom", 65, [20,25,20,20,20,20,25,20,25,1], 10.0, level
        elif choice == '2':
            return player_name, "Draco Malfoy", 75, [15,15,20,15,18,15,20,15,20,5], 8.0, level
        elif choice == '3':
            return player_name, "Harry Potter", 80, [13,12,23,12,12,12,20,12,20,3], 5.0, level
        elif choice == '4':
            return player_name, "Godric Gryffindor", 90, [10,10,10,10,12,10,15,10,15,5], 2.5, level
        elif choice == '5':
            return player_name, "Morgana La Fey", 100, [10,9,9,9,10,9,15,9,12,7], 2.0, level
        elif choice == '6':
            return player_name, "Salazar Slytherin", 125, [8,8,8,10,8,8,12,8,10,7], 1.8, level
        elif choice == '7':
            message = f"Gellert Grindelwald, the Master of the Elder Wand, now stands before you. A battle of wits and power begins..."
            for char in message:
                print(char, end='', flush=True)
                time.sleep(0.075 if char.isalpha() else 0.4 if char == ',' else 1.2 if char == '.' else 0.15)
            print()
            time.sleep(3)
            return player_name, "Gellert Grindelwald", 140, [7,7,11,7,7,7,10,7,8,6], 1.5, level
        elif choice == '8':
            message = (f"With a gentle smile and eyes that have seen centuries, Albus Dumbledore appears before {player_name}.\n"
                       "His presence radiates wisdom and power, and you sense that this duel will test both heart and mind.\n"
                       "Prepare yourself for a battle where knowledge meets magic...")
            for char in message:
                print(char, end='', flush=True)
                time.sleep(0.075 if char.isalpha() else 0.4 if char == ',' else 1.2 if char == '.' else 0.15)
            print()
            time.sleep(3)
            return player_name, "Albus Dumbledore", 150, [6,6,12,6,6,6,8,6,6,3], 1.2, level
        elif choice == '9':
            message = f"As the Dark Lord turned, giving {player_name} the coldest death stare, {player_name} looked at him with steady eyes, knowing that one will die after this battle... Only one shall rule, Only one shall win..."
            for char in message:
                print(char, end='', flush=True)
                time.sleep(0.075 if char.isalpha() else 0.4 if char == ',' else 1.2 if char == '.' else 0.15)
            print()
            time.sleep(3)
            return player_name, "Lord Voldemort", 175, [5,5,5,6,8,5,6,5,6,4], 1.0, level
        elif choice == '10':
            message = f"Merlin Wyllt, the Greatest Sorcerer of all Time, The Owner Of Magic himself, challenges you. This duel will be written in history... The Ultimate Duel is about to begin..."
            for char in message:
                print(char, end='', flush=True)
                time.sleep(0.075 if char.isalpha() else 0.4 if char == ',' else 1.2 if char == '.' else 0.15)
            print()
            time.sleep(3)
            return player_name, "Merlin", 200, [4,4,7,4,4,4,5,4,5,3], 0.8, level
        elif choice == '11':
            message = f"{player_name} knows his spells well... He will now duel a wizard that is as good as him... Prepare yourself, {player_name}, it is about to get a whole lot challenging than usual..."
            for char in message:
                print(char, end='', flush=True)
                time.sleep(0.075 if char.isalpha() else 0.4 if char == ',' else 1.2 if char == '.' else 0.15)
            print()
            time.sleep(3)
            return player_name, f"{Fore.RED}HERO{Fore.RESET}", 250, [3,4,5,3,4,3,4,3,4,2], 0.8, level
        elif choice == '12':
            message = f"This is the hardest of all... Although {player_name} won their last duel confidently, {player_name} is now actually scared. To defeat the final boss, {player_name} must lock in..."
            for char in message:
                print(char, end='', flush=True)
                time.sleep(0.075 if char.isalpha() else 0.4 if char == ',' else 1.2 if char == '.' else 0.15)
            print()
            time.sleep(3)
            return player_name, f"{Fore.RED}PRO{Fore.RESET}", 275, [2,3,4,2,2,2,3,2,3,1], 0.8, level
        elif choice == '13':
            print()
            password1 = input("Enter the Registry Password: ")
            if password1 == '2811':
                print(f"{Fore.BLUE}HOGWARST IV - THE QUIESSCENCE UNCHARTED"f"{Fore.RESET}")
                message = f"The wizard under the hood smiled, sending a shiver through {player_name}'s spine... His name was thought to be Alfredo Casinido, The Wizard known to distory everything in his path..."
                for char in message:
                    print(char, end='', flush=True)
                    time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.05 if char == '.' else 0.12)
                print()
                time.sleep(3)
                return player_name, f"{Fore.RED}Alfredo Casinido{Fore.RESET}", 300, [2,3,3,2,2,2,3,2,3,1], 0.8, level
            else:
                print(f"{Fore.RED}Password Incorrect")
                sys.exit()
        elif choice == '14':
            print()
            password2 = input("Enter the Registry Password: ")
            if password2 == '0228':
                print(f"{Fore.BLUE}HOGWARTS IV - THE QUIESSCENCE UNCHARTED"f"{Fore.RESET}")
                message = f"Calypso Scar, a wizard whoose name nobody has ever heard, stood infront of {player_name}, smiling, thinking you as another weakling standing on his path..."
                for char in message:
                    print(char, end='', flush=True)
                    time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.05 if char == '.' else 0.12)
                print()
                time.sleep(3)
                return player_name, f"{Fore.RED}Calypso Scar{Fore.RESET}", 325, [2,3,2,2,3,2,3,2,3,1], 0.8, level
            else:
                print(f"{Fore.RED}Password Incorrect")
                sys.exit()
        elif choice == '15':
            print()
            password3 = input("Enter the Registry Password: ")
            if password3 == '9568':
                print(f"{Fore.BLUE}HOGWARTS V - THE RESISTORS "f"{Fore.RESET}")
                message = f"Everybody knows that this is about to get dangerous... Dr.Cronus Kane, an ordinary wizard living in a small hut, was no longer ordinary... Turns out that he knows magic to it's limit, and has never lost a duel in 289 years..."
                for char in message:
                    print(char, end='', flush=True)
                    time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.05 if char == '.' else 0.12)
                print()
                time.sleep(3)
                return player_name, f"{Fore.BLUE}Dr.Cronus Kane{Fore.RESET}", 350, [2,3,2,2,3,2,3,2,3,1], 0.8, level
            else:
                print(f"{Fore.RED}Password Incorrect")
                sys.exit()
        elif choice == '16':
            print()
            password4 = input("Enter the Registry Password: ")
            if password4 == '2417':
                print(f"{Fore.BLUE}HOGWARTS V - THE RESISTORS "f"{Fore.RESET}")
                message = f"Another one... Dr.Xeno Zylius is an retired scientist, famous for discovering Dark Magic, and also being one of the few to ignite a war... He is also known to be the brother of Zeus from Olympus..."
                for char in message:
                    print(char, end='', flush=True)
                    time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.05 if char == '.' else 0.12)
                print()
                time.sleep(3)
                return player_name, f"{Fore.BLUE}Dr.Xeno Zylius{Fore.RESET}", 375, [2,3,2,2,3,2,3,2,3,1], 0.8, level
            else:
                print(f"{Fore.RED}Password Incorrect")
                sys.exit()
        elif choice == '17':
            print()
            password5 = input("Enter the Registry Password: ")
            if password5 == '7685':
                print(f"{Fore.BLUE}HOGWARTS VI - THE RISE AND FALL OF OLYMPUS "f"{Fore.RESET}")
                message = f"Never in a million years would have {player_name} thought of fighting with a Greek God... And this may not be the last time {player_name} does this... Although she is immortal, Athena can still be deafeated..."
                for char in message:
                    print(char, end='', flush=True)
                    time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.05 if char == '.' else 0.12)
                print()
                time.sleep(3)
                return player_name, f"{Fore.YELLOW}Athena{Fore.RESET}", 400, [2,3,2,2,3,2,3,2,3,1], 0.8, level
            else:
                print(f"{Fore.RED}Password Incorrect")
                sys.exit()
                
def choose_medallions(boss_level, player_level):
    chosen = set()
    print(f"\n{Fore.CYAN}Would you like to choose medallions for special powers?{Style.RESET_ALL}")
    response = input("Enter 'y' for yes or 'n' for no: ").strip().lower()
    if response != 'y':
        return chosen
    
    # For HERO/PRO levels (level 11 or 12), show advanced medallions:
    if player_level in [17, 18]:
        print(f"{Fore.CYAN}9. Zeus's Lightning Bolt Medallion - 10% chance to get a lightning bolt (damage becomes 1-100) and gain 75 shield")
    elif player_level in [11, 12, 13, 14, 15, 16]:
        print(f"{Fore.CYAN}7. Vespera's Medallion 2.0 - {Style.RESET_ALL} 17.5% chance for a critical hit (damage becomes 0-100) and gain 50 shield")
        print(f"{Fore.CYAN}8. The Medallion of Creation - {Style.RESET_ALL} Cast a secret spell by entering '0' (usable 5 times, damage 0-75) and gain 75 shield")
    elif boss_level:
        print(f"{Fore.CYAN}5. Aimbot - {Style.RESET_ALL} Increase damage threshold by 20")
        print(f"{Fore.CYAN}6. Thunderbolt - {Style.RESET_ALL} Increase your damage by 1.5x")
        print(f"{Fore.CYAN}7. Vespera's Medallion - {Style.RESET_ALL} 10% chance for a critical hit (damage becomes 0-100) and gain 50 shield")
        print(f"{Fore.CYAN}8. The Medallion of Creation - {Style.RESET_ALL} Cast a secret spell by entering '0' (usable 3 times, damage 0-50) and gain 75 shield")
    else:
        print(f"{Fore.CYAN}1. Time Blade - {Style.RESET_ALL} No reaction time limit")
        print(f"{Fore.CYAN}2. Siphon - {Style.RESET_ALL} Gain 2.5 health on every non-defensive spell cast")
        print(f"{Fore.CYAN}3. Over Shield - {Style.RESET_ALL} Gain an extra 150 shield")
        print(f"{Fore.CYAN}4. Unstoppable - {Style.RESET_ALL} Use Avada Kedavra once without penalty and gain extra 50 shield")
        print(f"{Fore.CYAN}5. Aimbot - {Style.RESET_ALL} Increase damage threshold by 20")
        print(f"{Fore.CYAN}6. Thunderbolt - {Style.RESET_ALL} Increase your damage by 1.5x")
    
    med_input = input("Your choice(s): ").strip()
    if med_input:
        for med in med_input.split(','):
            med = med.strip()
            if player_level in [17, 18]:
                if med == '9':
                    chosen.add("zeus")
            elif player_level in [11, 12, 13, 14, 15, 16]:
                if med == '7':
                    chosen.add("vespera2")
                elif med == '8':
                    chosen.add("creation2")
            elif boss_level:
                if med == '5':
                    chosen.add("aimbot")
                elif med == '6':
                    chosen.add("thunderbolt")
                elif med == '7':
                    chosen.add("vespera")
                elif med == '8':
                    chosen.add("creation")
            else:
                if med == '1':
                    chosen.add("time_blade")
                elif med == '2':
                    chosen.add("siphon")
                elif med == '3':
                    chosen.add("over_shield")
                elif med == '4':
                    chosen.add("unstoppable")
                elif med == '5':
                    chosen.add("aimbot")
                elif med == '6':
                    chosen.add("thunderbolt")
    return chosen

# --- Game Setup ---
player_name, opponent_name, opponent_max_health, opponent_weights, time_limit, level = choose_difficulty()
player_max_health = 100.0
player_health = 100.0
opponent_health = opponent_max_health

# Determine boss level: if opponent_max_health >= 140 then it's a boss level.
boss_level = opponent_max_health >= 140

player_medallions = choose_medallions(boss_level, level)

# Set opponent's shield based on medallion choice.
if player_medallions:
    opponent_shield = 100.0
else:
    opponent_shield = 0.0

# --- Player Shield Setup ---
if not boss_level:
    player_shield = 150.0 if "over_shield" in player_medallions else 0.0
    if "unstoppable" in player_medallions:
        player_shield += 50.0
else:
    player_shield = 0.0
    
# Zeus's Medallion
if level in [17, 18] and ("zeus" in player_medallions):
    player_shield += 75.0

# Apply advanced medallion bonuses (applied only once during setup)
if boss_level and ("creation" in player_medallions):
    creation_uses = 3
    player_shield += 75.0
elif level in [11, 12, 13, 14, 15, 16] and ("creation2" in player_medallions):
    creation_uses = 5
    player_shield += 75.0
else:
    creation_uses = 0

if level in [11, 12, 13, 14, 15, 16] and ("vespera2" in player_medallions):
    player_shield += 50.0

# --- Flashbangs Setup ---
# You get 4 flashbangs (one for each key: w, a, s, d) available only once each.
flashbangs_available = {'w', 'a', 's', 'd'}
flashbang_damage_ranges = {
    'w': (10, 20),  # Fire Flashbang
    'a': (10, 20),  # Water Flashbang
    's': (15, 20),  # Cracker Flashbang
    'd': (15, 20)   # Pump Flashbang
}
flashbang_names = {
    'w': "Fire Flashbang",
    'a': "Water Flashbang",
    's': "Cracker Flashbang",
    'd': "Pump Flashbang"
}

# Boons
boon = random.randint(1,200)
if boon == 1:
    print(f"{Fore.GREEN}HEALTH BOON ACTIVATED!!"f"{Fore.RESET}")
    player_health += 50.0
elif boon == 2:
    print(f"{Fore.GREEN}DAMAGE BOON ACTIVATED!!"f"{Fore.RESET}")
    opponent_health -= 50.0
    
# Curse     
curse = random.randint(1, 200)
if curse == 1:
    print(f"{Fore.RED}HEALTH CURSE ACTIVATED!!"f"{Fore.RESET}")
    opponent_health += 50.0
elif curse == 2:
    print(f"{Fore.RED}DAMAGE CURSE ACTIVATED!!"f"{Fore.RESET}")
    player_health -= 50.0

# Initialize additional variables.
opponent_disarmed = False
skip_opponent_turn = False
unstoppable_used = False

player_defensive_count = 0
player_non_defensive_count = 0
player_spell_count = 0
ai_spell_count = 0

spell_effects = {
    "1": "Opponent is stunned and unconscious! (30% chance to skip next turn)",
    "2": "Opponent's wand flies away! (Disarmed for one round)",
    "3": "Opponent's teeth grow rapidly, making them unable to speak properly!",
    "4": "Opponent forgets their last spell! (Lower chance of success)",
    "5": "Opponent is completely paralyzed and unable to move! (Random chance to skip next turn)",
    "6": "Opponent is laughing uncontrollably and can't cast spells this round! (Random chance to skip next turn)",
    "7": "A magical shield blocks attacks!",
    "8": "Opponent's legs move uncontrollably! Their aim is thrown off!",
    "9": "You swiftly dodge the incoming spell!",
    "10": f"{Fore.RED}Unforgivable Curse! Immediate game over!{Style.RESET_ALL}"
}
# Note: Spell "0" is reserved for the secret spell from the Medallion of Creation.

# --- Game Loop ---
while player_health > 0 and opponent_health > 0:
    player_defended = False
    
    if skip_opponent_turn:
        print(f"{Fore.CYAN}Opponent is stunned and skips their turn!{Style.RESET_ALL}")
        skip_opponent_turn = False
        opponent_turn_taken = True
    else:
        opponent_turn_taken = False
        
    # Display Health and Shield
    display_health_bar("Your Health", player_health, player_max_health)
    if player_shield > 0:
        display_shield_bar("Your", player_shield, 150 if not boss_level else 50)
    display_health_bar(f"{opponent_name}'s Health", opponent_health, opponent_max_health)
    if opponent_shield > 0:
        display_shield_bar(f"{opponent_name}'s", opponent_shield, 100)
    
    # For boss levels with secret spell availability.
    if boss_level and creation_uses > 0:
        print(f"{Fore.MAGENTA}Secret Spell available! Enter '0' to cast the unknown spell ({creation_uses} uses left).{Style.RESET_ALL}")
    
    print(f"{Fore.YELLOW}Enter your spell (type 'info' for details, 'q' to quit, or use a flashbang: w, a, s, d):{Style.RESET_ALL}")
    
    start_time = time.time()
    player_move = input().strip().lower()
    reaction_time = time.time() - start_time

    if "time_blade" in player_medallions:
        reaction_time = 0

    # --- Flashbang Handling ---
    if player_move in flashbang_damage_ranges:
        if player_move not in flashbangs_available:
            print(f"{Fore.RED}Flashbang already used!{Style.RESET_ALL}")
            continue
        damage_range = flashbang_damage_ranges[player_move]
        damage = random.randint(damage_range[0], damage_range[1])
        print(f"{Fore.GREEN}You used {flashbang_names[player_move]} and dealt {damage} damage!{Style.RESET_ALL}")
        opponent_health, opponent_shield = apply_damage(opponent_health, opponent_shield, damage)
        flashbangs_available.remove(player_move)
        player_spell_count += 1  # count as a move
        continue

    # Secret spell handling.
    if player_move == '0':
        if boss_level and (("creation" in player_medallions) or ("creation2" in player_medallions)):
            if creation_uses > 0:
                creation_uses -= 1
                damage = random.randint(spell_damage_ranges["0"][0], spell_damage_ranges["0"][1])
                print(f"{Fore.GREEN}You cast the secret spell from The Medallion of Creation and deal {damage} damage!{Style.RESET_ALL}")
                opponent_health, opponent_shield = apply_damage(opponent_health, opponent_shield, damage)
            else:
                print(f"{Fore.RED}No secret spell uses left!{Style.RESET_ALL}")
            continue
        else:
            print(f"{Fore.RED}Secret spell not available!{Style.RESET_ALL}")
            continue
            
    # Zeus's Medallion
    bolt_uses == 0
    if level in [17, 18] and ("zeus" in player_medallions):
        bolt_spawn = random.randint(1,10)
        if bolt_spawn == 1:
            bolt_uses += 1
            print(f"{Fore.GREEN}YOU JUST GOT A ZEUS LIGHTNING BOLT!!"f"{Fore.RESET}")
            
    # Zeus's Lightning Bolt        
    if player_move == '11' and ("zeus" in player_medallions and bolt_uses >= 1):
        damage = random.randint(1, 150)
        print(f"{Fore.GREEN}THE ZEUS'S LIGHTNING BOLT IS NOW IN USE, DEALT {damage} DAMAGE!!{Fore.RESET}")
        opponent_health, opponent_shield = apply_damage(opponent_health, opponent_shield, damage)
        bolt_uses -= 1  # Decrement after use
    elif player_move == '11' and ("zeus" in player_medallions and bolt_uses <= 0):
        print(f"{Fore.RED}YOU DON'T HAVE ANY BOLTS LEFT!!{Fore.RESET}")

            
    # Secret Creator's Spell        
    if player_move == '999':
        damage = random.randint(200, 200)
        print(f"{Fore.MAGENTA}THE SECRET CREATOR'S SPELL IS IN USE NOW, DEALT {damage} DAMAGE!!{Fore.RESET}")
        opponent_health, opponent_shield = apply_damage(opponent_health, opponent_shield, damage)

    # Information command.
    if player_move == 'info':
        for key, value in spell_effects.items():
            print(f"{Fore.YELLOW}{key}. {value}{Style.RESET_ALL}")
        continue
    
    # Quit command.
    if player_move == 'q':
        print("Exiting game. Goodbye!")
        break
    
    # Reaction time check.
    if reaction_time > time_limit:
        print(f"{Fore.RED}You took too long to cast your spell! The opponent gains an advantage!{Style.RESET_ALL}")
        player_health, player_shield = apply_damage(player_health, player_shield, 5)
        continue

    if player_move not in spell_effects:
        print(f"{Fore.RED}Invalid input! Try again.{Style.RESET_ALL}")
        continue

    # Count player's spell usage.
    player_spell_count += 1
    if player_move in ['7', '9']:
        player_defensive_count += 1
    else:
        player_non_defensive_count += 1

    print(f"{Fore.BLUE}YOUR MOVE ---- {player_move} ---- {spell_effects[player_move]}{Style.RESET_ALL}")
    
    # Handle defensive spells.
    if player_move in ['7', '9']:
        player_defended = True
        print(f"{Fore.CYAN}Your defensive spell shields you from the incoming attack!{Style.RESET_ALL}")
    elif player_move == '1' and random.random() < 0.3:
        skip_opponent_turn = True
    elif player_move == '2':
        opponent_disarmed = True
    elif player_move == '10':
        # Unstoppable Medallion
        if "unstoppable" in player_medallions:
            if not unstoppable_used:
                unstoppable_used = True
                damage_range = spell_damage_ranges.get("10", (0, 0))
                damage = random.randint(damage_range[0], damage_range[1])
                print(f"{Fore.GREEN}You unleash Avada Kedavra with unstoppable power and deal {damage} damage!{Style.RESET_ALL}")
                opponent_health, opponent_shield = apply_damage(opponent_health, opponent_shield, damage)
            else:
                print(f"{Fore.RED}You used Avada Kedavra more than once and got arrested!{Style.RESET_ALL}")
                player_health = 0
                break
        else:
            print(f"{Fore.RED}The Ministry detects dark magic! You lose automatically!{Style.RESET_ALL}")
            player_health = 0
            break
            
    # Siphon medallion activation.
    if "siphon" in player_medallions and (not boss_level and player_move not in ['7','9']):
        player_health += 2.5
        print(f"{Fore.CYAN}Siphon medallion activated! You gain 2.5 health.{Style.RESET_ALL}")
    
    # Opponent's turn.
    if not opponent_turn_taken and not opponent_disarmed:
        ai_spell_count += 1
        opponent_move = str(random.choices(list(spell_effects.keys()), weights=opponent_weights)[0])
        print(f"{Fore.MAGENTA}OPPONENT'S MOVE ---- {opponent_move} ---- {spell_effects[opponent_move]}{Style.RESET_ALL}")
        
        # Threshold
        if player_defended:
            if opponent_move == '10' and random.random() < 0.005:
                print(f"{Fore.RED}AVADA KEDAVRA! Your shield fails for a moment!{Style.RESET_ALL}")
                player_health = 0
                break
            else:
                print(f"{Fore.GREEN}Your protection spell blocks the attack completely!{Style.RESET_ALL}")
        else:
            threshold = {
                "Neville Longbottom": 85,
                "Draco Malfoy": 80,
                "Harry Potter": 75,
                "Godric Gryffindor": 70,
                "Morgana La Fey": 65,
                "Salazar Slytherin": 60,
                "Gellert Grindelwald": 55,
                "Albus Dumbledore": 50,
                "Lord Voldemort": 45,
                "Merlin": 40,
                "HERO": 35,
                "PRO": 35,
                "Alfredo Casinido": 35,
                "Calypso Scar": 35,
                "Dr.Cronus Kane": 35,
                "Dr.Xeno Zylius": 35,
                "Athena": 35
            }.get(opponent_name, 50)
            if "aimbot" in player_medallions:
                threshold += 20
            if random.randint(1, 100) <= threshold:
                damage_range = spell_damage_ranges.get(player_move, (0, 0))
                damage = random.randint(damage_range[0], damage_range[1])
                if "thunderbolt" in player_medallions:
                    damage = int(damage * 1.5)
                if "vespera" in player_medallions:
                    if random.random() < 0.100:
                        damage = random.randint(0, 100)
                        print(f"{Fore.MAGENTA}Critical hit from Vespera's Medallion!{Style.RESET_ALL}")
                if "vespera2" in player_medallions:
                    if random.random() < 0.175:
                        damage = random.randint(0, 100)
                        print(f"{Fore.MAGENTA}Critical hit from Vespera's 2.0 Medallion!{Style.RESET_ALL}")
                print(f"{Fore.GREEN}Your spell hit {opponent_name} and dealt {damage} damage!{Style.RESET_ALL}")
                opponent_health, opponent_shield = apply_damage(opponent_health, opponent_shield, damage)
            else:
                damage_range = spell_damage_ranges.get(opponent_move, (0, 0))
                damage = random.randint(damage_range[0], damage_range[1])
                print(f"{Fore.RED}{opponent_name}'s spell hit you and dealt {damage} damage!{Style.RESET_ALL}")
                player_health, player_shield = apply_damage(player_health, player_shield, damage)
                
        if opponent_move in ['7', '9'] and random.random() < 0.005:
            extra_damage = random.randint(1, 5)
            print(f"{Fore.RED}Your spell ricocheted back, dealing an extra {extra_damage} damage to you!{Style.RESET_ALL}")
            player_health, player_shield = apply_damage(player_health, player_shield, extra_damage)
        elif opponent_move == '10' and random.random() < 0.005:
            print(f"{Fore.RED}AVADA KEDAVRA! You are struck down instantly!{Style.RESET_ALL}")
            player_health = 0
            break

    if opponent_disarmed:
        print(f"{Fore.CYAN}Opponent fumbles to retrieve their wand!{Style.RESET_ALL}")
        opponent_disarmed = False

if player_health <= 0:
    print(f"{Fore.RED}Game Over! {player_name}, you have been defeated by {opponent_name}.{Style.RESET_ALL}")
elif opponent_health <= 0:
    print(f"{Fore.GREEN}Congratulations {player_name}! You have defeated {opponent_name}!{Style.RESET_ALL}")

# Ranking Calculation
if player_defensive_count > 0:
    ratio_points = player_non_defensive_count / player_defensive_count
else:
    ratio_points = player_non_defensive_count
level_points = level * 10
total_spell_points = player_spell_count + ai_spell_count

if opponent_health <= 0:
    if not boss_level:
        placement_points = 10
    else:
        if level == 7:
            placement_points = 15
        elif level == 8:
            placement_points = 20
        elif level == 9:
            placement_points = 25
        elif level == 10:
            placement_points = 30
        elif level == 11:
            placement_points = 40
        elif level == 12:
            placement_points = 50
        elif level == 13:
            placement_points = 60
        elif level == 14:
            placement_points = 70
        elif level == 15:
            placement_points = 80
        elif level == 16:
            placement_points = 90
        elif level == 17:
            placement_points = 100
        else:
            placement_points = 0
else:
    placement_points = -10

total_points = ratio_points + level_points + total_spell_points + placement_points

if total_points >= 420:
    rank = f"{Fore.YELLOW}MYTHIC"
elif total_points >= 410:
    rank = f"{Fore.BLACK}LEGEND III"
elif total_points >= 400:
    rank = f"{Fore.BLACK}LEGEND II"
elif total_points >= 390:
    rank = f"{Fore.BLACK}LEGEND I"
elif total_points >= 380:
    rank = f"{Fore.BLUE}HACKER III"
elif total_points >= 370:
    rank = f"{Fore.BLUE}HACKER II"
elif total_points >= 360:
    rank = f"{Fore.BLUE}HACKER I"
elif total_points >= 350:
    rank = f"{Fore.BLUE}GRANDMASTER III"
elif total_points >= 340:
    rank = f"{Fore.BLUE}GRANDMASTER II"
elif total_points >= 330:
    rank = f"{Fore.BLUE}GRANDMASTER I"
elif total_points >= 320:
    rank = f"{Fore.BLUE}MASTER III"
elif total_points >= 310:
    rank = f"{Fore.BLUE}MASTER II"
elif total_points >= 300:
    rank = f"{Fore.RED}MASTER I"
elif total_points >= 290:
    rank = f"{Fore.RED}PRO"
elif total_points >= 280:
    rank = f"{Fore.RED}HERO"
elif total_points >= 270:
    rank = f"{Fore.RED}GOD"
elif total_points >= 260:
    rank = f"{Fore.RED}Demi-God"
elif total_points >= 250:
    rank = "FNCS World Cup Winner"
elif total_points >= 240:
    rank = "FNCS Global Championship Winner"
elif total_points >= 230:
    rank = "FNCS Regional Winner"
elif total_points >= 220:
    rank = "FNCS Qualified"
elif total_points >= 210:
    rank = "FNCS Division 1"
elif total_points >= 200:
    rank = "FNCS Division 2"
elif total_points >= 190:
    rank = "FNCS Division 3"
elif total_points >= 180:
    rank = f"{Fore.BLACK}Unreal"
elif total_points >= 170:
    rank = f"{Fore.RED}Champion"
elif total_points >= 160:
    rank = f"{Fore.MAGENTA}Elite"
elif total_points >= 150:
    rank = "Diamond III"
elif total_points >= 140:
    rank = "Diamond II"
elif total_points >= 130:
    rank = "Diamond I"
elif total_points >= 120:
    rank = "Platinum III"
elif total_points >= 110:
    rank = "Platinum II"
elif total_points >= 100:
    rank = "Platinum I"
elif total_points >= 90:
    rank = "Gold III"
elif total_points >= 80:
    rank = "Gold II"
elif total_points >= 70:
    rank = "Gold I"
elif total_points >= 60:
    rank = "Silver III"
elif total_points >= 50:
    rank = "Silver II"
elif total_points >= 40:
    rank = "Silver I"
elif total_points >= 30:
    rank = "Bronze III"
elif total_points >= 20:
    rank = "Bronze II"
elif total_points >= 10:
    rank = "Bronze I"
else:
    rank = "Unranked"
    
creator = 'This game was officially created by Archit Ranjan with help from ChatGPT'

print(f"\n{Fore.MAGENTA}Your rank points: {total_points:.2f}{Style.RESET_ALL}")
print(f"   (Ratio Points: {ratio_points:.2f} | Level Points: {level_points} | Spell Points: {player_spell_count + ai_spell_count} | Placement Points: {placement_points})")
print(f"{Fore.MAGENTA}Your Rank: {rank}{Style.RESET_ALL}")
if total_points >= 150 and total_points <= 179:
    print("Your Status: " f"{Fore.GREEN}Eligible for Boss Levels")
elif total_points >= 180 and total_points <= 199:
    print("Your Status: " f"{Fore.GREEN}Eligible for Demi-God Mode")
elif total_points >= 200 and total_points <= 219:
    print("Your Status: " f"{Fore.GREEN}Eligible for God Mode")
elif total_points >= 220 and total_points <= 259:
    print("Your Status: " f"{Fore.GREEN}Eligible for HERO Mode")
elif total_points >= 260 and total_points <= 289:
    print("Your Status: " f"{Fore.GREEN}Eligible for PRO Mode")
elif total_points >= 290 and total_points <= 319:
    print("Your Status: " f"{Fore.GREEN}Eligible for Alfredo Casinido level")
elif total_points >= 320 and total_points <= 349:
    print("Your Status: "f"{Fore.GREEN}Eligible for Calypso Scar level")
elif total_points >= 350 and total_points <= 379:
    print("Your Status: "f"{Fore.GREEN}Eligible for Dr.Cronus Kane level")
elif total_points >= 380: # and total_points <= 409:
    print("Your Status: "f"{Fore.GREEN}Eligible for Dr.Xeno Zylius level")
else:
    print("Your Status: " f"{Fore.RED}You are Not Eligible for any Advanced Mode{Fore.RESET}")
    
if total_points >= 220 and total_points <= 259:
    print()
    print("Eligibility: "f"{Fore.GREEN}{player_name}, you are eligible for the 'HERO' level")
    print("Enter '11' when you are choosing your difficulty level"f"{Fore.RESET}")
elif total_points >= 260 and total_points <= 289:
    print()
    print("Eligibility: "f"{Fore.GREEN}{player_name}, you are eligible for the 'PRO' level")
    print("Enter '12' when you are choosing your difficulty level"f"{Fore.RESET}")
elif total_points >= 290 and total_points <= 319:
    print()
    print("Eligibility: "f"{Fore.GREEN}{player_name}, you are eligible for the 'Alfredo Casinido' level")
    print("Enter '13' when you are choosing your difficulty level")
    print(f"{Fore.BLUE}THE REGISTRY PASSWORD FOR LEVEL 13 IS 2811"f"{Fore.RESET}")
elif total_points >= 320 and total_points <= 349:
    print()
    print("Eligibility: "f"{Fore.GREEN}{player_name}, you are eligible for the 'Calypso Scar' level")
    print("Enter '14' when you are choosing your difficulty level")
    print(f"{Fore.BLUE}THE REGISTRY PASSWORD FOR LEVEL 14 IS 0228"f"{Fore.RESET}")
elif total_points >= 350 and total_points <= 379:
    print()
    print("Eligibility: "f"{Fore.GREEN}{player_name}, you are eligible for the 'Dr.Cronus Kane' level")
    print("Enter '15' when you are choosing your difficulty level")
    print(f"{Fore.BLUE}THE REGISTRY PASSWORD FOR LEVEL 15 IS 9568"f"{Fore.RESET}")
elif total_points >= 380: #and total_points <= 409:
    print()
    print("Eligibility: "f"{Fore.GREEN}{player_name}, you are eligible for the 'Dr.Xeno Zylius' level")
    print("Enter '16' when you are choosing your difficulty level")
    print(f"{Fore.BLUE}THE REGISTRY PASSWORD FOR LEVEL 16 IS 2417"f"{Fore.RESET}")
else:
    print()
    print("Eligibility: "f"{Fore.RED}None"f"{Fore.RESET}")
    print("You cannot go to the 'HERO' and 'PRO' Rank")
    
print()    
if level == 12 and placement_points == 50:
    message = f"As fireworks cracked over the head, celebrating {player_name}'s Victory over the Best of Anonymous Wizard in the World, {player_name} knew that the long fought war isn't over... He knew there is another wizard, the best of the best, lurking in the shadows..."
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.05 if char == '.' else 0.12)
    print()
    print(f"{Fore.GREEN}Congratulations!! "f"{Fore.BLUE}{player_name}"f"{Fore.GREEN}, you have finally beaten the game!!"f"{Fore.RESET}")
elif level == 11 and placement_points == 40:
    message = f"As {player_name} slashed his wand through the air, the wizard under the hood knew that his downfall was inevitable..."
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.05 if char == '.' else 0.12)
elif level == 13 and placement_points == 60:
    message = f"Alfredo Casinido's lifeless body flew through the air... Cheering erupted from all sides, celebrating {player_name}'s victory over him, but the fight still isn't over..."
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.05 if char == '.' else 0.12)
elif level == 14 and placement_points == 70:
    message = f"BANG... Calypso Scar fell down with a thud, {player_name} slowly realized that he has deafeated Calypso Scar... A Victory that will last forever..."
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.00 if char == '.' else 0.12)
elif level == 15 and placement_points == 80:
    message = f"As the Dark Magic high above in the sky swirled, {player_name} knew that to get rid of it, he has to do more... Many unseen legends are yet to be seen..."
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.00 if char == '.' else 0.12)
elif level == 16 and placement_points == 90:
    message = f"The Dark Magic in the Sky died as Dr.Xeno Zylius fell to the ground... Everybody cheered but {player_name} had already sensed The Rise of Olympus beforehand..."
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.00 if char == '.' else 0.12)
elif level == 17 and placement_points == 100:
    message = f"As {player_name}'s wand slahed through the cold air, a huge cloud of smoke appeared... Through the smoke {player_name} could see Athena slowly vanishing, although she was immortal, Athena could still be hurt... {player_name} slowly bowed to pay respect to the God whom he just defeated"
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.060 if char.isalpha() else 0.30 if char == ',' else 0.95 if char == '.' else 0.11)
        
print()    
print(creator)
if level == 17 and placement_points == 100:
    print(f"{Fore.BLUE}HOGWARTS VI - THE RISE AND FALL OF OLYMPUS"f"{Fore.RESET}")
elif level == 15 or level == 16 and placement_points == 80 or placement_points == 90:
    print(f"{Fore.BLUE}HOGWARTS V - THE RESISTORS"f"{Fore.RESET}")
elif level == 13 or level == 14 and placement_points == 60 or placement_points == 70:
    print(f"{Fore.BLUE}HOGWARTS IV - THE QUIESSCENCE UNCHARTED"f"{Fore.RESET}")
else:
    print(f"{Fore.BLUE}HOGWARTS III - THE LEGENDS"f"{Fore.RESET}")

if level == 12 and placement_points == 50:
    uncharted = input()
    print()
    message = f"After a long and lengthy search, {player_name} has got it, an invitation, to become a memebr of The Residence of some of the Greatest Anonymous Wizards in the World, The Quiesscence... {player_name} is now witnessing the rise of Uncharted"
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.00 if char == '.' else 0.12)
    print()
    print(f"{Fore.GREEN}You are now allowed to play - "f"{Fore.BLUE}HOGWARTS IV - THE QUIESSCENCE UNCHARTED"f"{Fore.RESET}")
elif level == 14 and placement_points == 70:
    resistor = input()
    print()
    message = f"Dark Magic is now everywhere... Anyone could be an Ally or an Enemy... To overcome the Dark Magic, a group if formed, The Resistors... {player_name} is invited to become a member of this group, to fight against the Rebellions... {player_name} is now witnessing the rise of The Resistors"
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.00 if char == '.' else 0.12)
    print()
    print(f"{Fore.GREEN}You are now allowed to play - "f"{Fore.BLUE}HOGWARTS V - THE RESISTORS")
elif level == 16 and placement_points == 90:
    olympus = input()
    print()
    message = f"As the Dark Magic got over, {player_name} felt the presence of a new type of Magic arising, a godly type of Magic... As {player_name} felt the ground shaking, he knew that this is it... This is The Rise Of Olympus..."
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.065 if char.isalpha() else 0.35 if char == ',' else 1.00 if char == '.' else 0.12)    
        print()
        print(f"{Fore.GREEN}You are now allowed to play - "f"{Fore.BLUE}HOGWARTS VI - THE RISE AND FALL OF OLYMPUS")
