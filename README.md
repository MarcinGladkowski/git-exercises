### Git - użyteczna wiedza


```git log --follow <file>``` wyświetla rewizje podczas których był dodany ten plik
```git checkout -- .``` przełączenie wszystkich plików na aktualny commit - możliwość przełączenia pliku,katalogu  
```git checkout test``` przelaczenie na gałąz

```git fetch origin (-a) && git reset --hard origin/master``` :pobierz zmiany i pobierz ostatnią historię z serwera dla gałęzi zdalnej master

```git rebase -i HEAD~3```
- umożliwia np. złączenie 3 ostatnich _commitów_ 
- zmiana nazwy zlaczonych commitow 
- po wykonaniu komendy otwiera sie domyślny edytor
- commity, ktore chcemy złączyć

*złaczanie commitów*
```
pick <sha1> <commit message>
fixup <sha1> <commit message>
fixup <sha1> <commit message>
```
- zmieniamy slowo z pick na fixup commitow ktore chcemy złączyć

Zmiana nazwy ostatniego commita ex.
```
pick <sha1> <commit message> 
```
na 
```
reword <sha1> <commit message> 
```
Przenosi nas na kolejny ekran wpisania nowej nazwy commita

```git push --force (-f)```
- nie należy wykonywać dla ważnych gałęzi z których korzystają inni developerzy! 
- przydatne w momencie gdy np. używaliśmy _rebase_ dla naszej lokalnej gałęzi i przepisana historia lokalnej gałęzi nie zgadza się z historią gałęzi zdalnej. (bez przełącznika _force_ należy wtedy usunąć gałąź). 

- lepszym rozwiązaniem jednak będzie uzycie innej komendy...
```git push –force-with-lease```
- przy wypushowaniu zmian git sprawdza czy nikt zdalnie już czegoś nie dodał
- jeśli tak to nie pozwoli na wysłanie zmian
- jest jednak mały wyjątek (gdy wykonaliśmy ```git fetch``` i kopie branchy zdalnego i lokalnego się zgadzają a nie wykonaliśmy jeszcze ```git pull```. Rozwiązaniem tego jest stosowanie ```git pull```.
- lepszym rozwiązaniem jednak będzie uzycie innej komendy...
```git push –force-with-lease```
- przy wypushowaniu zmian git sprawdza czy nikt zdalnie już czegoś nie dodał
- jeśli tak to nie pozwoli na wysłanie zmian
- jest jednak mały wyjątek (gdy wykonaliśmy ```git fetch``` i kopie branchy zdalnego i lokalnego się zgadzają a nie wykonaliśmy jeszcze ```git pull```. Rozwiązaniem tego jest stosowanie ```git pull```.

```git commit --fixup=<sha1>```
- komenda umożliwia dodanie poprawki do commita z przeszlosci (bedzie mozliwosc latwego zlaczenia jej z bazowa rewizją)  
- scenariusz: zauważyliśmy blad w przeszłości, wykonujemy poprawkę ale jedynie dodajemy ją do ```stage``` poprzez ```git add np <file>```, a nastepnie wykonujemy komende z skrótem rewizji do której jest to poprawka.
- otrzymujemy następujący rezultat:
```
910fecd fixup! add next command
```
- w tym przypadku przyda nam się kolejna ciekawa komenda:
```git rebase --autosquash [-a] --interactive [-i]  np <sha1> <tag>```
- umozliwi nam ona ladnie wyprostowanie historii i zlaczenie commitow z message takimi jak ```fixup!``` i ```squash!```

```git bisect```: umożliwia znalezienie rewizji powodującej błąd
- należy się przełączyć na wersję działąjącą np ```git checkout <sha1>``` lub wskazać commit przy starcie bisect
- procedura:
1. Rozpoczecie bisectowania ```git bisect start```
2. Oznaczene obecnego commita jako uszkodzonego - jeśli tak jest (kod z błędem) ```git bisect bad```
3. Wskazanie commita z działającą funkcjonalnością ```git bisect good <sha1>```
4. Każde kolejne wywołanie należy sprawdzić i oznaczyć commit jako ```git commit good``` albo ```git commit bad``` aż do skończenia działania algorytmu.


### Przydatne linki
* Simple doc: https://rogerdudler.github.io/git-guide/index.pl.html  
* --fixup=Commit: https://devstyle.pl/2013/10/24/git-commit-fixup/  
* pull --rebase!: https://poznajgita.pl/rebase-podczas-synchronizacji-repozytorium-polecenie-git-pull-rebase/
* git hooks: https://bedev.pl/git-hooks/ i https://githooks.com/
* auto-squashing commits: https://thoughtbot.com/blog/autosquashing-git-commits  
* Git commit fixup and autosquash: https://blog.sebastian-daschner.com/entries/git-commit-fixup-autosquash
