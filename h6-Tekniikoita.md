# H6 - Benchmark

06.05. klo 19.00
## Tiivistelmä

### [Windows Package Manager](https://docs.saltproject.io/en/latest/topics/windows/windows-package-manager.html)

- Salt tarjoaa Windowsille paketinhallintatyökalun
- Package definition -tiedosto määrittää mm. pakettien versiot ja nimet
- Kloonataan repositorio salt-winrepo-ng
- Luodaan tietokanta
- Ladataan paketteja komennolla ```pkg.install```
- Komennolla ```pkg.list_available``` voidaan tarkastella ladattavissa olevien pakettien versioita
- Paketteja voidaan poistaa komennolla ```pkg.remove```
- 
