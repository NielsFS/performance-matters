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

![Feature 3](https://lh3.googleusercontent.com/FSgkJHwYJCkwzwa3toqJhwhSTBeDiDjQgMBbR_XXUmtwrc3q4e-5JF6isarUPHB5toCG9gdphVNK_OvWqFdP_BQx_VHjgq7zAhcPi7xuuAF3NZJWAAxDnmZtR_CY_3yRN49K0pkZlb1AvZqshQe3mEF32tC-ZZYEEXW5VyklPKnJyZMQV74lCyFiyEfUnphZybaTxOZ_1CPbw0Se8O_5lUbEj1D4T4rvmBHI2u_jFKszl85WEHO8ZnJa3GyfU4L2138B-wA0vXizysivzyc7zoVIDTVWcmoSTOtGtGj5vXXu0Gt9CX7zaQ_yj9w2k2YCxliKRtOhrxZmqGX7DfF3vudoGVoQZGriM6pUlqX7rD6e14CoTIfNVytLmPE6FlumkL6mlJK9FQ1ailV1Kd7eEm_2j-G0iXtMAvODjg3_rdSksnDqh0hhpzaUEQYC2L0Xo5ms3maGemf42Yms2mQDq3-LW13lCUiksleANM-oQpXGVLhP9Wrm4t7BrcoYMjZIpQwqwbY5VkOmg7p-edH7EERSrVmR4of528DTn27ngvNfGMvpWAqAOCO2W7sk8EhLyIrrclpkXgTLpubB1KfCt0LgYVW-iIZGRkRisXQ=w1648-h1556-no)

De laadtijd van de pagina is met 8 seconden verbeterd naar ongeveer 23 seconden

## Feature/4-Asynchroon-laden-van-assets

Het asynchroon laden van de assets werd gedaan door de critical css pakket van www.npmjs.com . Deze was dus al aanwezig bij alle features. Ik heb twee tests uitgevoerd met het aan en uitzetten van het asynchroon inladen van assets. dit heb ik gedaan door de het volgende script en de css linkn files terug te zetten naar het origineel.

origineel: 

	<link href="/dist/css/fonts.css" rel="stylesheet">
    <link href="/dist/css/bootstrap.css" rel="stylesheet">
    <link href="/assets/css/src/docs.css" rel="stylesheet">

Dit leverde de volgende resultaten op:

![feature 4 origineel](https://lh3.googleusercontent.com/wy19T4rvVcCj-vtDCVMhI-gz68iHH3qyYqkmLRxJg3eaUR0Fz7C0qER3GJOH4nlt0iyIRd5II-AkIK1qRXLTjhjx6okS6KyN6YP6qVzSuFZVqFVo5CpJolBeamOZFEG7pOMZ83fGT9Oxd9YSfwjv13V4CtVQKCVLmvisT9z9tDiJHxRZLdFPysOq1NAyc8BE8dhAIvAhasEa0bEEX3JRBYryBwLeqnKN54NYUspQ9hHpKWv1Sjbqg-D36_iokrWyQX1l_0ty4aXkZZ6fJ7sAOSKoh2Jb66bkKLryofNHS5CU1DQTe-ZTlDSsMrlI88MMEUlGchvCFKIhhAw5-mbgasZQYOSmZByFfH6DQ0FvHwR8k6KnD5eqUO7HnGnkSs01mNSsXiVMtPlypbgvB4ZUtQbzZ1Bm01Ag1OdJq4E71d6u8mlC1tDfzlzaEDTkDEklCuN5E04H-_TL69tT6Au40iSRwJ_2H_QwczzR3TY5kBvXSR_sV0r0ZaYK5oid4N3Ouu34Boix1UZUT4MNbQToKJRrYaUaACiDIqCF9BWJbMTb6njvuKyb4hJnHiO6_euwOW-KK5sBAuplbYljIsIj9Ub8VSpbjfqsQf_ow9E=w1648-h1558-no)

Zoals te zien wordt de totale laadtijd niet veranderd. Echter zie je wel dat de first paint stukken trager is, die is er namelijk na 7 seconden pas.

Door de originele link tags en het het script toe te voegen wordt de first paint stukken enorm snel. Dit komt doordat de assets pas ingeladen worden nadat de critical css is uitgevoerd.

link:

	<link href="dist/css/fonts.css" rel="preload" as="style" onload="this.onload=null;this.rel='stylesheet'">
    <noscript><link href="dist/css/fonts.css" rel="stylesheet"></noscript>
    <link href="dist/css/bootstrap.css" rel="preload" as="style" onload="this.onload=null;this.rel='stylesheet'">
    <noscript><link href="dist/css/bootstrap.css" rel="stylesheet"></noscript>
    <link href="assets/css/src/docs.css" rel="preload" as="style" onload="this.onload=null;this.rel='stylesheet'">
    <noscript><link href="assets/css/src/docs.css" rel="stylesheet"></noscript>

script:

	<script>!function(n){"use strict";n.loadCSS||(n.loadCSS=function(){});var o=loadCSS.relpreload={};if(o.support=function(){var e;try{e=n.document.createElement("link").relList.supports("preload")}catch(t){e=!1}return function(){return e}}(),o.bindMediaToggle=function(t){var e=t.media||"all";function a(){t.media=e}t.addEventListener?t.addEventListener("load",a):t.attachEvent&&t.attachEvent("onload",a),setTimeout(function(){t.rel="stylesheet",t.media="only x"}),setTimeout(a,3e3)},o.poly=function(){if(!o.support())for(var t=n.document.getElementsByTagName("link"),e=0;e<t.length;e++){var a=t[e];"preload"!==a.rel||"style"!==a.getAttribute("as")||a.getAttribute("data-loadcss")||(a.setAttribute("data-loadcss",!0),o.bindMediaToggle(a))}},!o.support()){o.poly();var t=n.setInterval(o.poly,500);n.addEventListener?n.addEventListener("load",function(){o.poly(),n.clearInterval(t)}):n.attachEvent&&n.attachEvent("onload",function(){o.poly(),n.clearInterval(t)})}"undefined"!=typeof exports?exports.loadCSS=loadCSS:n.loadCSS=loadCSS}("undefined"!=typeof global?global:this);</script>


resulteert in:

![feature 4](https://lh3.googleusercontent.com/-zz1P_rpVid3ZXkxc1-Rn9Wu6zsP2wRuw4sRs_9AnX8nnSYkYkHd8u-usEtw7_zMQ75e5lCdhRTk3bp5b7tlGAOf4PPHgEvRumj25FnhpkPCTEvs-zO2exwMlrbE6MvOscjaNNk7ahXOsF7x4diZ7UTnPvRwSFoQgnddvuN91JQgCsJPW9NCvWVYWhmRnagGRUWs099E-KLbOeigFUdIue-FZeX6NI6QyEdJp_xIqKfsxU3wAPht3AezZ9F8IJ5buQ4xWNvwkkyDOIrIYnGh71H7x-45Bps7aGPIBzhqf4K3UiDDpN6BcsQSEIkiiF4TGyufVb77NYnBwdfi7hHkBR4Ln94U8G9eVzYTb5kiIjwh0bLsYKaInCBQxFulNFVYEThZO9QkUO4_QMou0JEkSthKkXQPgJlYuDnIfoEEAIQEG0lQLioWSwxnXsL8-KfMifWW1U8NdVaI7cIvcXUndZN65Fe2_Qa_nk6BuuOCzgfXypfrQI1Qc9Z2GZ_yX9lte6iijQRJjkx7YWkGsjbIx4k5mz_WORMenYnjcCUHQ0JuAIwLRC5h52eBeuR8-P3un81SPPQpaAOiC3a_Mqc46oOBl9PIBqVZM4hnykc=w1652-h1504-no)

## Toekomstige feature

Waar ik nu nog niet aan toe ben gekomen is het minifieën van de css assets. Dat zal in een snellere laadtijd resulteren. 

Ook zou ik de foto's naar betere formaten kunnen omzetten. Hoe meer de foto's gecomprimeerd kunnen worden hoe beter de laadtijd zal zijn.














