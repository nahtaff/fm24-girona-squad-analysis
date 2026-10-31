# Football Manager 24 Squad Analysis: Goals vs xG and Wage vs Contribution

A small data analysis project using data exported from my own Football Manager 24 save (Girona, January 2032, mid-season 2031/32). Player and club names come from the game, not from real-world data.

## Questions

1. Which players scored well above or below their expected goals (xG)?
2. Are player wages in line with their goal + assist contribution?

## Data

- Source: Squad table exported from FM24 (HTML format), 21 players, 36 columns.
- Main columns used: Gls, Ast, xG, Mins, Wage, Position, Av Rat.
- Filter: only players with at least 500 minutes played (17 players). Goalkeepers are excluded from both charts, leaving 16 outfield players.

## Method

1. Read the HTML export with `pandas.read_html`.
2. Cleaning: removed the " - Pick Player" suffix from names, fixed name encoding, split `Apps` into `Starts` and `Subs`, converted `Wage` ("£75,000 p/w") to a number, and converted `Transfer Value` ranges to their midpoint.
3. Derived metrics:
   - `xG_diff` = Goals - xG
   - `GA_per90` = (Goals + Assists) / Minutes x 90
4. Visualization with `matplotlib` (labels arranged with `adjustText`).
5. Position groups (Defender, Midfielder, Forward) were derived from the first listed position, then manually corrected for a few players (Nikolov, Moore, Román).

## Results

![Goals vs xG](chart_gol_vs_xg.png)

- Leny Yoro (centre-back) scored 10 goals from 4.47 xG (+5.5) and Lucas Román scored 8 from 4.33 xG (+3.7), both far above expectation.
- Abel Ruiz scored 6 from 8.37 xG (-2.4), the biggest underperformer.
- Ricard Tribulietx, the top scorer with 12 goals, almost exactly matched his xG (11.3).

![Wage vs contribution](chart_gaji_vs_kontribusi.png)

- There is no clear relationship between wage and goals + assists per 90 minutes; the points are widely scattered.
- Mikey Moore and Román produce high output (about 0.56 and 0.62 G+A per 90) on wages under £50,000 per week.
- Michał Karbownik has the highest wage (£120,000), but his output (about 0.58 G+A per 90) is still near the top of the squad, so he cannot simply be called overpaid.

## Limitations

- This is half a season of data, so a gap as large as Yoro's could be variance or set-piece goals. It is treated as an anomaly to verify at the end of the season, not a conclusion.
- G+A per 90 is unfair for defenders and defensive midfielders.
- The Ability and Potential columns were not exported (they are star icons), so player quality is judged only through ratings and match statistics.
- Position grouping is approximate.

## Next steps

- Re-export at the end of the season and check whether the xG gaps for Yoro and Román shrink.
- Add technical and physical attributes plus transfer history for a transfer-efficiency analysis.

## Repository contents

- `analisis_girona.ipynb`: notebook (cleaning and charts)
- `girona_squad_clean.csv`: cleaned data
- `chart_gol_vs_xg.png`, `chart_gaji_vs_kontribusi.png`: visualizations
