# icinga2
Useful Icinga2 commands and conf

Installation
Auf meinem Debian 10 System habe ich mir ein eigenes Verzeichnis zurecht gelegt, in dem ich via git clone das oben verlinkte Github Repo von Centreon kopiere. Updates mit git pull kann man in der Regel gefahrlos machen.

Wie ergründet man nun den Aufbau der einzelnen Befehle? Centreon bietet auf Kommandozeilenebene ein schönes Schema an, mit dem man sofort herausfinden kann, was jeder Befehl kann und welche Monitoringmöglichkeiten es gibt. Um zu herauszufinden, was alles möglich ist, folgenden Befehl verwenden:

1
perl centreon_plugins.pl --list-plugin | grep aws
Die Suche mittels grep ist hier case sensitive. Wenn man nun ein Plugin gefunden hat, kann man sich die verschiedenen Module fürs Monitoring anzeigen lassen – z.B.:

1
perl centreon_plugins.pl --plugin=cloud::aws::billing::plugin --list-mode
Im vorliegenden Beispiel braucht man zur genauen Untersuchung eines Moduls des AWS Billing Plugins die Custommode Definition, die festlegt, wie genau die Daten abgegriffen werden:

1
perl centreon_plugins.pl --plugin=cloud::aws::billing::plugin --mode=estimated-charges --list-custommode
Um nun die komplette Hilfe zum Modul estimated charges aufrufen zu können, braucht es diesen Befehl:

1
perl centreon_plugins.pl --plugin=cloud::aws::billing::plugin --mode=estimated-charges --custommode=awscli --help
Da es immer wieder vorkommt, dass im Betriebssystem bestimmte Perl Module beim Aufruf des Help-Befehls fehlen, müssen diese nachinstalliert werden. In der Regel sind die fehlenden Perl Module über apt-cache search perl json z.B. leicht zu finden.