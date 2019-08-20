### Git - użyteczna wiedza
```git fetch origin (-a) && git reset --hard origin/master``` :pobierz zmiany i pobierz ostatnią historię z serwera dla gałęzi zdalnej master

```git rebase -i HEAD~3```
- umożliwia np. złączenie 3 ostatnich _commitów_ 
- zmiana nazwy zlaczonych commitow 
- po wykonaniu komendy otwiera sie domyślny edytor
- commity, ktore chcemy złączyć
```
pick <sha1> <commit message>
fixup <sha1> <commit message>
fixup <sha1> <commit message>
```
- zmieniamy slowo z pick na fixup commitow ktore chcemy złączyć

```git push --force (-f)```
- nie należy wykonywać dla ważnych gałęzi z których korzystają inni developerzy! 
- przydatne w momencie gdy np. używaliśmy _rebase_ dla naszej lokalnej gałęzi i przepisana historia lokalnej gałęzi nie zgadza się z historią gałęzi zdalnej. (bez przełącznika _force_ należy wtedy usunąć gałąź). 


### Przydatne linki
https://rogerdudler.github.io/git-guide/index.pl.html
