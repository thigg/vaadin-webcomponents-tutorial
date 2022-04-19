# Webcomponents in Vaadin


## Überblick
Webcomponents sind wiederverwendbare Elemente einer Website (customElements).
Diese werden über eine Javascript oder Typescript API definiert und können dann als html tag verwendet werden.

Um eine Komponente zu erzeugen die die Zeit lokal im Browser umrechnet sähe das im Hintergrund dann so aus:
 1. Registriere die Komponente mit Javascript: `customElements.define('local-time', LocaleTimeImpl);`
 2. Benutze sie in HTML mit: `<local-time value="21908391"/>`

Webcomponents haben in Vaadin zur Zeit im wesentlichen Zwei Anwendungsbereiche:
 1. Layouts in HTML abbilden
 2. Third-Party Webcomponents einbinden

## Setup
Ihr braucht dafür ein kleines Vaadin-Projekt in dem ihr das ganze implementieren könnt.
Das Projekt könnt ihr mit dem folgenden Befehl erzeugen und dann in eurer IDE öffnen:

```
mvn -B archetype:generate \
-DarchetypeGroupId=com.vaadin \
-DarchetypeArtifactId=vaadin-archetype-application \
-DarchetypeVersion=14.8.8 \
-DgroupId=org.example \
-DartifactId=my-webapp \
-Dversion=1.0-SNAPSHOT
```

### Polymer/Lit
Grundsätzlich braucht man keine Bibliothek um Webcomponents zu erzeugen, Vaadin verwendet dafür aus Gründen
aber Polymer oder Lit. Die beiden Bibliotheken unterscheiden sich, vor allem in der
Art wie Daten gebunden werden. Für neue Webcomponents sollte man Lit verwenden, da polymer ab Vaadin 18 deprecated ist.

### Typescript
Typescript ist ein Javascript Dialekt mit statischer Typisierung der in Javascript übersetzt wird.
Es ist in vaadin grundsätzlich möglich die Webcomponents in Typescript anzulegen.


### Dokumentation
Die Einführung von vaadin zu webcomponents gibt es hier:
 - https://vaadin.com/docs/v14/flow/templates/basic

## Übungen

### Layouts mit Webcomponents:

Erzeuge ein Formular mit einem Textfeld einem Span und einem Button in HTML.
Bei Klick auf den Button soll die Eingabe von dem Textfeld in den Span übertragen werden.
Die einzelnen Elemente sollen an Member Variablen in der dazugehörigen Java Klasse referenziert werden.
Das übertragen des Textes soll Serverseitig geschehen.

[Doku](https://vaadin.com/docs/v14/flow/templates/basic)

### Styling mit Webcomponents
Style den Text im Span direkt in der Webcomponent Fett. Verwende hierfür ein `style` element direkt in der Komponente.

### Adaptieren einer existierenden Webcomponent.
Benutzt ein [paper-badge](https://www.webcomponents.org/element/@polymer/paper-badge) in eurer Anwendung.

Hierfür müsst ihr eine Java-Klasse `Component` extenden lassen und entsprechend mit NpmPackage annotieren.
Aus diesem Package könnt ihr dann ein javascript file wählen, dass ihr mit `@JSModule` an die Klasse annotieren könnt.

Das Badge wird standardmäßig oben rechts angezeigt. Um es an eine eurer Komponenten zu kleben, erweitert den Konstruktor
um eine Komponente als Parameter, die beklebt werden soll. Dann könnt ihr mit `getElement().setAttribute("for", targetId);`
die Komponente bekleben.

[Doku](https://vaadin.com/docs/latest/flow/components/web-components/#integrating-a-js-module-into-vaadin)

### Bonus: Daten in der Komponente umwandeln

Vaadin empfiehlt, anders als bei Polymer, bei Lit nicht mehr Daten in den Webcomponents umzuwandeln.
Es ist aber [möglich](https://gist.github.com/thigg/df438419d32113b9318be1026820c6fc)
