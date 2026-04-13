# 娴忚鍣ㄨ嚜鍔ㄥ寲 MCP 鍏ㄩ潰瀵规瘮鎶ュ憡

<table width="100%">
<tr>
<td><a href="../">鈫?杩斿洖 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

## 鎵ц鎽樿

鍩轰簬瀵逛綘鎴浘涓袱绉嶆柟妗堜互鍙婄涓変釜涓绘祦鏂规鐨勭爺绌讹紝杩欎唤鎶ュ憡姣旇緝浜嗭細

1. **Chrome DevTools MCP**
2. **Claude in Chrome**
3. **Playwright MCP**

鐩爣鏄府鍔╀綘涓鸿嚜鍔ㄥ寲娴嬭瘯銆佹祻瑙堝櫒璋冭瘯鍜屾棩甯搁獙璇侀€夋嫨鏈€鍚堥€傜殑宸ュ叿銆?
---

## 1. 涓変釜鍊欓€夋柟妗?
### A. Chrome DevTools MCP锛堟埅鍥?1锛?
- **鏉ユ簮**锛欸oogle Chrome 瀹樻柟鍥㈤槦
- **鍙戝竷鏃堕棿**锛?025 骞?9 鏈堝叕寮€棰勮
- **鏋舵瀯**锛氬熀浜?Chrome DevTools Protocol锛圕DP锛変笌 Puppeteer
- **Token 鍗犵敤**锛氱害 19.0k tokens锛堜笂涓嬫枃鐨?9.5%锛?- **宸ュ叿鏁伴噺**锛?6 涓紝瑕嗙洊 6 澶х被

### B. Claude in Chrome锛堟埅鍥?2锛?
- **鏉ユ簮**锛欰nthropic 瀹樻柟鎵╁睍
- **鐘舵€?*锛欱eta锛岄€愭鍚?Pro / Max / Team / Enterprise 鐢ㄦ埛寮€鏀?- **鏋舵瀯**锛氭祻瑙堝櫒鎵╁睍 + computer-use 鑳藉姏
- **Token 鍗犵敤**锛氱害 15.4k tokens锛堜笂涓嬫枃鐨?7.7%锛?- **宸ュ叿鏁伴噺**锛?6 涓紝鍖呭惈娴忚鍣ㄦ帶鍒朵笌鐢佃剳鎿嶄綔鑳藉姏

### C. Playwright MCP锛堝己鍔涙浛浠ｆ柟妗堬級

- **鏉ユ簮**锛歁icrosoft 瀹樻柟涓庣ぞ鍖虹敓鎬?- **鏋舵瀯**锛氬熀浜庡彲璁块棶鎬ф爲鐨勬祻瑙堝櫒鑷姩鍖?- **Token 鍗犵敤**锛氱害 13.7k tokens锛堜笂涓嬫枃鐨?6.8%锛?- **宸ュ叿鏁伴噺**锛?1 涓?
---

## 2. 璇︾粏鑳藉姏瀵规瘮

| 鑳藉姏 | Chrome DevTools MCP | Claude in Chrome | Playwright MCP |
|------|---------------------|------------------|----------------|
| **涓昏鐢ㄩ€?* | 璋冭瘯涓庢€ц兘鍒嗘瀽 | 閫氱敤娴忚鍣ㄨ嚜鍔ㄥ寲 | UI 娴嬭瘯涓?E2E |
| **娴忚鍣ㄦ敮鎸?* | 浠?Chrome | 浠?Chrome | Chromium銆丗irefox銆乄ebKit |
| **Token 鏁堢巼** | 19.0k锛?.5%锛?| 15.4k锛?.7%锛?| 13.7k锛?.8%锛?|
| **鍏冪礌瀹氫綅** | CSS / XPath | 瑙嗚 + DOM | 鍙闂€ф爲锛堣涔夊寲锛?|
| **鎬ц兘杩借釜** | 寰堝己 | 涓嶆敮鎸?| 鏈夐檺 |
| **缃戠粶璇锋眰妫€鏌?* | 寰堝己 | 鍩虹 | 鍩虹 |
| **鎺у埗鍙版棩蹇?* | 瀹屾暣璁块棶 | 瀹屾暣璁块棶 | 鏈夐檺 |
| **璺ㄦ祻瑙堝櫒** | 鍚?| 鍚?| 鏄?|
| **CI/CD 闆嗘垚** | 寰堥€傚悎 | 寰堝樊锛堜緷璧栫櫥褰曟€侊級 | 寰堥€傚悎 |
| **Headless 妯″紡** | 鏀寔 | 涓嶆敮鎸?| 鏀寔 |
| **璁よ瘉鏂瑰紡** | 闇€瑕佸崟鐙厤缃?| 鐩存帴澶嶇敤浣犵殑娴忚鍣ㄤ細璇?| 闇€瑕佸崟鐙厤缃?|
| **瀹氭椂浠诲姟** | 涓嶆敮鎸?| 鏀寔 | 涓嶆敮鎸?|
| **鎴愭湰** | 鍏嶈垂 | 闇€瑕佷粯璐规柟妗?| 鍏嶈垂 |
| **鏈湴瀹夎** | 闇€瑕?Node.js | 瀹夎娴忚鍣ㄦ墿灞曞嵆鍙?| 闇€瑕?Node.js |

---

## 3. 宸ュ叿鏋勬垚

### Chrome DevTools MCP锛?6 涓伐鍏凤級

```text
杈撳叆鑷姩鍖栵紙8锛? click, drag, fill, fill_form, handle_dialog,
                 hover, press_key, upload_file

椤甸潰瀵艰埅锛?锛?   close_page, list_pages, navigate_page,
                 new_page, select_page, wait_for

鐜妯℃嫙锛?锛?   emulate, resize_page

鎬ц兘鍒嗘瀽锛?锛?   performance_analyze_insight,
                 performance_start_trace, performance_stop_trace

缃戠粶锛?锛?       get_network_request, list_network_requests

璋冭瘯锛?锛?       evaluate_script, get_console_message,
                 list_console_messages, take_screenshot,
                 take_snapshot
```

### Claude in Chrome锛?6 涓伐鍏凤級

```text
娴忚鍣ㄦ帶鍒?      navigate, read_page, find, computer
                锛堢偣鍑汇€佽緭鍏ャ€佹粴鍔級

琛ㄥ崟浜や簰:        form_input, javascript_tool

濯掍綋:            upload_image, get_page_text, gif_creator

鏍囩椤电鐞?      tabs_context_mcp, tabs_create_mcp

寮€鍙戣緟鍔?        read_console_messages, read_network_requests

瀹炵敤宸ュ叿:        shortcuts_list, shortcuts_execute,
                 resize_window, update_plan
```

### Playwright MCP锛?1 涓伐鍏凤級

```text
瀵艰埅:            navigate, goBack, goForward, reload

浜や簰:            click, fill, select, hover, press,
                 drag, uploadFile

鍏冪礌鏌ヨ:        getElement, getElements, waitForSelector

鏂█:            assertVisible, assertText, assertTitle

椤甸潰鐘舵€?        screenshot, getAccessibilityTree,
                 evaluateScript

娴忚鍣ㄧ鐞?      newPage, closePage
```

---

## 4. 鐢ㄤ緥鍒嗘瀽锛氳嚜鍔ㄥ寲娴嬭瘯鏃惰鎬庝箞閫?
### Chrome DevTools MCP 鏈€閫傚悎

- **鎬ц兘娴嬭瘯**
  - 褰曞埗鎬ц兘 trace 涓?Core Web Vitals
  - 鏌ユ壘娓叉煋鐡堕涓庡竷灞€鍋忕Щ
  - 鍋?CPU 鍒嗘瀽涓庡唴瀛樻硠婕忔帓鏌?- **娣卞害璋冭瘯**
  - 鏌ョ湅璇锋眰澶淬€佸搷搴斾綋銆佹椂闂寸嚎
  - 鍒嗘瀽鎺у埗鍙伴敊璇笌鍫嗘爤
  - 瀹炴椂妫€鏌?DOM
- **CI/CD 鍦烘櫙**
  - 鏀寔 headless
  - 鏇撮€傚悎鑴氭湰鍖栦笌绋冲畾鎵ц
  - 涓嶄緷璧栫湡瀹炵敤鎴风櫥褰曟€?
鏈€鍏稿瀷鐨勯棶棰樻槸锛?
- 鈥滆繖涓〉闈负浠€涔堟參锛熲€?- 鈥滆繖涓帴鍙ｈ姹傚埌搴曞摢閲屽嚭闂浜嗭紵鈥?
### Claude in Chrome 鏈€閫傚悎

- **浜哄伐娴嬭瘯杈呭姪**
  - 鍦ㄥ凡鐧诲綍璐︽埛鐘舵€佷笅娴嬭瘯
  - 鍋氬甫瑙嗚涓婁笅鏂囩殑鎺㈢储寮忛獙璇?  - 褰曞埗骞堕噸鏀炬搷浣滄祦绋?- **蹇€熼獙鏀?*
  - 瀵圭収璁捐绋挎鏌ョ晫闈?  - 蹇€熺‘璁ゆ柊鍔熻兘鏄惁姝ｅ父
  - 寮€鍙戞椂鐩存帴璇诲彇 console 閿欒
- **鏃ュ父閲嶅娴忚鍣ㄦ搷浣?*
  - 瀹氭椂妫€鏌?  - 澶氭爣绛惧伐浣滄祦
  - 鍩轰簬浣犵殑鐪熷疄鎿嶄綔涔犳儻瀹屾垚浠诲姟

鍏稿瀷闂鏄細

- 鈥滄垜鍒氭敼瀹岋紝杩欎釜椤甸潰鐪嬭捣鏉ュ鍚楋紵鈥?- 鈥滃府鎴戠敤鐜板湪鐨勭櫥褰曟€佹妸琛ㄥ崟璧颁竴閬嶃€傗€?
### Playwright MCP 鏈€閫傚悎

- **绔埌绔祴璇曡嚜鍔ㄥ寲**
  - 璺ㄦ祻瑙堝櫒娴嬭瘯
  - 鐢熸垚鍙鐢ㄦ祴璇曡剼鏈?  - 閫傚悎 Page Object Model
- **绋冲畾 UI 娴嬭瘯**
  - 鍩轰簬鍙闂€ф爲锛岄€夋嫨鍣ㄦ洿绋?  - 浜や簰鏇寸‘瀹氾紝灏戜緷璧栬剢寮?DOM
  - 涓嶅鏄撳洜 UI 灏忔敼鍔ㄥ氨鏁翠綋澶辨晥
- **CI/CD 闆嗘垚**
  - 鍙?headless 璺戞祦姘寸嚎
  - 鍙粠鑷劧璇█鐢熸垚 Playwright 鑴氭湰
  - 鏂逛究鎺ュ叆娴嬭瘯骞冲彴

鍏稿瀷闂鏄細

- 鈥滅粰杩欎釜鐢ㄦ埛娴佺▼鍐欎竴濂?E2E銆傗€?- 鈥滃府鎴戞妸杩欐潯璺緞鍦ㄥ涓祻瑙堝櫒涓婇兘璺戜竴閬嶃€傗€?
---

## 5. Token 鏁堢巼瀵规瘮

| 宸ュ叿 | Token 鍗犵敤 | 涓婁笅鏂囧崰姣?| 鏁堢巼璇勭骇 |
|------|------------|------------|----------|
| Playwright MCP | 绾?13.7k | 6.8% | 鏈€浼?|
| Claude in Chrome | 绾?15.4k | 7.7% | 鑹ソ |
| Chrome DevTools MCP | 绾?19.0k | 9.5% | 鍙帴鍙?|

濡傛灉浣犵殑涓婁笅鏂囩獥鍙ｆ槸 200k锛?
- Playwright 澶х害杩樿兘鐣欎笅 186.3k 缁欎唬鐮佸拰浠诲姟涓婁笅鏂?- Claude in Chrome 澶х害杩樿兘鐣欎笅 184.6k
- Chrome DevTools 澶х害杩樿兘鐣欎笅 181k

褰撲綘鍦ㄥ鏉備粨搴撻噷鍋氶暱閾捐矾浠诲姟鏃讹紝杩欏嚑鍗?token 鐨勫樊璺濇槸鏈夊疄闄呮剰涔夌殑銆?
---

## 6. 瀹夊叏鎬ц€冭檻

### Chrome DevTools MCP

- 榛樿浣跨敤闅旂娴忚鍣ㄩ厤缃?- 涓嶄緷璧栦簯绔?- 鏈湴鍙帶鎬у己
- 闇€瑕佹敞鎰忚繙绋嬭皟璇曠鍙ｇ殑瀹夊叏杈圭晫

### Claude in Chrome

- 鍦ㄧ己灏戦槻鎶ゆ椂锛屾浘鎶ュ憡绾?**23.6%** 鐨勬敾鍑绘垚鍔熺巼锛涘姞闃叉姢鍚庡彲闄嶈嚦 **11.2%**
- 鐩存帴澶嶇敤浣犵湡瀹炴祻瑙堝櫒浼氳瘽锛屽瓨鍦?cookie 鏆撮湶椋庨櫓
- 瀵归噾铻嶃€佹垚浜恒€佺洍鐗堢瓑绔欑偣鏈夎闂檺鍒?- 浠嶅睘浜?Beta锛屽凡鐭ラ闄╁皻鏈畬鍏ㄦ敹鏁?
### Playwright MCP

- 浣跨敤闅旂涓婁笅鏂?- 涓嶄緷璧栦簯绔?- 鐢?Microsoft 缁存姢锛屽畨鍏ㄦā鍨嬫垚鐔?- 鍙互杈冨畨鍏ㄥ湴绠＄悊璁よ瘉娴佺▼

---

## 7. 瀹夎鍛戒护

### Chrome DevTools MCP

```bash
claude mcp add chrome-devtools npx chrome-devtools-mcp@latest
```

### Claude in Chrome

```text
浠?Chrome Web Store 瀹夎锛堥渶瑕?Pro / Max / Team / Enterprise 鏂规锛?```

### Playwright MCP

```bash
# 鍏堝畨瑁呮祻瑙堝櫒
npx playwright install

# 鍐嶆妸 MCP 鍔犲埌 Claude Code
claude mcp add playwright -s user -- npx @playwright/mcp@latest
```

---

## 8. 鎺ㄨ崘鏂规

### 浣犵殑鑷姩鍖栨祴璇曞伐浣滄祦棣栭€夛細Playwright MCP

閫傜敤鍦烘櫙锛?
- 鏃ュ父 E2E 娴嬭瘯
- 璺ㄦ祻瑙堝櫒楠岃瘉
- 鐢熸垚鍙鐢ㄦ祴璇曡剼鏈?
鍘熷洜锛?
- Token 鍗犵敤鏈€浣?- 鏀寔璺ㄦ祻瑙堝櫒
- 鍩轰簬鍙闂€ф爲锛屽畾浣嶆洿绋?- 闈炲父閫傚悎 CI/CD
- 鑳界洿鎺ョ敓鎴?Playwright 娴嬭瘯鏂囦欢
- 鍏嶈垂锛屼笉渚濊禆楂樼骇璁㈤槄

### 绗簩鎺ㄨ崘锛欳hrome DevTools MCP

閫傜敤鍦烘櫙锛?
- 鎬ц兘璋冧紭
- 缃戠粶璇锋眰鍒嗘瀽
- Core Web Vitals 鎺掓煡

鍘熷洜锛?
- 鍦ㄦ€ц兘杩借釜鍜岃皟璇曚笂鍑犱箮娌℃湁鏇夸唬鍝?- 缃戠粶灞傚彲瑙佹€ф渶濂?- 鐢?Google 瀹樻柟缁存姢
- 褰撻棶棰樺彉鎴愨€滀负浠€涔堟參鈥濇椂锛屽畠灏辨槸鏈€寮哄伐鍏?
### 鏈夋潯浠跺啀鐢細Claude in Chrome

閫傜敤鍦烘櫙锛?
- 鐧诲綍鎬佷笅鐨勬墜宸ラ獙鏀?- 鎺㈢储寮忔祴璇?- 瑙嗚灞傚揩閫熸鏌?
鍘熷洜锛?
- 寰堥€傚悎寮€鍙戣繃绋嬩腑鐨勫揩閫熺‘璁?- 鑳藉鐢ㄤ綘褰撳墠娴忚鍣ㄩ噷鐨勭湡瀹炵姸鎬?- 閫傚悎鈥滃厛鐪嬩竴涓嬫槸鍚︽甯糕€濊繖绉嶄换鍔?- 涓嶉€傚悎鍋氫弗鑲冪殑 CI/CD 鑷姩鍖栦富鍔?
---

## 9. 寤鸿鐨勭粍鍚堝畨瑁呮柟寮?
```bash
npx playwright install
claude mcp add playwright -s user -- npx @playwright/mcp@latest
claude mcp add chrome-devtools -s user -- npx chrome-devtools-mcp@latest
```

寤鸿宸ヤ綔娴侊細

```text
1. 寮€鍙?      -> Claude Code锛堢粓绔級
2. 娴嬭瘯       -> Playwright MCP锛圗2E / 璺ㄦ祻瑙堝櫒锛?3. 璋冭瘯       -> Chrome DevTools MCP锛堟€ц兘 / 缃戠粶锛?4. 楠屾敹       -> Claude in Chrome锛堝揩閫熻瑙夋鏌ワ級
5. CI/CD      -> Playwright MCP锛堟棤澶磋嚜鍔ㄥ寲锛?```

---

## 10. 鏈€缁堢粨璁?
| 浣犵殑闇€姹?| 鎺ㄨ崘宸ュ叿 |
|----------|----------|
| 璺ㄦ祻瑙堝櫒 E2E | **Playwright MCP** |
| 鎬ц兘鍒嗘瀽 | **Chrome DevTools MCP** |
| 缃戠粶璋冭瘯 | **Chrome DevTools MCP** |
| 蹇€熻瑙夐獙鏀?| **Claude in Chrome** |
| CI/CD 鑷姩鍖?| **Playwright MCP** |
| 鐢熸垚娴嬭瘯鑴氭湰 | **Playwright MCP** |
| 鏈€浣?token 鍗犵敤 | **Playwright MCP** |
| 鐧诲綍鎬佹祴璇?| **Claude in Chrome** |
| Console 鏃ュ織鎺掓煡 | **Chrome DevTools MCP** |

### TL;DR

**寤鸿鍚屾椂瀹夎 Playwright MCP 鍜?Chrome DevTools MCP銆?*

- 鎶?**Playwright MCP** 褰撴垚涓绘祴璇曞伐鍏枫€?- 鎶?**Chrome DevTools MCP** 褰撴垚鎬ц兘涓庤皟璇曞伐鍏枫€?- 鎶?**Claude in Chrome** 鐣欑粰闇€瑕佺櫥褰曟€佸拰瑙嗚鍒ゆ柇鐨勮交閲忓満鏅€?
---

## 璧勬枡鏉ユ簮

- [Chrome DevTools MCP - GitHub](https://github.com/ChromeDevTools/chrome-devtools-mcp)
- [Anthropic - Piloting Claude in Chrome](https://claude.com/blog/claude-for-chrome)
- [Claude in Chrome Help Center](https://support.claude.com/en/articles/12012173-getting-started-with-claude-in-chrome)
- [Playwright MCP - GitHub](https://github.com/microsoft/playwright-mcp)
- [Simon Willison - Using Playwright MCP with Claude Code](https://til.simonwillison.net/claude-code/playwright-mcp-claude-code)
- [Testomat.io - Playwright MCP Claude Code](https://testomat.io/blog/playwright-mcp-claude-code/)
- [MCP Integration Guide - Scrapeless](https://www.scrapeless.com/en/blog/mcp-integration-guide)
- [Chrome DevTools MCP Guide - Vladimir Siedykh](https://vladimirsiedykh.com/blog/chrome-devtools-mcp-ai-browser-debugging-complete-guide-2025)
- [Addy Osmani - Give your AI eyes](https://addyosmani.com/blog/devtools-mcp/)

---

*杩欎唤鎶ュ憡鐢?Claude Code 鐢熸垚锛屽師濮嬬増鏈娇鐢?Opus 4.5 妯″瀷缂栧啓浜?2025 骞?12 鏈?19 鏃ャ€?

