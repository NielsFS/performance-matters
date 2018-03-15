# Performance matters

## Project setup

This project serves an adapted version of the [Bootstrap documentation website](http://getbootstrap.com/). It is based on the [github pages branche of Bootstrap](https://github.com/twbs/bootstrap/tree/gh-pages). 

Differences from actual Bootstrap documentation:

- Added custom webfont
- Removed third party scripts
- The src directory is served with [Express](https://expressjs.com/).
- Templating is done with [Nunjucks](https://mozilla.github.io/nunjucks/)

## Getting started

- Install dependencies: `npm install`
- Serve: `npm start`
- Expose localhost: `npm run expose`


# Features

De basistest voor de Bootstrap pagina:

![Basistest](https://lh3.googleusercontent.com/XatWix35Pg9aRMD0ftblER6HP7BQHx_Yu417R_DWEAsqLahzsFuWkFeQaA_cIamxXuHYnBec54SkDcJ4nBlSCo3wbjRpyr8xVwqj35h0RFUT17U5KhCcNrg3X5Qx80Nx7QiJoKhf-0nZlxj7QeEgrRdYJp8h5rRv97uU1zI5htgWnvV_zjuqtJx7-y1SjroidQRyMkCbSlX3ga6JMwqZmA3aybwb1rirkLTwe146zbV68c9tmP3jhEi15shDpnGUym_ZX0__WjbAYEGikVMXtfvyhBrS-VzZt6-HlwMyw1iPR_3JHnlRtZeV7MYgVfPAgRhuzd79WEvLQuLtDgA42YXzeaA1sr2BG_GFmiH0Penrrr5K9ig7ZDyjaQcv6Q8qeYlJiT1mrj5ZVaVaDg1y506lfvSHyzDrP2LEV9esnB3q-xBIumcESNLj_yZlwZm0vpEDlezBMngPO6IFwgOmOuBZn5tE9lTADG-qHXJdYdGnxPy6Sgn6HzeWMkdzWcfteH3viOlmQupg-FeeSV92H5Wx5YSXilOkJWo3bpPRxFXQLYNmzewuYu0AlxWVqsUWmp6_h4oleHmCwLWy7CWpmSHM8HHbSu4zxCjewg=w1452-h1496-no)

## Feature/1-Critical-CSS

Critical CSS zorgt ervoor dat de rendering path van de pagina veranderd wordt. Alles wat in browser view is wordt als eerste gestyled door css, en daarna wordt de rest van de pagina gestyled. Dit zorgt voor een betere perceived performance. Op langzamere netwerken zorgt dit er voor dat je minder lang naar een blanco pagina staart.

Op de basistest is te zien dat de first paint ongeveer op 10 seconden zit. Door Critical css toe te voegen aan de pagina is de first paint versneld naar 3,45 seconden. Zie foto hier onder:

![feature 1](https://lh3.googleusercontent.com/QjtLvuanPVACN3qJgep_xEYpLgB4wu-toBfjUfW8XDQIRe2GZBrZfb-Jhc7uLPIYbwh7rNyvhWLSL828tgMkAPlq4UjEdDA3rVNJHfrKczsJ1QOthao8VAeDha-V3tq6yj6ZfMDikcmAItrzqkE0eZeQtlCHY6J7_imHJ6CC9bofGa97hPJMdTeam4TFz7-QkCRZUqo74sB7rfNq_O_5CG8GyMLDGjuXw5Vl4YYRkksH34TlsIHOk32imgMG82ptLjAZT-uWJ5E_teGfZz7inhmiaggAxLypX21kUdxhBPkKHFYp7NzgVN03OdGAOsStu9WoT--T6rO1dnijJaCH6sf2xOBg97RcS7HdpX2OU56Kwpb6E8CCv_dxxmrNgl8A7CVOyP8k9-GM2mEkKnfDDGLxrSNR8aFfvzhMqFNFuOkCles8cqTMahDVvlxiaXJ8p59RQekynTBBdWPFsSYzuup6HMXZPJ3rPw21YkbGRsDvHcACIbNXrWVjB8ahDRzjzNj542Aa4xgEhFDfc6cYTe_jzilSZy-RH02i7zceBE78I6WFotfDqUmiKFDRDP15t5ph4hfO1IeW2fcRDmay1fgmUi-SDS3T1p8xfA=w1420-h1558-no)

De critical css Kon op twee manieren worden gemaakt. Zo is er de volgende online tool: https://jonassebastianohlsson.com/criticalpathcssgenerator/

Wat ik heb gedaan (met hulp van Bas Kager) is nog makkelijker, doormiddel van een tool op npmjs.com. Deze tool installeer je en scant een pagina waarna hij critical CSS genereert.
https://www.npmjs.com/package/critical

Vervolgens wordt de css in de layout.html pagina bovenin de head ingeladen. De basis CSS files worden ook nog ingeladen, maar deze worden ingeladen nadat de critical css is ingeladen. 

## Feature/2-font-loading

De 3,45 seconden laadtijd tot en met first paint kan nog enorm verkleint worden door de fonts pas nadat alles is ingeladen te swappen. Door de Fonts uit de critical css te halen, en font swap toe te voegen aan het fonts.css bestand worden de custom fonts pas later ingeladen. Dit zorgt voor een enorme verbetering in de first paint. Die is nu 373 ms. 

zie de resultaten hier:

![Feature 2](https://lh3.googleusercontent.com/x200Vi5j34S6iMQCXcR3v0YtIEp9dqrwZGgbMaFbBnBBNBEeYkmjge-_4Z7Wu11hFqTvgZeqdSrwqR13koFDN51IMS8_ifW9jkp7UjFBeC0JqCpFTydDgqISKVjtibrjoKo6wDjNkAzdqF-sVAVznPvARJEplfMwEvNh7h_k-z7TfaESxAfsDHa0FWE8s34WLWAwy-HchU1BeSCa2y7u8B3WoMwoK_8esBEgtW-8S3t0e_vD8TT-bSRwbAZRiC_Jyr-Aq9VeUMuKUVdLrt_s1_W9rq8vLK1d3ckSE9Ay6IJKsVn06fxYRkopDZ3V3mRyKx7YCZJDmICP2-QX0jw5Qr3Chw_S93ilY-WJrwH-7tAvDGIZ9z9xNV3Z99uteTHViOwDBcEzgJsv6rVD6qG27uzfUAIIiRDLEMyBmIyhFc1D8XYc3odyGkZh1YmXyJIR-HGCrY4x0z9XpdyHLU5btxsDP5fVFjmRGgsubzXtAHs7YRko3qE6RPUUqCnwDNCqJIaOu46U_3MTSqq7PPvmmi8GIjxus3poQTPMuoFYKawbilltw5Kbk8waeSjuhK9zppoZG2g5iMTx_x6JZbn0w3-N9HTCcYLHDg6tDw=w1600-h1560-no)

## Feature/3-Image-Optimalisatie

Na de fonts en de critical css te hebben verbeterd is de first paint op een enorm goed niveau. Echter heeft dit nog niet geresulteerd in het verbeteren van de algehele laadtijd van de pagina. Die staat nogsteeds op 31 seconden. De beste en eerste optimizatie voor het verbeteren van de laadtijd is het comprimeren van de foto's. Deze heb ik verkleind doormiddel van een online tool genaamd optimizilla: http://optimizilla.com/nl/

![Optimizilla images](https://lh3.googleusercontent.com/kagafzSXdjdG_Dpmko5VJ_s8EEakbE0mO9KA1BG6JAtCgXEwKgEmoFv7M8FC7E5SGYO5Tnxaftqw_PsQroDkVdDgoT_Aj2n7N2D8-epmFw-vFl-QQWI1KF9O7nDEi5ejVKe-rlekGyuqzLOGe8jYWnmwdP7QEgpXYtvhoAh_Hupuq1-cflILLNdLBmpEuSuG0g88bm_ru9Yk5BGxYxmvFrPHHiVq-9p8LMe6iT6iaordHxMtp7YntdcA0OMmwDemMr2zwMjLTDu60lvuOqOBhb9shlfhTph8SCNG9VVpj5LOMVeskOUZdfKLpUm9tMXGeNa86_8Lxfato3SubUVFbDetrvT0aWo2Hl9y-IfA0eoCLzWW-PkV-6ame8sdep3WzjXHq3GiaVKdCttucKwmyglrqE7NXtkm1mBzVJVEfbG4I4o-Iy4ayBoRZoW1zUZgUxfkHdMr57Sq2JkuhE0xoU2uUZfZm2hQ-DMLqnQKtNuUvBJF60Fn2ppNsFxJNvVFksv-dV5OZ4Rm_BhveW4oxDCy5LFUVguS_WBogZ6HeSW1m92JAgIfEiep2q4WltaboQfDOsCAIIY-e5nCv9tFxwrWrwkSRqoZNOP-MkA=w1864-h548-no)

De foto's heb ik vervolgens vervangen. Zie de resultaten hier:

![Feature 3](https://lh3.googleusercontent.com/UEQMFZB88lTWABupLG9iU5e1iGPEpTlSIFMTvXfoicWDJRenpEFaQ0t6Gk2vJy1qKKrwbShcT5jLJR2KP9W-xY-8oyOacQrIiTEknBNU-hRJoJ8ZEbIFTtj5IxQvUtHCHN1VypdIyzycxpRkj0Xrjt2fN4fyCpxwTZYvreflgZ91XyThXVOSKEzXhYWXk-2Cz0ZslH1V0gLU3sr1KdKEXnbfOHDY-Eu_OYy7AQ3BdMWK9yna42ye4Kn4jX7Ag1wEwrG4zWTcWuz85WtpfHGwuGDklaXU4FMNB1Yu1v9gJ9g2cX4fYrPgIGUWbT8KQStt4WUu-5Io6RdLNjBS8cDuhXYT6f41zB9b1FFKiw5j2-vZuIC0auEQ17F2LDRgp7SF_URJiNUcqNHYk3DXUUhFfJviAtcwypEgYzIct_oirm0uhD3H3Kc2JzZGIBQo-1AOBRFQhQkniRKMCWKuNAEtaxutoMs49XftINjaDjWQ801DsSVYyWb1biOrkZZhJPHuIIXA8_R0JicCoCoNKMAofVX4Zpe4gfeU7kP36Kejf1lrys9-8RzKxw4-LI7XI5FWt5MFPm1riwP9OTr9C682GeR6ebkkoitNGog99gw=w1652-h1506-no)

De laadtijd van de pagina is met 8 seconden verbeterd naar ongeveer 23 seconden

## Feature/4-Asynchroon-laden-van-assets






#










