# Testování aplikace na tipování cen kryptoměn

Tento nápad zahrnuje vytvoření aplikace, která umožní uživatelům tipovat na to, zda se cena kryptoměn bude pohybovat nad nebo pod prodejní cenou v určité časové době.

## Funkce aplikace

- Uživatel zvolí kryptoměnu, na kterou bude vsazovat.
- Uživatel vybere dobu, po kterou bude tipovat, např. 10s, 30s nebo 60s.
- Uživatel zvolí, zda cena bude nad nebo pod prodejní cenou, která byla v momentu sazení.
- Pokud uživatel uhodne vyhraje, jeho kurz se odvíjí od časového úseku, 10s = kurz 1.2, 30s = kurz 1.5, 60s = kurz 2.0.
- Pokud uživatel neuhodne, přijde o vloženou částku.
- Pokud cena trhu bude na stejné úrovni, sázka se vyhodnotí jako neplatná.

Představme si, že uživatel chce vsadit na cenu Bitcoinu, která se momentálně pohybuje na hodnotě 16200 USD. Uživatel si zvolí dobu 10s a vsadí na to, že cena bude nad touto hodnotou. Pokud se cena skutečně zvýší nad 16200 USD v průběhu následujících 10 sekund, uživatel vyhraje profit s kurzem 1.2. Pokud se cena nezvýší, uživatel přijde o svou vkladovou částku.

## Výhody aplikace

- Uživatelé mohou využít své znalosti a zkušenosti s kryptoměnami k získání finančních prostředků.
- Aplikace umožňuje uživatelům rychle a snadno vsadit na pohyb cen kryptoměn, což může být užitečné pro krátkodobé obchodování.
- Díky jednoduchému použití a intuitivnímu rozhraní je tato aplikace vhodná pro uživatele s různou úrovní zkušeností v oblasti kryptoměn a sázení.

## Závěr

Tato aplikace nabízí uživatelům zábavnou a potenciálně výhodnou možnost vsadit na pohyb cen kryptoměn v krátkodobém časovém horizontu. Pokud by byla správně navržena a implementována, může být tato aplikace velmi užitečným nástrojem pro obchodníky s kryptoměnami, díky vysokým kurzům.

## Propojení API s burzou bybit

- Pomocí REST API se do aplikace nahraje Price Kline https://bybit-exchange.github.io/docs/v5/market/mark-kline
- Nastavení KLine interval 1, 3 a 5
- Nastavení SYMBOL je libovolné na klientovy
- Pri otevření sázky aplikace počítá s hodnotou > list[1]: openPrice	string	Open price
- Po uzavření se porovnává Open price s > list[4]: closePrice	string	Close price
- zde je možnost vygenerování zdrojového kódu https://bybit-exchange.github.io/docs/api-explorer/v5/market/kline
- nastaví se zde category: linear, symbol: BTCUSD, interval: 1/3/5 (podle nastavení aplikace v daný moment)

### Příklad nastavení

- GET /v5/market/mark-price-kline?category=linear&symbol=BTCUSDT&interval=15&start=1670601600000&end=1670608800000&limit=1 HTTP/1.1
Host: api-testnet.bybit.com

- `{
    "retCode": 0,
    "retMsg": "OK",
    "result": {
        "symbol": "BTCUSDT",
        "category": "linear",
        "list": [
            [
            "1670608800000"
            "17164.16",
            "17164.16",
            "17121.5",
            "17131.64"
            ]
        ]
    }
    "retExtInfo": {},
    "time": 1672026361839
 }`

## Testování aplikace
- Pro realné využití je potřeba zjistit na DEMO aplikaci, zda klienti budou více prohrávat či vyhrávat.
- Pokud více prohrávají, je možnost nasadit aplikaci do realného provozu, protože výhry klientů se vyplácí z proher ostatních klientů.
- Dále je za potřebá nastavit možnost v kladu za pomocí platební karty a výběru na bankovní účet.
- Neobchoduje se přímo na burze, tudíž z ní získáváme pouze data trhu pro stanovení podmínek dané sázky.

## Nastavení kurzu sázky
- Ke zvolenému časovému úseků patří daný kurzu sázky.
- 10s = kurz 1.2
- 30s = kurz 1.5
- 60s = kurz 2.0

## Disign aplikace
- Aplikace má jednoduchý vzhled pro co nejvíce individzální použití.
- Do aplikace je možný přístup až po přihlášení.
- V nastavení profilu je možnost VKLADU a VÝBĚRU.
- Dále je v profilu vidět historie zisků s ztrát.
- zpracování designu - https://www.figma.com/file/yIQMG45BMBjEDDWGqzDNtZ/mockup?node-id=0%3A1&t=qRh0OQrHwCfPeQmK-1



