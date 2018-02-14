---
layout: post
title:  Wie man mit oauth in Perl autentifiziert (Dancer, GitHub, LWP::UserAgent)
tags:
- perl
- web-dev
---

In letzter Zeit habe ich viel mit Perl herumgespielt und nachdem ich letztens mit Catalyst herumgebastelt habe, habe ich mich Dancer gewidmet.

Für Dancer gibt es dieses [nette Tutorial][1] mit einer [einfachen Dummy-Blog-Anwendung. Die App ist auf GitHub hier verfügbar][2]. Es beschreibt wirklich einige Aspekte von Danver, inklusive sessions, routes, Speicherung und Seitenanzeite.

Es ein übersichtliches kleines Beispiel in dem es nur einige wenige Dateien gibt.

Natürlich wollte ich mir die Hände schmutzig machen und die OAuth-Authentifizierung mit github ausprobieren und implementierenOAuth authentication. Ich meine damit narülich nicht ein hübsches CPAN Modul aus dem Hut zaubern (gibt's hier nicht) sondern den ganze OAuth-Ablauf selbst schreiben. Zum Glück hat sich das als eine ziemlich einfache Aufgabe herausgestellt.

Ich habe es hinbekommen, dass die Authentifizierung der Beispiel-Dancer-App sich bei github einloggt. [Ich habe das in ein forked project hinzugefügt.][3]

Das werde ich im Folgenden beschreiben:

* Benutze [LWP::UserAgent][4] um einen request (Anfrage) an github zu stellen
* Benutze [JSON::Parse][5] um die response (Antwort) von GitHub einzusammeln
* Setze ein session object auf die Username- und Avatar-img url und benutze diese auf der masterpage (main.tt).

Jetzt kann man die forked project Dateien (Abspaltung) sehen. Ich habe einfach die [dancr.pl][6] und [main.tt][7] geändert. Außerdem habe ich die `login.tt` entfernt, da sie nicht weiter benötigt wird. Dann muss die [Applikation zu github hinzugefügt][8] werden und man bekommt eine "client id" (Klienten-ID) und ein "client secret" (Klientengeheimnis).

### Schritt 1:
Um sich einzuloggen muss man eine Weiterleitung auf "https://github.com/login/oauth/authorize" mit den folgenden Parametern setzen: `YOUR CLIENT ID` ("Deine Klienten-ID"), `redirect url` ("Weiterleitungs-URL"), `scope` ("Bereich", dies beschreibt die permissions (Genehmigungen), die man zuweisen möchte) und zu guter Letzt `state`(Zustand), der dazu genutzt wird um [Cross-Site Request Forgery Attacks ("Siteübergreifende Aufruf-Manipulation")][9] zu verhindern.

				#oben auf // on the top
				my $client_id = "YOUR CLIENT ID HERE";
				my $client_secret = "YOUR SECRET ID HERE";

				#route to login
				get '/login' => sub {
				  #Umleitung des Benutzers auf die githubs login/authorize-Seite
				  #//XX ask gideon // we pass in a silly state (x12) ideally this should be generated
				  redirect "https://github.com/login/oauth/authorize?&client_id=$client_id&state=x12";
				};

Obendrauf habe ich zwei Variablen hinzugefügt und die login route ("Loginroutine") hat sich verändert, so dass die Benutzer auf githubs Login-Page umgeleitet werden. Wenn der Benutzer es der App gestattet, stellt github der App einen speziellen Code ausstellen, indem sie deine **callback url** (Rückruf-URL) aufruft.
// XX ask gideon about the original meaning of the sentence


### Schritt 2 :
 Gehe zu deiner `Github > Account Settings (Benutzereinstellungen) -> Applications (Anwendungen) -> Your App (Deine App) -> Callback Url (Rückruf-URL)`. 
 **Anmerkung** Man kann das auf den localhost byt setzen, indem man es folgendermaßen spezifiziert `127.0.0.1:<SOMEPORT>`. Ich habe die URL auf `/auth/github/callback` gesetzt. In meiner `dancr.pl` habe ich diese Route hinzugefügt und ich hoffe die Kommentare bieten dafür eine gute Erklärung:

is route, hopefully the comments should be a good explanation:
			get '/auth/github/callback' => sub {
				#github sendet uns einen Code zum authentifizieren. Jetzt muessen wir es abrufen
					my $code = params->{'code'};
					#erstelle eine neue Instanz von LWP:UserAgent
				my $browser = LWP::UserAgent->new;
				#sende einen post request fuer einen Zugangs-token (access token)
				my $resp  = $browser->post('https://github.com/login/oauth/access_token',
					[
					#diese zwei sind globale Variablen innerhalb unserer Dancer-App
					 client_id     => $client_id,
					 client_secret => $client_secret, 
					 #das her ist der Code den wir von github bekommen
					 code          => $code,
					 #das ist ein random state das wir durch den login weitergeben haben //XX ask gideon
					 #idealer Weise sollte ein nicht zu erratender String sein
					 state         => 'x12'
					]);
				#ueberpfuefe ob alles gut abgelaufen ist
				die "error while fetching: ", $resp->status_line
					unless $resp->is_success;
				#parse den query string (Anfrage-String), wir bekommen einen access token von github...    
				my %querystr = parse_query_str($resp->decoded_content);
				#greife auf den access token zu
				my $acc = $querystr{access_token};
				#stelle eine weitere GET request an github mit unserem access token um die eingelogte Benutzerinformationen zu bekommen
				my $jresp  = $browser->get("https://api.github.com/user?access_token=$acc");
				#das decodieren der JSON gibt uns folgendes zurueck
				my $json = json_to_perl($jresp->decoded_content);
				#setze unsere session variables auf deb github-Krempel
				session 'username' => $json->{login};
				session 'avatar' => $json->{avatar_url};
				session 'logged_in' => true;
				#zurueckleitung zur Homepage
				redirect "/";
			};

 Diese Teilstrecke nutzt eine Hilfsmethode, die folgendermaßen aussieht. Sie parst den query string (Anfrage-String) in einen hash.

				#dies ist eine Nutzenfunktion die den query string in einen hash konvertiert
				sub parse_query_str {
				  my $str = shift;
					my %in = ();
					if (length ($str) > 0){
						  my $buffer = $str;
						  my @pairs = split(/&/, $buffer);
						  foreach my $pair (@pairs){
							   my ($name, $value) = split(/=/, $pair);
							   $value =~ s/%([a-fA-F0-9][a-fA-F0-9])/pack("C", hex($1))/eg;
							   $in{$name} = $value; 
						  }
					 }
					return %in;
				}


### Schritt 3 :
Wenn alles gut geht, fügt der vorherige Schritt einige wenige Session-Variablen hinzu, die dann wie folgt in der main.tt-Page benutzt werden können:

<!doctype html>
<html>
<head>
  <title>Dancr</title>
  <link rel=stylesheet type=text/css href="<% css_url %>">
</head>
<body>
  <div class=page>
  <h1>Dancr</h1>
     <div class=metanav>
     <% IF not session.logged_in %>
       <a href="<% login_url %>">log in</a>
     <% ELSE %>
   	<!-- Wir werden den Benutzernamen anzeigen, den wir in unserem Anwendungsobjekt haben. -->
		<p>Hello, <% session.username %> from GitHub
		<!-- Wir haben außerdem die Avatar-URL in der Anwendung gespeichert, diese nutzen wir hier -->
			<img src='<% session.avatar %>' alt='avatar' />			
		<p>
       <a href="<% logout_url %>">log out</a>
     <% END %>
  </div>
  <% IF msg %>
    <div class=flash> <% msg %> </div>
  <% END %>
  <% content %>
</div>
</body>
</html>

Und das wars. Wenn alles glatt geht, sollte die Homepage jetzt so aussehen:

![Dancr screenie][10]

Kommentare, Feedback und Beleidungen für diesen Artikel sind sehr willkommen! :)

  [1]: http://search.cpan.org/dist/Dancer/lib/Dancer/Tutorial.pod
  [2]: https://github.com/PerlDancer/dancer-tutorial
  [3]: https://github.com/gideondsouza/dancer-tutorial
  [4]: http://search.cpan.org/~gaas/libwww-perl-6.04/lib/LWP/UserAgent.pm
  [5]: https://metacpan.org/module/JSON::Parse
  [6]: https://github.com/gideondsouza/dancer-tutorial/blob/master/dancr.pl
  [7]: https://github.com/gideondsouza/dancer-tutorial/blob/master/views/layouts/main.tt
  [8]: https://github.com/settings/applications
  [9]: http://www.codinghorror.com/blog/2008/09/cross-site-request-forgeries-and-you.html
  [10]: http://i.imgur.com/Or4ksr7.png
