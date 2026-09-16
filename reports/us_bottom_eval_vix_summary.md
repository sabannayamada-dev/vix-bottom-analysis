# 米国株の底評価とVIXの関係 分析メモ

- 元CSV: stock_analysis_全部入り.csv
- 米国株抽出ルール: 銅柄コードに市場サフィックス（例: .T）が無い行
- 米国株の検出行: 158件
- VIX突合件数: 150件、候補日範囲: 1990-06-06 - 2026-06-02
- VIXデータ範囲: 1990-01-02 - 2026-07-21
- 日付突合: 候補日当日、なければ直前営業日（最大7暦日前）
- 評価カテゴリ別ANOVA permutation p: 0.0270
- 評価スコア（早すぎ=0、許容=1、成功=2）とのSpearman相関: 0.1492

## カテゴリ別VIX水準

| eval | count | mean | median | std | q25 | q75 | pct_ge_20 | pct_ge_25 | pct_ge_30 | pct_ge_40 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 成功 | 25 | 19.072 | 16.57 | 5.036 | 15.41 | 24.28 | 40.0 | 8.0 | 4.0 | 0.0 |
| 早すぎ | 89 | 18.042 | 16.62 | 6.228 | 13.61 | 20.63 | 27.0 | 10.1 | 6.7 | 0.0 |
| 許容 | 36 | 22.424 | 18.815 | 13.144 | 13.512 | 24.102 | 44.4 | 19.4 | 19.4 | 8.3 |

## VIX四分位別

| quartile | n | early_rate | ok_rate | mean_val | min_val | max_val |
| --- | --- | --- | --- | --- | --- | --- |
| Q1_low | 39 | 66.7 | 33.3 | 12.62 | 9.9 | 13.65 |
| Q2 | 36 | 61.1 | 38.9 | 15.39 | 13.67 | 16.87 |
| Q3 | 37 | 62.2 | 37.8 | 19.22 | 16.95 | 21.25 |
| Q4_high | 38 | 47.4 | 52.6 | 29.8 | 21.33 | 60.9 |

## VIX閾値別

| threshold | n | early_rate | ok_rate |
| --- | --- | --- | --- |
| >=15 | 98 | 56.1 | 43.9 |
| >=20 | 50 | 48.0 | 52.0 |
| >=25 | 18 | 50.0 | 50.0 |
| >=30 | 14 | 42.9 | 57.1 |
| >=35 | 5 | 40.0 | 60.0 |
| >=40 | 3 | 0.0 | 100.0 |

## 抽出銅柄例

| index | ticker_clean | 名称 | 底打ち候補日 | 成否 | vix_close |
| --- | --- | --- | --- | --- | --- |
| 0 | ADI | Analog Devices, Inc. | 1990/6/6 | 早すぎ | 17.42 |
| 1 | KLIC | Kulicke and Soffa Industries, Inc. | 1992/11/20 | 早すぎ | 13.67 |
| 2 | COST | Costco Wholesale Corporation | 1993/6/17 | 早すぎ | 11.66 |
| 3 | BSX | Boston Scientific Corporation | 1994/8/22 | 成功 | 12.62 |
| 4 | ROST | Ross Stores, Inc. | 1995/7/19 | 許容 | 13.49 |
| 5 | REGN | Regeneron Pharmaceuticals, Inc. | 1997/9/19 | 早すぎ | 22.74 |
| 6 | CPRT | Copart, Inc. | 1998/4/14 | 許容 | 21.61 |
| 7 | NKE | NIKE, Inc. | 1998/4/23 | 早すぎ | 20.6 |
| 8 | DE | Deere & Company | 1999/3/19 | 早すぎ | 24.32 |
| 9 | APH | Amphenol Corporation | 1999/7/19 | 許容 | 19.07 |
| 10 | DHR | Danaher Corporation | 2000/4/3 | 許容 | 24.03 |
| 11 | NOC | Northrop Grumman Corporation | 2000/4/19 | 成功 | 27.02 |
| 12 | XLB | State Street Materials Select Sector SPDR ETF | 2000/12/27 | 早すぎ | 28.14 |
| 13 | WM | Waste Management, Inc. | 2001/6/15 | 早すぎ | 22.81 |
| 14 | CCEP | Coca-Cola Europacific Partners PLC | 2001/10/18 | 早すぎ | 34.95 |
| 15 | CTSH | Cognizant Technology Solutions Corporation | 2002/4/18 | 早すぎ | 19.29 |
| 16 | ISRG | Intuitive Surgical, Inc. | 2002/4/25 | 早すぎ | 20.95 |
| 17 | DIOD | Diodes Incorporated | 2002/5/16 | 早すぎ | 18.5 |
| 18 | XLF | State Street Financial Select Sector SPDR ETF | 2002/10/17 | 早すぎ | 34.1 |
| 19 | TMO | Thermo Fisher Scientific Inc. | 2002/10/25 | 許容 | 30.0 |
| 20 | COHR | Coherent Corp. | 2002/11/6 | 成功 | 30.73 |
| 21 | QQQ | Invesco QQQ Trust | 2003/3/17 | 許容 | 31.75 |
| 22 | QQQ | Invesco QQQ Trust | 2003/3/17 | 許容 | 31.75 |
| 23 | MCK | McKesson Corporation | 2003/5/2 | 早すぎ | 20.63 |
| 24 | AAPL | Apple Inc. | 2003/5/8 | 許容 | 21.24 |
| 25 | XLU | State Street Utilities Select Sector SPDR ETF | 2003/5/28 | 許容 | 20.03 |
| 26 | ROP | Roper Technologies, Inc. | 2003/6/2 | 成功 | 20.85 |
| 27 | ASX | ASE Technology Holding Co., Ltd. | 2003/6/19 | 早すぎ | 19.8 |
| 28 | SOXX | iShares Semiconductor ETF | 2003/8/20 | 早すぎ | 17.82 |
| 29 | SOXX | iShares Semiconductor ETF | 2003/8/20 | 早すぎ | 17.82 |
