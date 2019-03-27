# Instrukcja

## Przedstawienie postaci
Mamy sobie dwóch developerów: 
 * dev0
 * dev1

Developerzy Ci postanowili nauczyc się w końcu gita w konsoli, no bo czemu nie. No więc zaczynajmy

### Dev0
Dev0 ma za zadanie stworzyc u siebie lokalne repozytorium, wrzucic do niego plik o nazwie file.txt z wiadomoscią powitalną oraz zacommitowac zmiany.
```
git init
git add file.txt
git commit -m "init"
```

### Dev1
Dev1 ma za adanie stworzyc w tym samym momencie Repozytorium na bitbucket, następnie zaprosic do niego swojego kolegę, Dev0, z uprawnieniami do wrzucania zmian do repozytorium.

### Dev0
Dev ten ma za zadanie ustawic origin swojego lokalnego repozytorium na zdalne repozytorium założone przez Dev1. Następnie musi on zsynchronizowac zdalne repozytorium ze swoim lokalnym.
```
git remote add origin <link>
git push -u origin master
```

### Dev1
Tym razem Dev ten klonuje swoje zdalne repozytorium i sam dodaje w nim plik o nazwie file2.txt z dowolną wiadomoscią. Po zacommitowaniu pliku pushujemy go na zdalne repozytorium.
```
git clone <link>
git add file2.txt
git commit -m "Added file2.txt"
git push
```

### Dev0
Dodajemy nowy plik - file3.txt z dowolną wiadomoscią. Commitujemy zmiany i próbujemy pushowac. Wyskoczy nam wiadomosc, że mamy niepobrane zmiany na zdalnym repozytorium. Pobieramy zmiany (zalecaną metodą) a następnie robimy push do zdalnego repozytorium.
```
git add file3.txt
git commit -m "Added file3.txt"
git push
git pull --rebase
git push
```

### Dev1
Tworzymy z obecnie posiadanych zmian brancha o nazwie feature 1. W branchu tym zmieniamy wiadomosc powitalną w pliku file.txt. Następnie, na gałęzi master, zaciągamy zmiany ze zdalnego repozytorium, po czym robimy rebase naszego brancha feature1 na branchu master.
```
git checkout -b feature1
git add file.txt
git commit -m "Edited file"
git checkout master
git pull --rebase
git checkout feature1
git rebase master
```

### Dev0
Tworzymy z naszego aktualnego mastera brancha feature2. Również zmieniamy plik file.txt (inaczej niż nasz kolega dev). Następnie przełączamy się na naszego brancha master i robimy merge naszego nowego brancha feature2 do mastera. Pushujemy na zdalne repozytorium.
```
git checkout -b feature2
git add file.txt 
git commit -m "Also edited file"
git checkout master
git merge --commit feature2
git push 
```

### Dev1
Zaczynamy zabawę. W tym momencie nasz kolega Dev0 zrobił merge ze zmianami w tym samym pliku co my. W momencie mergeowania brancha feature1 do mastera będziemy musieli rozwiązac konflikt. Podczas rozwiązywania pozostawiamy obie wiadomosci.
```
git checkout master
git pull --rebase
git merge --commit feature1
git add .
git merge --continue
git push
```