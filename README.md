# v0 Ready-to-Paste Prompts — Pokémon TCG 訓練家網站

AGC網站生成結果：https://v0-pokemon-tcg-website-navy.vercel.app/

對齊 PRD: [V0_PRD_POKEMON_TCG.md](./V0_PRD_POKEMON_TCG.md)

**使用順序**：
1. 主 prompt（一次到位、最快）
2. 若 v0 一次吃不下 → 改用三段式 prompt（A → B → C）
3. 生成後用 iteration prompt 微調

---

## 🚀 主 Prompt（一次到位版）

> 直接複製貼到 v0.dev 第一個 message。如 v0 中斷請改用下方三段式。

```
Build a Next.js 14 (App Router) + TypeScript + Tailwind CSS website inspired by the official Pokémon TCG Trainer Site.

# Project
A 3-page brand site for "Pokémon TCG 訓練家網站":
- `/` Home (reads `data/welcome.json`)
- `/tutorial` 新手指南 (reads `data/tutorial.json`)
- `/products` 卡牌商品 (reads `data/products.json`)

All page content MUST come from JSON files in `data/` folder. Do not hardcode any copy.

# Visual Style (mandatory — match official Pokémon TCG site)
- Pure black background `#000000`
- Pokémon gold yellow accent `#FFCB05`
- Purple glow rays `#A78BFA` radiating from center
- Bold beveled logo with white border + black fill + yellow outline (top-left navbar)
- Radial-gradient + linear-gradient lines for hero background light rays
- Type-based color coding:
  - Electric `#F7D02C`
  - Fire `#EE8130`
  - Water `#6390F0`
  - Psychic `#F95587`
  - Grass `#7AC74C`
- Typography: Noto Sans TC + Inter, headlines 80–96pt bold with black shadow box
- Yellow horizontal banner strip for tutorial section titles (like "首先記住基本遊戲規則吧！")
- Round yellow circle arrow button (top-right of cards / pagination)

# Pages

## `/` Home
- Sticky navbar (logo left + menu center + search/user icons right)
- Full-width hero ≥80vh with radiating light rays background
- Big title 96pt + subtitle + 2 CTA buttons (primary yellow / secondary outline)
- Featured cards grid (3 cards) with hover translateY(-8px) + glow shadow
- Footer

## `/tutorial`
- Sticky navbar
- Breadcrumb: 首頁 > 新手指南
- Big section title "新手指南" with subtitle
- Tab navigation for 4 steps
- Step content: yellow banner strip + 2 example cards side-by-side + black container with purple glow
- Round yellow next-arrow button bottom-right

## `/products`
- Sticky navbar
- Title "卡牌商品" + subtitle
- Type filter chips (All / Electric / Fire / Water / Psychic / Grass) — rounded chip buttons with active state
- 12-column responsive grid (mobile 1 / tablet 2 / desktop 4 cols)
- Each card: image top, name + type icon, HP value, rarity tag (different colors), price NT$XXX
- Hover effect: lift + type-color glow

# Data Files

Create these files in `data/` folder with EXACT content below.

## `data/welcome.json`
```json
{
  "hero": {
    "title": "Pokémon TCG",
    "subtitle": "集換 · 對戰 · 成為訓練家大師",
    "background_image": "/images/hero-pokemon.jpg",
    "tagline": "訓練家網站"
  },
  "cta": {
    "primary": { "label": "開始集換", "href": "/tutorial" },
    "secondary": { "label": "瀏覽卡牌", "href": "/products" }
  },
  "featured_cards": [
    { "id": "pikachu", "name": "皮卡丘", "type": "Electric", "image": "/images/card-pikachu.png" },
    { "id": "charizard", "name": "噴火龍", "type": "Fire", "image": "/images/card-charizard.png" },
    { "id": "mewtwo", "name": "超夢", "type": "Psychic", "image": "/images/card-mewtwo.png" }
  ]
}
```

## `data/tutorial.json`
```json
{
  "title": "新手指南",
  "subtitle": "5 分鐘學會寶可夢卡牌對戰",
  "intro_banner": "首先記住基本遊戲規則吧！",
  "steps": [
    { "step_number": 1, "title": "認識屬性相剋", "description": "Fire 剋 Grass、Water 剋 Fire、Electric 剋 Water — 屬性決定攻擊倍率", "image": "/images/tutorial-types.png" },
    { "step_number": 2, "title": "卡牌種類", "description": "寶可夢卡（戰鬥用）/ 訓練家卡（道具技能）/ 能量卡（驅動技能）三大類缺一不可", "image": "/images/tutorial-cards.png" },
    { "step_number": 3, "title": "出牌規則", "description": "每回合抽 1 張、進化需要 1 回合、擊倒對手寶可夢拿獎賞卡、先拿 6 張獎賞卡獲勝", "image": "/images/tutorial-rules.png" },
    { "step_number": 4, "title": "組牌建議", "description": "60 張一副：寶可夢 ~20 / 訓練家 ~25 / 能量 ~15。先選一個主屬性再配副屬性", "image": "/images/tutorial-deck.png" }
  ]
}
```

## `data/products.json`
```json
{
  "title": "卡牌商品",
  "subtitle": "經典寶可夢 × 稀有 EX/GX",
  "type_filters": ["All", "Electric", "Fire", "Water", "Psychic", "Grass"],
  "products": [
    { "id": "card_001", "name": "皮卡丘 V", "type": "Electric", "rarity": "Rare", "hp": 200, "price": 120, "image_url": "/images/card-pikachu-v.png", "description": "電氣系經典代表，初心者首選" },
    { "id": "card_002", "name": "噴火龍 VMAX", "type": "Fire", "rarity": "Ultra Rare", "hp": 330, "price": 580, "image_url": "/images/card-charizard-vmax.png", "description": "高 HP + 高爆發傷害的火系王者" },
    { "id": "card_003", "name": "超夢 GX", "type": "Psychic", "rarity": "Ultra Rare", "hp": 270, "price": 480, "image_url": "/images/card-mewtwo-gx.png", "description": "超能系終極輸出，GX 技能一擊必殺" },
    { "id": "card_004", "name": "傑尼龜", "type": "Water", "rarity": "Common", "hp": 60, "price": 30, "image_url": "/images/card-squirtle.png", "description": "御三家經典水系，進化路線完整" },
    { "id": "card_005", "name": "妙蛙種子", "type": "Grass", "rarity": "Common", "hp": 60, "price": 30, "image_url": "/images/card-bulbasaur.png", "description": "草系御三家，平衡型寶可夢" },
    { "id": "card_006", "name": "卡比獸 ex", "type": "Psychic", "rarity": "Epic", "hp": 280, "price": 350, "image_url": "/images/card-snorlax.png", "description": "高 HP 肉盾，沉睡狀態反擊" }
  ]
}
```

# Tech Requirements
- Next.js 14 App Router
- TypeScript strict mode
- Tailwind CSS with custom theme for type colors
- Use `next/font` for Noto Sans TC + Inter
- All pages: `import data from '@/data/[name].json'` then render
- Use placeholder.com or Pokemon-style placeholder images
- Create TypeScript types in `types/content.ts` matching JSON schema

# Components to Create
- `Navbar` (sticky, beveled logo, menu, icons)
- `Footer`
- `HeroSection` (radiating light bg + title + CTAs)
- `FeaturedCardGrid` (3 cards with hover)
- `TutorialStep` (yellow banner + content + cards)
- `ProductCard` (image + name + HP + rarity + price + hover glow)
- `TypeChip` (filter chip with active state)

# Acceptance Criteria
- Black background with Pokémon yellow + purple glow throughout
- Beveled logo top-left looks like official Pokémon TCG logo
- All 3 pages render data from JSON
- Mobile responsive (1 col mobile, 4 col desktop on products)
- Card hover lifts + glows in type color
- Tutorial tab switching works
- Type filter chips work on products page

Generate the complete project now.
```

---

## 📦 三段式 Prompt（v0 一次吃不下時用）

### 段 A — 架構與風格

```
Build a Next.js 14 (App Router) + TypeScript + Tailwind CSS website inspired by the official Pokémon TCG Trainer Site.

Visual style (mandatory):
- Pure black background `#000000`
- Pokémon gold yellow `#FFCB05` as primary accent
- Purple glow `#A78BFA` radiating light rays from center
- Bold beveled logo with white border + black fill + yellow outline edges (top-left)
- Type colors: Electric `#F7D02C`, Fire `#EE8130`, Water `#6390F0`, Psychic `#F95587`, Grass `#7AC74C`
- Typography: Noto Sans TC + Inter, headlines 80–96pt bold with black shadow boxes
- Yellow horizontal banner strips for section highlights
- Round yellow circular arrow buttons

Pages structure:
- `/` Home with sticky navbar + hero (radiating light rays bg, ≥80vh) + featured cards section + footer
- `/tutorial` with breadcrumb + title + tab navigation for 4 steps + step content panel
- `/products` with title + type filter chips + 12-col responsive grid (1/2/4 cols)

Sticky navbar: black bg, white text, beveled logo left, menu center (新手指南 / 商品資訊 / 卡牌 / 牌組構築 / 規則 / 活動 / 店鋪搜尋), search + user icons right.

Tech: Next.js 14 App Router, TypeScript strict, Tailwind with type-color theme, next/font for Noto Sans TC + Inter.

Build the layout, navbar, footer, and 3 empty pages with placeholder structure first. Use `data/*.json` files for content (I'll provide schemas next).
```

### 段 B — JSON 資料

> 在段 A 完成後貼這段

```
Now create three JSON data files in `data/` folder with this exact content, and update the 3 pages to read from them.

## data/welcome.json
[貼上 welcome.json 完整內容]

## data/tutorial.json
[貼上 tutorial.json 完整內容]

## data/products.json
[貼上 products.json 完整內容]

For each page:
- `/` reads `welcome.json` → render hero + featured cards
- `/tutorial` reads `tutorial.json` → tabs for steps, each step shows yellow banner + content + image
- `/products` reads `products.json` → filter chips + product card grid

Also create TypeScript types in `types/content.ts` matching the JSON schemas.

Do not hardcode any copy in the pages.
```

### 段 C — 元件細節與互動

> 段 B 完成後貼這段

```
Refine the components with these specifications:

## Navbar
- Sticky `top-0 z-50`, height 64px
- Beveled logo: white border 3px + black fill + yellow outer outline, slanted right edge (like official Pokémon TCG logo)
- Menu items horizontal with hover yellow underline

## HeroSection
- Full-width, min-height 80vh
- Background: radial-gradient from center black-to-deeper-black + overlay linear-gradient lines simulating light rays
- Center: 96pt title with black shadow box, 32pt subtitle, two CTAs (primary yellow filled / secondary outline)
- Subtle scroll-down arrow at bottom

## FeaturedCardGrid
- 3 cards horizontal grid
- Each card: black bg + purple glow background + card image centered
- Hover: `translateY(-8px)` + box-shadow glow in card type color
- `transition: all 0.3s ease`

## TutorialStep
- Yellow horizontal banner strip with bold text on top (like "首先記住基本遊戲規則吧！")
- Black container below with purple light scatter background
- Two example cards side-by-side with HP/attack/damage labels
- Round yellow circle button bottom-right with black arrow icon

## ProductCard
- Image top, name + type icon below, HP value, rarity tag (color-coded: Common gray / Rare blue / Epic purple / Ultra Rare gold)
- Price "NT$ XXX" bottom
- Hover: lift 8px + glow in type color
- Active filter chip: filled bg with type color; inactive: outline

## TypeChip
- Rounded pill button
- Active state: filled with type color
- Inactive: transparent bg with type color outline
- Click toggles filter on products page

Make all hover/transition effects smooth (0.3s ease).
Mobile responsive: products grid drops to 1 col on mobile, 2 on tablet, 4 on desktop.
```

---

## 🔄 Iteration Prompts（生成後微調）

### 視覺微調

```
The current design looks too generic. Make it more like the official Pokémon TCG site:

1. The logo top-left should be more "beveled" — add a steeper slanted right edge, thicker white border (3px), and yellow outline that creates a 3D pop effect.
2. The hero background needs MORE dramatic radiating light rays. Use multiple linear-gradients at different angles (every 30 degrees) overlaid on the black background.
3. The yellow banner strips for tutorial sections should have a slight inner shadow and be more prominent — bigger text, bolder.
4. Card images should have a subtle purple glow scatter behind them, like spotlight from below.

Apply these changes.
```

### 互動微調

```
The hover effects are too subtle. Adjust:

1. Featured cards on home: hover should lift by 12px (not 8px), add a stronger glow shadow in the card's type color (e.g., yellow glow for Electric, red for Fire).
2. Product cards: same hover treatment.
3. Add a slight rotate-y(2deg) on hover for cards to feel more 3D.
4. Buttons (CTAs): on hover, add scale(1.05) + brightness(1.1).
5. Type filter chips: when active, add a pulsing glow animation.

Keep all transitions at 0.3s ease.
```

### 資料結構修正

```
There's a schema issue. Update the product card component:

1. The rarity tag should map to specific colors:
   - Common → gray `#9CA3AF`
   - Rare → blue `#3B82F6`
   - Epic → purple `#A855F7`
   - Ultra Rare → gold `#FFCB05`

2. HP should display as "HP 200" (with "HP" prefix), bold, top-right of card.
3. Type icon should be a colored circle with the type's symbol/emoji inside.
4. Price format: "NT$ 120" with thousand separator if ≥ 1000 (e.g., "NT$ 1,200").

Apply these to all product cards.
```

### Mobile 優化

```
Mobile experience needs work:

1. Sticky navbar on mobile should collapse menu into a hamburger icon (right side), keep logo left.
2. Hero title size should scale down: 48pt on mobile, 64pt on tablet, 96pt on desktop.
3. Tutorial tab navigation on mobile: change from horizontal tabs to a dropdown selector.
4. Product grid: 1 column on mobile, no margin gaps too tight (gap-4 min).
5. Type filter chips should horizontal scroll on mobile (overflow-x-auto), not wrap.

Update responsive classes accordingly.
```

---

## 🎯 v0 操作 SOP（給課堂示範用）

### 步驟 1：開新專案
1. 開 [v0.dev](https://v0.dev)
2. 登入 GitHub
3. 新對話

### 步驟 2：第一輪生成
- 複製「主 prompt」整段貼進去
- 等待 v0 生成（約 30-60 秒）
- 看 preview

### 步驟 3：截圖 + 評估
- 截圖目前狀態
- 對照 PRD 的 Success Criteria 8 項打勾
- 找出 3 個最不滿意的點

### 步驟 4：iteration
- 從 3 個不滿意點選最重要一個
- 找對應 iteration prompt 貼上
- 等 v0 修
- 重複 3-5 輪

### 步驟 5：Export
- 點 v0 右上「Export to GitHub」
- 自動建 repo
- 學生 fork 後修 JSON

---

## 💡 v0 使用心法（給學生講）

1. **第一版 60% 對就好** — 不要苛求一次到位
2. **分小步要求** — 一次只改一個視覺點，不要連改五處
3. **數值比形容詞精準** — 說「translateY(-12px)」不要說「再浮起來一點」
4. **截圖對照官網** — 把寶可夢官網開旁邊、貼截圖叫 v0 對齊
5. **改不動就回 PRD** — AI 改不出來通常是 PRD 沒講清楚，回去補 PRD 比硬 prompt 有用

---

## 🔗 相關檔案

- [V0_PRD_POKEMON_TCG.md](./V0_PRD_POKEMON_TCG.md) — 完整 PRD（教學用）
- [CH1_SLIDE_BRIEF.md](./CH1_SLIDE_BRIEF.md) — Ch1 講綱
- [CH2_SLIDE_BRIEF.md](./CH2_SLIDE_BRIEF.md) — Ch2 講綱
- [SLIDE_BRIEF.md](./SLIDE_BRIEF.md) — 30 分版講者 brief
