## PRÀCTICA: AMPLIANT EL COMPTADOR

#### 1. ANÀLISI DE L'ESTRUCTURA DEL PROJECTE.

#### Comentari sobre el projecte:

Aquest projecte és una ampliació del projecte base Comptador, al qual se li ha afegit dos nous botons amb dues diferents funcionalitats, una per a restar i l'altra per a restablir el comptador, a més se li ha corregit un problema el qual provocava que cada vegada que es girara la pantalla el comptador es restablira.

#### Anàlisi de l'estructura:

Els elements mes importants d'aquest projecte son els següents: 

* Els scripts Gradle de construcció del projecte, en format Kotlin DSL (build.gradle.kts), tant el general, situat en l’arrel, amb informació comuna a tots els mòduls, com el propi del mòdul de l’aplicació (app/build.gradle.kts).

* Dins de la carpeta del mòdul (app) trobem la carpeta src, que conté els el codi font de l’aplicació (app/src/main).

* La carpeta app/src/res, que contindrà els recursos de l’aplicació (imatges, dissenys, cadenes de text, etc). Aquesta carpeta conté bastants subcarpetas, per als diferents tipus de recursos.

* El fitxer descriptor de l’aplicació: app/AndroidManifest.xml, amb informació associada a aquesta. Es tracta d’un dels fitxers més importants del nostre projecte, ja que defineix aspectes com el nom de l’aplicació i el paquet, la icona, i els seus diferents components.

#### 2. ANÀLISI DEL CICLE DE VIDA I EL PROBLEMA DE LA PÈRDUA D'ESTAT.

En aquest cicle de vida ens trobem amb un problema de perduda d'estat, el qual ens restablirà la variable comptador **cada vegada que es fa una rotació de pantalla** per a això he buscat una solució per a no perdre el valor de comptador ja que cada vegada que es fa una rotació es torna a iniciar l'aplicació.

Després d'estar investigant he trobat dos possibles mètodes callback que serviran per al següent:

- **onSaveInstanceState()**: Guardara el valor recollit entre el onStop() i onDestroy().

- **onRestoreInstanceState**(): Recupera el valor del comptador i el posarà entre onStart() i onResum().

#### 3. SOLUCIÓ A LA PÈRDUA D'ESTAT.

Per a solucionar aquest problema he implementat els dos mètodes en el programa principal en el fitxer MainActivity de la següent forma:


Una vegada implementats els mètodes m'ha sorgit un altre problema, quan la pantalla fa una rotació continua apareixent el comptador a 0 però quan interactuem amb el comptador incrementa el valor guardat abans de la rotació, és a dir, que el programa esta guardant aquest valor quan es fa la rotació gràcies a les funcions implementades anteriorment de tal forma que només queda afegir-li que mostre el vertader valor de comptador quan es fa la rotació per a això he implementat el següent:

![Alt text](<PMDM (7).png>)

#### 4. AMPLIANT LA FUNCIONALITAT.

Per a afegir els nous botons he accedit al fitxer xml que es troba en la carpeta layout, per a afegir els nous botons s'accedit a l'apartat design per a crear els botons i poder donar-los el disseny que jo volguera amb mes facilitat.

![Alt text](<PMDM (1).png>)

Una vegada creats els botons cal donar-li a cadascun una nova funcionalitat:

**BOTÓ RESTA**:

Aquest botó va a decrementar el valor de comptador:

![Alt text](<PMDM (2) RES.png>)

*(PROBLEMA: Al decrementar el valor arriba un punt en què el valor és negatiu per a això he realitzat una condició la qual resol aquest problema).*

**BOTÓ RESET**:

Aquest botó iguala el valor de comptador a 0 per a així tindre de nou el comptador com al principi:

![Alt text](<PMDM (2) RESTORE.png>)

#### 5. CANVIS PER IMPLEMENTAR EL VIEW BINDING.

1.Activar el ViewBinding a les buildFeatures de l’script Gradle del mòdul.

![Alt text](<PMDM (3).png>)

2.Sincronitzar el projecte amb aquest script, per a que genere les classes de vinculació.

![Alt text](<PMDM (4).png>)

3.Importar la classe de vinculació en el fitxer de la classe on l’anem a utilitzar.

![Alt text](<PMDM (5).png>)

4.Declarar l’objecte (binding) que accedirà a aquesta classe (generalment com a lateinit) i definir-lo mitjançant l’unflat de la vista.

![Alt text](<PMDM (6).png>)

5.Modificar el SetContentView per afegir-lo l’arrel del binding (binding.root).

6.Accedir als elements de la interfície a través d’aquest objecte de vinculació.

