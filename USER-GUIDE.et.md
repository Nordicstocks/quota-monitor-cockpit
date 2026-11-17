# Quota Monitor — kasutusjuhend

Quota Monitor näitab, kui palju on sul alles **GitHub Copiloti**, **Claude Code'i** ja **Codexi** limiitidest. Numbrid on näha Visual Studio Code'i olekuribal, külgpaneelil ja graafilises ülevaates.

*Microsoft, GitHub, Anthropic ega OpenAI ei ole Quota Monitoriga seotud ega ole seda heaks kiitnud. Quota Monitor kasutab iga tööriista andmete lugemiseks sisselogimisi, mis sul arvutis juba olemas on (Claude Code, Codex ja GitHubi konto Visual Studio Code'is), ega küsi kunagi parooli.*

---

Käskude nimed on siin kirjas nii, nagu käsupalett neid näitab: ingliskeelse Visual Studio Code'i puhul inglise keeles. Sulgudes on nende tähendus eesti keeles.

## 1. Alustamine

1. Paigalda Quota Monitor. Laienduse ikoon ilmub vasakul olevale tegevusribale (*Activity Bar*).
2. Varsti näitab olekuriba iga leitud tööriista kohta lühikest silti, näiteks `Cl 64% · Cx 82% · Co 35%` (Claude Code'i esimese näiduni võib kuluda minut või kaks). `Cl` on Claude Code, `Cx` on Codex, `Co` on GitHub Copilot. **Iga number näitab, kui palju on alles** selle tööriista limiidist, millest on kõige vähem järel, mitte seda, kui palju oled ära kasutanud.
3. Claude Code'i ja Codexi leiab Quota Monitor ise, kui need on paigaldatud ja oled neisse sisse loginud. GitHub Copilot vajab üht klõpsu: vaata 3. jagu.
4. Kui ühelgi tööriistal pole veel numbreid (ükski pole paigaldatud, ühessegi pole sisse logitud ega ühtki ühendatud), on olekuribal kirjas **AI-limiidid: ühenda**. Klõpsa sellel ja näed, mida iga tööriist vajab.

## 2. Kus numbrid on näha

- **Olekuriba.** Klõpsa sildil ja avaneb kiirtoimingute menüü (ülevaade, värskendamine, sätted, kasutusjuhend). Kui viid kursori sildi kohale, näed kõiki limiite ja seda, kui palju igaühest alles on (Pro-ga ka seda, millal limiit uueneb).
- **Külgpaneel.** Klõpsa tegevusribal Quota Monitori ikoonil. Paneel näitab samu limiite (iga tööriist eraldi real) ja nuppe tööriistade ühendamiseks.
- **Graafiline ülevaade.** Käsupalett (*Command Palette*, `Ctrl+Shift+P`, Macis `Cmd+Shift+P`) → **Quota Monitor: Open Visual Dashboard** („Ava graafiline ülevaade“). Ülevaates on kolm vahekaarti:
  - **Ülevaade:** iga limiidi kohta kaart, millel on näha, kui palju on alles (ja Pro-ga ka see, millal limiit uueneb).
  - **Analüütika:** sinu kasutusajalugu ning Pro-ga trendid ja soojuskaart nädalapäevade ja tundide kaupa.
  - **Sätted:** kõik, mida kirjeldab 6. jagu.
- **Veebibrauseris (Pro):** **Quota Monitor: Open Dashboard in Web Browser (Pro)** („Ava ülevaade veebibrauseris (Pro)“) avab sama ülevaate sinu brauseris, näiteks teisel monitoril. See töötab ainult sinu enda arvutis (`127.0.0.1`).

Kaarti saad lohistada selle `⋮⋮` pidemest, valida sellele ühe kuuest värvist või peita ristiga ×. Peidetud kaardid saad tagasi tuua realt **Peidetud**. Kaardi peitmine muudab ainult seda, mida sa näed; limiidid jäävad samaks.

## 3. Kolm tööriista

### Claude Code

Quota Monitor käivitab sinu arvutis käsu `claude -p /usage` ja saab samad numbrid, mida Claude Code näitab käsuga `/usage`. See ei alusta vestlust ega kuluta sinu limiiti.

- Vaikimisi loeb Quota Monitor Claude Code'i limiite iga **15 minuti** järel (võid valida ka 30 või 60) sel ajal, kui kasutad Visual Studio Code'i. Kui mõnest Claude Code'i limiidist on alles alla 20%, loeb ta iga 5 minuti järel, alla 5% juures iga 3 minuti järel.
- Kui avad graafilise ülevaate ja viimane näit on vanem kui 2 minutit, loeb Quota Monitor Claude Code'i limiidid kohe uuesti.
- Claude Code ei teata alati 5 tunni limiiti. Kui näed ainult nädalalimiite, siis just need Claude Code tol hetkel andis.

### Codex

Quota Monitor küsib sinu arvutis olevalt Codexi programmilt (`codex app-server`) sinu kontotüüpi ja limiite, muud mitte midagi. Vaikimisi loeb Quota Monitor Codexi limiite iga 5 minuti järel (sätetes saad valida 2–30 minutit).

### GitHub Copilot

GitHub Copiloti andmed tulevad GitHubist, nii et selleks pead ühe korra loa andma:

1. Klõpsa külgpaneelil nuppu **Ühenda GitHubiga**.
2. Visual Studio Code küsib, kas Quota Monitor võib kasutada sinu GitHubi sisselogimist. Klõpsa **Allow** (luba). Kui sa pole Visual Studio Code'is veel GitHubisse sisse loginud, avab see kõigepealt brauseri, kus saad seda teha.
3. Copiloti kasutus ilmub mõne sekundi pärast. Edaspidi loeb Quota Monitor seda sama vahega kui Codexi limiite, kuid kõige tihemini kord 10 minuti jooksul.

Quota Monitor küsib ainult luba lugeda sinu e-posti aadressi (või avalikku profiili, kui Visual Studio Code'il see luba juba on) ja loeb ainult sinu Copiloti kasutust. Ligipääsu sinu koodile ei küsi ta kunagi.

**Teine võimalus:** kui sa ei taha lubada Quota Monitoril Visual Studio Code'i GitHubi sisselogimist kasutada, käivita **Quota Monitor: Use a GitHub Token for Copilot Usage** („Kasuta GitHubi tokenit (Copiloti kasutus)“) ja kleebi avanevasse lahtrisse GitHubi isiklik token (GitHubis *fine-grained personal access token*), millele on antud kasutajaõigus **Plan: read**. Quota Monitor hoiab tokenit Visual Studio Code'i turvalises hoidlas ja saadab selle ainult aadressile `api.github.com`. Käsk **Quota Monitor: Remove the GitHub Token for Copilot Usage** („Eemalda GitHubi token (Copiloti kasutus)“) kustutab selle.

### Kui tööriist numbreid ei näita

Iga tööriista real on lihtsate sõnadega kirjas, miks:

| Real on kirjas | Mida teha |
| :--- | :--- |
| pole paigaldatud | Paigalda tööriist või lülita see jaotises **Sätted → Tööriistad** välja, kui sa seda ei kasuta |
| pole sisse logitud | Logi sisse tööriistas endas (näiteks käivita terminalis üks kord `claude` või `codex`) |
| pole ühendatud (Copilot) | Klõpsa **Ühenda GitHubiga** (3. jagu) |
| lugemine ebaõnnestus (ooteaeg sai täis, ühendust pole …) | Quota Monitor proovib ise uuesti, esimest korda minuti või kahe pärast ja siis harvemini. Viimased numbrid jäävad alles ja on märgitud vanaks |

**Quota Monitor: Refresh Data Now** („Värskenda andmeid kohe“) loeb limiidid kohe uuesti (Claude Code'i limiite kõige tihemini kord 2 minuti jooksul, teiste tööriistade limiite kord minutis).

Ükskõik mitu Visual Studio Code'i akent sul lahti on, loeb andmeid ainult üks neist. Teised näitavad selle numbreid.

## 4. Tasuta ja Pro

**Alati tasuta:** olekuriba, külgpaneel ja graafiline ülevaade, kõik kolm tööriista, edenemisriba stiilid, kaartide värvid ja värviteemad, hoiatused redaktoris, kui limiit hakkab otsa saama või uueneb, ning 24 tunni kasutusajalugu.

**Pro lisab:**

- **Aeg uuenemiseni ja uuenemise kellaaeg** igal limiidil ning **otsasaamise prognoos**: kas limiit saab praeguses tempos otsa enne, kui see uueneb?
- **Reserve Guard:** hoiatus, kui limiidi jääk langeks praeguses tempos alla sinu määratud kvoodivaru (vaikimisi 20%).
- **Soovitus tööriista vahetada:** kui ühe tööriista limiit hakkab otsa saama, nimetab hoiatus mõne teise tööriista, mida kasutad ja millel on veel palju alles, näiteks „Codex: veel 82% alles.“
- **90 päeva kasutusajalugu**, trendijooned ja soojuskaart nädalapäevade ja tundide kaupa.
- **Telefoni- ja sõnumiteavitused** ntfy.sh, Telegrami, Discordi või Slacki kaudu (5. jagu).
- **Teavita mind, kui limiit uueneb** (kaardil 🔔) ja **hommikune kokkuvõte** kord päevas kella 06:00 ja 11:59 vahel.
- **Nädalaaruanne** HTML- ja Markdown-vormingus, iga tööriista kohta üks tabel.
- **Helid**, kui limiit uueneb või hakkab otsa saama.
- **Kasutusajaloo eksport** CSV- või JSON-failina (kuni 90 päeva).
- **Terminali olekufail ja koodilõigud** (7. jagu) ning **brauserivaade** (2. jagu).

### 14-päevane prooviaeg

Iga uue paigaldusega on kaasas **14 päeva täis-Pro-d**, ilma kaardi ja registreerumiseta. Prooviaeg algab siis, kui ilmub sinu **esimene näit**, mitte paigaldamisel, nii et seadistamisele kulunud päev ei lähe arvesse. Külgpaneel näitab, mitu päeva on jäänud.

Kui prooviaega on jäänud 3 päeva, annab Quota Monitor sellest ühe korra teada. Kui prooviaeg lõpeb, lülituvad Pro-võimalused välja ja tasuta osa töötab edasi. **Sinu kasutusajalugu jääb alles.** Kõik, mis on vanem kui 24 tundi, on peidetud, mitte kustutatud, ja tuleb tagasi kohe, kui Pro avad.

### Pro ostmine

Pro eest **maksad ühe korra 9,99 €** — püsitellimust pole. Kui ei meeldi, saad 30 päeva jooksul kogu raha tagasi.

1. Klõpsa külgpaneelil või graafilises ülevaates nuppu **Ava Pro — 9,99 €** või käivita käsk **Quota Monitor: Unlock Pro (€9.99 one-time)** („Ava Pro (9,99 € ühe korra)“).
2. Visual Studio Code küsib kõigepealt **„Do you want Code to open the external website?“** (kas lubad Code'il avada välise veebilehe) ja näitab aadressi `buy.polar.sh`. See on Visual Studio Code'i enda turvakontroll ja see ilmub iga laienduse puhul, mis veebilehe avab. Klõpsa **Open**.
3. Maksa Polari lehel. Polar on pood, mis müüb Quota Monitor Pro-d ja tegeleb maksega. Quota Monitor sinu kaarti ei näe.
4. Litsentsivõti tuleb sulle e-postiga. See algab tähtedega `QMV-`.
5. Käivita **Quota Monitor: Enter Pro License Key** („Sisesta Pro-litsentsivõti“) ja kleebi võti. Pro hakkab kohe tööle.

Üks võti töötab kuni 5 redaktoris, näiteks 5 arvutis. **Quota Monitor: Remove Pro License Key** („Eemalda Pro-litsentsivõti“) vabastab selle arvuti litsentsikoha, nii et saad võtit kasutada teises arvutis. Teise laienduse võti (näiteks selline, mis algab tähtedega `PRO-`) Quota Monitoris Pro-d ei ava.

## 5. Telefoni- ja sõnumiteavitused (Pro)

Ava graafilises ülevaates **Sätted → Telefon ja sõnumid**.

- **ntfy.sh (kõige lihtsam, kontot pole vaja):** paigalda tasuta äpp ntfy, lisa sinna teema nimi, mida ülevaade näitab (Androidis võid skannida QR-koodi), ja klõpsa siis **Salvesta ja saada testteavitus**. ntfy.sh-teemad on avalikud, nii et hoia ülevaate pakutud juhuslik teemanimi enda teada.
- **Telegram:** loo @BotFatheri abil bot, määra boti token käsuga **Quota Monitor: Set Telegram Bot Token (Pro)** („Määra Telegrami boti token (Pro)“), kirjuta oma botile üks kord ja sisesta oma vestluse ID. Ülevaate abitekst (ⓘ) juhendab sind samm-sammult.
- **Discord või Slack:** kleebi sissetuleva webhooki URL.

**Quota Monitor: Send Test Notification (Pro)** („Saada testteavitus (Pro)“) kontrollib kõiki kanaleid, mille oled seadistanud.

## 6. Sätted

Graafilise ülevaate vahekaardil **Sätted** või Visual Studio Code'i sätetes jaotises **Quota Monitor**:

| Säte | Mida see teeb |
| :--- | :--- |
| Kasutajaliidese keel | Automaatne, inglise või eesti keel. Automaatne järgib redaktori keelt, ingliskeelse redaktori puhul aga süsteemi keelt. |
| Teema | Öö, päev või redaktori järgi |
| Olekuriba kuvamisrežiim | Kõik tööriistad, ainult kõige väiksema jäägiga limiit või üks tööriist |
| Edenemisriba stiil | Kaheksa stiili, värvilised või ühevärvilised |
| Hoiatuslävi ja kriitiline lävi | Olekuriba muutub kollaseks, kui limiidist on alles määratud protsent või vähem (vaikimisi 30%), ja punaseks 15% juures |
| Tööriistad | Lülita välja tööriist, mida sa kunagi ei kasuta |
| Kui tihti limiite loetakse | Codex ja GitHub Copilot 2–30 minutit (Copilot kõige tihemini kord 10 minuti jooksul); Claude Code 15, 30 või 60 minutit |
| Helid, hommikune kokkuvõte | Sees või väljas (Pro) |
| Prognoosihoiatus, kvoodivaru | Hoiatab, kui limiit saab praeguses tempos otsa enne uuenemist ja hiljemalt määratud arvu minutite pärast (vaikimisi 25); kvoodivaru, mida Reserve Guard hoiab (20%) |
| Ajalugu | Mitu päeva ajalugu alles hoitakse (vaikimisi 90) |

## 7. Terminali olekufail (Pro)

Pärast iga näitu kirjutab Quota Monitor faili `~/.quota-cockpit/status.json`, kui palju on alles (ainult numbrid ja kellaajad). **Quota Monitor: Terminal Snippets (Pro)** („Terminali koodilõigud (Pro)“) annab valmis read zsh-i, Starshipi ja tmuxi jaoks macOS-is ja Linuxis ning PowerShelli ja Starshipi jaoks Windowsis. Nii näitab sinu käsuviip limiite.

## 8. Sinu andmed

Sinu arvutis:

- kasutusajalugu Visual Studio Code'i andmehoidlas, mis on eraldatud ainult sellele laiendusele;
- kaust `~/.quota-cockpit/`: viimane näit, mida kõik aknad jagavad, ja Pro-ga terminali olekufail;
- sinu Pro-litsentsivõti ning GitHubi token või Telegrami boti token, kui oled selle määranud, Visual Studio Code'i turvalises hoidlas.

Võrgu kaudu ainult:

- **GitHub** (`api.github.com`): sinu Copiloti kasutus, kui oled Copiloti ühendanud;
- **Claude Code ja Codex** toovad sinu limiidid Anthropicult ja OpenAI-lt ise, oma sisselogimisega, nagu ikka, kui neid kasutad;
- **Polar** (`api.polar.sh`): sinu litsentsivõti, kui oled selle sisestanud — et kontrollida seda sisestamisel ja edaspidi kord päevas ning vabastada litsentsikoht, kui võtme eemaldad;
- **ntfy.sh, Telegram, Discord, Slack:** ainult teavitused, mille oled seadistanud;
- **Open VSX:** kontroll, kas Quota Monitorist on uuem versioon.

Meile ei saadeta midagi: ei kasutusnumbreid, faile ega kontoandmeid. See versioon ei saada meile vearaporteid. Ajaloos on iga konto juures sinu e-posti aadressi asemel lühike kood.

## 9. Abi

- Kas midagi ei tööta nii, nagu peaks? Käivita **Quota Monitor: Refresh Data Now** ja vaata siis külgpaneelil selle tööriista rida: seal on kirjas, mis puudu on.
- Kirjuta aadressile **support@nordicmoonlight.com**. Lisa kirja oma operatsioonisüsteem, Visual Studio Code'i versioon ja tööriista real olev tekst.
