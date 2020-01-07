# Jenkins használata

## Jenkins telepítése saját gépre Windows esetén

* `jenkins.war` letöltése a https://jenkins.io/download/ oldalról
* `java -jar jenkins.war` (csak Java 8-cal), a `%HOME%\.jenkins` fájlba dolgozik, ami nálam a `C:\Users\jtechlog\.jenkins`
* http://localhost:8080 oldalon elérhető
* jelszó bemásolása a konzolról
* Install plugins
* Felhasználó létrehozás
* Next, Start

# Pipeline és szkriptek megadása a projekten belül

* `Jenkinsfile` és `deploy.bat`, Linux esetén `deploy.sh` létrehozása

(Jenkinsben van egy Pipeline syntax gomb, ott megtalálható a dokumentációja, sőt részleteket is tud generálni.)

A példa egy három stage-ből álló pipeline-t definiál:

* `package`: Gitről letölti az alkalmazást, majd meghívja a `mvnw -DskipTests clean package` parancsot (unit teszteket sem futtat, valójában kéne)
* `test`: `mvnw test` parancsot futtatja (unit tesztek futtatása), valójában az integrációs teszteknek kéne itt futtatnia
* `deploy`: meghívja a különálló, így külön tesztelhető `deploy.sh` szkriptet, ez telepíthet, vagy csomagolhat, fájlokat másolhat, bármilyen op. rendszerbeli
  parancsot használhat

A példa [Jenkinsfile](Jenkinsfile) azt az esetet tartalmazza, amikor Maven wrapper van a projekthez. A http://start.spring.io
alapból generál a Spring Boot projekthez. E nélkül a Mavent még konfigurálni kell.

## Job létrehozása

* Új Item
* Projektnév megadása `jenkins-demo`
* Pipeline
* Pipeline/Definition Pipeline script from SCM
* Git
* Repository URL kitöltése, pl. `https://github.com/vicziani/jenkins-demo`
