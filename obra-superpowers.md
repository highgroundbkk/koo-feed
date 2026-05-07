# 📓 Obra: Superpowers Development Journal

> A living record of this system's evolution.
> Syncs to: github.com/highgroundbkk/gstack-private

---

### 2026-05-07 17:38 — Genesis

System born. 4 tiers, 40+ commands. Full git automation,
AI agent orchestration (Ruflo), self-updating, and this journal.

Philosophy:
- ไม่เปลือง token — update weekly only
- ดีขึ้นเรื่อยๆ — learns from patterns
- ไม่พัง — snapshots before every change
- บันทึกทุกอย่าง — feed + journal auto-syncs

Architecture:
- ~/.bashrc.gstack → all shell functions
- ~/.gstack/feed.md → activity log
- ~/.gstack/obra-superpowers.md → this journal
- github.com/highgroundbkk/gstack-private → remote sync

The 4 Tiers:

| Tier | Focus | Commands |
|------|-------|----------|
| 1 | Git workflow | 10 (clone, branch, push, PR...) |
| 2 | Advanced DevOps | 10 (AI review, test, deploy...) |
| 3 | AI Orchestration | 15 (Ruflo, swarms, workflows...) |
| 4 | Autonomous | 7 (feed, journal, dashboard, self-update) |

---

### Notes

- Weekly self-update: `gself-update` (checks gstack repo + syncs private)
- Feed logs everything automatically
- This journal is for thoughts, decisions, ideas
- Private repo keeps the full backup always

---

### 2026-05-07 17:57 — Recommendations (from the system)

**สิ่งที่อยากแนะนำ:**

1. **PAT Token จะหมดอายุ** — token ที่ใช้อยู่ (ghp_71fc...) ควรตั้ง expiration
   ที่เหมาะสม หรือสร้าง fine-grained token ที่ scope แคบลง (แค่ repo access)
   ปลอดภัยกว่า classic token ที่มี full access

2. **เปลี่ยนจาก PAT → SSH เป็นหลัก** — SSH key ที่สร้างไว้แล้ว (ed25519)
   ปลอดภัยกว่า token ในระยะยาว ไม่หมดอายุ ไม่ต้อง rotate

3. **อย่าเก็บ token ใน shell history** — ตอนนี้ token อาจอยู่ใน
   ~/.bash_history ควร clear: `history -c && history -w`

4. **Private repo = journal ของเรา** — ใช้เป็นที่อ่านย้อนหลังได้เลย
   ทุกครั้งที่ `gself-update` จะ sync feed + journal ไปที่นั่น

5. **Weekly rhythm ดีที่สุด** — อย่า over-automate
   สัปดาห์ละครั้ง `gself-update` พอ ไม่เปลือง ไม่รก

6. **ถ้าอยากให้ดีขึ้นอีก:**
   - ใช้ `gfeed add` บันทึกทุกครั้งที่ทำอะไรสำคัญ
   - ใช้ `gjournal add` เขียนความคิด/ไอเดีย
   - อ่าน obra ย้อนหลังจะเห็น pattern ของตัวเอง

---

---

### 2026-05-07 18:15 — KOO SUPERDEV

ชื่อทีมและระบบทั้งหมดได้รับการตั้งชื่อใหม่เป็น **KOO SUPERDEV**

- 📡 `signal.md` — dispatch journal ของ KOO SUPERDEV
- 🤖 `signal-bot.sh` — bot ที่คัดของดีจากชุมชนทุกสัปดาห์
- สไตล์: fsck.com-inspired — minimal, dated, link + verdict

Philosophy ของ KOO SUPERDEV:
> "รู้ก่อน ตัดสินก่อน ใช้ก่อน — ไม่รอให้คนอื่นบอก"


---

### 2026-05-07 18:47 — System Complete

GitHub Actions workflows + README published.

KOO SUPERDEV now **fully autonomous**:
- ✅ 42 shell commands
- ✅ 8 bots (signal-bot, hn-monitor, etc)
- ✅ 6 power tools (fzf, delta, bat, eza, zoxide, git-cliff)
- ✅ GitHub Actions (Mon 9am UTC)
- ✅ SSH remote (no PAT workflow limit)
- ✅ Documentation (README.md)
- ✅ Restore script (team ready)

No codespace needed. Runs on GitHub free tier.


---

[2026-05-07 19:48] DECISION · Two-repo architecture — public feed + private vault

**Why split into two repos?**

GitHub Pages only works on public repos (free plan). But all bots, secrets, and configs must stay private. The solution: separate concerns cleanly.

- `gstack-private` — private vault, all secrets, 8 bots, 42 commands, 238 context files
- `koo-feed` — public blog site, curated markdown only, zero secrets

**Bot sync process:**
1. `sync-bot.sh` reads from gstack-private
2. Strips any lines matching credential patterns (ghp_, ANTHROPIC_KEY, etc.)
3. Copies only `.md` files to koo-feed clone
4. Pushes via PAT — public read, private write

**Result:** Team reads at `https://highgroundbkk.github.io/koo-feed/` — no secrets ever exposed.

Reference: `~/.gstack/bots/sync-bot.sh`, `.github/workflows/daily-signal.yml`
