# Smart Kitchen 資料模型｜Data Model

> 本文件定義 Smart Kitchen 首個原型使用的核心資料結構、欄位、關係及驗證規則。
>
> 本文件是資料設計規格，不代表最終資料庫結構。JSON、Python、API、Flutter 及後續資料庫實作應盡量遵循本文件。

---

## 文件資訊

- 項目名稱：Smart Kitchen｜今晚煮乜？
- 文件版本：v0.2
- 項目階段：資料模型設計
- 最後更新日期：2026-11-03
- 項目成員：
  - 颜照兴 Jason Yan
  - 陈玉雯 Viven Chen

---

# 1. 資料建模原則

## 1.1 內部識別碼使用英文

程式內部使用穩定的英文識別碼，例如：

```text
tomato
egg
mushroom
beginner
healthy
frying_pan
```

使用者介面顯示對應的繁體中文：

```text
tomato → 番茄
egg → 雞蛋
mushroom → 蘑菇
beginner → 新手
healthy → 食得健康啲
frying_pan → 平底鑊
```

不應直接使用繁體中文名稱作為程式判斷條件。

---

## 1.2 JSON 欄位命名

JSON 及 API 欄位暫定使用 `camelCase`：

```text
userId
ingredientId
expiryDate
skillLevel
availableCookware
```

Python 內部可以使用 `snake_case`，但對外 API 應保持一致。

---

## 1.3 日期及時間

日期使用 ISO 8601 格式：

```text
2026-11-03
```

完整時間使用：

```text
2026-11-03T19:30:00+08:00
```

---

## 1.4 金額

金額只儲存數值，不在數值中加入貨幣符號：

```json
{
  "estimatedCostHkd": 65
}
```

介面顯示時再轉換為：

```text
約 HK$65
```

首個版本的預算按整道菜計算，不按每人計算。

菜式預計費用需要配合菜式份量理解。例如：

```json
{
  "baseServings": 2,
  "estimatedCostHkd": 65
}
```

表示一整道兩人份菜式的預計費用約為 HK$65。

---

## 1.5 多語言文字

需要顯示給使用者的菜式名稱、介紹及煮食步驟，使用可擴展的多語言物件：

```json
{
  "zh_HK": "番茄炒蛋",
  "en": null
}
```

首個版本只要求填寫 `zh_HK`。

`en` 欄位暫時使用 `null`，不需要在首批食材及菜式資料中提供英文內容。保留該欄位是為了日後增加英文介面時，不需要重新設計資料結構。

---

## 1.6 選填資料

選填欄位沒有資料時使用 `null` 或空陣列。

不應混用以下內容表示空值：

```text
N/A
unknown
沒有
-
```

---

## 1.7 首個版本的帳戶處理

首個原型暫時不實現正式電郵認證系統。

Figma 及頁面規格可以保留註冊和登入畫面，用於展示完整產品流程；但首個可運行版本暫定使用本地演示帳戶。

首個版本暫不處理：

- 真實電郵註冊；
- 電郵驗證；
- 忘記密碼；
- 密碼重設；
- 多裝置帳戶同步。

因此，`UserProfile` 暫時不保存電郵地址及密碼。

正式認證功能會在核心煮食及推薦流程穩定後，再透過獨立認證服務實現。密碼不會直接儲存在 `UserProfile` 中。

---

# 2. 核心資料模型

首個版本包含以下核心模型：

1. `UserProfile`
2. `Ingredient`
3. `PantryItem`
4. `Recipe`
5. `RecipeIngredient`
6. `RecipeStep`
7. `CookingSession`
8. `UserFeedback`

推薦系統另外使用：

9. `RecommendationRequest`
10. `RecommendationResult`

---

# 3. UserProfile

## 3.1 用途

保存使用者的基本資料、飲食限制、偏好、臨期提醒設定及一般煮食設定。

帳戶密碼不會儲存在 `UserProfile` 中。

---

## 3.2 欄位

| 欄位 | 類型 | 必填 | 說明 |
|---|---|---:|---|
| `id` | string | 是 | 使用者唯一識別碼 |
| `nickname` | string | 是 | 使用者暱稱 |
| `avatarId` | string | 是 | 預設頭像識別碼 |
| `allergies` | string[] | 是 | 已知食物過敏原 |
| `dietaryRestrictions` | string[] | 是 | 飲食限制 |
| `dislikedIngredients` | string[] | 是 | 明確不想食用的食材 |
| `primaryGoal` | string | 是 | 主要飲食目標 |
| `flavorPreferences` | string[] | 是 | 口味偏好 |
| `skillLevel` | string | 是 | 廚藝程度 |
| `availableCookware` | string[] | 是 | 可用煮食工具 |
| `defaultTimeMinutes` | integer/null | 否 | 一般可用煮食時間 |
| `defaultBudgetPerRecipeHkd` | number/null | 否 | 一般每道菜的預算 |
| `expiryReminderEnabled` | boolean | 是 | 是否啟用臨期食材提醒 |
| `expiryReminderDays` | integer | 是 | 提前多少日顯示臨期提醒 |
| `onboardingCompleted` | boolean | 是 | 是否完成首次設定 |
| `createdAt` | datetime | 是 | 建立時間 |
| `updatedAt` | datetime | 是 | 最後更新時間 |

---

## 3.3 示例

```json
{
  "id": "user_demo_001",
  "nickname": "Jason",
  "avatarId": "avatar_01",
  "allergies": [
    "peanut"
  ],
  "dietaryRestrictions": [],
  "dislikedIngredients": [
    "coriander"
  ],
  "primaryGoal": "healthy",
  "flavorPreferences": [
    "light"
  ],
  "skillLevel": "beginner",
  "availableCookware": [
    "stove",
    "frying_pan",
    "rice_cooker"
  ],
  "defaultTimeMinutes": 30,
  "defaultBudgetPerRecipeHkd": 80,
  "expiryReminderEnabled": true,
  "expiryReminderDays": 2,
  "onboardingCompleted": true,
  "createdAt": "2026-11-03T10:00:00+08:00",
  "updatedAt": "2026-11-03T10:00:00+08:00"
}
```

---

# 4. Ingredient

## 4.1 用途

保存標準食材或使用者自訂食材的基本資料。

`Ingredient` 是食材目錄中的記錄，例如：

```text
tomato
egg
mushroom
```

它不是使用者雪櫃中的實際庫存。

例如：

```text
Ingredient：蘑菇這種食材
PantryItem：Jason 雪櫃裏剩餘的 1 盒蘑菇
```

---

## 4.2 欄位

| 欄位 | 類型 | 必填 | 說明 |
|---|---|---:|---|
| `id` | string | 是 | 食材唯一英文識別碼 |
| `name` | LocalizedText | 是 | 食材顯示名稱 |
| `aliases` | string[] | 是 | 搜尋別名 |
| `category` | string | 是 | 食材分類 |
| `defaultUnit` | string | 是 | 預設單位 |
| `allowedUnits` | string[] | 是 | 此食材可使用的預設單位 |
| `commonAllergens` | string[] | 是 | 食材常見過敏原 |
| `defaultStorageLocation` | string/null | 否 | 建議存放位置 |
| `source` | string | 是 | 系統食材或使用者自訂食材 |
| `ownerUserId` | string/null | 否 | 自訂食材的建立者 |
| `canonicalIngredientId` | string/null | 否 | 對應的標準食材 |
| `active` | boolean | 是 | 是否可在產品中使用 |

---

## 4.3 標準食材示例

```json
{
  "id": "tomato",
  "name": {
    "zh_HK": "番茄",
    "en": null
  },
  "aliases": [
    "蕃茄",
    "西紅柿"
  ],
  "category": "vegetable",
  "defaultUnit": "piece",
  "allowedUnits": [
    "piece",
    "gram",
    "kilogram",
    "catty"
  ],
  "commonAllergens": [],
  "defaultStorageLocation": "refrigerated",
  "source": "system",
  "ownerUserId": null,
  "canonicalIngredientId": null,
  "active": true
}
```

---

## 4.4 自訂食材示例

```json
{
  "id": "custom_user_demo_001_cherry_tomato",
  "name": {
    "zh_HK": "細粒車厘茄",
    "en": null
  },
  "aliases": [],
  "category": "vegetable",
  "defaultUnit": "box",
  "allowedUnits": [
    "box",
    "piece",
    "gram"
  ],
  "commonAllergens": [],
  "defaultStorageLocation": "refrigerated",
  "source": "user_created",
  "ownerUserId": "user_demo_001",
  "canonicalIngredientId": "tomato",
  "active": true
}
```

---

## 4.5 自訂食材規則

首個版本允許使用者建立自訂食材。

自訂食材需要遵守以下規則：

- 必須輸入繁體中文名稱；
- 必須選擇食材分類；
- 必須從預設單位中選擇單位；
- 不允許自由輸入新的單位；
- 自訂食材預設只屬於建立該食材的使用者；
- 自訂食材不會自動加入所有使用者的公共食材目錄；
- 如自訂食材與現有標準食材相同或相近，可以設定 `canonicalIngredientId`；
- 如沒有對應的標準食材，`canonicalIngredientId` 使用 `null`；
- 未能對應標準食材的自訂食材，可能無法自動匹配現有菜式。

示例：

```text
使用者自訂「細粒車厘茄」
→ 對應標準食材 tomato
→ 推薦系統可以將其視為番茄類食材
```

如果使用者自訂一種系統完全不認識的食材：

```text
使用者自訂「家鄉醃菜」
→ canonicalIngredientId = null
→ 可以加入雪櫃
→ 暫時不會自動匹配普通菜式
```

---

# 5. PantryItem

## 5.1 用途

表示某位使用者實際擁有的一項食材庫存。

---

## 5.2 欄位

| 欄位 | 類型 | 必填 | 說明 |
|---|---|---:|---|
| `id` | string | 是 | 庫存項目唯一識別碼 |
| `userId` | string | 是 | 所屬使用者 |
| `ingredientId` | string | 是 | 對應標準或自訂食材 |
| `quantity` | number | 是 | 目前數量 |
| `unit` | string | 是 | 數量單位 |
| `storageLocation` | string | 是 | 存放位置 |
| `purchaseDate` | date/null | 否 | 購買日期 |
| `expiryDate` | date/null | 否 | 預計到期日 |
| `status` | string | 是 | 庫存狀態 |
| `notes` | string/null | 否 | 使用者備註 |
| `createdAt` | datetime | 是 | 建立時間 |
| `updatedAt` | datetime | 是 | 最後更新時間 |

---

## 5.3 示例

```json
{
  "id": "pantry_item_001",
  "userId": "user_demo_001",
  "ingredientId": "mushroom",
  "quantity": 1,
  "unit": "box",
  "storageLocation": "refrigerated",
  "purchaseDate": "2026-11-01",
  "expiryDate": "2026-11-05",
  "status": "available",
  "notes": null,
  "createdAt": "2026-11-01T18:00:00+08:00",
  "updatedAt": "2026-11-01T18:00:00+08:00"
}
```

---

## 5.4 庫存狀態

`status` 允許：

```text
available
used_up
discarded
archived
```

說明：

- `available`：目前仍在雪櫃或儲物區；
- `used_up`：已經用完；
- `discarded`：已經丟棄；
- `archived`：保留紀錄，但不再用於推薦。

只有 `available` 狀態的食材會參與推薦。

---

## 5.5 臨期食材判斷

首個版本預設在食材到期前 2 日開始顯示臨期提醒。

判斷方式：

```text
expiryDate - currentDate <= expiryReminderDays
```

預設設定：

```json
{
  "expiryReminderEnabled": true,
  "expiryReminderDays": 2
}
```

示例：

```text
目前日期：2026-11-03
預計到期日：2026-11-05
提醒日數：2

結果：屬於臨期食材
```

如果食材沒有填寫 `expiryDate`：

```text
不顯示臨期提醒
```

如果使用者關閉提醒：

```text
expiryReminderEnabled = false
```

首個版本統一使用提前 2 日提醒，暫時不按肉類、蔬菜或冷凍食品設定不同提醒日數。

---

# 6. Recipe

## 6.1 用途

保存一道菜式的基本資料、限制、標籤、食材及煮食步驟。

---

## 6.2 欄位

| 欄位 | 類型 | 必填 | 說明 |
|---|---|---:|---|
| `id` | string | 是 | 菜式唯一識別碼 |
| `name` | LocalizedText | 是 | 菜式名稱 |
| `description` | LocalizedText | 是 | 簡短介紹 |
| `imagePath` | string/null | 否 | 圖片位置 |
| `baseServings` | integer | 是 | 基礎份量 |
| `timeMinutes` | integer | 是 | 預計總時間 |
| `difficulty` | string | 是 | 難度 |
| `estimatedCostHkd` | number/null | 否 | 按基礎份量計算的整道菜預計費用 |
| `cookware` | string[] | 是 | 必要煮食工具 |
| `tags` | string[] | 是 | 推薦標籤 |
| `dietaryLabels` | string[] | 是 | 飲食類型 |
| `allergens` | string[] | 是 | 已知過敏原 |
| `ingredients` | RecipeIngredient[] | 是 | 所需食材 |
| `steps` | RecipeStep[] | 是 | 煮食步驟 |
| `nutritionEstimate` | NutritionEstimate/null | 否 | 營養估算 |
| `source` | RecipeSource | 是 | 菜式來源 |
| `status` | string | 是 | 菜式狀態 |
| `createdAt` | datetime | 是 | 建立時間 |
| `updatedAt` | datetime | 是 | 最後更新時間 |

---

## 6.3 示例

```json
{
  "id": "tomato_mushroom_egg_001",
  "name": {
    "zh_HK": "番茄蘑菇炒蛋",
    "en": null
  },
  "description": {
    "zh_HK": "一款材料簡單、適合煮食初學者的家常菜式。",
    "en": null
  },
  "imagePath": null,
  "baseServings": 2,
  "timeMinutes": 20,
  "difficulty": "beginner",
  "estimatedCostHkd": 65,
  "cookware": [
    "stove",
    "frying_pan",
    "spatula",
    "knife",
    "chopping_board"
  ],
  "tags": [
    "quick",
    "beginner_friendly",
    "one_pan",
    "low_cleanup"
  ],
  "dietaryLabels": [
    "vegetarian"
  ],
  "allergens": [
    "egg"
  ],
  "ingredients": [],
  "steps": [],
  "nutritionEstimate": null,
  "source": {
    "type": "team_created",
    "reference": null
  },
  "status": "draft",
  "createdAt": "2026-11-03T10:00:00+08:00",
  "updatedAt": "2026-11-03T10:00:00+08:00"
}
```

---

## 6.4 菜式狀態

`status` 允許：

```text
draft
reviewed
published
archived
```

說明：

- `draft`：仍在整理；
- `reviewed`：已完成內容檢查；
- `published`：可以進入正式推薦；
- `archived`：保留資料，但不再推薦。

只有 `published` 狀態的菜式可以進入正式推薦。

---

# 7. RecipeIngredient

## 7.1 用途

表示一道菜式需要的一項食材及其份量。

---

## 7.2 欄位

| 欄位 | 類型 | 必填 | 說明 |
|---|---|---:|---|
| `ingredientId` | string | 是 | 對應標準食材 |
| `quantity` | number/null | 否 | 所需數量 |
| `unit` | string/null | 否 | 數量單位 |
| `required` | boolean | 是 | 是否為必要食材 |
| `substitutions` | string[] | 是 | 可替代食材 |
| `preparation` | LocalizedText/null | 否 | 預處理方式 |
| `notes` | LocalizedText/null | 否 | 補充說明 |

---

## 7.3 示例

```json
{
  "ingredientId": "mushroom",
  "quantity": 1,
  "unit": "box",
  "required": true,
  "substitutions": [
    "shiitake_mushroom"
  ],
  "preparation": {
    "zh_HK": "切成薄片",
    "en": null
  },
  "notes": null
}
```

---

# 8. RecipeStep

## 8.1 用途

表示一道菜式的單個煮食步驟。

每個步驟應盡量只包含一個主要操作。

---

## 8.2 欄位

| 欄位 | 類型 | 必填 | 說明 |
|---|---|---:|---|
| `stepNumber` | integer | 是 | 步驟順序 |
| `instruction` | LocalizedText | 是 | 主要步驟內容 |
| `durationSeconds` | integer/null | 否 | 建議計時秒數 |
| `heatLevel` | string/null | 否 | 建議火力 |
| `skill` | string/null | 否 | 涉及的煮食技巧 |
| `beginnerTip` | LocalizedText/null | 否 | 初學者提示 |
| `safetyNote` | LocalizedText/null | 否 | 食品安全提示 |
| `imagePath` | string/null | 否 | 步驟圖片 |

---

## 8.3 示例

```json
{
  "stepNumber": 1,
  "instruction": {
    "zh_HK": "將番茄洗淨後切成小塊，蘑菇切成薄片。",
    "en": null
  },
  "durationSeconds": null,
  "heatLevel": null,
  "skill": "slicing",
  "beginnerTip": {
    "zh_HK": "蘑菇厚度盡量保持一致，煮熟時會比較均勻。",
    "en": null
  },
  "safetyNote": null,
  "imagePath": null
}
```

---

# 9. CookingSession

## 9.1 用途

記錄使用者一次煮食過程，包括開始時間、目前步驟、完成狀態及實際用時。

---

## 9.2 欄位

| 欄位 | 類型 | 必填 | 說明 |
|---|---|---:|---|
| `id` | string | 是 | 煮食紀錄唯一識別碼 |
| `userId` | string | 是 | 所屬使用者 |
| `recipeId` | string | 是 | 所煮菜式 |
| `servings` | integer | 是 | 本次份量 |
| `status` | string | 是 | 煮食狀態 |
| `currentStepNumber` | integer | 是 | 目前步驟 |
| `startedAt` | datetime | 是 | 開始時間 |
| `completedAt` | datetime/null | 否 | 完成時間 |
| `actualDurationMinutes` | integer/null | 否 | 實際用時 |
| `usedExpiringIngredients` | string[] | 是 | 使用的臨期食材 |
| `substitutions` | IngredientSubstitution[] | 是 | 實際替代食材 |
| `createdAt` | datetime | 是 | 建立時間 |
| `updatedAt` | datetime | 是 | 最後更新時間 |

---

## 9.3 狀態

`status` 允許：

```text
in_progress
paused
completed
abandoned
```

---

## 9.4 示例

```json
{
  "id": "session_001",
  "userId": "user_demo_001",
  "recipeId": "tomato_mushroom_egg_001",
  "servings": 2,
  "status": "in_progress",
  "currentStepNumber": 2,
  "startedAt": "2026-11-03T19:00:00+08:00",
  "completedAt": null,
  "actualDurationMinutes": null,
  "usedExpiringIngredients": [
    "mushroom"
  ],
  "substitutions": [],
  "createdAt": "2026-11-03T19:00:00+08:00",
  "updatedAt": "2026-11-03T19:10:00+08:00"
}
```

---

# 10. UserFeedback

## 10.1 用途

保存使用者完成煮食後的評價，用於改善未來推薦。

---

## 10.2 欄位

| 欄位 | 類型 | 必填 | 說明 |
|---|---|---:|---|
| `id` | string | 是 | 回饋唯一識別碼 |
| `sessionId` | string | 是 | 對應煮食紀錄 |
| `userId` | string | 是 | 所屬使用者 |
| `recipeId` | string | 是 | 對應菜式 |
| `tasteRating` | integer/null | 否 | 味道評分，1–5 |
| `difficultyRating` | string/null | 否 | 實際難度感受 |
| `wouldCookAgain` | string/null | 否 | 是否願意再次煮食 |
| `actualDurationMinutes` | integer/null | 否 | 使用者確認的實際時間 |
| `issues` | string[] | 是 | 遇到的問題標籤 |
| `notes` | string/null | 否 | 自由文字回饋 |
| `createdAt` | datetime | 是 | 建立時間 |

---

## 10.3 示例

```json
{
  "id": "feedback_001",
  "sessionId": "session_001",
  "userId": "user_demo_001",
  "recipeId": "tomato_mushroom_egg_001",
  "tasteRating": 4,
  "difficultyRating": "as_expected",
  "wouldCookAgain": "yes",
  "actualDurationMinutes": 24,
  "issues": [
    "too_much_liquid"
  ],
  "notes": "下次可以少放一點水。",
  "createdAt": "2026-11-03T19:30:00+08:00"
}
```

---

# 11. RecommendationRequest

## 11.1 用途

表示一次推薦請求的輸入。

該模型主要用於推薦算法及 API，不一定需要永久保存。

---

## 11.2 欄位

| 欄位 | 類型 | 必填 | 說明 |
|---|---|---:|---|
| `userId` | string | 是 | 使用者 |
| `pantryItems` | PantryItem[] | 是 | 目前可用食材 |
| `maxTimeMinutes` | integer/null | 否 | 最多可用時間 |
| `maxBudgetPerRecipeHkd` | number/null | 否 | 整道菜的最高預算 |
| `servings` | integer | 是 | 用餐人數 |
| `priorities` | string[] | 是 | 本餐優先條件 |
| `preferredIngredientIds` | string[] | 是 | 優先使用食材 |
| `excludedIngredientIds` | string[] | 是 | 本次不想使用的食材 |

---

## 11.3 示例

```json
{
  "userId": "user_demo_001",
  "pantryItems": [
    {
      "ingredientId": "egg",
      "quantity": 6,
      "unit": "piece",
      "expiryDate": "2026-11-10"
    },
    {
      "ingredientId": "tomato",
      "quantity": 3,
      "unit": "piece",
      "expiryDate": "2026-11-07"
    },
    {
      "ingredientId": "mushroom",
      "quantity": 1,
      "unit": "box",
      "expiryDate": "2026-11-04"
    }
  ],
  "maxTimeMinutes": 25,
  "maxBudgetPerRecipeHkd": 80,
  "servings": 2,
  "priorities": [
    "use_expiring_ingredients",
    "low_cleanup",
    "healthy"
  ],
  "preferredIngredientIds": [
    "mushroom"
  ],
  "excludedIngredientIds": []
}
```

---

# 12. RecommendationResult

## 12.1 用途

表示推薦算法返回的一道候選菜式及其評分理由。

---

## 12.2 欄位

| 欄位 | 類型 | 必填 | 說明 |
|---|---|---:|---|
| `recipeId` | string | 是 | 推薦菜式 |
| `score` | number | 是 | 推薦總分 |
| `reasonCodes` | string[] | 是 | 結構化推薦理由 |
| `matchedIngredientIds` | string[] | 是 | 已有食材 |
| `missingIngredientIds` | string[] | 是 | 缺少食材 |
| `usedExpiringIngredientIds` | string[] | 是 | 使用的臨期食材 |
| `estimatedTimeMinutes` | integer | 是 | 預計時間 |
| `estimatedCostHkd` | number/null | 否 | 按本次份量計算的整道菜預計費用 |
| `eligible` | boolean | 是 | 是否符合硬性限制 |
| `exclusionReasons` | string[] | 是 | 被排除原因 |

---

## 12.3 示例

```json
{
  "recipeId": "tomato_mushroom_egg_001",
  "score": 87.5,
  "reasonCodes": [
    "high_ingredient_coverage",
    "uses_expiring_ingredient",
    "within_time_limit",
    "low_cleanup"
  ],
  "matchedIngredientIds": [
    "egg",
    "tomato",
    "mushroom"
  ],
  "missingIngredientIds": [
    "cooking_oil"
  ],
  "usedExpiringIngredientIds": [
    "mushroom"
  ],
  "estimatedTimeMinutes": 20,
  "estimatedCostHkd": 65,
  "eligible": true,
  "exclusionReasons": []
}
```

---

# 13. 共用資料類型

## 13.1 LocalizedText

```json
{
  "zh_HK": "番茄炒蛋",
  "en": null
}
```

規則：

- `zh_HK` 首個版本必填；
- `en` 首個版本可以為 `null`；
- 不在同一個字串中混合兩種語言。

---

## 13.2 NutritionEstimate

```json
{
  "caloriesKcal": null,
  "proteinG": null,
  "fatG": null,
  "carbohydrateG": null,
  "source": null
}
```

沒有可靠來源時，營養欄位必須使用 `null`。

不得由大型語言模型隨意生成看似精確的營養數值。

---

## 13.3 RecipeSource

```json
{
  "type": "team_created",
  "reference": null
}
```

`type` 可以使用：

```text
team_created
public_dataset
official_source
licensed_source
user_created
```

不得直接複製來源不明或受版權保護的完整菜譜內容。

---

## 13.4 IngredientSubstitution

```json
{
  "originalIngredientId": "butter",
  "replacementIngredientId": "cooking_oil",
  "quantity": 10,
  "unit": "milliliter"
}
```

---

# 14. 枚舉值

## 14.1 廚藝程度

```text
beginner
intermediate
experienced
```

---

## 14.2 飲食目標

```text
taste
healthy
calorie_control
low_oil_low_sugar
budget
quick
no_specific_goal
```

---

## 14.3 口味偏好

```text
light
spicy
sweet_and_sour
rich
soup
crispy
new_flavors
no_preference
```

---

## 14.4 飲食限制

```text
vegetarian
vegan
halal
no_beef
no_pork
```

---

## 14.5 常見過敏原

```text
peanut
tree_nut
milk
egg
wheat
soy
fish
shellfish
```

---

## 14.6 存放位置

```text
refrigerated
frozen
room_temperature
```

---

## 14.7 食材分類

```text
vegetable
fruit
meat
seafood
egg_and_dairy
staple
seasoning
beverage
other
```

---

## 14.8 菜式難度

```text
beginner
intermediate
advanced
```

---

## 14.9 火力

```text
low
medium_low
medium
medium_high
high
```

---

## 14.10 推薦優先條件

```text
quick
healthy
use_expiring_ingredients
low_cleanup
budget
new_flavor
low_energy
filling
```

---

## 14.11 推薦理由代碼

```text
high_ingredient_coverage
uses_expiring_ingredient
within_time_limit
within_budget
matches_skill_level
matches_health_goal
low_cleanup
uses_available_cookware
offers_new_flavor
```

---

## 14.12 排除理由代碼

```text
contains_allergen
violates_dietary_restriction
contains_disliked_ingredient
missing_required_cookware
exceeds_time_limit
exceeds_budget
missing_core_ingredient
```

---

## 14.13 食材單位

首個版本不允許使用者自由輸入食材單位，只能從預設單位中選擇。

```text
piece
gram
kilogram
milliliter
liter
pack
box
bottle
can
bunch
slice
bowl
cup
tablespoon
teaspoon
catty
```

介面對應：

| 內部值 | 繁體中文 |
|---|---|
| `piece` | 個／隻 |
| `gram` | 克 |
| `kilogram` | 公斤 |
| `milliliter` | 毫升 |
| `liter` | 公升 |
| `pack` | 包 |
| `box` | 盒 |
| `bottle` | 樽 |
| `can` | 罐 |
| `bunch` | 扎 |
| `slice` | 片 |
| `bowl` | 碗 |
| `cup` | 杯 |
| `tablespoon` | 湯匙 |
| `teaspoon` | 茶匙 |
| `catty` | 斤 |

不同食材透過 `allowedUnits` 限制可選單位。

示例：

```text
雞蛋：隻、盒
牛奶：毫升、公升、盒、樽
雞肉：克、公斤、斤、包
番茄：個、克、公斤、斤
```

`piece` 在介面的顯示方式由食材決定：

```text
egg + piece → 隻
tomato + piece → 個
chicken_wing + piece → 隻
```

首個版本暫時不另外建立 `unitDisplayOverrides` 模型。

---

## 14.14 食材來源

```text
system
user_created
```

---

# 15. 模型關係

```text
UserProfile
├── PantryItem[]
├── CookingSession[]
└── UserFeedback[]

Ingredient
├── PantryItem[]
└── RecipeIngredient[]

Recipe
├── RecipeIngredient[]
├── RecipeStep[]
├── CookingSession[]
└── UserFeedback[]

CookingSession
└── UserFeedback
```

主要關係：

- 一個使用者可以擁有多個雪櫃食材；
- 一個使用者可以建立多個自訂食材；
- 一個標準食材可以出現在多個使用者的雪櫃中；
- 一道菜式包含多個菜式食材；
- 一道菜式包含多個煮食步驟；
- 一個使用者可以多次煮同一道菜；
- 一次煮食紀錄最多對應一份回饋；
- 自訂食材可以透過 `canonicalIngredientId` 對應標準食材。

---

# 16. 核心驗證規則

## 16.1 UserProfile

- `nickname` 不得為空；
- `skillLevel` 必須是允許的枚舉值；
- 必須明確記錄過敏資料，即使內容為空陣列；
- `defaultTimeMinutes` 如有值，必須大於零；
- `defaultBudgetPerRecipeHkd` 如有值，必須大於或等於零；
- `expiryReminderDays` 必須是大於或等於零的整數；
- 首個版本預設 `expiryReminderDays` 為 2；
- `onboardingCompleted` 必須是布林值。

---

## 16.2 Ingredient

- `name.zh_HK` 不得為空；
- `category` 必須是允許的食材分類；
- `defaultUnit` 必須包含在 `allowedUnits` 中；
- `allowedUnits` 不得為空；
- 使用者不能自由建立新單位；
- `source = user_created` 時，`ownerUserId` 不得為空；
- 自訂食材如能對應標準食材，應設定 `canonicalIngredientId`；
- `canonicalIngredientId` 如有值，必須對應有效的標準食材。

---

## 16.3 PantryItem

- `quantity` 必須大於零；
- `ingredientId` 必須對應有效的標準或自訂食材；
- `unit` 必須包含在該食材的 `allowedUnits` 中；
- `expiryDate` 如存在，不得早於 `purchaseDate`；
- 只有 `available` 狀態的食材會參與推薦。

---

## 16.4 Recipe

- 至少包含一項必要食材；
- 至少包含一個煮食步驟；
- `baseServings` 必須大於零；
- `timeMinutes` 必須大於零；
- `estimatedCostHkd` 如有值，必須大於或等於零；
- `allergens` 必須經過人工檢查；
- `ingredients` 中使用的單位必須屬於預設單位；
- 只有 `published` 狀態的菜式可以進入正式推薦。

---

## 16.5 RecipeIngredient

- `ingredientId` 必須對應有效的標準食材；
- `quantity` 如有值，必須大於零；
- `unit` 如有值，必須屬於預設單位；
- `required` 必須是布林值；
- 可替代食材必須對應有效食材。

---

## 16.6 RecipeStep

- `stepNumber` 必須大於零；
- `instruction.zh_HK` 不得為空；
- `durationSeconds` 如有值，必須大於零；
- `heatLevel` 如有值，必須是允許的枚舉值；
- 同一道菜式的步驟編號不得重複。

---

## 16.7 CookingSession

- `currentStepNumber` 不得小於 1；
- `servings` 必須大於零；
- 已完成紀錄必須包含 `completedAt`；
- `completedAt` 不得早於 `startedAt`；
- `actualDurationMinutes` 如有值，必須大於零。

---

## 16.8 UserFeedback

- `tasteRating` 如有值，只能為 1–5；
- `actualDurationMinutes` 如有值，必須大於零；
- 每項回饋必須對應有效的 `CookingSession`；
- 同一次煮食紀錄最多對應一份回饋。

---

## 16.9 RecommendationRequest

- `servings` 必須大於零；
- `maxTimeMinutes` 如有值，必須大於零；
- `maxBudgetPerRecipeHkd` 如有值，必須大於或等於零；
- `priorities` 最多選擇三項；
- 所有食材識別碼必須對應有效食材。

---

## 16.10 RecommendationResult

以下情況必須排除菜式，不得只降低分數：

- 包含使用者已知過敏原；
- 違反使用者飲食限制；
- 包含使用者明確拒絕的食材；
- 缺少不可替代的必要煮食工具。

如菜式被排除：

```text
eligible = false
```

並在 `exclusionReasons` 中記錄原因。

---

# 17. 私隱與敏感資料

以下資料可能具有敏感性：

- 食物過敏；
- 飲食限制；
- 未來可能加入的體重及健康資料。

資料設計原則：

- 只收集產品功能所需資料；
- 不把過敏或健康資料用於廣告；
- 不在日誌中直接輸出完整個人資料；
- API Key 不存放在手機 App 中；
- 正式版本需要允許使用者刪除個人資料；
- 首個原型盡量使用模擬資料；
- GitHub 倉庫不得包含真實使用者資料；
- 正式認證系統的密碼不得直接儲存在 `UserProfile` 中。

---

# 18. 首個版本暫不處理

首個版本暫不建立以下複雜資料模型：

- 真實電郵認證；
- 支付及訂閱；
- 社交關係；
- 評論及讚好；
- 外賣訂單；
- 網購訂單；
- Apple Health 資料；
- 醫療診斷；
- 正式營養治療計劃；
- 多家庭共享雪櫃；
- 複雜食材批次追蹤；
- 多幣種價格；
- 餐廳及供應商資料；
- 使用者自訂食材單位。

---

# 19. 後續實作順序

```text
data-model.md
→ ingredients.seed.json
→ recipes.seed.json
→ Python 資料類別
→ 推薦算法
→ 自動化測試
→ FastAPI 請求及回應模型
→ 本地資料儲存
→ 正式資料庫
→ Flutter 資料類別
```

目前不需要立即建立正式資料庫。

---

# 20. 已確認事項

- [x] 首個版本暫不保存真實電郵及密碼；
- [x] 首個版本使用本地演示帳戶；
- [x] 臨期食材預設提前 2 日提醒；
- [x] 預算按整道菜計算；
- [x] 允許使用者建立自訂食材；
- [x] 首批食材及菜式暫不需要英文內容；
- [x] 首個版本不允許使用者自由輸入食材單位；
- [x] 食材單位必須從預設清單中選擇。

---

# 21. 尚待確認事項

- [ ] 自訂食材是否需要人工審核後才可分享給其他使用者；
- [ ] 未能對應標準食材的自訂食材如何參與推薦；
- [ ] 菜式是否允許缺少必要食材後仍進入推薦；
- [ ] 食材替代關係由菜式保存，還是單獨建立；
- [ ] 是否需要記錄菜式收藏；
- [ ] 是否需要保存被使用者拒絕的推薦；
- [ ] 煮食紀錄是否允許刪除；
- [ ] 未來是否允許使用者修改臨期提醒日數。

---

# 22. 變更紀錄

| 版本 | 日期 | 變更內容 |
|---|---|---|
| v0.1 | 2026-11-03 | 建立核心資料模型 |
| v0.2 | 2026-11-03 | 首個版本改為本地演示帳戶，暫不保存真實電郵 |
| v0.2 | 2026-11-03 | 臨期食材預設提前 2 日提醒 |
| v0.2 | 2026-11-03 | 預算改為按整道菜計算 |
| v0.2 | 2026-11-03 | 加入使用者自訂食材及標準食材映射 |
| v0.2 | 2026-11-03 | 首批菜式暫不要求英文內容 |
| v0.2 | 2026-11-03 | 食材單位改為只能從預設單位中選擇 |
