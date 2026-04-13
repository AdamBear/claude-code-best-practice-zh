# Claude Code锛氬叏灞€鍔熻兘涓庨」鐩骇鍔熻兘瀵圭収

杩欎唤鎶ュ憡绯荤粺姣旇緝浜?Claude Code 涓摢浜涜兘鍔涘彧鑳芥斁鍦ㄥ叏灞€鐩綍 `~/.claude/` 涓嬩娇鐢紝鍝簺鑳藉姏鍚屾椂鏀寔鍏ㄥ眬涓庨」鐩袱绾ч厤缃€?
<table width="100%">
<tr>
<td><a href="../">鈫?杩斿洖 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

## 鐩綍

1. [姒傝](#姒傝)
2. [浠呮敮鎸佸叏灞€鐨勫姛鑳絔(#浠呮敮鎸佸叏灞€鐨勫姛鑳?
3. [鍚屾椂鏀寔鍏ㄥ眬涓庨」鐩骇鐨勫姛鑳絔(#鍚屾椂鏀寔鍏ㄥ眬涓庨」鐩骇鐨勫姛鑳?
4. [璁剧疆浼樺厛绾(#璁剧疆浼樺厛绾?
5. [鐩綍缁撴瀯瀵圭収](#鐩綍缁撴瀯瀵圭収)
6. [Tasks 浠诲姟绯荤粺](#tasks-浠诲姟绯荤粺)
7. [Agent Teams 鏅鸿兘浣撳洟闃焆(#agent-teams-鏅鸿兘浣撳洟闃?
8. [璁捐鍘熷垯](#璁捐鍘熷垯)
9. [璧勬枡鏉ユ簮](#璧勬枡鏉ユ簮)

---

## 姒傝

Claude Code 閲囩敤浜?*浣滅敤鍩熷垎灞?*璁捐锛氭湁浜涘姛鑳藉悓鏃跺瓨鍦ㄤ簬鍏ㄥ眬鐩綍 `~/.claude/` 鍜岄」鐩洰褰?`.claude/` 涓紝鑰屾湁浜涘姛鑳藉垯鍙厑璁告斁鍦ㄥ叏灞€灞傘€?
鏍稿績鍘熷垯寰堢畝鍗曪細

- 灞炰簬**涓汉鐘舵€?*銆?*璺ㄩ」鐩崗璋冪姸鎬?*鐨勫唴瀹癸紝閫氬父鏀惧湪鍏ㄥ眬灞傘€?- 灞炰簬**鍥㈤槦鍙叡浜殑椤圭洰閰嶇疆**锛屽垯鍙互鏀惧湪椤圭洰灞傘€?
鍙互鎶婁袱灞傜悊瑙ｄ负锛?
- `~/.claude/`锛氫綘鐨?*鐢ㄦ埛绾т富鐩綍**锛屽鎵€鏈夐」鐩敓鏁堛€?- `.claude/`锛氫粨搴撻噷鐨?*椤圭洰绾т富鐩綍**锛屽彧瀵瑰綋鍓嶉」鐩敓鏁堛€?
---

## 浠呮敮鎸佸叏灞€鐨勫姛鑳?
涓嬪垪鑳藉姏**鍙兘**瀛樻斁鍦?`~/.claude/` 涓嬶紝涓嶈兘涓嬫矇鍒伴」鐩洰褰曪細

| 鍔熻兘 | 浣嶇疆 | 浣滅敤 |
|------|------|------|
| **Tasks** | `~/.claude/tasks/` | 鍦ㄤ笉鍚屼細璇濄€佷笉鍚屾櫤鑳戒綋涔嬮棿鎸佷箙鍖栦换鍔″垪琛?|
| **Agent Teams** | `~/.claude/teams/` | 澶氭櫤鑳戒綋鍗忎綔閰嶇疆锛堝疄楠屾€э紝2026 骞?2 鏈堬級 |
| **Auto Memory** | `~/.claude/projects/<hash>/memory/` | Claude 涓烘煇涓」鐩嚜鍔ㄥ啓涓嬬殑涓汉璁板繂锛屼笉闈㈠悜鍥㈤槦鍏变韩 |
| **鍑嵁涓?OAuth** | 绯荤粺閽ュ寵涓?+ `~/.claude.json` | API 瀵嗛挜銆丱Auth token 绛夋晱鎰熶俊鎭?|
| **Keybindings** | `~/.claude/keybindings.json` | 鑷畾涔夊揩鎹烽敭 |
| **MCP 鐢ㄦ埛绾ф湇鍔″櫒** | `~/.claude.json` 涓殑 `mcpServers` | 瀵瑰叏閮ㄩ」鐩彲瑙佺殑涓汉 MCP 鏈嶅姟鍣?|
| **鍋忓ソ涓庣紦瀛?* | `~/.claude.json` | 涓婚銆佹ā鍨嬨€佽緭鍑洪鏍笺€佷細璇濈姸鎬佺瓑涓汉鍋忓ソ |

---

## 鍚屾椂鏀寔鍏ㄥ眬涓庨」鐩骇鐨勫姛鑳?
杩欎簺鑳藉姏鏃㈠彲浠ュ畾涔夊湪鍏ㄥ眬灞傦紝涔熷彲浠ュ畾涔夊湪椤圭洰灞傘€傞€氬父鐢?*椤圭洰灞傝鐩栧叏灞€灞?*锛?
| 鍔熻兘 | 鍏ㄥ眬浣嶇疆 | 椤圭洰浣嶇疆 | 浼樺厛绾?|
|------|----------|----------|--------|
| **CLAUDE.md** | `~/.claude/CLAUDE.md` | `./CLAUDE.md` 鎴?`.claude/CLAUDE.md` | 椤圭洰浼樺厛 |
| **Settings** | `~/.claude/settings.json` | `.claude/settings.json` + `.claude/settings.local.json` | 椤圭洰浼樺厛 |
| **Rules** | `~/.claude/rules/*.md` | `.claude/rules/*.md` | 椤圭洰浼樺厛 |
| **Agents / Subagents** | `~/.claude/agents/*.md` | `.claude/agents/*.md` | 椤圭洰浼樺厛 |
| **Commands** | `~/.claude/commands/*.md` | `.claude/commands/*.md` | 涓よ竟閮藉彲鐢?|
| **Skills** | `~/.claude/skills/` | `.claude/skills/` | 涓よ竟閮藉彲鐢?|
| **Hooks** | `~/.claude/hooks/` | `.claude/hooks/` | 涓よ竟閮戒細鎵ц |
| **MCP Servers** | `~/.claude.json`锛堢敤鎴风骇锛?| `.mcp.json`锛堥」鐩骇锛?| 灞€閮?> 椤圭洰 > 鐢ㄦ埛 |

---

## 璁剧疆浼樺厛绾?
鐢ㄦ埛鍙啓璁剧疆鐨勮鐩栭『搴忓涓嬶紝瓒婇潬鍓嶄紭鍏堢骇瓒婇珮锛?
| 浼樺厛绾?| 浣嶇疆 | 浣滅敤鍩?| 鏄惁寤鸿绾冲叆鐗堟湰鎺у埗 | 鐢ㄩ€?|
|--------|------|--------|----------------------|------|
| 1 | 鍛戒护琛屽弬鏁?| 褰撳墠浼氳瘽 | 鍚?| 鍗曟浼氳瘽涓存椂瑕嗙洊 |
| 2 | `.claude/settings.local.json` | 椤圭洰 | 鍚︼紙閫氬父 gitignore锛?| 涓汉鐨勯」鐩眬閮ㄨ缃?|
| 3 | `.claude/settings.json` | 椤圭洰 | 鏄?| 鍥㈤槦鍏变韩璁剧疆 |
| 4 | `~/.claude/settings.local.json` | 鐢ㄦ埛 | 鍚?| 涓汉鍏ㄥ眬灞€閮ㄨ鐩?|
| 5 | `~/.claude/settings.json` | 鐢ㄦ埛 | 鍚?| 涓汉鍏ㄥ眬榛樿璁剧疆 |

鍙﹀杩樻湁涓€涓?*绛栫暐灞?*锛?
- `managed-settings.json` 灞炰簬缁勭粐寮哄埗涓嬪彂鐨勯厤缃紝浼樺厛绾ч珮浜庢湰鍦拌缃€?- `deny` 鏉冮檺瑙勫垯鍏锋湁鏈€楂樺畨鍏ㄤ紭鍏堢骇锛屼笉鑳借浣庝紭鍏堢骇鐨?`allow` 鎴?`ask` 瑕嗙洊銆?
---

## 鐩綍缁撴瀯瀵圭収

### 鍏ㄥ眬浣滅敤鍩?`~/.claude/`

```text
~/.claude/
鈹溾攢鈹€ settings.json              # 鐢ㄦ埛绾ц缃紝瀵规墍鏈夐」鐩敓鏁?鈹溾攢鈹€ settings.local.json        # 涓汉鍏ㄥ眬瑕嗙洊
鈹溾攢鈹€ CLAUDE.md                  # 鐢ㄦ埛绾ц蹇?鈹溾攢鈹€ agents/                    # 鐢ㄦ埛绾?subagents
鈹?  鈹斺攢鈹€ *.md
鈹溾攢鈹€ rules/                     # 鐢ㄦ埛绾ц鍒?鈹?  鈹斺攢鈹€ *.md
鈹溾攢鈹€ commands/                  # 鐢ㄦ埛绾у懡浠?鈹?  鈹斺攢鈹€ *.md
鈹溾攢鈹€ skills/                    # 鐢ㄦ埛绾ф妧鑳?鈹?  鈹斺攢鈹€ */SKILL.md
鈹溾攢鈹€ tasks/                     # 浠呭叏灞€锛氫换鍔″垪琛?鈹?  鈹斺攢鈹€ {task-list-id}/
鈹溾攢鈹€ teams/                     # 浠呭叏灞€锛氭櫤鑳戒綋鍥㈤槦閰嶇疆
鈹?  鈹斺攢鈹€ {team-name}/
鈹?      鈹斺攢鈹€ config.json
鈹溾攢鈹€ projects/                  # 浠呭叏灞€锛氭瘡涓」鐩殑鑷姩璁板繂
鈹?  鈹斺攢鈹€ {project-hash}/
鈹?      鈹斺攢鈹€ memory/
鈹?          鈹溾攢鈹€ MEMORY.md
鈹?          鈹斺攢鈹€ *.md
鈹溾攢鈹€ keybindings.json           # 浠呭叏灞€锛氬揩鎹烽敭
鈹斺攢鈹€ hooks/                     # 鐢ㄦ埛绾?hooks
    鈹溾攢鈹€ scripts/
    鈹斺攢鈹€ config/

~/.claude.json                 # 浠呭叏灞€锛歁CP銆丱Auth銆佸亸濂姐€佺紦瀛?```

### 椤圭洰浣滅敤鍩?`.claude/`

```text
.claude/
鈹溾攢鈹€ settings.json              # 鍥㈤槦鍏变韩璁剧疆
鈹溾攢鈹€ settings.local.json        # 涓汉椤圭洰瑕嗙洊锛堥€氬父 gitignore锛?鈹溾攢鈹€ CLAUDE.md                  # 椤圭洰璁板繂锛屼篃鍙斁鍦ㄤ粨搴撴牴鐩綍
鈹溾攢鈹€ agents/                    # 椤圭洰绾?subagents
鈹?  鈹斺攢鈹€ *.md
鈹溾攢鈹€ rules/                     # 椤圭洰绾ц鍒?鈹?  鈹斺攢鈹€ *.md
鈹溾攢鈹€ commands/                  # 鑷畾涔?slash commands
鈹?  鈹斺攢鈹€ *.md
鈹溾攢鈹€ skills/                    # 鑷畾涔夋妧鑳?鈹?  鈹斺攢鈹€ {skill-name}/
鈹?      鈹溾攢鈹€ SKILL.md
鈹?      鈹斺攢鈹€ supporting-files/
鈹溾攢鈹€ hooks/                     # 椤圭洰绾?hooks
鈹?  鈹溾攢鈹€ scripts/
鈹?  鈹斺攢鈹€ config/
鈹斺攢鈹€ plugins/                   # 宸插畨瑁呮彃浠?
.mcp.json                      # 椤圭洰绾?MCP 鏈嶅姟鍣紙浣嶄簬浠撳簱鏍圭洰褰曪級
```

---

## Tasks 浠诲姟绯荤粺

Tasks 浜?**Claude Code v2.1.16**锛?026-01-22锛夊紩鍏ワ紝鐢ㄦ潵鏇夸唬鏃х殑 TodoWrite 鏈哄埗銆?
### 瀛樺偍浣嶇疆

浠诲姟鏁版嵁瀛樻斁鍦ㄦ湰鍦版枃浠剁郴缁熶腑鐨?`~/.claude/tasks/`锛岃€屼笉鏄簯绔暟鎹簱銆傝繖鎰忓懗鐫€锛?
- 鍙互瀹¤
- 鍙互绾冲叆鐗堟湰鎺у埗锛堝鏋滀綘鎰挎剰锛?- 绋嬪簭宕╂簝鍚庝篃鑳芥仮澶?
### 鐩稿叧宸ュ叿

| 宸ュ叿 | 鐢ㄩ€?|
|------|------|
| **TaskCreate** | 鍒涘缓浠诲姟锛屽寘鍚?`subject`銆乣description` 鍜?`activeForm` |
| **TaskGet** | 鎸?ID 璇诲彇浠诲姟璇︽儏 |
| **TaskUpdate** | 淇敼鐘舵€併€佽缃?owner銆佹坊鍔犱緷璧栨垨鍒犻櫎 |
| **TaskList** | 鍒楀嚭褰撳墠鎵€鏈変换鍔″強鐘舵€?|

### 鐢熷懡鍛ㄦ湡

```text
pending -> in_progress -> completed
```

### 渚濊禆绠＄悊

Tasks 鏀寔閫氳繃 `addBlockedBy` 鍜?`addBlocks` 寤虹珛渚濊禆鍥撅紝閬垮厤涓嬫父浠诲姟鍦ㄥ墠缃换鍔℃湭瀹屾垚鏃惰繃鏃╂墽琛屻€?
### 澶氫細璇濆崗浣?
```bash
CLAUDE_CODE_TASK_LIST_ID=my-project-tasks claude
```

澶氫釜浼氳瘽鍙鍏变韩鐩稿悓鐨勪换鍔″垪琛?ID锛屽氨鑳藉疄鏃剁湅鍒颁换鍔″彉鏇达紝闈炲父閫傚悎骞惰宸ヤ綔涓庝細璇濇仮澶嶃€?
### 涓庢棫 Todo 鐨勫尯鍒?
| 鑳藉姏 | 鏃?Todo | 鏂?Tasks |
|------|---------|----------|
| 浣滅敤鍩?| 鍗曚細璇?| 璺ㄤ細璇濄€佽法鏅鸿兘浣?|
| 渚濊禆鍏崇郴 | 鏃?| 鏀寔瀹屾暣渚濊禆鍥?|
| 瀛樺偍鏂瑰紡 | 浠呭唴瀛?| 鏂囦欢绯荤粺 `~/.claude/tasks/` |
| 鎸佷箙鍖?| 浼氳瘽缁撴潫鍗充涪澶?| 閲嶅惎鍜屽穿婧冨悗浠嶄繚鐣?|
| 澶氫細璇濆崗浣?| 涓嶆敮鎸?| 鏀寔 |

---

## Agent Teams 鏅鸿兘浣撳洟闃?
Agent Teams 浜?**2026-02-05** 浠ュ疄楠屾€ц兘鍔涘彂甯冿紝鐢ㄤ簬璁╁涓?Claude Code 浼氳瘽鍗忓悓澶勭悊鍚屼竴浠藉伐浣溿€?
### 鍚敤鏂瑰紡

```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

### 閰嶇疆浣嶇疆

鍥㈤槦閰嶇疆瀛樻斁鍦?`~/.claude/teams/{team-name}/`锛屾敮鎸佷袱绉嶆ā寮忥細

| 妯″紡 | 璇存槑 | 渚濊禆 |
|------|------|------|
| **In-process**锛堥粯璁わ級 | 鎵€鏈夐槦鍙嬮兘鍦ㄥ綋鍓嶇粓绔唴杩愯 | 鏃?|
| **Split panes** | 姣忎釜闃熷弸鍚勫崰涓€涓?pane | 闇€瑕?tmux 鎴?iTerm2锛屼笉閫傜敤浜?VS Code 鍐呯疆缁堢 |

---

## 璁捐鍘熷垯

鍏ㄥ眬涓撳睘涓庡弻灞備綔鐢ㄥ煙鐨勫垝鍒嗭紝鑳屽悗鏈変竴濂椾竴鑷寸殑璁捐閫昏緫锛?
| 绫诲埆 | 鎺ㄨ崘浣滅敤鍩?| 鍘熷洜 |
|------|------------|------|
| **鍗忚皟鐘舵€?*锛坱asks銆乼eams锛?| 浠呭叏灞€ | 闇€瑕佽法瓒婂崟涓€椤圭洰鎸佺画瀛樺湪 |
| **瀹夊叏鐘舵€?*锛堝嚟鎹€丱Auth锛?| 浠呭叏灞€ | 閬垮厤鎰忓鎻愪氦鍒扮増鏈簱 |
| **涓汉瀛︿範缁撴灉**锛坅uto-memory锛?| 浠呭叏灞€ | 灞炰簬涓汉缁忛獙锛屼笉閫傚悎鍥㈤槦鍏变韩 |
| **杈撳叆鍋忓ソ**锛坘eybindings锛?| 浠呭叏灞€ | 灞炰簬涓汉涔犳儻锛屼笉搴旂敱椤圭洰鍐冲畾 |
| **閰嶇疆**锛坰ettings銆乺ules銆乤gents锛?| 鍏ㄥ眬 + 椤圭洰 | 椤圭洰鍥㈤槦闇€瑕佸叡浜」鐩骇琛屼负 |
| **宸ヤ綔娴佸畾涔?*锛坈ommands銆乻kills锛?| 鍏ㄥ眬 + 椤圭洰 | 鏃㈠彲鑳芥槸涓汉鍋忓ソ锛屼篃鍙兘鏄洟闃熻鑼?|

鍏朵腑涓€涓緢鍏稿瀷鐨勬贩鍚堝瀷渚嬪瓙鏄?auto-memory锛?
- 瀹冪殑鍐呭纭疄涓庢煇涓」鐩浉鍏筹紱
- 浣嗗畠浠ｈ〃鐨勬槸**鐢ㄦ埛涓汉鐨勫涔犵Н绱?*锛屾墍浠ュ瓨鍌ㄥ湪鍏ㄥ眬鐩綍涓紝鑰屼笉鏄」鐩洰褰曢噷銆?
---

## 璧勬枡鏉ユ簮

- [Claude Code Settings Documentation](https://code.claude.com/docs/en/settings)
- [Orchestrate Teams of Claude Code Sessions](https://code.claude.com/docs/en/agent-teams)
- [What are Tasks in Claude Code - ClaudeLog](https://claudelog.com/faqs/what-are-tasks-in-claude-code/)
- [Claude Code Task Management - ClaudeFast](https://claudefa.st/blog/guide/development/task-management)
- [Claude Code Tasks Update - VentureBeat](https://venturebeat.com/orchestration/claude-codes-tasks-update-lets-agents-work-longer-and-coordinate-across)
- [Where Are Claude Code Global Settings - ClaudeLog](https://claudelog.com/faqs/where-are-claude-code-global-settings/)
- [Claude Opus 4.6 Agent Teams - VentureBeat](https://venturebeat.com/technology/anthropics-claude-opus-4-6-brings-1m-token-context-and-agent-teams-to-take)
- [How to Set Up Claude Code Agent Teams (Full Walkthrough) - r/ClaudeCode](https://www.reddit.com/r/ClaudeCode/comments/1qz8tyy/how_to_set_up_claude_code_agent_teams_full/)
- [Anthropic replaced Claude Code's old 'Todos' with Tasks - r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/comments/1qkjznp/anthropic_replaced_claude_codes_old_todos_with/)

