---
layout: default
---

Il seguente documento fornisce le istruzioni necessarie per installare gli strumenti di sviluppo utilizzati nel contesto del corso di Programmazione ad Oggetti.
La guida presenta le procedure di installazione e configurazione su Linux (varie distribuzioni), MacOS X e Windows del **Java Development Kit** (JDK) e dell'ambiente di sviluppo integrato **Eclipse**.

# Java Development Kit (JDK)

Il JDK è l'insieme degli strumenti necessari a sviluppare software standard in Java.
Include la virtual machine Java, le librerie Java, di base, il compilatore, e i tool di contorno.

Esistono varie versioni del JDK, quella di riferimento è OpenJDK, a partire dalla quale ne vengono sviluppate altre sia gratuite che a pagamento (fra cui [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html), [Eclipse OpenJ9](https://www.eclipse.org/openj9/), [Amazon Corretto](https://aws.amazon.com/corretto/), [GraalVM](https://www.graalvm.org/), [Bellsoft Liberica JDK](https://bell-sw.com/), [Azul Zulu](https://www.azul.com/downloads/zulu-community/?&show-old-builds=true)...).

A sua volta, OpenJDK è distribuito in forma di sorgente, e vari distributori ne forniscono versioni binarie.
Fra questi, [AdoptOpenJDK](https://adoptopenjdk.net/) (recentemente diventato [Adoptium](https://adoptium.net/)).
La macchina virtuale Java di riferimento sarà OpenJDK 11 come fornita da AdoptOpenJDK.

Seguono le istruzioni di installazione e configuazione per i vari sistemi operativi.

**NOTA**: Qualora il sistema operativo non consentisse di installare il JDK attraverso Jabba o se durante l'installazione via Jabba dovessero emergere problematiche di qualunque genere, procedere con l'installazione alternativa, proposta più avanti in questo documento. In particolare, nonostante Jabba sia compatibile con Windows 10, con le ultime versioni l'installazione presenta alcuni bug e dunque non è consigliata: si preferisca l'installazione alternative attraverso file `.msi` descritta più avanti.

## Installazione su distribuzioni Linux e MacOS via Jabba

Data la varietà di versioni, distribuzioni sorgenti, e distribuzioni binarie di JVM, esiste un tool Linux che consente di installare quella desiderata e cambiarla rapidamente.
Il tool è [Jabba](https://github.com/shyiko/jabba).

Per installare Jabba su Linux o Mac OS X, si lanci il seguente comando da terminale:

{% highlight bash %}
curl -sL https://github.com/shyiko/jabba/raw/master/install.sh | bash && . ~/.jabba/jabba.sh
{% endhighlight %}

Una volta che Jabba è installato, può essere utilizzato per installare il JDK.
Si elenchino tutte le versioni di AdoptOpenJDK utilizzando

{% highlight bash %}
jabba ls-remote adopt@
{% endhighlight %}

Quindi si selezioni la più recente fra le versioni 11, ad esempio se l'output è:

{% highlight bash %}
adopt@1.12.33-0
adopt@1.12.0-2
adopt@1.12.0-1
adopt@1.11.28-0
adopt@1.11.0-4
adopt@1.11.0-3
adopt@1.11.0-2
adopt@1.11.0-1
adopt@1.10.0-2
adopt@1.9.181-0
adopt@1.9.0-4
adopt@1.8.222-10
adopt@1.8.212-04
adopt@1.8.212-03
adopt@1.8.202-08
adopt@1.8.192-12
adopt@1.8.181-13
adopt@1.8.172-11
{% endhighlight %}

Si scelga `adopt@1.11.28-0`.
A questo punto si installi utilizzando i seguenti comandi:

{% highlight bash %}
jabba install adopt@1.11.28-0
jabba use adopt@1.11.28-0
{% endhighlight %}

### Windows (tramite installer `.msi`)

I passi in comune a tutte le versioni di Windows sono i seguenti (di seguito si fa riferimento a Windows 10, analogamente per le versioni precedenti con eventuali variazioni in termini di interfaccia utente):

1. Scaricare il JDK dalla [pagina di download ufficiale di Adoptium][Adoptium download page].
   Scegliere la versione OpenJDK 11 (LTS) e cliccare sul pulsante "Latest release".
   
   ![Missing image](img/win10/adopt1.png)
   
2. Eseguire l'installer scaricato e seguire il wizard di installazione passo-passo.

   ![Missing image](img/win10/adopt2.png)

   Nella schermata dell'installer sopra riportata è possibile optare per la configurazione automatica delle variabili d'ambiente (si suggerisce di spuntare tutte le opzioni e procedere con l'installazione.
   In questo caso, terminata l'installazione passare direttamente al punto 4)

3. Configurazione delle variabili d'ambiente (come riportato di seguito, se necessario).

4. (Dopo aver configurato le variabili d'ambiente, se necessario)
   Aprire un prompt dei comandi per verificare l'esito positivo dello step precedente (per aprire il prompt dei comandi è sufficente cercare `cmd.exe` nel menù di Start):

5. Verificare l'avvenuta installazione eseguendo i seguenti due comandi su un prompt dei comandi:
    {% highlight bash %}
    javac -version  # Output atteso: 'javac <version>'
    java -version   # Output atteso: 'java version "<version>" ...'
    {% endhighlight %}

## Installazione alternativa su specifici OS

### Arch e derivate (Manjaro, Bridge…)

Arch offre il pacchetto OpenJDK 11 direttamente nel repository principale:

{% highlight bash %}
sudo pacman -S jdk11-openjdk
{% endhighlight %}

È possibile avere più ambienti Java installati contemporaneamente, si può selezionare quello corrente utilizzando il comando ``archlinux-java``.
Per assicurarsi di star lavorando con OpenJDK 11, si utilizzi:

{% highlight bash %}
sudo archlinux-java set java-11-openjdk
{% endhighlight %}

### Windows (tramite package manager)

Su Windows sono disponibli diversi pacakge manager non ufficiali o semi-ufficiali che permettono l'installazione di distribuzioni OpenJDK.

#### Opzione 1: Chocolatey

Se sulla macchina [è installato Chocolatey](https://chocolatey.org/docs/installation), è possibile installare AdoptOpenJDK 11 Hotspot eseguendo il seguente comando su un terminale con permessi di amministratore:

{% highlight powershell %}
choco install adoptopenjdk11
{% endhighlight %}

L'installazione dovrebbe eseguire una configurazione automatica delle variabili d'ambiente.

#### Opzione 2: Scoop

Se sulla macchina [è installato Scoop](https://scoop.sh), è possibile installare AdoptOpenJDK 11 Hotspot eseguendo il seguente comando su un terminale:

{% highlight powershell %}
scoop bucket add java

scoop install adoptopenjdk-lts-hotspot
{% endhighlight %}

Non è necessario utilizzare un terminale con permessi di amministratore.
L'installazione dovrebbe eseguire una configurazione automatica delle variabili d'ambiente.

#### Opzione 3: Jabba

**Nota**: le ultime versioni presentano alcuni bug nell'installazione e dunque questa soluzione non è consigliata

Per installare Jabba su Windows 10, si lanci il seguente comando su un terminale Powershell:

{% highlight powershell %}
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Invoke-Expression (
  Invoke-WebRequest https://github.com/shyiko/jabba/raw/master/install.ps1 -UseBasicParsing
).Content
{% endhighlight %}

A questo punto si installi utilizzando i seguenti comandi:

{% highlight bash %}
jabba install adopt@1.11.28-0
jabba use adopt@1.11.28-0
{% endhighlight %}

## Impostazione delle variabli d'ambiente

### Linux con installazione da package manager

Operazione non necessaria.

### Linux con installazione via Jabba, Mac OS X

Per impostare una versione di default del JDK da usare (senza dover ogni volta utilizzare `jabba use`) all'apertura di un nuovo terminale, si usi il seguente comando:

{% highlight bash %}
jabba alias default <default-version>
{% endhighlight %}

Infatti, all'installazione, Jabba modifica file nella `$HOME` come`.bashrc`, `.bash_profile`, o `.zshrc` per chiamare `$HOME/.jabba/jabba.sh`; in quest'ultimo script, un comando `jabba use default` viene invocato: l'effetto è che all'apertura di un nuovo terminale, verrà automaticamente indicato di usare la versione di default del JDK indicata con Jabba.

### Windows

Jabba installa il JDK desiderato in una cartella dedicata nella user home dell'utente, ovvero: `%HOMEPATH%\.jabba\jdk\<version>`.
È necessario quindi definire una variabile d'ambiente (`JAVA_HOME`) relativa a tale percorso ed includerla nel `Path` di sistema, come segue (si fa riferimento a Windows 10, per versioni precedenti la procedura è analoga).

1. Aprire il menù d'avvio e digitare __"Modifica variabili d'ambiente relative al sistema"__:

   ![Missing image](img/win10/env_vars/1.png)

2. Cliccando su __Apri__ Si aprirà la finestra "Proprietà del sistema":

   ![Missing image](img/win10/env_vars/2.png "System Properties")

   dalla quale sarà necessario cliccare sul bottone __Variabili d'ambiente__.

3. Si aprirà la finestra di dialogo __"Variabili d'ambiente"__.

   Cliccando poi sul pulsante __"Nuova"__ (_quello più in basso, relativo alle variabili d'ambiente di sistema_)

   ![Missing image](img/win10/env_vars/3.png "Envarionment Variables")

4. Creare la variabile denonimata __"JAVA_HOME"__ con uno dei valori seguenti e cliccare sul pulsante __"OK"__:

   - `%HOMEPATH%\.jabba\jdk\<version>` se si è utilizzato Jabba;
   - `C:\Program Files\AdoptOpenJDK\jdk-<version>-hotspot` se si è utilizzato l'installer di AdoptOpenJDK;

   ![Missing image](img/win10/env_vars/5.png "Creating JAVA_HOME")

   - __Nota bene__: il percorso specifico del JDK potrebbe variare da quelli qui descritti in caso di installazioni personalizzate.

5. Tornando alla schermata __"Variabili d'ambiente"__, modificare la variabile `Path` (_quella più in basso!_), cliccando sul pulsante __"Modifica"__.

6. Alla lista di percorsi che apparirà, aggingere la voce `%JAVA_HOME%\bin`:

   ![Missing image](img/win10/env_vars/6.png)

7. Premere su __"OK"__ su tutte le finestre sin qui aperte per confermare le modifiche.

8. Fatto!
   Verificare la corretta installazione del JDK eseguendo __entrambi__ i comandi `javac -version` e `java -version` dal prompt dei comandi.

## Verifica del funzionamento

Al fine di testare l'esecuzione, si chiuda il terminale, si apra un nuovo terminale, e si eseguano i comandi:

{% highlight bash %}
java -version
javac -version
{% endhighlight %}

e si osservi il risultato. L'output atteso dovrà essere analogo a:

{% highlight bash %}
$ java -version
openjdk version "11" 2018-09-25
OpenJDK Runtime Environment AdoptOpenJDK (build 11+28)
OpenJDK 64-Bit Server VM AdoptOpenJDK (build 11+28, mixed mode)

$ javac -version
javac 11
{% endhighlight %}

Si noti, in particolare, la versione 11, ed il provider AdoptOpenJDK.

# Eclipse

## Arch Linux e derivate (Manjaro, Bridge, SteamOS...)

Si consiglia l'utilizzo della versione manutenuta nel repository
[Chaotic AUR](https://aur.chaotic.cx/).

Si utilizzino i seguenti comandi:

```bash
# Download the Chaotic-AUR key
sudo pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com
# Trust the key
sudo pacman-key --lsign-key 3056513887B78AEB
# Force-install the whole Chaotic Keyring
sudo pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst'
# Add the repository to the pacman configuration file
echo '' | sudo tee -a /etc/pacman.conf
echo '[chaotic-aur]' | sudo tee -a /etc/pacman.conf
echo 'Include = /etc/pacman.d/chaotic-mirrorlist' | sudo tee -a /etc/pacman.conf
# Refresh the database
sudo pacman -Sy
# Install Eclipse
sudo pacman -S eclipse-java
```

## Tutti gli altri sistemi operativi

1. Scaricare “Eclipse IDE” (ultima versione disponibile) dalla [pagina di download ufficiale (qui)][Eclipse Download].
2. Seguire le istruzioni per l'installazione, selezionando "Eclipse IDE for Java Developers".
3. Si lanci l'IDE: se l’installazione è andata a buon fine si dovrebbe aprire la schermata di benvenuto dell'IDE.

![Missing image](img/win10/install_eclipse/download/6.png)

# Plugin di Eclipse

Eclipse utilizza un'architettura a plug-in. Lungo il corso ne utilizzeremo alcuni che ci forniranno funzionalità aggiuntive.

## Installazione rapida su Linux (e sistemi operativi dove il comando `eclipse` è disponibile su terminale)

Se il vostro sistema (tipicamente tutti i sistemi Linux) risponde al lancio da terminale del comando `eclipse`
avviando l'interfaccia grafica dell'IDE, allora potete optare per installare tutto il necessario direttamente da terminale col comando:

```bash
eclipse -nosplash -application org.eclipse.equinox.p2.director\
 -repository http://download.eclipse.org/releases/2020-12/,\
http://download.eclipse.org/releases/2021-03/,\
http://download.eclipse.org/releases/2021-06/,\
http://www.acanda.ch/eclipse-pmd/release/latest/,\
https://checkstyle.org/eclipse-cs-update-site/,\
https://spotbugs.github.io/eclipse/\
 -installIU ch.acanda.eclipse.pmd.feature.feature.group,\
net.sf.eclipsecs.feature.group,\
com.github.spotbugs.plugin.eclipse.feature.group
```

## SpotBugs (precedentemente noto come FindBugs)
* In Eclipse, click Help -> Eclipse Marketplace...

![Missing image](img/win10/install_eclipse/install_plugins_marketplace/1.png)

* Nella barra di ricerca, inserire "spotbugs", quindi premere Invio
* Uno dei plugin trovati dovrebbe essere "SpotBugs Eclipse Plugin", si usi l'immagine seguente per verificare che corrisponda:

![Missing image](img/eclipse/spotbugs.png)

* clickare su `"Install Now >"`
* Seguire le istruzioni, accettare la licenza, attendere che Eclipse scarichi ed installi il prodotti, accettare l'installazione e riavviare l'IDE.

## PMD
* In Eclipse, click Help -> Eclipse Marketplace...

![Missing image](img/win10/install_eclipse/install_plugins_marketplace/1.png)

* Nella barra di ricerca, inserire "pmd", quindi premere Invio
* Appariranno più plugin, uno dei plugin trovati dovrebbe essere eclipse-pmd. *ATTENZIONE:* I diversi plugin PMD *confliggono fra loro*, installare solo quello suggerito. Lo si identifichi utilizzando l'immagine seguente:

![Missing image](img/eclipse/pmd.png)

* clickare su `"Install Now >"`
* Seguire le istruzioni, accettare la licenza, attendere che Eclipse scarichi ed installi il prodotti, accettare l'installazione e riavviare l'IDE.

## Checkstyle
* In Eclipse, click Help -> Eclipse Marketplace...

![Missing image](img/win10/install_eclipse/install_plugins_marketplace/1.png)

* Nella barra di ricerca, inserire "checkstyle", quindi premere Invio
* Appariranno più plugin, uno dei plugin trovati dovrebbe essere "Checkstyle Plug-in X.Y.Z" (con X.Y.Z numero di versione). Lo si identifichi utilizzando l'immagine seguente:

![Missing image](img/eclipse/checkstyle.png)

* clickare su `"Install Now >"`
* Seguire le istruzioni, accettare la licenza, attendere che Eclipse scarichi ed installi il prodotti, accettare l'installazione e riavviare l'IDE.

# Git

Git è un decentralized version control system (DVCS), che consente di tenere traccia della storia di un progetto, versionarla, tornare allo stato precedente, e lavorare in parallelo.

Al termine del processo di installazione, per verificarne la correttezza, è possibile eseguire da shell il comando: ``git``, accertandosi che l’output prodotto sia del tipo:

{% highlight bash %}
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
{% endhighlight %}

## Linux

Git è preinstallato in molte distribuzioni.
Si raccomanda quindi di testare se sia già presente eseguendo `git` su terminale prima di partire con l'eventuale installazione.
Se già presente, ovviamente, non occorre intraprendere alcuna azione.

Se non fosse installato, è di norma installabile dal package manager.
Le istruzioni per tutte le distribuzioni più comuni [sono disponibili qui](https://git-scm.com/download/linux).

## Windows
1. Scaricare “GIT for Windows” (nella versione specifica per la propria architettura x86 o x64) dalla [pagina di download ufficiale][GIT-Windows Download].
2. Eseguire il programma di installazione
    * Accettare la licenza > Next > Next > Next > Next
    * Selezionare come editor di testo uno tra:
        * "Use the nano editor by default"
        * "Use Notepad++ as Git's default editor" (se Notepad++ non è già presente, richiede di installarlo prima di poter proseguire con l'installazione di git)
    * Premere Next > Next > Next
    * Selezionare "Checkout as-is, commit as-is" quindi Next
    * Accettare le successive opzioni proposte dall'installer > Install > Finish
3. Verificare la correttezza dell'installazione
    * Aprire il prompt dei comandi (`cmd.exe`)
    * Se il tool è stato installato correttamente, digitando il comando `git` apparirà l'help relativo al comando stesso

## Mac OS X
1. Scaricare l'installer di Git per OS X dalla [pagina di download ufficiale][GIT-OSX Download]
2. Eseguire il programma per l'installazione
    * Eventualmente, eseguire l'installer anche se non sviluppato da una fonte identificata da Apple Store (vedi System preferences > Security > General)
    * Continue > Install
3. Verificare la correttezza dell'installazione
    * Aprire una shell
    * Eseguire il comando `git`: se l'installazione è andata a buon fine, apparirà il menu di help per il comando

# Docker

Docker si appoggia al kernel linux per l'esecuzione di container.

L'engine Docker può essere installato nativamente sulle distribuzioni Linux, mentre su Windows e MacOS è suggerita l'installazione tramite Docker Desktop.

## Installare Docker Engine su Linux

### Installare automaticamente Docker Engine su Linux tramite [`docker-install`](https://github.com/docker/docker-install)

Per semplificare l'installazione di Docker su distribuzioni Linux supportate, Docker mette a disposizione uno script per l'installazione veloce.

Aprire un terminale ed eseguire:

{% highlight bash %}
curl -sSL https://get.docker.com | sh
{% endhighlight %}

Al termine dell'esecuzione Docker Engine sarà installato correttamente.

### Configurazioni aggiuntive per Linux

Su Linux, è necessario abilitare il servizio `docker.service` manualmente con:

{% highlight bash %}
sudo systemctl start docker.service
sudo systemctl enable docker.service
{% endhighlight %}

Inoltre, se si desidera utilizzare `docker` come utente non-`root`, aggiungere il proprio utente al gruppo `docker` col seguente comando:

{% highlight bash %}
sudo usermod -aG docker $USER
{% endhighlight %}

### Installare Docker Engine manualmente su Arch Linux e derivate (Manjaro, Bridge...)

Il pacchetto `docker` è disponibile nei repository Arch e può essere installato con:

{% highlight bash %}
sudo pacman -S docker
{% endhighlight %}

### Installare Docker Engine manualmente su Debian 9 e 10

Assicurarsi che i pacchetti necessari siano installati con:

{% highlight bash %}
sudo apt-get update

sudo apt-get install \
   apt-transport-https \
   ca-certificates \
   curl \
   gnupg-agent \
   software-properties-common
{% endhighlight %}

Fatto ciò, aggiungere la chiave GPG utilizzata dal repository Docker e poi aggiungerlo:

{% highlight bash %}
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
{% endhighlight %}

Infine, aggiornare l'indice dei pacchetti di `apt` e installare `docker-ce`

{% highlight bash %}
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io
{% endhighlight %}

### Installare Docker Engine manualmente su Ubuntu 16.04, 18.04 e 20.04

Assicurarsi che i pacchetti necessari siano installati con:

{% highlight bash %}
sudo apt-get update

sudo apt-get install \
   apt-transport-https \
   ca-certificates \
   curl \
   gnupg-agent \
   software-properties-common
{% endhighlight %}

Fatto ciò, aggiungere la chiave GPG utilizzata dal repository Docker e poi aggiungerlo:

{% highlight bash %}
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
{% endhighlight %}

Infine, aggiornare l'indice dei pacchetti di `apt` e installare `docker-ce`

{% highlight bash %}
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io
{% endhighlight %}

## Installare Docker Desktop su MacOS

Seguendo la [documentazione ufficiale](https://docs.docker.com/docker-for-mac/install/), scaricare il file [`Docker.dmg`](https://download.docker.com/mac/stable/Docker.dmg) dal [Docker Hub](https://hub.docker.com/editions/community/docker-ce-desktop-mac/) ed effettuare l'installazione guidata.

## Installare la macchina virtuale basata su Docker per il laboratorio

### Su Linux e MacOS X

- Eseguire in un terminale:

  {% highlight bash %}
  docker pull danysk/linux-didattica
  {% endhighlight %}

  Questo scaricherà l'immagine Docker localmente; potrebbe richiedere molto tempo.

- Lanciare l'immagine con il seguente comando:

  {% highlight bash %}
  docker run --rm --net=host --env="DISPLAY" -v <WHERE_TO_LOCALLY_PERSIST>:/home/user --volume="$HOME/.Xauthority:/.Xauthority:rw" -it danysk/linux-didattica
  {% endhighlight %}

  Sostituire `<WHERE_TO_LOCALLY_PERSIST>` con il percorso alla cartella sulla quale i dati di lavoro dovranno essere salvati.

### Su Windows

Installare l'immagine come distribuzione WSL2, in modo da non dover appoggiarsi su Docker (che in ogni caso si sarebbe appoggiato su WSL2). Per farlo, si seguano [le istruzioni fornite nel repository che contiene il codice dell'immagine](https://github.com/DanySK/docker-linux-didattica/#import-as-a-wsl2-distro)

[JDK download page]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Adopt JDK download page]: https://adoptopenjdk.net/index.html?variant=openjdk11&jvmVariant=hotspot
[Adoptium download page]: https://adoptium.net/
[Eclipse Download]: https://www.eclipse.org/downloads/
[GIT-Windows Download]: https://git-for-windows.github.io/
[GIT-OSX Download]: http://git-scm.com/download/mac

# IDE C# #

## Visual Studio 2019 su Windows

Si consiglia di seguire la guida ufficiale: [https://docs.microsoft.com/it-it/visualstudio/install/install-visual-studio?view=vs-2019](https://docs.microsoft.com/it-it/visualstudio/install/install-visual-studio?view=vs-2019)

**N.B.**
Per il punto 4 della guida assicurarsi che sia selezionata la voce *Sviluppo per desktop .NET*, le restanti voci non sono richieste per questo corso, come nell'immagine seguente

![](./img/VisualStudio/win-workload.png)

I punti 5, 6 e 7 sono facoltativi, ma se si vogliono apportare modifiche è preferibile farlo prima di proseguire con l'installazione

## Visual Studio 2019 su MacOS

Si consiglia di seguire la guida ufficiale: [https://docs.microsoft.com/it-it/visualstudio/mac/installation?view=vsmac-2019](https://docs.microsoft.com/it-it/visualstudio/mac/installation?view=vsmac-2019)

**N.B.**
Arrivati al punto 6 assicurarsi che la voce *.NET Core* sia selezionata, le restanti voci non sono richieste per questo corso.

## JetBrains Rider su tutti i sistemi operativi

Operazione preliminare **da fare:** installare *.NET Core 3.1* (se non già presente sul pc) seguendo la guida ufficiale: [https://dotnet.microsoft.com/download](https://dotnet.microsoft.com/download).

Per l'installazione di *JetBrains Rider* si rimanda alla guida ufficiale: [https://www.jetbrains.com/help/rider/Installation_guide.html](https://www.jetbrains.com/help/rider/Installation_guide.html).
