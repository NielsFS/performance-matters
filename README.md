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



## Feature/4-Asynchroon-laden-van-assets












