Node-Sass
Unterstützte Node.js-Versionen variieren je nach Release. Weitere Informationen finden Sie auf der Release- Seite . Unten finden Sie eine Kurzanleitung für minimale Unterstützung:
NodeJS	Minimale Node-Sass-Version	Knotenmodul
Knoten 14	4.14+	83
Knoten 13	4.13+	79
Knoten 12	4.12+	72
Knoten 11	4.10+	67
Knoten 10	4,9+	64
Knoten 8	4.5.3+	57
Sass-Logo	
Build-Status Build-Status npm Version Abhängigkeitsstatus devDependency Status Abdeckungsstatus Inline-Dokumente Mach mit bei Slack

Node-sass ist eine Bibliothek, die Node.js für LibSass , die C-Version des beliebten Stylesheet-Präprozessors Sass , bindet .

Sie können .scss-Dateien nativ mit unglaublicher Geschwindigkeit und automatisch über eine Connect-Middleware zu CSS kompilieren.

Finden Sie es auf npm: https://www.npmjs.com/package/node-sass

Folgen Sie @nodesass auf Twitter, um Updates zu erhalten: https://twitter.com/nodesass

Installieren
npm install node-sass
Einige Benutzer haben Probleme bei der Installation unter Ubuntu gemeldet, weil nodesie für ein anderes Paket registriert wurden. Befolgen Sie die offiziellen NodeJS-Dokumente , um NodeJS so zu installieren, dass es #!/usr/bin/env nodekorrekt aufgelöst wird.

Das Kompilieren auf Windows-Computern erfordert die Node-Gyp-Voraussetzungen .

Sehen Sie den folgenden Fehler? Lesen Sie unsere Anleitung zur Fehlerbehebung . **

SyntaxError: Use of const in strict mode.
Haben Sie Installationsprobleme? Lesen Sie unsere Anleitung zur Fehlerbehebung .

Installieren Sie vom Spiegel in China
npm install -g mirror-config-china --registry = http: //registry.npm.taobao.org
npm install node-sass
Verwendung
var  sass  =  require ( 'node-sass' ) ; 
Sass . render ( { 
  Datei : scss_filename , 
  [ ,  Optionen . . ] 
} ,  Funktion ( err ,  Ergebnis )  {  /*...*/  } ) ; 
// ODER 
var  result  =  sass . renderSync ( { 
  Daten : scss_content 
  [ ,  Optionen . .] 
} ) ;
Optionen
Datei
Art: String
Standard: null
Spezial : fileoder datamuss angegeben werden

Pfad zu einer Datei, die LibSass kompilieren soll.

Daten
Art: String
Standard: null
Spezial : fileoder datamuss angegeben werden

Eine Zeichenfolge, die zum Kompilieren an LibSass übergeben werden soll. Es wird empfohlen, dass Sie includePathsin Verbindung damit verwenden, damit LibSass bei Verwendung der @importDirektive Dateien finden kann .

Importeur (> = v2.0.0) - experimentell
Dies ist eine experimentelle LibSass-Funktion. Mit Vorsicht verwenden.

Typ: Function | Function[]Unterschriftfunction(url, prev, done)
Standard: undefined
Funktionsparameter und Informationen:

url (String)- Der Pfad beim Import wie er ist , auf den LibSass gestoßen ist
prev (String) - der zuvor aufgelöste Pfad
done (Function) - Eine Rückruffunktion, die bei asynchronem Abschluss aufgerufen werden soll, verwendet ein Objektliteral, das enthält
file (String)- ein alternativer Pfad für LibSass zur Verwendung von OR
contents (String) - die importierten Inhalte (z. B. aus dem Speicher oder dem Dateisystem gelesen)
Behandelt, wenn LibSass auf die @importDirektive stößt . Ein benutzerdefinierter Importer ermöglicht die synchrone und asynchrone Erweiterung der LibSass- Engine. In beiden Fällen besteht das Ziel darin, entweder ein Objektliteral returnaufzurufen oder mit diesem aufzurufen done(). Abhängig vom Wert des Objektliteral wird eines von zwei Dingen passieren.

Bei Rückkehr oder Aufruf done()mit { file: "String" }wird der neue Dateipfad für das angenommen @import. Es wird empfohlen, den Wert previn Fällen zu berücksichtigen, in denen eine relative Pfadauflösung erforderlich sein kann.

Bei der Rückgabe oder beim Aufrufen done()mit { contents: "String" }wird der Zeichenfolgenwert so verwendet, als ob die Datei über eine externe Quelle eingelesen worden wäre.

Ab Version 3.0.0:

thisbezieht sich auf einen Kontextbereich für den sofortigen Ablauf von sass.renderodersass.renderSync

Importeure können Fehler zurückgeben, und LibSass gibt diesen Fehler als Antwort aus. Zum Beispiel:

erledigt ( neuer  Fehler ( 'existiert nicht!' ) ) ; 
// oder synchron zurückgeben 
return  new  Error ( 'hier nichts zu tun' ) ;
Importer kann ein Array von Funktionen sein, die von LibSass in der Reihenfolge ihres Auftretens im Array aufgerufen werden. Dies hilft dem Benutzer, einen speziellen Importer für eine bestimmte Art von Pfad (Dateisystem, http) anzugeben. Wenn ein Importeur einen bestimmten Pfad nicht verarbeiten möchte, sollte er zurückkehren null. Siehe Abschnitt Funktionen für weitere Details über Sass - Typen.

Funktionen (> = v3.0.0) - experimentell
Dies ist eine experimentelle LibSass-Funktion. Mit Vorsicht verwenden.

functionsist Objecteine Sammlung von benutzerdefinierten Funktionen, die von den zu kompilierenden sass-Dateien aufgerufen werden können. Sie können null oder mehr Eingabeparameter annehmen und müssen einen Wert entweder synchron ( return ...;) oder asynchron ( done();) zurückgeben. Diese Parameter sind Instanzen eines der im require('node-sass').typesHash enthaltenen Konstruktoren . Der Rückgabewert muss ebenfalls von einem dieser Typen sein. Siehe die Liste der verfügbaren Typen unten:

types.Number (Wert [, Einheit = ""])
getValue()/ setValue(value): erhält / setzt den numerischen Teil der Zahl
getUnit()/ setUnit(unit): holt / setzt den Einheitenteil der Zahl
types.String (Wert)
getValue()/ setValue(value): holt / setzt den eingeschlossenen String
types.Color (r, g, b [, a = 1,0]) oder types.Color (argb)
getR()/ setR(value): rote Komponente (Ganzzahl von 0bis 255)
getG()/ setG(value): grüne Komponente (Ganzzahl von 0bis 255)
getB()/ setB(value): blaue Komponente (Ganzzahl von 0bis 255)
getA()/ setA(value): Alpha-Komponente (Nummer von 0bis 1.0)
Beispiel:

var  Color  =  require ( 'node-sass' ) . Typen . Farbe , 
  c1  =  neue  Farbe ( 255 ,  0 ,  0 ) , 
  c2  =  neue  Farbe ( 0xff0088cc ) ;
types.Boolean (Wert)
getValue() : Erhält den beiliegenden Booleschen Wert
types.Boolean.TRUE: Singleton-Instanz types.Booleandavon hält "wahr"
types.Boolean.FALSE: Singleton-Instanz types.Booleandavon hält "false"
types.List (Länge [, commaSeparator = true])
getValue(index)/ setValue(index, value): valuemuss selbst eine Instanz eines der Konstruktoren in sein sass.types.
getSeparator()/ setSeparator(isComma): ob Kommas als Trennzeichen verwendet werden sollen
getLength()
types.Map (Länge)
getKey(index) /. setKey(index, value)
getValue(index) /. setValue(index, value)
getLength()
types.Null ()
types.Null.NULL: Singleton-Instanz von types.Null.
Beispiel
Sass . renderSync ( { 
  Daten : '# {Überschriften (2,5)} {Farbe: # 08c;}' , 
  Funktionen : { 
    'Überschriften ($ von: 0, $ bis: 6)' : Funktion ( von ,  bis )  { 
      var  i ,  f  =  von . getValue ( ) ,  t  =  bis . getValue ( ) , 
          list  =  new  sass . types . List ( t  - f  +  1 ) ;

      für  ( i  =  f ;  i <= t ;  i ++ )  { 
        Liste . setValue ( i  -  f ,  neue  sass . Typen . String ( 'h'  +  i ) ) ; 
      }}

      Rück  Liste ; 
    } 
  } 
} ) ;
includePaths
Art: Array<String>
Standard: []
Ein Array von Pfaden, in die LibSass schauen kann, um zu versuchen, Ihre @importDeklarationen aufzulösen . Bei der Verwendung datawird empfohlen, diese zu verwenden.

eingerücktSyntax
Art: Boolean
Standard: false
trueWerte aktivieren die Sass Indented Syntax zum Parsen der Datenzeichenfolge oder -datei.

Hinweis: node-sass / libsass kompiliert eine gemischte Bibliothek von scss- und eingerückten Syntaxdateien (.sass) mit der Standardeinstellung (false), solange die Erweiterungen .sass und .scss in Dateinamen verwendet werden.

indentType (> = v3.0.0)
Art: String
Standard: space
Wird verwendet, um zu bestimmen, ob Leerzeichen oder Tabulatorzeichen zum Einrücken verwendet werden sollen.

indentWidth (> = v3.0.0)
Art: Number
Standard: 2
Maximal: 10
Wird verwendet, um die Anzahl der Leerzeichen oder Tabulatoren zu bestimmen, die zum Einrücken verwendet werden sollen.

Zeilenvorschub (> = v3.0.0)
Art: String
Standard: lf
Wird verwendet , um festzustellen , ob die Verwendung cr, crlf, lfoder lfcrSequenz für Zeilenumbruch.

omitSourceMapUrl
Art: Boolean
Standard: false
Besonderheit: Wenn Sie dies verwenden, sollten Sie auch angeben outFile, um unerwartetes Verhalten zu vermeiden.

true Werte deaktivieren die Aufnahme von Quellkarteninformationen in die Ausgabedatei.

outFile
Art: String | null
Standard: null
Spezial: Erforderlich, wenn sourceMapes sich um einen wahrheitsgemäßen Wert handelt

Geben Sie den beabsichtigten Speicherort der Ausgabedatei an. Es wird dringend empfohlen, Quellkarten auszugeben, damit sie ordnungsgemäß auf die beabsichtigten Dateien zurückgreifen können.

Wenn Sie diese Option aktivieren, wird die Datei nicht für Sie auf die Festplatte geschrieben, sondern nur zu internen Referenzzwecken (zum Beispiel zum Generieren der Karte).

Beispiel, wie man es auf die Festplatte schreibt

Sass . rendern ( {
    ...
    outFile : yourPathTotheFile , 
  } ,  Funktion ( Fehler ,  Ergebnis )  {  // Rückruf im Knotenstil ab Version 3.0.0 
    Wenn ( ! Fehler ) { 
      // Keine Fehler während der Kompilierung, schreiben Sie dieses Ergebnis auf die Festplatte 
      fs . writeFile ( yourPathTotheFile ,  result . css ,  function ( err ) { 
        if ( ! err ) { 
          // auf die Festplatte geschriebene Datei 
        } 
      } );; 
    } 
  } ) ; 
} ) ;
outputStyle
Art: String
Standard: nested
Werte: nested, expanded, compact,compressed
Bestimmt das Ausgabeformat des endgültigen CSS-Stils.

Präzision
Art: Integer
Standard: 5
Wird verwendet, um zu bestimmen, wie viele Stellen nach der Dezimalstelle zulässig sind. Wenn Sie beispielsweise eine Dezimalzahl 1.23456789und eine Genauigkeit von hatten 5, befindet sich das Ergebnis 1.23457im endgültigen CSS.

sourceComments
Art: Boolean
Standard: false
trueAktiviert die Zeilennummer und Datei, in der ein Selektor definiert ist, als Kommentar in das kompilierte CSS. Nützlich zum Debuggen, insbesondere bei der Verwendung von Importen und Mixins.

sourceMap
Art: Boolean | String | undefined
Standard: undefined
Aktiviert die Generierung von Quellkarten während renderund renderSync.

Wenn sourceMap === true, wird der Wert von outFileals Zielausgabeposition für die Quellzuordnung mit dem .mapangehängten Suffix verwendet . Wenn nein outFilegesetzt ist, wird der sourceMapParameter ignoriert.

Wann typeof sourceMap === "string"wird der Wert von sourceMapals Schreibspeicherort für die Datei verwendet.

sourceMapContents
Art: Boolean
Standard: false
trueEnthält die contentsin der Quellkarte enthaltenen Informationen

sourceMapEmbed
Art: Boolean
Standard: false
true bettet die Quellkarte als Daten-URI ein

sourceMapRoot
Art: String
Standard: undefined
Der Wert wird wie sourceRootin den Quellkarteninformationen ausgegeben

render Rückruf (> = v3.0.0)
node-sass unterstützt asynchrone Rückrufe im Standardknotenstil mit der Signatur von function(err, result). Unter Fehlerbedingungen wird das errorArgument mit dem Fehlerobjekt gefüllt. Unter Erfolgsbedingungen wird das resultObjekt mit einem Objekt gefüllt, das das Ergebnis des Renderaufrufs beschreibt.

Fehlerobjekt
message (String) - Die Fehlermeldung.
line (Nummer) - Die Zeilennummer des Fehlers.
column (Nummer) - Die Spaltennummer des Fehlers.
status (Nummer) - Der Statuscode.
file(String) - Der Dateiname des Fehlers. Falls die fileOption nicht (zugunsten von data) festgelegt wurde, spiegelt dies den Wert wider stdin.
Ergebnisobjekt
css(Puffer) - Das kompilierte CSS. Schreiben Sie dies in eine Datei oder stellen Sie es nach Bedarf bereit.
map (Puffer) - Die Quellkarte
stats(Objekt) - Ein Objekt, das Informationen zur Kompilierung enthält. Es enthält die folgenden Schlüssel:
entry(String) - Der Pfad zur scss-Datei oder datawenn die Quelle keine Datei war
start (Nummer) - Date.now () vor der Kompilierung
end (Nummer) - Date.now () nach der Kompilierung
duration(Nummer) - Ende - Start
includedFiles (Array) - Absolute Pfade zu allen zugehörigen scss-Dateien in keiner bestimmten Reihenfolge.
Beispiele
var  sass  =  require ( 'node-sass' ) ; 
Sass . render ( { 
  file : '/path/to/myFile.scss' , 
  data : 'body {background: blue; a {color: black;}}' , 
  Importer : function ( url ,  prev ,  done )  { 
    // url is Der Pfad im Import wie er ist, auf den LibSass gestoßen ist. 
    // prev ist der zuvor aufgelöste Pfad. 
    // done ist ein optionaler Rückruf, entweder verbrauchen oder synchron zurückgeben.
    // this.options enthält diesen Options-Hash, this.callback enthält den 
    knotenartigen Rückruf someAsyncFunction ( url ,  prev ,  function ( result ) { 
      done ( { 
        file : result . path ,  // nur einer von ihnen ist erforderlich, siehe Abschnitt Spezielle Verhaltensweisen. 
        Inhalt : Ergebnis . Daten 
      } ) ; 
    } ) ; 
    // ODER 
    var  result  =  someSyncFunction ( url ,  prev );; 
    return  { file : result . Pfad ,  Inhalt : Ergebnis . Daten } ; 
  } , 
  includePaths : [  'lib /' ,  'mod /'  ] , 
  outputStyle : 'compress' 
} ,  Funktion ( Fehler ,  Ergebnis )  {  // Rückruf im Knotenstil ab Version 3.0.0 
  if  ( Fehler )  { 
    Konsole . log ( Fehler .Status ) ;  // war früher "Code" in v2x und unter der 
    Konsole . log ( Fehler . Spalte ) ; 
    Konsole . log ( Fehler . Meldung ) ; 
    Konsole . log ( Fehler . Linie ) ; 
  } 
  else  { 
    Konsole . log ( Ergebnis . css . toString ( ) ) ;

    Konsole . log ( Ergebnis . Statistiken ) ;

    Konsole . log ( Ergebnis . map . toString ( ) ) ; 
    // oder besser 
    Konsole . log ( JSON . stringify ( Ergebnis . Map ) ) ;  // beachte, JSON.stringify akzeptiert auch Puffer 
  } 
} ) ; 
// ODER 
var  result  =  sass . renderSync ( { 
  Datei : '/path/to/file.scss' , 
  Daten :'Körper {Hintergrund: blau; a {color: black;}}‘ , 
  outputStyle : 'komprimierte' , 
  outFile : '/to/my/output.css' , 
  sourceMap : wahr ,  // oder ein absoluter oder relativer (zu outFile) -Pfad 
  Importeur : Funktion ( url ,  prev ,  done )  { 
    // url ist der Pfad beim Importieren, auf den LibSass gestoßen ist. 
    // prev ist der zuvor aufgelöste Pfad. 
    // done ist ein optionaler Rückruf, entweder verbrauchen oder synchron zurückgeben. 
    // this.options enthält diese Optionen hash 
    someAsyncFunction (url ,  zurück ,  Funktion ( Ergebnis ) { 
      getan ( { 
        Datei : Ergebnis . Pfad ,  // nur einer von ihnen erforderlich ist, siehe Abschnitt Besondere Behaviors. 
        Inhalt : Ergebnis . Daten 
      } ) ; 
    } ) ; 
    // ODER 
    var  result  =  someSyncFunction ( url ,  prev ) ; 
    return  { file : result . Pfad , Inhalt : Ergebnis . Daten } ; 
  } 
} ) ;

Konsole . log ( Ergebnis . CSS ) ; 
Konsole . log ( Ergebnis . Karte ) ; 
Konsole . log ( Ergebnis . Statistiken ) ;
Besondere Verhaltensweisen
Für den Fall, dass sowohl fileals auch dataOptionen festgelegt sind, hat Node-Sass Vorrang vor dataund wird filezur Berechnung von Pfaden in Quellkarten verwendet.
Versionsinformationen (> = v2.0.0)
Beide node-sassund libsassVersionsinformationen werden jetzt über die folgende infoMethode angezeigt:

var  sass  =  require ( 'node-sass' ) ;

Konsole . log ( sass . info ) ;

/ * 
  es wird etwas ausgeben wie:

  node-sass 2.0.1 (Wrapper) [JavaScript] 
  libsass 3.1.0 (Sass Compiler) [C / C ++] 
* /
Da node-sass> = v3.0.0 ist, wird die LibSass-Version zur Laufzeit ermittelt.

Integrationen
Auflistung der Community-Verwendungen von Node-Sass in Build-Tools und Frameworks.

Klammerverlängerung
@jasonsanjose hat eine Brackets- Erweiterung basierend auf Node-Sass erstellt: https://github.com/jasonsanjose/brackets-sass . Beim Bearbeiten von Sass-Dateien kompiliert die Erweiterung Änderungen beim Speichern. Die Erweiterung lässt sich auch in die Live-Vorschau integrieren, um Sass-Änderungen im Browser anzuzeigen, ohne sie zu speichern oder zu kompilieren.

Brunch Plugin
Das offizielle Sass-Plugin von Brunch verwendet standardmäßig Node-Sass und greift automatisch auf Ruby zurück, wenn die Verwendung von Compass erkannt wird: https://github.com/brunch/sass-brunch

Connect / Express-Middleware
Kompilieren Sie .scssDateien automatisch neu für verbindungs- und expressbasierte http-Server.

Diese Funktionalität wurde node-sass-middlewarein Node-Sass v1.0.0 verschoben

DocPad Plugin
@ 10xLaCroixDrinker hat ein DocPad- Plugin geschrieben, das .scssDateien mit node-sass kompiliert: https://github.com/10xLaCroixDrinker/docpad-plugin-nodesass

Duo.js Erweiterung
@stephenway hat eine Erweiterung erstellt, die Sass mithilfe von node-sass mit duo.js https://github.com/duojs/sass in CSS umwandelt

Grunzerweiterung
@sindresorhus hat eine Reihe von Grunzaufgaben basierend auf Node-Sass erstellt: https://github.com/sindresorhus/grunt-sass

Gulp-Erweiterung
@dlmanning hat ein gulp sass Plugin basierend auf node-sass erstellt: https://github.com/dlmanning/gulp-sass

Harfe
Der Harp-Webserver von @sintaxi kompiliert implizit .scssDateien mit node-sass: https://github.com/sintaxi/harp

Metalsmith Plugin
@stevenschobert hat ein Metallschmied-Plugin basierend auf Node-Sass erstellt: https://github.com/stevenschobert/metalsmith-sass

Meteor Plugin
@fourseven hat ein Meteor-Plugin basierend auf Node-Sass erstellt: https://github.com/fourseven/meteor-scss

Mimosenmodul
@dbashford hat ein Mimosa-Modul für sass erstellt, das Node-sass enthält: https://github.com/dbashford/mimosa-sass

Beispiel App
Hier gibt es auch eine Beispiel-Verbindungs-App: https://github.com/andrew/node-sass-example

Binärdateien neu erstellen
Node-sass enthält vorkompilierte Binärdateien für gängige Plattformen. Um eine Binärdatei für Ihre Plattform hinzuzufügen, gehen Sie folgendermaßen vor:

Schauen Sie sich das Projekt an:

git clone --recursive https://github.com/sass/node-sass.git
 cd node-sass
npm installieren
Knotenskripte / build -f   # Verwenden Sie den Schalter -d für das Debug-Release 
#. Wenn dies erfolgreich ist, wird 
die Binärdatei im Herstellerverzeichnis generiert und # verschoben .
Befehlszeilenschnittstelle
Die Schnittstelle für die Befehlszeilennutzung ist zu diesem Zeitpunkt recht simpel, wie im folgenden Verwendungsabschnitt dargestellt.

Die Ausgabe wird an stdout gesendet, wenn das --outputFlag weggelassen wird.

Verwendung
node-sass [options] <input> [output] Oder: cat <input> | node-sass > output

Beispiel:

node-sass src/style.scss dest/style.css

Optionen:

    -w, --watch Beobachten Sie ein Verzeichnis oder eine Datei
    -r, --recursive Verzeichnisse oder Dateien rekursiv überwachen
    -o, --output Ausgabeverzeichnis
    -x, --omit-source-map-url Quell- URL-Kommentar aus der Ausgabe auslassen
    -i, --indented-syntax Behandle Daten von stdin als Sass-Code (versus scss)
    -q, --quiet Unterdrückt die Protokollausgabe außer bei einem Fehler
    -v, --version Druckt Versionsinformationen
    - CSS-Ausgabestil im Ausgabestil (verschachtelt | erweitert | kompakt | komprimiert)
    --indent-Typ einrücken Typ  für Ausgabe CSS (Raum | tab)
    - Einrückungsbreite Einrückungsbreite ; Anzahl der Leerzeichen oder Tabulatoren (Maximalwert: 10)
    --linefeed Linefeed Stil (cr | crlf | lf | lfcr)
    --source-Kommentare Debug-Informationen in die Ausgabe aufnehmen
    --source-Karte Emit Quelle Karte
    --source-map-content Einbetten von Inhalten in die Karte
    --source-map-embedded Betten Sie sourceMappingUrl als Daten-URI ein
    --source-map root-Basispfad wird emittiert werden in Source-Karte wie
    --include-path Pfad zum Suchen nach importierten Dateien
    --follow Folgen Sie den verknüpften Verzeichnissen
    --precision Die in Dezimalzahlen zulässige Genauigkeit
    --error-bell Gibt bei Fehlern ein Glockenzeichen aus
    --importer Pfad zur .js-Datei mit dem benutzerdefinierten Importer
    --functions Pfad zur .js-Datei mit benutzerdefinierten Funktionen
    --help Verwendungsinformationen drucken
Das inputkann entweder ein einzelnes .scssoder .sassoder ein Verzeichnis sein. Wenn die Eingabe ein Verzeichnis ist, --outputmuss auch das Flag angegeben werden.

Außerdem nimmt note --importerden Pfad (absolut oder relativ zu pwd) zu einer js-Datei, für die standardmäßig module.exportsdie Importerfunktion festgelegt werden muss. Siehe zum Beispiel unsere Testvorrichtungen .

Die --source-mapOption akzeptiert einen booleschen Wert. In diesem Fall ersetzt sie die Zielerweiterung durch .css.map. Es akzeptiert auch den Pfad zur .mapDatei und sogar den Pfad zum gewünschten Verzeichnis. Beim Kompilieren kann ein Verzeichnis --source-mapentweder ein boolescher Wert oder ein Verzeichnis sein.

Binäre Konfigurationsparameter
node-sass unterstützt verschiedene Konfigurationsparameter, um Einstellungen für die sass-Binärdatei zu ändern, z. B. Binärname, Binärpfad oder alternativer Downloadpfad. Folgende Parameter werden von Node-Sass unterstützt:

Variablennamen	Parameter .npmrc	Prozessargument	Wert
SASS_BINARY_NAME	sass_binary_name	--sass-binärer-Name	Pfad
SASS_BINARY_SITE	sass_binary_site	--sass-binary-site	URL
SASS_BINARY_PATH	sass_binary_path	--sass-binärer Pfad	Pfad
SASS_BINARY_DIR	sass_binary_dir	--sass-binary-dir	Pfad
Diese Parameter können als Umgebungsvariable verwendet werden:

Z.B export SASS_BINARY_SITE=http://example.com/
Als lokale oder globale .npmrc- Konfigurationsdatei:

Z.B sass_binary_site=http://example.com/
Als Prozessargument:

Z.B npm install node-sass --sass-binary-site=http://example.com/
Build nach der Installation
Bei der Installation werden nur zwei Mocha-Tests ausgeführt, um festzustellen, ob Ihr Computer den vorgefertigten LibSass verwenden kann, wodurch während der Installation einige Zeit gespart wird. Wenn ein Test fehlschlägt, wird er aus dem Quellcode erstellt.

Betreuer
Dieses Modul wird Ihnen von folgenden Personen zur Verfügung gestellt und gewartet:

Michael Mifsud - Projektleiter ( Github / Twitter )
Andrew Nesbitt ( Github / Twitter )
Dean Mao ( Github / Twitter )
Brett Wilkins ( Github / Twitter )
Keith Cirkel ( Github / Twitter )
Laurent Goderre ( Github / Twitter )
Nick Schonning ( Github / Twitter )
Adeel Mujahid ( Github / Twitter )
Mitwirkende
Wir <3 unsere Mitwirkenden! Ein besonderer Dank geht an alle, die einige Entwicklungszeit für dieses Projekt aufgewendet haben. Wir schätzen Ihre harte Arbeit sehr. Sie können finden Sie eine vollständige Liste der Menschen hier.

Hinweis zu Patches / Pull-Anfragen
Lesen Sie unseren Beitragsleitfaden

Urheberrechte ©
Copyright (c) 2015 Andrew Nesbitt. Siehe LIZENZ für Details.
