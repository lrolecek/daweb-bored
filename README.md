# Nudím se

Tvým cílem bude napsat jednoduchou aplikaci **Nudím se** na zahnání nudy. Aplikace doporučí uživateli náhodnou činnost, kterou může jít dělat, když se nudí.

## Vytvoření komponenty Aktivita

1. Klasickým postupem pomocí `create-czechitas-app` založ novou React aplikaci s názvem `nuda`.
1. V hlavní komponentně `App` nech pouze hlavní nadpis **Nudím se**,
1. V samostatné složce vytvoř komponentu `Aktivita`, která zatím bude jako výstup vracet odstavec s textem `do something`.
1. Komponentu naimportuj do hlavní komponenty `App` a přidej ji pod hlavní nadpis.

## Zobrazení aktivity

Veškerou další práci už budeme provádět uvnitř komponenty `Aktivita`.

1. Do komponenty přidej stav `activity`, jehož výchozí hodnota bude prázdný řetězec.
1. Obsah stavu `activity` vlož do odstavce místo textu *"do something"*.
1. Uvnitř komponenty vytvoř jednoduchý efekt, který se spustí při prvním zobrazení komponenty. Uvnitř efektu zatím pouze vypiš něco do konzole prohlížeče, abys ověřila, že se efekt spouští.
1. Nahraď `console.log` v efektu kódem, který nastaví stav `activity` na nějakou hodnotu. Zkontroluj, zda vše funguje a zda se nastavená hodnota správně zobrazí na stránce.

## Získání aktivity ze serveru

Použijeme veřejné api *boredapi.com*, která ná následujícím endpointu vrací JSON s náhodně doporučenou aktivitou.

1. Uprav efekt tak, aby nenastavoval aktivitu napřímo, ale aby ji získal ze serveru. Použij `fetch` na následující adresu a zpracuj odpověď ze serveru:
	```
	https://www.boredapi.com/api/activity
	```
2. Server vrací odpověď v tomto formátu:
	```
	{
		"activity": "Catch up with a friend over a lunch date",
		"type": "social",
		"participants": 2,
		"price": 0.2,
		"link": "",
		"key": "5590133",
		"accessibility": 0.15
	}
	```
	Z odpovědi serveru vezmi hodnotu vlastnosti `activity` a ulož ji do našeho stavu `activity`.

## Výběr typu aktivity

Předpokládejme, že uživatel ještě není natolik znuděný, aby se smířil s jakýmkoliv doporučením, ale chce si alespoň vybrat, jaký typ aktivitu mu máme doporučit.

1. Do komponenty přidej formulář, ve kterém si uživatel může vybrat typ aktivity. Ve formuláři bude tento `select`:
	```
	<select>
		<option value="relaxation">Relaxace a odpočinek</option>
		<option value="education">Vzdělávání</option>
		<option value="music">Hudba</option>
		<option value="social">S přáteli</option>
		<option value="busywork">Nějak mě zaměstnej</option>
	</select>
	```
1. Vytvoř stav `activityType` a funkci `handleActivityTypeChange`, která propojí stav s hodnotou uvnitř prvku select. Jako výchozí hodnotu pro stav zvol `relaxation`.
1. Zařid, aby efekt při každé změně stavu `activityType` poslal na server dotaz na náhodou aktivitu daného typu. To uděláš tak, že za adresu, kterou jsme používali doposud přidáš ještě `?type=relaxation`. Hodnotu za rovnítkem samozřejmě budeš měnit podle toho, co je vybrané v selectu. Celá adresa tedy bude vypadat takto:
	```
	https://www.boredapi.com/api/activity?type=relaxation
	```
1. Pokud jsi vše udělala správně, při každé změně hodnoty v selectu by ti aplikace měla doporučit novou činnost podle vybraného typu.