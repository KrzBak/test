# -*- coding: utf-8 -*-
 
#%% zad 1 [2 pkt]
'''
Wygeneruj przy użyciu pętli lub innych narzędzi następujący wzór:
(1 pkt za każde narzędzie, max. 2 pkt.)
    
* * * * *
* * * *
* * *
* *
*
* *
* * *
* * * *
* * * * *

'''
z = 6
n = 5 
for i in range(z - 1, 0, -1):
    print("* " * i)
for i in range(1, n + 1):
    print("* " * i)


#%% zad 2 [2 pkt]
'''
Korzystając z modułu calendar wygeneruj:

  January -  01
 February -  02
    March -  03
    April -  04
      May -  05
     June -  06
     July -  07
   August -  08
September -  09
  October -  10
 November -  11
 December -  12
'''
import calendar
months = [
    'January', 'February', 'March', 'April',
    'May', 'June', 'July', 'August',
    'September', 'October', 'November', 'December'
]

for index, month in enumerate(months, start=1):
    month_number = str(index).zfill(2)
    print(month + ' - ' + month_number)


#%% zad 3 [4 pkt]
'''
Wygeneruj dwie listy pseudolosowych liczb całkowitych o długości 10 elementów 
z zakresu 1-29. Pierwsza lista to wysokość walca, druga to jego średnica. 
Oblicz:
(A) objętość wszystkich 10 walców 
(B) ich objętość średnią. 
Sformatowany jak najładniej wynik podaj z dokładnością do 2 miejsc dziesiętnych.
'''
import random
import math

h = [random.randint(1, 29) for _ in range(10)]
d = [random.randint(1, 29) for _ in range(10)]

objętości = []
for i in range(10):
    radius = d[i] / 2
    objętość = math.pi * radius**2 * h[i]
    objętości.append(objętość)

total_objętość = sum(objętości)
average_objętość = total_objętość / 10
print("Wysokości walców:", h)
print("Średnice walców:", d)
print("Suma objętości wszystkich walców:", round(total_objętość, 2))
print("Średnia objętość walca:", round(average_objętość, 2))

#%% zad 4 [3 pkt]
'''
Napisz funkcję, która oblicza ilość spółgosek i samogłosek w dowolnym tekście.
samogłoski: aeiouóyąęAEIOUÓYĄĘ
spółgłoski: bcćdfghjklłmnńprsśtwzźżBCĆDFGHJKLŁMNŃPRSŚTWZŹŻ
'''

def licz_w_tekscie(text):
    samogłoski = set('aeiouóyąęAEIOUÓYĄĘ')
    spółgłoski = set('bcćdfghjklłmnńprsśtwzźżBCĆDFGHJKLŁMNŃPRSŚTWZŹŻ')
    samogłoski_count = 0
    spółgłoski_count = 0

    for char in text:
        if char in samogłoski:
            samogłoski_count += 1
        elif char in spółgłoski:
            spółgłoski_count += 1
    return samogłoski_count, spółgłoski_count

text = "Przykładowy tekst do analizy"
samogłoski_count, spółgłoski_count = licz_w_tekscie(text)
print("Ilość samogłosek:", samogłoski_count)
print("Ilość spółgłosek:", spółgłoski_count)

#%% zad 5 [1 + 0,5 + 0,5 + 1 + 3 + 3 = 9 pkt]
'''
Wczytaj z załączonego pliku Epilog "Pana Tadeusza" autorstwa Adama Mickiewicza. 
5_1. Znajdź w EpiloguPT wszystkie wyrazy zaczynające się Wielką Literą. 
    Podaj ich ilość.

5_2. Wstaw do listy wygenerowanej w pkt. 5_1 swoje imię i nazwisko (osobno).

5_3. Uporządkuj w liście wygenerowanej w pkt. 5_2 wyrazy alfabetycznie.

5_4. Przekształć listę wygenerowaneą w pkt 5_3 w łańcuch słów oddzielonych znakiem ' & '.  dodałem po kol.

5_5. Dokonaj przekształceń łańcucha wygenerowanego w pkt 5_4 (jeśli będą potrzebne) 
    i wydrukuj wykaz słów do pliku tekstowego tak, aby wszystkie słowa 
    były wymienione osobno w kolejnych wierszach bez żadnych dodatkowych znaków. 
    Przykład:
Chrobrego
Europy

5_6. Znajdź w EpiloguPT wszystkie wyrazy zaczynające się Wielką Literą, 
     które nie są zarazem początkiem wiersza. Podaj ich ilość.
'''
# 5_1. Znajdź w EpiloguPT wszystkie wyrazy zaczynające się Wielką Literą. Podaj ich ilość.
with open(r"C:\Users\user\Desktop\Zal_Python\EpilogPT.txt", "r", encoding="utf-8") as file:
    epilog_text = file.read()
wielkie = [word for word in epilog_text.split() 
           if word[0].isupper()]
print("Liczba wyrazów zaczynających się wielką literą:", len(wielkie))

# 5_2. Wstaw do listy wygenerowanej w pkt. 5_1 swoje imię i nazwisko (osobno).
imie = ["Krzysztof", "Bąkowski"]
wielkie.extend(imie)

# 5_3. Uporządkuj w liście wygenerowanej w pkt. 5_2 wyrazy alfabetycznie.
wielkie.sort()

# 5_4. Przekształć listę wygenerowaneą w pkt 5_3 w łańcuch słów oddzielonych znakiem ' & '
words_joined_with_ampersand = ' & '.join(wielkie)

# 5_5. Dokonaj przekształceń łańcucha wygenerowanego w pkt 5_4
#      i wydrukuj wykaz słów do pliku tekstowego
with open("words_list.txt", "w", encoding="utf-8") as file:
    file.write(words_joined_with_ampersand)

# 5_6. Znajdź w EpiloguPT wszystkie wyrazy zaczynające się Wielką Literą,
#      które nie są zarazem początkiem wiersza. Podaj ich ilość.
lines = epilog_text.split("\n")
non_starting_upper_words = []
for line in lines:
    words = line.split()
    for i, word in enumerate(words):
        if word[0].isupper() and i != 0:
            non_starting_upper_words.append(word)
print("Liczba wyrazów zaczynających się wielką literą, które nie są początkiem wiersza:", len(non_starting_upper_words))

#%%
def zgadywanka():
    liczba = random.randint(1, 100)  
    proba = 0

    while True:
        proba += 1
        odgadnij = int(input("Podaj liczbe: "))
        if odgadnij < liczba:
            print("Za mało")
        elif odgadnij > liczba:
            print("Za dużo")
        else:
            print(f"Odgadłeś liczbę {liczba} w {proba} próbach.")
            break
if __name__ == "__main__":
    zgadywanka()

