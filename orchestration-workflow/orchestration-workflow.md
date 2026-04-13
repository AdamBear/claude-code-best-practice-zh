# 缂栨帓宸ヤ綔娴?
鏈枃妗ｄ粙缁?**Command 鈫?Agent锛堝甫鎶€鑳斤級鈫?Skill** 鐨勭紪鎺掑伐浣滄祦锛屽苟閫氳繃涓€涓ぉ姘旀暟鎹幏鍙栦笌 SVG 娓叉煋绯荤粺鏉ユ紨绀恒€?
<table width="100%">
<tr>
<td><a href="../">鈫?杩斿洖 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

## 绯荤粺姒傝

澶╂皵绯荤粺鍦ㄥ悓涓€涓紪鎺掑伐浣滄祦涓紨绀轰簡涓ょ涓嶅悓鐨勬妧鑳芥ā寮忥細
- **Agent Skills**锛堥鍔犺浇锛夛細`weather-fetcher` 浼氬湪鍚姩鏃朵綔涓洪鍩熺煡璇嗘敞鍏ュ埌 `weather-agent`
- **Skills**锛堢嫭绔嬭皟鐢級锛歚weather-svg-creator` 鐢卞懡浠ら€氳繃 Skill 宸ュ叿鐩存帴璋冪敤

杩欏睍绀轰簡 **Command 鈫?Agent 鈫?Skill** 鏋舵瀯妯″紡锛屽叾涓細
- 鍛戒护璐熻矗缂栨帓宸ヤ綔娴佸苟澶勭悊鐢ㄦ埛浜や簰
- 浠ｇ悊浣跨敤鑷繁棰勫姞杞界殑鎶€鑳借幏鍙栨暟鎹?- 鎶€鑳界嫭绔嬪垱寤哄彲瑙嗗寲杈撳嚭

## 缁勪欢鎽樿

| 缁勪欢 | 瑙掕壊 | 绀轰緥 |
|------|------|------|
| **Command** | 鍏ュ彛鐐广€佺敤鎴蜂氦浜?| [`/weather-orchestrator`](../.claude/commands/weather-orchestrator.md) |
| **Agent** | 浣跨敤棰勫姞杞芥妧鑳借幏鍙栨暟鎹紙Agent 鎶€鑳斤級 | [`weather-agent`](../.claude/agents/weather-agent.md) 鎼厤 [`weather-fetcher`](../.claude/skills/weather-fetcher/SKILL.md) |
| **Skill** | 鐙珛鍒涘缓杈撳嚭锛堟妧鑳斤級 | [`weather-svg-creator`](../.claude/skills/weather-svg-creator/SKILL.md) |

## 娴佺▼鍥?
```text
+----------------------------------------------------------------------------------+
|                                   缂栨帓宸ヤ綔娴?                                    |
|                           Command -> Agent -> Skill                              |
+----------------------------------------------------------------------------------+

                              +----------------------+
                              |      鐢ㄦ埛浜や簰        |
                              +----------------------+
                                          |
                                          v
        +-------------------------------------------------------------------+
        | /weather-orchestrator - Command锛堝叆鍙ｇ偣锛?                         |
        +-------------------------------------------------------------------+
                                          |
                                     姝ラ 1
                                          |
                                          v
                          +----------------------------------+
                          | AskUser锛氶€夋嫨 C掳 杩樻槸 F掳锛?      |
                          +----------------------------------+
                                          |
                               姝ラ 2 - Agent 宸ュ叿
                                          |
                                          v
        +-------------------------------------------------------------------+
        | weather-agent - Agent + 鎶€鑳斤細weather-fetcher                     |
        +-------------------------------------------------------------------+
                                          |
                               杩斿洖锛氭俯搴?+ 鍗曚綅
                                          |
                               姝ラ 3 - Skill 宸ュ叿
                                          |
                                          v
        +-------------------------------------------------------------------+
        | weather-svg-creator - Skill + SVG 鍗＄墖 + 杈撳嚭                     |
        +-------------------------------------------------------------------+
                                          |
                           +------------------+   +------------------+
                           |   weather.svg    |   |    output.md     |
                           +------------------+   +------------------+
```

## 缁勪欢璇︽儏

### 1. Command

#### `/weather-orchestrator`锛圕ommand锛?- **浣嶇疆**锛歚.claude/commands/weather-orchestrator.md`
- **鐢ㄩ€?*锛氬叆鍙ｇ偣锛岃礋璐ｇ紪鎺掑伐浣滄祦骞跺鐞嗙敤鎴蜂氦浜?- **鍔ㄤ綔**锛?  1. 璇㈤棶鐢ㄦ埛鍋忓ソ鐨勬俯搴﹀崟浣嶏紙鎽勬皬 / 鍗庢皬锛?  2. 閫氳繃 Agent 宸ュ叿璋冪敤 weather-agent
  3. 閫氳繃 Skill 宸ュ叿璋冪敤 weather-svg-creator
- **妯″瀷**锛歨aiku

### 2. 甯﹂鍔犺浇鎶€鑳界殑 Agent锛圓gent Skill锛?
#### `weather-agent`锛圓gent锛?- **浣嶇疆**锛歚.claude/agents/weather-agent.md`
- **鐢ㄩ€?*锛氫娇鐢ㄩ鍔犺浇鎶€鑳借幏鍙栧ぉ姘旀暟鎹?- **鎶€鑳?*锛歚weather-fetcher`锛堜綔涓洪鍩熺煡璇嗛鍔犺浇锛?- **鍙敤宸ュ叿**锛歐ebFetch銆丷ead
- **妯″瀷**锛歴onnet
- **棰滆壊**锛歡reen
- **璁板繂**锛歱roject

璇ヤ唬鐞嗕細鍦ㄥ惎鍔ㄦ椂鎶?`weather-fetcher` 棰勫姞杞借繘涓婁笅鏂囥€傚畠鎸夌収鎶€鑳戒腑鐨勮鏄庤幏鍙栨俯搴︼紝鐒跺悗鎶婄粨鏋滆繑鍥炵粰鍛戒护銆?
### 3. Skill

#### `weather-svg-creator`锛圫kill锛?- **浣嶇疆**锛歚.claude/skills/weather-svg-creator/SKILL.md`
- **鐢ㄩ€?*锛氬垱寤哄彲瑙嗗寲 SVG 澶╂皵鍗＄墖骞跺啓鍑鸿緭鍑烘枃浠?- **璋冪敤鏂瑰紡**锛氱敱鍛戒护閫氳繃 Skill 宸ュ叿璋冪敤锛屼笉浼氶鍔犺浇鍒颁换浣曚唬鐞嗛噷
- **杈撳嚭**锛?  - `orchestration-workflow/weather.svg` - SVG 澶╂皵鍗＄墖
  - `orchestration-workflow/output.md` - 澶╂皵鎽樿

### 4. 棰勫姞杞芥妧鑳?
#### `weather-fetcher`锛圫kill锛?- **浣嶇疆**锛歚.claude/skills/weather-fetcher/SKILL.md`
- **鐢ㄩ€?*锛氭彁渚涜幏鍙栧疄鏃舵俯搴︽暟鎹殑璇存槑
- **鏁版嵁婧?*锛氳开鎷滐紙闃胯仈閰嬶級鐨?Open-Meteo API
- **杈撳嚭**锛氭俯搴﹀€间笌鍗曚綅锛堟憚姘忔垨鍗庢皬锛?- **璇存槑**锛氳繖鏄竴涓?Agent 鎶€鑳斤紝浼氶鍔犺浇杩?`weather-agent`锛岃€屼笉鏄鐩存帴璋冪敤

## 鎵ц娴佺▼

1. **鐢ㄦ埛璋冪敤**锛氱敤鎴疯繍琛?`/weather-orchestrator` 鍛戒护
2. **鐢ㄦ埛鎻愮ず**锛氬懡浠よ闂敤鎴锋兂瑕佺殑娓╁害鍗曚綅锛堟憚姘?/ 鍗庢皬锛?3. **璋冪敤浠ｇ悊**锛氬懡浠ら€氳繃 Agent 宸ュ叿璋冪敤 `weather-agent`
4. **鎶€鑳芥墽琛?*锛堝湪浠ｇ悊涓婁笅鏂囧唴锛夛細
   - 浠ｇ悊鎸夌収 `weather-fetcher` 鎶€鑳借鏄庝粠 Open-Meteo 鑾峰彇娓╁害
   - 浠ｇ悊鎶婃俯搴﹀€煎拰鍗曚綅杩斿洖缁欏懡浠?5. **鍒涘缓 SVG**锛氬懡浠ら€氳繃 Skill 宸ュ叿璋冪敤 `weather-svg-creator`
   - 鎶€鑳藉湪 `orchestration-workflow/weather.svg` 鐢熸垚 SVG 澶╂皵鍗＄墖
   - 鎶€鑳芥妸鎽樿鍐欏叆 `orchestration-workflow/output.md`
6. **鏄剧ず缁撴灉**锛氬悜鐢ㄦ埛鏄剧ず鎽樿锛屽寘鎷細
   - 璇锋眰鐨勬俯搴﹀崟浣?   - 鑾峰彇鍒扮殑娓╁害
   - SVG 鍗＄墖璺緞
   - 杈撳嚭鏂囦欢璺緞

## 鎵ц绀轰緥

```text
杈撳叆锛?weather-orchestrator
鈹溾攢 姝ラ 1锛氳闂細Celsius 杩樻槸 Fahrenheit锛?鈹? 鈹斺攢 鐢ㄦ埛锛欳elsius
鈹溾攢 姝ラ 2锛欰gent 宸ュ叿 -> weather-agent
鈹? 鈹溾攢 棰勫姞杞芥妧鑳斤細
鈹? 鈹? 鈹斺攢 weather-fetcher锛堥鍩熺煡璇嗭級
鈹? 鈹溾攢 浠?Open-Meteo 鑾峰彇 -> 26掳C
鈹? 鈹斺攢 杩斿洖锛歵emperature=26, unit=Celsius
鈹溾攢 姝ラ 3锛歋kill 宸ュ叿 -> /weather-svg-creator
鈹? 鈹溾攢 鍒涘缓锛歰rchestration-workflow/weather.svg
鈹? 鈹斺攢 鍐欏叆锛歰rchestration-workflow/output.md
鈹斺攢 杈撳嚭锛?   鈹溾攢 鍗曚綅锛欳elsius
   鈹溾攢 娓╁害锛?6掳C
   鈹溾攢 SVG锛歰rchestration-workflow/weather.svg
   鈹斺攢 鎽樿锛歰rchestration-workflow/output.md
```

## 鍏抽敭璁捐鍘熷垯

1. **涓ょ鎶€鑳芥ā寮?*锛氬悓鏃跺睍绀?Agent 鎶€鑳斤紙棰勫姞杞斤級涓庢櫘閫氭妧鑳斤紙鐩存帴璋冪敤锛?2. **Command 浣滀负缂栨帓鍣?*锛氬懡浠よ礋璐ｇ敤鎴蜂氦浜掑苟鍗忚皟鏁翠釜宸ヤ綔娴?3. **Agent 璐熻矗鍙栨暟**锛氫唬鐞嗙敤鑷繁鐨勯鍔犺浇鎶€鑳借幏鍙栨暟鎹悗杩斿洖
4. **Skill 璐熻矗杈撳嚭**锛歋VG 鍒涘缓鍣ㄧ嫭绔嬭繍琛岋紝浠庡懡浠や笂涓嬫枃鎺ユ敹鏁版嵁
5. **鑱岃矗娓呮櫚鍒嗙**锛氳幏鍙栵紙Agent锛夆啋 娓叉煋锛圫kill锛夛紝姣忎釜缁勪欢鍙仛涓€浠朵簨

## 鏋舵瀯妯″紡

### Agent Skill锛堥鍔犺浇锛?
```yaml
# In agent definition (.claude/agents/weather-agent.md)
---
name: weather-agent
skills:
  - weather-fetcher    # Preloaded into agent context at startup
---
```

- **鎶€鑳戒細棰勫姞杞?*锛氬畬鏁存妧鑳藉唴瀹逛細鍦ㄥ惎鍔ㄦ椂娉ㄥ叆浠ｇ悊涓婁笅鏂?- **浠ｇ悊浣跨敤鎶€鑳界煡璇?*锛氫唬鐞嗘寜鐓ч鍔犺浇鎶€鑳戒腑鐨勮鏄庢墽琛?- **娌℃湁鍔ㄦ€佽皟鐢?*锛氳繖浜涙妧鑳芥槸鍙傝€冭祫鏂欙紝鑰屼笉鏄崟鐙皟鐢ㄧ殑鎵ц鍗曞厓

### Skill锛堢洿鎺ヨ皟鐢級

```yaml
# In skill definition (.claude/skills/weather-svg-creator/SKILL.md)
---
name: weather-svg-creator
description: Creates an SVG weather card...
---
```

- **閫氳繃 Skill 宸ュ叿璋冪敤**锛氬懡浠よ皟鐢?`Skill(skill: "weather-svg-creator")`
- **鐙珛鎵ц**锛氬畠杩愯鍦ㄥ懡浠ょ殑涓婁笅鏂囦腑锛岃€屼笉鍦ㄦ煇涓唬鐞嗗唴閮?- **浠庝笂涓嬫枃鎺ユ敹鏁版嵁**锛氫娇鐢ㄥ璇濅腑宸叉彁渚涚殑娓╁害鏁版嵁

