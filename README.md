# 台股版時光機 trader-timemachine-tw

把 [day-trader-skill](https://github.com/Jakeschincariol/day-trader-skill) 的 Time Machine 改成台灣證券交易所版本的 Claude Skill：
用個股最近 60 天的 5 分鐘 K 棒，模擬 10,000 次當天剩餘走勢，算出先碰停利、先碰停損或都沒碰到的機率，並回測同一規則的歷史結果。

- 時區：台北（UTC+8）
- 交易時段：09:00–13:25 連續交易，每天 53 根 5 分鐘 K 棒（13:25–13:30 收盤集合競價 Yahoo 不提供）
- 代號：`2337` 自動轉成 `2337.TW`；上櫃股請輸入 `6488.TWO`
- 只用 Python 標準函式庫，不需安裝套件
- 附旺宏（2337）60 天資料 `2337.TW-60d5m.json.gz`，可離線測試

## 安裝

把 `trader-timemachine-tw` 資料夾壓成 zip（資料夾本身要在 zip 根目錄），到 Claude 的 Customize › Skills 上傳。

## 範例

```bash
python3 trader-timemachine-tw/timemachine_tw.py run --offline trader-timemachine-tw/2337.TW-60d5m.json.gz \
  --symbol 2337 --date 2026-10-20 --entry 102 --stop 100.75 --target 103.25 --entry-time "9:30 AM" --now "2026-10-27 14:00"
```

結果：先碰停利 45.7%、先碰停損 54.1%，平均 R −0.084，接近擲銅板。

## 注意

這是用過去 60 天資料做的模擬，不是預測，也不是投資建議。台股有 10% 漲跌停，跌停鎖死時停損可能賣不掉，實際虧損可能超過 −1R。

## 授權

MIT。原作：Jake Schincariol（day-trader-skill）。
