🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*


# L'Art de la linea d'ordres

[![Feu una pregunta](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

[![Uniu-vos al xat a https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


- [Meta](#meta)
- [Conceptes Bàsics](#basics)
- [Ús diari](#diari)
- [Tractament de Fitxers i dades](#processament-de-fitxers-i-dades)
- [Sistema de depuració](#sistema-de-depuració)
- [One-liners](#one-liners)
- [Obscur però útil](#obscur-però-útil)
- [Només MacOS](#només-macos)
- [Només Windows](#només-windows)
- [Més Recursos](#més-recursos)
- [Renúncia de Responsabilitat](#renúncia-de-responsabilitat)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

La fluïdesa de la línia de comandes és una habilitat sovint descuidada o considerada arcana, però millora la vostra flexibilitat i productivitat com a enginyer de maneres òbvies i subtils. Es tracta d’una selecció de notes i consells sobre l’ús de la línia de comandaments que hem trobat útils quan es treballa amb Linux. Alguns consells són elementals, i alguns són bastant específics, sofisticats o obscurs. Aquesta pàgina no és llarga, però si podeu utilitzar i recordar tots els elements aquí, ja sabeu molt.

Aquest treball és el resultat de [molts autors i traductors](AUTHORS.md).
Part d'aquest
[originalment](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[publicidad](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
en [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
però des de llavors s'ha traslladat a GitHub, on la gent amb més talent que l’autor original ha fet moltes millores.
[**Si us play, envieu una pregunta**](https://airtable.com/shrzMhx00YiIVAWJg) si teniu una pregunta relacionada amb la línia d'ordres. [**Si us plau, contribuïu amb**](/CONTRIBUTING.md) si veieu un error o alguna cosa que podria ser millor!

## Meta

Abast:

- Aquesta guia és per a principiants i experimentats. Els objectius són * ample * (tot important), * especificitat * (donen exemples concrets del cas més comú), i * brevetat * (eviteu coses que no siguin essencials o digressions que pugueu buscar fàcilment en un altre lloc). Cada consell és essencial en alguna situació o estalvia significativament el temps per les alternatives.
- Això està escrit per a Linux, amb l'excepció de les seccions "[Només MacOS](#només-macos)" i "[Només Windows](#només-windows)". Molts dels altres articles s’apliquen o es poden instal·lar en altres Unices o macOS (o fins i tot Cygwin).
- El focus es basa en Bash interactiu, encara que molts consells s'apliquen a altres shell i al script Bash general.
- Inclou tant ordres Unix "estàndard" com aquells que requereixen instal·lacions especials de paquets, sempre que siguin prou importants com per ser incloses.

Notes:

- Per mantenir aquesta pàgina a una pàgina, el contingut està inclòs implícitament per referència. Ets prou intel·ligent com per buscar més detalls en un altre lloc quan conegueu la idea o el comandament a Google. Utilitzeu "apt", "yum", "dnf", "pacman", "pip" o "brew" (segons el cas) per instal·lar nous programes.
- Utilitzeu [Explainshell](http://explainshell.com/)  per obtenir un desglossament útil de les ordres, les opcions, les canonades, etc.


## Conceptes Bàsics

- Aprendre Bash bàsic. En realitat, escriviu `man bash` i, almenys, desmarqueu tot allò; és bastant fàcil de seguir i no tant de temps. Els dipòsits alternatius poden ser bons, però Bash és potent i sempre disponible (l'aprenentatge de * només * zsh, peix, etc., tot i que proveu el vostre propi ordinador portàtil, us restringeix en moltes situacions, com ara servidors existents).

- Aprendre bé com a mínim un editor de text. L’editor `nano`és un dels més senzills per a l’edició bàsica (obertura, edició, estalvi i cerca). No obstant això, per a l'usuari de potència en un terminal de text, no hi ha substitut per a Vim (`vi`), l'editor difícil d'aprendre però venerable, ràpid i amb totes les funcions. Moltes persones també utilitzen el clàssic Emacs, especialment per a tasques d’edició més grans. (Per descomptat, qualsevol desenvolupador de programari modern que treballi en un projecte extens no és probable que utilitzi només un editor basat en text i també hauria de familiaritzar-se amb les IDE i les eines gràfiques modernes).

- Cerca de documentació:
   - Saber llegir la documentació oficial amb `man` (per a la curiositat,` man man` enumera els números de secció, p. Ex. 1 és ordres "regular", 5 és fitxers / convencions i 8 són per a administració). Cerqueu pàgines man amb `apropos`.
  - Sàpiga que algunes ordres no són executables, sinó integracions de Bash, i que podeu obtenir ajuda sobre ells amb `help` i `help -d`. Podeu esbrinar si una ordre és un executable, un shell integrat o un àlies mitjançant l’ordre `type`.
  - `curl cheat.sh / command` donarà un "full de trucs" breu amb exemples comuns sobre com utilitzar una ordre de shell.

- Conegueu la redirecció de la sortida i l'entrada utilitzant `>` i `<` i canonades utilitzant `|`. Saber `>` sobreescriu el fitxer de sortida i ` >> ` afegeix. Més informació sobre stdout i stderr.

- Obtingueu informació sobre l’expansió de fitxers de fitxers amb `*` (i potser `?` I `[` ... `]`) i citant i la diferència entre les `'` simples i les dobles.(Vegeu més sobre l’expansió de variables a continuació.)

- Familiaritzar-se amb la gestió de treballs de Bash: `&`, ** ctrl-z **, ** ctrl-c **, `jobs`,` fg`, `bg`,` kill`, etc.

- Coneixeu `ssh` i els conceptes bàsics d’autenticació sense contrasenya, a través de` ssh-agent`, `ssh-add`, etc.

- Gestió bàsica de fitxers: `ls` i` ls -l` (en particular, descobreix què significa cada columna a `ls -l`),` less`, `head`,` tail` i `tail -f` (o encara millor, `less + F`),` ln` i `ln -s` (aprendre les diferències i avantatges dels enllaços durs versus soft),` chown`, `chmod`,` du` (per a un resum ràpid del disc ús: `du -hs *`). Per a la gestió del sistema de fitxers, `df`,` mount ', `fdisk`,` mkfs`, `lsblk`. Més informació sobre el que és un inode (`ls -i» o `df -i`).

- Gestió bàsica de la xarxa: "ip" o "ifconfig", "dig", "traceroute", "route".

- Aprendre i utilitzar un sistema de gestió de control de versions, com ara "git".

- Coneix bé les expressions regulars i les diferents banderes a `grep` /` egrep`. Val la pena conèixer les opcions "-i", "-o", "-v", "-A", "-B" i "-C".

- Apreneu a utilitzar "apt-get", "yum", "dnf" o "pacman" (segons la distribució) per trobar i instal·lar paquets. I assegureu-vos que teniu "pip" per instal·lar eines de línia d’ordres basades en Python (algunes de les següents són més fàcils d’instal·lar a través de "pip").


## Ús diari

- A Bash, utilitzeu ** Tab ** per completar els arguments o llistar totes les ordres disponibles i ** ctrl-r ** per cercar a través de l'historial d'ordres (després de prémer, escriviu per cercar, premeu ** ctrl-r ** repetidament per ciclar a través de més coincidències, premeu ** Introdueix ** per executar l’ordre trobat, o bé premeu la fletxa dreta per posar el resultat a la línia actual per permetre l’edició).

- A Bash, utilitzeu ** ctrl-w ** per esborrar la darrera paraula, i ** ctrl-u ** per esborrar el contingut del cursor actual de nou a l'inici de la línia. Utilitzeu ** alt-b ** i ** alt-f ** per moure's per paraula, ** ctrl-a ** per moure el cursor al començament de la línia, ** ctrl-e ** per moure el cursor al final de la línia , ** ctrl-k ** per matar fins al final de la línia, ** ctrl-l ** per esborrar la pantalla. Vegeu `man readline 'per a totes les combinacions de tecles per defecte de Bash. Hi ha molts. Per exemple, ** alt -. ** recorre els arguments anteriors i ** alt - *** amplia un globus.


- Alternativament, si us agrada l'enllaç de claus a l'estil de vi, utilitzeu `set -o vi` (i` set -o emacs` per posar-lo de nou).

- Per editar comandes llargues, després de configurar l’editor (per exemple `export EDITOR = vim`), ** ctrl-x ** ** ctrl-e ** obrirà l’ordre actual en un editor per a l’edició de diverses línies. O en un estil vi, ** escape-v **.

- Per veure les ordres recents, utilitzeu el fitxer "history". Seguiu amb `! N` (on` n` és el número de comanda) que es vol executar de nou. També hi ha moltes abreviatures que podeu fer servir, la més útil probablement sigui `! $ 'Per a l'últim argument i" !! "per a l'últim comandament (vegeu" HISTORY EXPANSION "a la pàgina de manual). Tanmateix, sovint es reemplacen fàcilment amb ** ctrl-r ** i ** alt -. **.

- Aneu al vostre directori personal amb `cd '. Accediu als fitxers relacionats amb el vostre directori personal amb el prefix `~` (per exemple, `~ / .bashrc`). A les seqüències `sh` referiu-vos al directori inicial com a` $ HOME`.

- Per tornar al directori de treball anterior: `cd -`.

- Si està a mig camí escrivint una ordre però canvieu de parer, premeu ** alt - # ** per afegir un "#" al principi i introduïu-lo com a comentari (o utilitzeu ** ctrl-a **, ** # **, ** introduïu **). A continuació, podeu tornar-hi més tard a través de l’historial d’ordres.

- Utilitzeu `xargs` (o` paral·lel »). És molt potent. Tingueu en compte que podeu controlar quants elements executen per línia (`-L`), així com el paral·lelisme (` -P`). Si no sabeu si farà el correcte, utilitzeu primer "xargs echo". A més, `-I {}` és útil. Exemples:
`` `bash
      trobar. -name '* .py' | xargs grep some_function
      amfitrions de gats | xargs -I {} ssh root @ {} hostname
`` `

- `pstree -p` és una visualització útil de l'arbre de processos.

- Utilitzeu `pgrep` i` pkill` per trobar o assenyalar processos per nom (`-f` és útil).

- Coneixeu els diferents senyals que podeu enviar. Per exemple, per suspendre un procés, utilitzeu `kill -STOP [pid]`. Per a la llista completa, consulteu el senyal "home 7"

- Utilitzeu `nohup` o` renegat 'si voleu que un procés de fons continuï funcionant per sempre.

- Comproveu els processos que escoltem mitjançant `netstat -lntp 'o` ss -plat` (per a TCP; afegiu `-u` per UDP) o` lsof -iTCP -sTCP: LISTEN -P -n` (que també funciona en macOS) ).

- Vegeu també `lsof` i` fuser` per a sockets o fitxers oberts.

- Vegeu "temps d’activitat" o "w" per saber quant de temps ha funcionat el sistema.

- Utilitzeu `alias 'per crear dreceres per a ordres comunament utilitzades. Per exemple, `alias ll = 'ls -latr'` crea un nou àlies` ll`.

- Desa els àlies, la configuració del shell i les funcions que normalment utilitzeu a `~ / .bashrc`, i [arregleu els dipòsits d’inici de sessió per originar-la] (http://superuser.com/a/183980/7106). Això farà que la vostra configuració estigui disponible a totes les sessions de l'intèrpret d'ordres.

- Col·loqueu la configuració de les variables d’entorn i les ordres que s’hauran d’executar quan inicieu la sessió a `~ / .bash_profile`. Es necessitarà una configuració separada per als dipòsits que s’iniciïn d’inici de sessió d’entorns gràfics i de treballs de cron.

- Sincronitzeu els fitxers de configuració (p. Ex. `.Bashrc` i` .bash_profile`) entre diversos equips amb Git.

- Comprendre que cal tenir cura quan les variables i els noms de fitxer inclouen espais en blanc. Envolta les variables de Bash amb cometes, p. Ex. "" $ FOO "`. Preferiu les opcions `-0` o` -print0` per habilitar caràcters nuls per delimitar els noms de fitxer, p. `localitzar -0 patró | xargs -0 ls -al` o `find / -print0 -type d | xargs -0 ls -al`. Per a repetir els noms de fitxer que contenen espais en blanc per a un bucle, configureu el vostre IFS com a nova línia només utilitzant `IFS = $ 'n`.

- A les seqüències d’ordres de Bash, utilitzeu `set -x` (o la variant` set -v`, que registra l’entrada en brut, incloses les variables i comentaris no expandits) per a la depuració de la sortida. Utilitzeu modes estrictes a menys que tingueu un bon motiu per no: Utilitzeu `set -e` per avortar els errors (codi de sortida no zero). Utilitzeu "set -u" per detectar usos de variables que no es troben. Tingueu en compte `set -o pipefail` també, per avortar errors en canonades (encara que llegeixin-ne més si ho feu, ja que aquest tema és una mica subtil). Per a scripts més implicats, també utilitzeu `trap 'a EXIT o ERR. Un hàbit útil és iniciar un script com aquest, que el farà detectar i interrompre errors comuns i imprimir un missatge:
`` `bash
      set -euo pipefail
      error "echo" error: el script ha fallat: vegeu l'ordre fallida a sobre "" ERR
`` `

- En els scripts Bash, els subshells (escrits amb parèntesis) són maneres convenients per agrupar comandes. Un exemple comú és passar temporalment a un directori de treball diferent, p. Ex.
`` `bash
      # fer alguna cosa a la direcció actual
      (cd / some / other / dir && other-command)
      # continueu a la direcció original
`` `

- A Bash, tingueu en compte que hi ha molts tipus d'expansió de variables. Comprovació d’una variable existeix: `$ {name:? Message d'error}`. Per exemple, si un script Bash requereix un únic argument, només cal que escriviu "fitxer_entrada" = $ {1:? Use: $ 0 fitxer_entrada "}. Utilitzant un valor per defecte si una variable està buida: `$ {name: -default}`. Si voleu afegir un paràmetre addicional (opcional) a l’exemple anterior, podeu utilitzar alguna cosa com `output_file = $ {2: -logfile}`. Si s'omet el missatge "$ 2" i, per tant, el fitxer "fitxer de sortida" es definirà com a "fitxer de registre". Expansió aritmètica: `i = $ (((i + 1)% 5))`. Seqüències: `{1..10}`. Retallar cadenes: `$ {var% suffix}` i `$ {var # prefix}`. Per exemple, si `var = foo.pdf`, llavors` echo $ {var% .pdf} .txt` imprimeix `foo.txt`.

- L’expansió d’estiració mitjançant `{` ... `}` pot reduir el fet de tornar a escriure text similar i automatitzar combinacions d’articles. Això és útil en exemples com `mv foo. {Txt, pdf} some-dir` (que mou els dos fitxers),` cp somefile {,. Bak} `(que s'expandeix a` cp somefile somefile.bak`) o `mkdir -p test- {a, b, c} / subtest- {1,2,3} `(que expandeix totes les combinacions possibles i crea un arbre de directoris). L’expansió d’estiraments es realitza abans de qualsevol altra expansió.

- L’ordre d’expansions és: l’expansió d’enllaços; expansió de la tilde, expansió de paràmetres i variables, expansió aritmètica i substitució d'ordres (feta de manera esquerra a dreta); divisió de paraules; i l’expansió del nom de fitxer. (Per exemple, un interval com `{1..20} 'no es pot expressar amb variables utilitzant` {$ a .. $ b} `. Utilitzeu` seq` o un bucle de `per`, per exemple,` seq $ a $ b` o `per a ((i = a; i <= b; i ++)); fer ...; fet".)

- La sortida d’una ordre es pot tractar com un fitxer a través de `<(algun comando)` (conegut com a substitució de processos). Per exemple, compareu `` / etc / hosts` locals amb un remot:
`` `sh
      diff / etc / hosts <(ssh somehost cat / etc / hosts)
`` `

- Quan escriviu scripts és possible que vulgueu posar tot el vostre codi en claus. Si no es troba el claudàtor de tancament, el vostre script no es podrà executar a causa d'un error de sintaxi. Això té sentit quan el vostre script s’ha de descarregar del web, ja que impedeix l’execució d’escriptures parcialment descarregades:
`` `bash
{
      # El vostre codi aquí
}
`` `

- Un "document aquí" permet [la redirecció de múltiples línies d’entrada] (https://www.tldp.org/LDP/abs/html/here-docs.html) com si des d’un fitxer:
`` `
cat << EOF
entrada
en múltiples línies
EOF
`` `

- A Bash, redirigeix ​​tant la sortida estàndard com l’error estàndard a través de: `some-command> logfile 2> & 1` o` some-command &> logfile`. Sovint, per assegurar que una ordre no deixa un controlador de fitxer obert a l'entrada estàndard, lligant-lo al terminal en què es troba, també és bo afegir `/ / dev / null`.

- Utilitzeu `man ascii` per a una bona taula ASCII, amb valors hexadecimal i decimal. Per a informació de codificació general, són útils `man unicode`,` man utf-8` i `man latin1`.

- Utilitzeu "pantalla" o [`tmux`] (https://tmux.github.io/) per multiplicar la pantalla, especialment útil per a sessions ssh remotes i per separar-les i tornar-les a afegir a una sessió. `byobu` pot millorar la pantalla o el tmux proporcionant més informació i una gestió més senzilla. Una alternativa més mínima per a la persistència de la sessió només és [`dtach`] (https://github.com/bogner/dtach).

- A ssh, és útil saber com portar túnel amb "-L" o "-D" (i de vegades `-R`), p. Ex. per accedir a llocs web des d'un servidor remot.

- Pot ser útil fer algunes optimitzacions a la vostra configuració ssh; per exemple, aquest fitxer `/ / .ssh / config` conté paràmetres per evitar connexions caigudes en determinats entorns de xarxa, utilitza compressió (que és útil per a connexions de baixa amplada de banda) i canals multiplex al mateix servidor amb un fitxer de control local :
`` `
      TCPKeepAlive = sí
      ServerAliveInterval = 15
      ServerAliveCountMax = 6
      Compressió = sí
      ControlMaster auto
      ControlPath / tmp /% r @% h:% p
      ControlPersist sí
`` `

- Algunes altres opcions rellevants per a ssh són sensibles a la seguretat i haurien d'estar habilitades amb cura, p. Ex. per subxarxa o amfitrió o per xarxes de confiança: `StrictHostKeyChecking = no`,` ForwardAgent = yes?

- Tingueu en compte [`mosh`] (https://mosh.mit.edu/) una alternativa a ssh que utilitza UDP, evitant connexions caigudes i afegint comoditat a la carretera (cal configurar el servidor).

- Per obtenir els permisos en un fitxer de forma octal, que és útil per a la configuració del sistema però no disponible a `ls` i fàcil de bungle, utilitzeu alguna cosa com
`` `sh
      stat -c '% A% a% n' / etc / zona horària
`` `

- Per a la selecció interactiva de valors de la sortida d’una altra comanda, utilitzeu [`percol`] (https://github.com/mooz/percol) o [` fzf`] (https://github.com/junegunn/fzf ).

- Per a la interacció amb fitxers basats en la sortida d’una altra comanda (com `git`), utilitzeu` fpp` ([PathPicker] (https://github.com/facebook/PathPicker)).

- Per a un servidor web senzill per a tots els fitxers del directori actual (i subdirectors), disponibles per a qualsevol persona de la vostra xarxa, utilitzeu:
`python-m SimpleHTTPServer 7777` (per al port 7777 i Python 2) i` python -m http.server 7777` (per al port 7777 i Python 3).

- Per executar una ordre com a un altre usuari, utilitzeu "sudo". Per defecte, s'executa com a root; utilitzeu `-u` per especificar un altre usuari. Utilitzeu `-i` per iniciar sessió com a aquest usuari (se us demanarà _la vostra_ contrasenya).

- Per canviar el shell a un altre usuari, utilitzeu `su username 'o` su - username'. Aquest últim amb "-" obté un entorn com si un altre usuari només iniciés la sessió. Omissant el nom d’usuari per defecte a root. Se us demanarà la contrasenya de l’usuari que esteu canviant a.

- Saber sobre el [128K limit] (https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong) a les línies d'ordres. Aquest error "Llista d'arguments massa llarg" és comú quan un comodí coincideix amb un gran nombre de fitxers. (Quan això succeeix, poden ajudar alternatives com `find` i` xargs`).

- Per obtenir una calculadora bàsica (i, per descomptat, accedir a Python en general), utilitzeu l'intèrpret de "python". Per exemple,
```
>>> 2 + 3
5
```


## Processament de fitxers i dades

- Per localitzar un fitxer per nom al directori actual, `trobar. -iname '* something *' '(o similar). Per trobar un fitxer en qualsevol lloc pel nom, utilitzeu "localitzar alguna cosa" (però tingueu en compte que "updatedb" pot no haver indexat fitxers creats recentment).

- Per a la cerca general a través de fitxers d'origen o de dades, hi ha diverses opcions més avançades o més ràpides que `grep -r`, incloent-hi (en brut des del més antic al més recent) [` ack`] (https://github.com/beyondgrep / ack2), [`ag`] (https://github.com/ggreer/the_silver_searcher) (" el cercador de plata ") i [` rg "] (https://github.com/BurntSushi/ripgrep) ( ripgrep).

- Per convertir HTML a text: `lynx -dump -stdin`

- Per a Markdown, HTML i tot tipus de conversions de documents, proveu [`pandoc`] (http://pandoc.org/). Per exemple, per convertir un document Markdown en format Word: `pandoc README.md --des del marcatge --to docx -o temp.docx

- Si heu de gestionar XML, `xmlstarlet` és vell però bo.

- Per a JSON, utilitzeu [`jq`] (http://stedolan.github.io/jq/). Per a un ús interactiu, vegeu també [`jid`] (https://github.com/simeji/jid) i [` jiq`] (https://github.com/fiatjaf/jiq).

- Per a YAML, utilitzeu [`shyaml`] (https://github.com/0k/shyaml).

- Per a fitxers Excel o CSV, [csvkit] (https://github.com/onyxfish/csvkit) proporciona "in2csv", "csvcut", "csvjoin", "csvgrep", etc.

- Per a Amazon S3, [`s3cmd`] (https://github.com/s3tools/s3cmd) és convenient i [` s4cmd`] (https://github.com/bloomreach/s4cmd) és més ràpid. Amazon [`aws`] (https://github.com/aws/aws-cli) i [` saws] millorades (https://github.com/donnemartin/saws) són essencials per a altres tasques relacionades amb AWS .

- Coneixeu sobre `sort 'i` uniq`, incloent-hi les opcions `-u` i` -d` de uniq: vegeu les línies següents. Vegeu també `comm`.

- Saber sobre `cut`,` paste` i `join` per manipular fitxers de text. Molta gent utilitza `cut 'però oblida` join'.

- Saber sobre `wc 'per comptar les noves línies (` -l`), caràcters (`-m`), paraules (` -w`) i bytes (`-c`).

- Coneixeu sobre `tee` per copiar des de stdin a un fitxer i també a stdout, com a` ls -al | tee file.txt`.

- Per a càlculs més complexos, incloent l’agrupació, els camps inversos i els càlculs estadístics, tingueu en compte [`datamash`] (https://www.gnu.org/software/datamash/).

- Saber que la localitat afecta moltes eines de línia de comandes de manera subtil, incloent ordre d’ordenació (col·lació) i rendiment. La majoria de les instal·lacions de Linux establiran "LANG" o altres variables de localització en una configuració local com l’anglès dels EUA. Però tingueu en compte que l’ordenació canviarà si canvieu de lloc. I saber que les rutines i18n poden fer que les ordres d’ordenació o altres executades queden moltes vegades més lentes. En algunes situacions (com ara les operacions del conjunt o les operacions de singularitat següents), podeu ignorar completament les rutines lentes i18n i utilitzar l’ordre de classificació basat en bytes tradicionals, utilitzant `export LC_ALL = C`.

- Podeu definir l’entorn d’una ordre específica amb el prefix de la seva invocació amb la configuració de la variable d’entorn, com a `TZ = data de Pacífic / Fiji '.

- Coneixeu `awk` i` sed 'bàsics per a la informació senzilla. Vegeu [Un solapi] (# un-liners) per obtenir exemples.

- Per substituir totes les aparicions d'una cadena en un o més fitxers:
`` `sh
      perl -pi.bak -e 's / old-string / new-string / g' els meus fitxers - *. txt
`` `

- Per canviar el nom de diversos fitxers i / o cercar i substituir en fitxers, proveu [`repren`] (https://github.com/jlevy/repren). (En alguns casos, la comanda `rename`` també permet canviar el nom de múltiples noms, però aneu en compte perquè la seva funcionalitat no és la mateixa en totes les distribucions de Linux.)
`` `sh
      # Canviar el nom de noms de fitxers, directoris i continguts foo -> bar:
      repren --full --preserve-case --de foo --to bar.
      # Recuperar fitxers de seguretat del que sigui.
      repren --renames --de '(. *) bak' --to '1' * .bak
      # Igual que a dalt, mitjançant el canvi de nom, si està disponible:
      canviar el nom de s / / bak $ // '* .bak
`` `

- Com diu la pàgina man, `rsync` és realment una eina de copia de fitxers ràpida i versàtil. Es coneix per sincronitzar entre màquines, però és igualment útil localment. Quan les restriccions de seguretat permeten, l’ús de `rsync` en lloc de` scp` permet recuperar una transferència sense haver de reiniciar des de zero. També es troba entre les [maneres més ràpides] (https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge- nombre-de-fitxers.html) per eliminar un gran nombre de fitxers:
`` `sh
mkdir buit && rsync -r --deleteu buit / some-dir && rmdir some-dir
`` `

- Per supervisar l’avanç en processar fitxers, utilitzeu [`pv`] (http://www.ivarch.com/programs/pv.shtml), [` pycp`] (https://github.com/dmerejkowsky/pycp) , [`pmonitor`] (https://github.com/dspinellis/pmonitor), [` progrés '] (https://github.com/Xfennec/progress), `rsync --progress`, o, per a bloquejar còpia del nivell, `dd status = progress '.

- Utilitzeu `shuf` per barrejar o seleccionar línies aleatòries d’un fitxer.

- Conèixer les opcions de "sort". Per als números, utilitzeu `-n` o` -h` per gestionar els números llegibles per humans (per exemple, de `du -h`). Saber com funcionen les claus (`-t` i` -k`). En particular, tingueu en compte que heu d’escriure `-k1,1` per ordenar només el primer camp; `-k1` significa ordenar segons la línia sencera. El tipus estable ("sort -s") pot ser útil. Per exemple, per ordenar primer el camp 2, després secundàriament pel camp 1, podeu utilitzar `sort -k1,1 | sort -s -k2,2`.

- Si alguna vegada necessiteu escriure una pestanya literal en una línia d'ordres a Bash (per exemple, per a l'argument -t per ordenar), premeu ** ctrl-v ** ** [Tab] ** o escriviu `$ ' `(aquest últim és millor, ja que el podeu copiar / enganxar).

- Les eines estàndard per reparar el codi font són "diff" i "patch". Vegeu també "diffstat" per a les estadístiques de resum d’un diff i de "sdiff" per a un diff. Nota `diff -r` funciona per a directoris sencers. Utilitzeu `diff -r tree1 tree2 | diffstat` per a un resum dels canvis. Utilitzeu `vimdiff` per comparar i editar fitxers.

- Per a fitxers binaris, utilitzeu `hd`,` hexdump` o `xxd` per a dipòsits hexagonals simples i` bvi`, `hexedit` o` biew` per a l'edició binària.

- També per a fitxers binaris, `cadenes` (més` grep`, etc.) us permeten trobar fragments de text.

- Per a difs binaris (compressió delta), utilitzeu `xdelta3`.

- Per convertir codificacions de text, proveu `iconv`. O `uconv` per a un ús més avançat; admet algunes coses Unicode avançades. Per exemple:
`` `sh
      # Mostra codis hexagonals o noms reals de caràcters (útils per a la depuració):
      uconv -f utf-8 -t utf-8 -x ':: Any-Hex;' <input.txt
      uconv -f utf-8 -t utf-8 -x ':: Any-Name;' <input.txt
      # Minúscules i elimina tots els accents (ampliant-los i deixant-los anar):
      uconv -f utf-8 -t utf-8 -x ':: Any-Lower; :: Any-NFD; [: Marca no espacial:]>; :: Qualsevol-NFC; ' <input.txt> output.txt
`` `

- Per dividir fitxers en trossos, vegeu `split '(per dividir per mida) i` csplit` (per dividir per un patró).

- Data i hora: per obtenir la data i l'hora actual en el format útil [ISO 8601] (https://en.wikipedia.org/wiki/ISO_8601), utilitzeu `date -u +"% Y-% m-% dT% H:% M:% SZ "" (altres opcions [són] (https://stackoverflow.com/questions/7216358/date-command-on-os-x-doesnt-have-iso-8601-i- opció) [problemàtica] (https://unix.stackexchange.com/questions/164826/date-command-iso-8601-option)). Per manipular expressions de data i hora, utilitzeu `dateadd`,` datated``, `strptime` etc. de [` dateutils`] (http://www.fresse.org/dateutils/).

- Utilitzeu `zless`,` zmore`, `zcat` i` zgrep` per operar en fitxers comprimits.

- Els atributs dels fitxers es poden configurar mitjançant `chattr` i ofereixen una alternativa de baix nivell als permisos dels fitxers. Per exemple, per protegir contra la supressió de fitxers accidentals, el senyalador immutable: `sudo chattr + i / critical / directory / or / file`

- Utilitzeu `getfacl` i` setfacl` per desar i restaurar els permisos del fitxer. Per exemple:
`` `sh
   getfacl -R / some / path> permissions.txt
   setfacl --restore = permissions.txt
`` `

- Per crear fitxers buits ràpidament, utilitzeu `truncate` (crea [fitxer dispers] (https://en.wikipedia.org/wiki/Sparse_file)),` fallocate` (ext4, xfs, btrfs i ocfs2 filesystem), `xfs_mkfile `(gairebé qualsevol sistema de fitxers, ve en paquet xfsprogs),` mkfile` (per a sistemes similars a Unix com Solaris, Mac OS).

## Depuració del sistema

- Per a la depuració web, `curl` i` curl -I` són útils, o els seus equivalents `wget`, o el més modern [` httpie »] (https://github.com/jkbrzt/http).

- Per conèixer l'estat actual del CPU / disc, les eines clàssiques són `top` (o millor` htop`), `iostat` i` iotop`. Utilitzeu `iostat -mxz 15` per a CPU bàsica i estadístiques detallades de disc per partició i coneixement del rendiment.

- Per a detalls de connexió de xarxa, utilitzeu `netstat` i` ss`.

- Per a una visió general ràpida del que passa en un sistema, `dstat` és especialment útil. Per obtenir una visió general més àmplia amb els detalls, utilitzeu [`looks '] (https://github.com/nicolargo/glances).

- Per conèixer l'estat de la memòria, executar i comprendre la sortida de `free` i` vmstat`. En particular, tingueu en compte que el valor "en memòria cau" és la memòria del nucli Linux com a memòria cau de fitxers, de manera que compta amb eficàcia cap al valor "lliure".

- La depuració del sistema Java és una tetera de peix diferent, però un simple truc a Oracle i alguns altres JVM és que podeu executar `kill -3 <pid>` i un resum de pila completa (incloent detalls de recollida de deixalles generacionals, que pot ser molt informatiu) es farà anar a stderr / logs. El JDK, "jps", "jstat", "jstack", "jmap" són útils. [Eines SJK] (https://github.com/aragozin/jvm-tools) són més avançades.

- Utilitzeu [`mtr`] (http://www.bitwizard.nl/mtr/) com a millor traceroute, per identificar problemes de xarxa.

- Per veure per què un disc està ple, [`ncdu`] (https://dev.yorhel.nl/ncdu) estalvia temps amb les ordres habituals com` du -sh * `.

- Per trobar quin socket o procés utilitza ample de banda, proveu [`iftop`] (http://www.ex-parrot.com/~pdw/iftop/) o [` nethogs`] (https://github.com) / raboof / nethogs).

- L'eina ʻab` (que ve amb Apache) és útil per comprovar ràpidament el rendiment del servidor web. Per a proves de càrrega més complexes, proveu "setge".

- Per a la depuració de la xarxa més seriosa, [`wireshark`] (https://wireshark.org/), [` tshark`] (https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) o [ `ngrep`] (http://ngrep.sourceforge.net/).

- Saber sobre `strace` i` ltrace`. Això pot ser útil si un programa està fallant, penjat o es bloqueja, i no sabeu per què, o si voleu tenir una idea general del rendiment. Tingueu en compte l’opció de perfilació (`-c`) i la possibilitat d’adjuntar-vos a un procés en execució (` -p`). Utilitzeu l’opció de traça fill (`-f`) per evitar que no es facin trucades importants.

- Coneixeu `ldd` per comprovar les biblioteques compartides, etc. - però [no el feu mai en fitxers no confiables] (http://www.catonmat.net/blog/ldd-arbitrary-code-execution/).

- Saber connectar-se a un procés en execució amb `gdb` i obtenir els seus rastres de pila.

- Utilitzeu `/ proc`. És increïblement útil de vegades en depurar problemes en viu. Exemples: `/ proc / cpuinfo`,` / proc / meminfo`, `/ proc / cmdline`,` / proc / xxx / cwd`, ​​`/ proc / xxx / exe`,` / proc / xxx / fd / ` , `/ proc / xxx / smaps` (on` xxx` és el identificador o pid del procés).

- En depurar per què alguna cosa va sortir malament en el passat, [`sar`] (http://sebastien.godard.pagesperso-orange.fr/) pot ser molt útil. Mostra estadístiques històriques sobre CPU, memòria, xarxa, etc.

- Per a anàlisis de rendiment i sistemes més profunds, mireu `stap` ([SystemTap] (https://sourceware.org/systemtap/wiki)), [` perf`] (https://en.wikipedia.org/wiki/ Perf_% 28Linux% 29) i [`sysdig`] (https://github.com/draios/sysdig).

- Comproveu què és el sistema operatiu amb `uname` o` uname -a` (informació general de Unix / nucli) o `lsb_release -a` (informació de distribució de Linux).

- Utilitzeu `dmesg` sempre que alguna cosa actuï realment divertit (podria ser problemes de maquinari o controladors)

- Si suprimiu un fitxer i no allibera l’espai de disc esperat, segons el que informa `du`, comproveu si el fitxer s’utilitza per un procés:
`lsof | grep eliminat | grep "nom de fitxer-del-meu-gran-fitxer" `


## One-liners

Alguns exemples d’ordenacions conjuntes:

- De vegades és molt útil que pugueu establir la intersecció, la unió i la diferència de fitxers de text a través de "sort" / "uniq". Suposem que "a" i "b" són fitxers de text que ja són únics. Això és ràpid i funciona amb fitxers de mida arbitrària, fins a molts gigabytes. (L’ordenació no està limitada per la memòria, encara que potser haureu d’utilitzar l’opció `-T` si` / tmp` està en una partició arrel petita.) opció u` (no es pot veure clarament a continuació).
`` `sh
      sort a b | uniq> c # c és una unió b
      sort a b | uniq -d> c # c és una intersecció b
      sort a b b | uniq -u> c # c es defineix la diferència a - b
`` `

- Utilitzeu `grep. * `per examinar ràpidament el contingut de tots els fitxers d’un directori (de manera que cada línia s’aparelli amb el nom del fitxer), o` head -100 *` (per tant, cada fitxer té un encapçalament). Això pot ser útil per a directoris plens de configuració de configuració com a `/ sys`,` / proc`, `/ etc`.


- S'està sumant tots els números a la tercera columna d’un fitxer de text (probablement 3X més ràpid i 3X menys codi que Python equivalent):
`` `sh
      awk '{x + = $ 3} END {print x}' myfile
`` `

- Per veure mides / dates en un arbre de fitxers, això és com un `ls -l` recursiu, però és més fàcil de llegir que` ls -lR ':
`` `sh
      trobar. -tipo f -ls
`` `

- Digueu que teniu un fitxer de text, com un registre del servidor web, i un determinat valor que apareix en algunes línies, com ara un paràmetre `acct_id 'que es troba a la URL. Si voleu comptabilitzar quantes sol·licituds per a cada "acct_id":
`` `sh
      egrep -o 'acct_id = [0-9] +' access.log | cut -d = -f2 | ordenar | uniq -c | sort -rn
`` `

- Per supervisar contínuament els canvis, utilitzeu `watch ', p. Ex. comproveu els canvis als fitxers en un directori amb `watch -d -n 2 'ls -rtlh | tail'` o als paràmetres de xarxa mentre solucioneu els vostres paràmetres de wifi amb `watch -d -n 2 ifconfig`.

- Executeu aquesta funció per obtenir un suggeriment aleatori d’aquest document (analitza Markdown i extreu un element):
`` `sh
      funció taocl () {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          sed '/cowsay[.]png/d' |
          pandoc -f marcatge -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html / body / ul / li [count (p)> 0]) [$ RANDOM mod last () + 1]" |
          xmlstarlet unesc | fmt -80 | iconv -t EUA
      }
`` `


## obscur però útil

- `expr`: realitzar operacions aritmètiques o booleanes o avaluar expressions regulars

- `m4`: processador de macros simple

- "sí": imprimiu moltes cadenes

- `cal`: bon calendari

- "env": executeu una ordre (útil en scripts)

- `printenv`: imprimeix variables d'entorn (útils en depuració i scripts)

- `look`: trobar paraules en anglès (o línies en un fitxer) que comencin per una cadena

- "tallar", "enganxar" i "unir": manipulació de dades

- `fmt`: formatar paràgrafs de text

- `pr`: formateu text en pàgines / columnes

- "fold": embolica les línies de text

- "column": formateu els camps de text en columnes o taules d’amplada fixa

- `expand` i` unexpand`: converteix entre pestanyes i espais

- `nl`: afegir números de línia

- `seq`: números d’impressió

- `bc`: calculadora

- `factor`: factor sencer

- [`gpg`] (https://gnupg.org/): xifra i signa fitxers

- "toe": taula de les entrades terminfo

- `nc`: depuració de xarxa i transferència de dades

- `socat`: transmissor de connexions socket i portador TCP (similar a` netcat »)

- [`slurm`] (https://github.com/mattthias/slurm): visualització del trànsit de xarxa

- `dd`: moure dades entre fitxers o dispositius

- `file`: identifica el tipus d’un fitxer

- `tree`: mostra directoris i subdirectoris com a arbre de nidificació; com `ls`, però recursiva

- `stat`: informació del fitxer

- "temps": executa i executa una ordre

- "timeout": executeu una ordre per a una quantitat de temps especificada i atureu el procés quan es completi la quantitat de temps especificada.

- `lockfile`: creeu un fitxer de semàfor que només es pot eliminar mitjançant` rm -f`

- `logrotate`: rotació, compressió i registres de correu.

- `watch`: executeu una ordre repetidament, mostrant resultats i / o canvis de ressaltat

- [`quan ha canviat"] (https://github.com/joh/when-changed): executa qualsevol ordre que especifiqueu sempre que vegi el fitxer canviat. Vegeu també "inotifywait" i "entr".

- `tac`: imprimeix fitxers al revés

- `comm`: compara els fitxers ordenats per línia

- `cadenes`: extreu el text dels fitxers binaris

- `tr`: traducció o manipulació de caràcters

- `iconv` o` uconv`: conversió per a codificacions de text

- "split" i "csplit": dividir fitxers

- "esponja": llegiu totes les entrades abans d’escriure-la, útil per a llegir des d’ara escrivint al mateix fitxer, per exemple, `grep -v alguna cosa algun fitxer | esponja d'algun arxiu

- "unitats": conversions i càlculs de les unitats; converteix furlongs per quinze dies a twips per blink (vegeu també `/ usr / share / units / definitions.units`)

- `apg`: genera contrasenyes aleatòries

- "xz": compressió de fitxers d'alta relació

- `ldd`: informació de la biblioteca dinàmica

- `nm`: símbols dels fitxers objecte

- `ab` o [` wrk`] (https://github.com/wg/wrk): servidors web de benchmarking

- `strace`: sistema de depuració de trucades

- [`mtr`] (http://www.bitwizard.nl/mtr/): millor traceroute per a la depuració de la xarxa

- `cssh`: shell concurrent visual

- `rsync`: sincronitza fitxers i carpetes a través de SSH o en un sistema de fitxers local

- [`wireshark`] (https://wireshark.org/) i [` tshark`] (https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): captura de paquets i depuració de xarxa

- [`ngrep`] (http://ngrep.sourceforge.net/): grep per a la capa de xarxa

- "host" i "dig": cerques de DNS

- `lsof`: informació de descriptor i socket de procés

- `dstat`: estadístiques útils del sistema

- [`mirades '] (https://github.com/nicolargo/glances): visió general de nivell alt i de múltiples subsistemes

- "iostat": estadístiques d'ús del disc

- `mpstat`: estadístiques d’ús de la CPU

- `vmstat`: estadístiques d’ús de memòria

- `htop`: versió millorada de la part superior

- "last": login history

- `w`: qui ha iniciat la sessió

- `id`: informació d'identitat d'usuari / grup

- [`sar`] (http://sebastien.godard.pagesperso-orange.fr/): estadístiques del sistema històric

- [`iftop`] (http://www.ex-parrot.com/~pdw/iftop/) o [` nethogs`] (https://github.com/raboof/nethogs): utilització de la xarxa per socket o procés

- `ss`: estadístiques de socket

- `dmesg`: missatges d’arrencada i d’error del sistema

- `sysctl`: visualitzeu i configureu els paràmetres del nucli Linux en temps d'execució

- `hdparm`: manipulació / rendiment del disc SATA / ATA

- `lsblk`: llista dispositius de bloc: una vista d’arbre dels vostres discs i particions de disc

- "lshw", "lscpu", "lspci", "lsusb", "dmidecode": informació de maquinari, incloses CPU, BIOS, RAID, gràfics, dispositius, etc.

- `lsmod` i` modinfo`: llistar i mostrar els detalls dels mòduls del nucli.

- "fortuna", "ddate" i "sl": um, bé, depèn de si considereu que les locomotores de vapor i les cites de zippy "són útils"


## només MacOS

Són articles rellevants * només * a macOS.

- Gestió de paquets amb `brew` (Homebrew) i / o` port` (MacPorts). Es poden utilitzar per instal·lar en macOS moltes de les ordres anteriors.

- Copieu la sortida de qualsevol ordre a una aplicació d’escriptori amb `pbcopy` i enganxeu una entrada d’una amb` pbpaste`.

- Per habilitar la clau d’opció de la terminal de macOS com a tecla alt (com ara les ordres anteriors com ** alt-b **, ** alt-f **, etc.), obriu Preferències -> Perfils -> Teclat i seleccioneu "Utilitza l'opció com a tecla Meta".

- Per obrir un fitxer amb una aplicació d'escriptori, utilitzeu `open 'o` open -a / Applications / Whatever.app`.

- Spotlight: cerca fitxers amb `mdfind` i llista de metadades (com ara informació EXIF ​​de fotos) amb` mdls`.

- Tingueu en compte que MacOS es basa en BSD Unix i moltes ordres (per exemple, "ps", "ls", "tail", "awk", "sed") tenen moltes variacions subtils de Linux, que estan en gran part influïdes per System V eines Unix i GNU en estil. Sovint es pot dir la diferència notant una pàgina de manual amb el títol "Manual de comandaments generals de BSD". En alguns casos, també es poden instal·lar versions GNU (com ara "gawk" i "gsed" per a GNU awk i sed). Si escriviu scripts de Bash multiplataforma, eviteu aquestes ordres (per exemple, penseu en Python o `perl`) o proveu acuradament.

- Per obtenir informació sobre la publicació de macOS, utilitzeu `sw_vers '.

## Només Windows

Aquests elements només són rellevants * a Windows.

### Formes d'obtenir eines Unix a Windows

- Accediu a la potència del shell Unix a Microsoft Windows instal·lant [Cygwin] (https://cygwin.com/). La majoria de les coses que es descriuen en aquest document s’aplicaran a la caixa.

- A Windows 10, podeu utilitzar [Subsistema de Windows per a Linux (WSL)] (https://msdn.microsoft.com/commandline/wsl/about), que proporciona un entorn familiar de Bash amb utilitats de línia d'ordres Unix.

- Si voleu utilitzar principalment les eines de desenvolupament de GNU (com ara GCC) a Windows, penseu a [MinGW] (http://www.mingw.org/) i al seu [MSYS] (http://www.mingw.org/) wiki / msys), que proporciona utilitats com bash, gawk, make i grep. MSYS no té totes les funcions en comparació amb Cygwin. MinGW és especialment útil per a la creació de ports Windows originals d’eines Unix.

- Una altra opció per aconseguir que Unix aparegui sota Windows sigui [Efectiu] (https://github.com/dthree/cash). Tingueu en compte que només hi ha poques ordres i opcions de línia d’ordres Unix disponibles en aquest entorn.

### Útils eines de línia d'ordres de Windows

- Podeu executar i escriure la majoria de les tasques d'administració del sistema de Windows des de la línia de comandes aprenent i utilitzant `wmic`.

- Les eines natives de xarxes de Windows de la línia de comandes que us poden resultar útils inclouen `ping`,` ipconfig`, `tracert` i` netstat`.

- Podeu realitzar [moltes tasques útils de Windows] (http://www.thewindowsclub.com/rundll32-shortcut-commands-windows) invocant l’ordre `Rundll32`.

### Consells i trucs de Cygwin

- Instal·leu programes Unix addicionals amb el gestor de paquets de Cygwin.

- Utilitzeu "mintty" com a finestra de la línia d’ordres.

- Accedir al porta-retalls de Windows a través de `/ dev / clipboard`.

- Executeu `cygstart` per obrir un fitxer arbitrari a través de la seva aplicació registrada.

- Accediu al registre de Windows amb "regtool".

- Tingueu en compte que un camí de la unitat de Windows `C: 'es converteix en` / cygdrive / c` sota Cygwin i que `/` de Cygwin apareix sota `C: cgwin` a Windows. Converteix entre Cygwin i camins de fitxers d’estil de Windows amb `cygpath`. Això és molt útil en scripts que criden als programes de Windows.

## Més recursos

- [awesome-shell] (https://github.com/alebcay/awesome-shell): una llista de recursos i eines de shell.
- [impressionant línia d'ordres-osx] (https://github.com/herrbischoff/awesome-osx-command-line): una guia més detallada per a la línia d'ordres del macOS.
- [Mode estricte] (http://redsymbol.net/articles/unofficial-bash-strict-mode/) per escriure millors scripts de shell.
- [shellcheck] (https://github.com/koalaman/shellcheck): una eina d'anàlisi estàtica d'un script de shell. Essencialment, pèls per bash / sh / zsh.
- [Noms de fitxers i noms de ruta a Shell] (http://www.dwheeler.com/essays/filenames-in-shell.html): Les minúcies tristament complexes sobre com gestionar els noms de fitxer correctament en scripts de shell.
- [Data Science a la línia d'ordres] (http://datascienceatthecommandline.com/#tools): més comandes i eines útils per fer ciències de dades, a partir del llibre del mateix nom

## Disclaimer

Amb l'excepció de tasques molt petites, el codi s'escriu perquè els altres la puguin llegir. Amb el poder ve la responsabilitat. El fet que * pugueu fer alguna cosa a Bash no significa necessàriament que hagueu de fer alguna cosa a Bash. ;)


## Llicència

[! [Llicència Creative Commons] (https://i.creativecommons.org/l/by-sa/4.0/88x31.png)] (http://creativecommons.org/licenses/by-sa/4.0/)

Aquest treball està sota llicència sota una [Llicència internacional de Reconeixement-CompartirIgual 4.0 de Creative Commons] (http://creativecommons.org/licenses/by-sa/4.0/).
