# Smart-Kitchen
# Smart Kitchen｜今晚煮乜？

> 一款為香港學生及獨居年輕人設計的情境感知智能煮食助手。  
> A context-aware cooking assistant designed for students and young adults living alone in Hong Kong.

---

## 項目狀態｜Project Status

🚧 本項目目前處於概念設計及原型開發階段。

現階段的目標是完成一個可在手機上運行的產品原型，展示從食材管理、個人化推薦到分步煮食指導的完整使用流程。

🚧 This project is currently in the concept design and prototype development stage.

The current objective is to build a functional mobile prototype demonstrating a complete user journey, from pantry management and personalized recipe recommendations to step-by-step cooking guidance.

---

## 項目簡介｜Project Overview

Smart Kitchen 是一款面向香港學生、獨居年輕人及煮食初學者的智能煮食助手。

當使用者「唔知今晚食乜」時，系統會根據家中現有食材、食材保鮮期、可用時間、每餐預算、廚藝程度、煮食工具及飲食目標，推薦合適的菜式，並解釋推薦原因。

Smart Kitchen 不只希望回答「可以煮甚麼」，亦希望協助使用者減少選擇困難、善用現有食材、減少食物浪費，並逐步建立基本煮食能力。

Smart Kitchen is an intelligent cooking assistant designed for students, young adults living alone, and beginner cooks in Hong Kong.

When users are unsure what to eat, the system recommends suitable dishes based on their available ingredients, ingredient expiry dates, available time, budget, cooking ability, kitchen equipment, and dietary goals. It also explains why each dish has been recommended.

Rather than simply answering “What can I cook?”, Smart Kitchen aims to reduce decision fatigue, make better use of available ingredients, reduce household food waste, and help users gradually develop practical cooking skills.

---

## 項目目標｜Project Objectives

本項目希望協助使用者：

- 減少每日決定食甚麼的壓力；
- 優先使用即將到期的食材；
- 減少不必要的食物浪費；
- 在有限時間和預算內完成一餐；
- 根據個人口味、目標及限制獲得合適推薦；
- 逐步學習及掌握基本煮食技巧；
- 根據過往的煮食結果獲得更適合自己的推薦。

This project aims to help users:

- reduce the effort involved in deciding what to eat;
- prioritize ingredients that may expire soon;
- reduce unnecessary household food waste;
- prepare meals within limited time and budget;
- receive recommendations that reflect personal preferences, goals, and restrictions;
- gradually learn and master basic cooking skills;
- receive increasingly personalized recommendations based on previous cooking experiences.

---

## 目標使用者｜Target Users

本項目主要為以下使用者設計：

- 在香港生活的學生；
- 獨居或與室友居住的年輕人；
- 煮食經驗較少的初學者；
- 家中廚房空間或煮食工具有限的人；
- 希望節省時間、控制預算或改善飲食習慣的人；
- 經常因為不知道食甚麼而感到困擾的人。

The primary target users are:

- students living in Hong Kong;
- young adults living alone or with flatmates;
- beginner cooks with limited cooking experience;
- people with limited kitchen space or cooking equipment;
- users who want to save time, control spending, or improve their eating habits;
- people who frequently struggle to decide what to eat.

---

## 使用情境｜Example User Scenario

> 一名在香港獨居的學生晚上回家後，不知道今晚食甚麼。
>
> 雪櫃內有雞蛋、番茄和一盒即將到期的蘑菇。他只有 25 分鐘，希望食得清淡一點，而且不想使用太多煮食工具。
>
> Smart Kitchen 根據現有食材、保鮮期、時間和個人偏好，推薦三道合適的菜式，並說明每項推薦的原因。
>
> 使用者選擇菜式後，系統會按照其廚藝程度提供分步指導。完成煮食後，使用者可以評價味道、難度及是否願意再次烹調，讓系統改善日後的推薦。

> A student living alone in Hong Kong arrives home in the evening without knowing what to cook.
>
> The refrigerator contains eggs, tomatoes, and a box of mushrooms that may expire soon. The user has only 25 minutes, prefers a lighter meal, and does not want to use or clean multiple pieces of cookware.
>
> Smart Kitchen recommends three suitable dishes based on the available ingredients, expiry dates, available time, and personal preferences. It also explains why each dish has been selected.
>
> After choosing a dish, the user receives step-by-step guidance adapted to their cooking experience. Once the meal is completed, the user can rate its taste and difficulty and indicate whether they would cook it again, helping the system improve future recommendations.

---

## 核心設計概念｜Core Design Concept

Smart Kitchen 的首頁會以一個可互動的個人廚房呈現。

主要互動元素包括：

- **雪櫃**：管理現有食材，查看食材數量及預計到期日；
- **煮食爐**：開始菜式搜尋或個人化推薦流程；
- **留言板**：顯示情境問候、食材提醒及今日建議；
- **窗戶**：根據時間顯示早上、下午或晚上的視覺狀態；
- **使用者頭像**：管理個人資料、飲食偏好及應用程式設定。

首頁會在保留廚房情境感的同時，使用清晰的按鈕、標籤及視覺提示，協助使用者理解哪些元素可以互動。

The Smart Kitchen home screen is presented as an interactive personal kitchen.

Its main interactive elements include:

- **Refrigerator:** manages available ingredients, quantities, and estimated expiry dates;
- **Stove:** starts recipe search or the personalized recommendation process;
- **Message board:** displays contextual greetings, ingredient reminders, and daily suggestions;
- **Window:** reflects the current time of day through different visual states;
- **User avatar:** provides access to personal information, dietary preferences, and application settings.

The home screen combines an illustrated kitchen environment with clear buttons, labels, and visual cues so that users can easily identify interactive elements.

---

## 核心功能｜Core Features

### 1. 個人化飲食檔案｜Personalized Food Profile

首次使用時，系統會引導使用者建立個人飲食檔案，包括：

- 暱稱及頭像；
- 已知食物過敏；
- 飲食禁忌；
- 主要飲食目標；
- 口味偏好；
- 廚藝程度；
- 可使用的煮食工具；
- 每餐預算；
- 可用煮食時間。

系統會區分不可違反的安全限制與可以靈活調整的個人偏好。

During onboarding, users are guided through the creation of a personalized food profile that may include:

- nickname and avatar;
- known food allergies;
- dietary restrictions;
- primary dietary goals;
- flavor preferences;
- cooking skill level;
- available cooking equipment;
- budget per meal;
- available cooking time.

The system distinguishes between mandatory safety restrictions and flexible personal preferences.

### 2. 食材及雪櫃管理｜Pantry and Refrigerator Management

使用者可以：

- 手動加入現有食材；
- 記錄食材數量及單位；
- 記錄購買日期及預計到期日；
- 區分冷藏、冷凍及常溫食材；
- 查看即將到期的食材；
- 優先尋找能使用臨期食材的菜式。

Users can:

- manually add available ingredients;
- record ingredient quantities and units;
- record purchase and estimated expiry dates;
- organize refrigerated, frozen, and shelf-stable ingredients;
- identify ingredients that may expire soon;
- prioritize recipes that use ingredients nearing expiry.

### 3. 多條件菜式推薦｜Multi-Constraint Recipe Recommendation

系統會綜合考慮：

- 現有食材；
- 食材到期時間；
- 飲食目標；
- 食物過敏及飲食禁忌；
- 可用時間；
- 每餐預算；
- 廚藝程度；
- 可用煮食工具；
- 預計清潔工作量；
- 過往評價及近期曾煮過的菜式。

每次推薦都會顯示簡短原因，例如：

> 雪櫃已經有齊大部分材料，仲可以用埋就快到期嘅蘑菇。預計 20 分鐘完成，而且只需要一個平底鑊。

The recommendation system considers:

- available ingredients;
- ingredient expiry dates;
- dietary goals;
- food allergies and dietary restrictions;
- available cooking time;
- budget per meal;
- cooking ability;
- available cooking equipment;
- expected cleanup effort;
- previous feedback and recently prepared dishes.

Each recommendation includes a short explanation, for example:

> You already have most of the required ingredients, and this dish uses the mushrooms that may expire soon. It takes approximately 20 minutes and only requires one frying pan.

### 4. 「已經諗好」搜尋模式｜Recipe Search Mode

如果使用者已經知道想食甚麼，可以直接輸入菜式名稱。

系統會搜尋相關菜式，並檢查：

- 現有食材是否足夠；
- 缺少哪些食材；
- 是否包含已知過敏原或禁忌食材；
- 是否符合時間及預算；
- 是否需要使用者沒有的煮食工具。

If users already know what they want to eat, they can search for a specific dish.

The system checks:

- whether the user has the required ingredients;
- which ingredients are missing;
- whether the recipe contains known allergens or restricted ingredients;
- whether it fits the available time and budget;
- whether it requires unavailable cooking equipment.

### 5. 「唔知食乜」推薦模式｜“I Don’t Know What to Eat” Mode

當使用者未決定想食甚麼時，可以選擇目前最重視的條件，例如：

- 想快啲煮好；
- 想食得健康啲；
- 想清理雪櫃；
- 唔想洗太多嘢；
- 想慳錢；
- 想轉吓口味；
- 今日比較攰。

系統會根據使用者當下的情境調整推薦次序，協助使用者找出一個較不容易後悔的選擇。

When users have not decided what to eat, they can indicate what matters most in the current situation, such as:

- cooking quickly;
- eating more healthily;
- clearing ingredients from the refrigerator;
- minimizing cleanup;
- saving money;
- trying something different;
- cooking while tired.

The system adjusts recommendation priorities according to the user’s current context, helping them select an option they are less likely to regret.

### 6. 分步煮食模式｜Step-by-Step Cooking Mode

選擇菜式後，使用者可以：

- 逐步查看煮食指引；
- 根據用餐人數調整食材份量；
- 使用步驟計時器；
- 查看煮食術語解釋；
- 獲得適合初學者的額外提示；
- 查看常見錯誤及安全提醒。

After selecting a recipe, users can:

- follow one cooking instruction at a time;
- adjust ingredient quantities according to serving size;
- use step timers;
- view explanations of cooking terms;
- receive additional beginner-friendly guidance;
- view common mistakes and safety reminders.

### 7. 煮食回饋｜Cooking Feedback

完成煮食後，使用者可以記錄：

- 味道評分；
- 實際難度；
- 實際所需時間；
- 是否願意再次烹調；
- 使用了哪些替代食材；
- 過程中遇到的問題。

這些資料會用於改善日後的推薦。

After completing a recipe, users can record:

- taste rating;
- perceived difficulty;
- actual cooking time;
- whether they would cook the dish again;
- ingredient substitutions;
- problems encountered during cooking.

This information will be used to improve future recommendations.

### 8. 自適應煮食學習｜Adaptive Cooking Support

系統會記錄使用者接觸過的基本煮食技巧，例如切片、炒蛋、控制火力及收汁。

初次接觸某項技巧時，系統會提供較詳細的指導。隨着使用者逐漸熟悉，提示會適度簡化；如果使用者表示遇到困難，系統會再次提供詳細說明。

The system records cooking skills encountered by the user, such as slicing, frying eggs, controlling heat, and reducing a sauce.

Detailed guidance is provided when a skill is first introduced. Instructions may gradually become shorter as the user gains experience. Detailed support can be restored when the user reports difficulty.

---

## 首個原型版本｜First Prototype Scope

首個可演示版本計劃完成以下功能：

The first demonstrable prototype is planned to include:

- [ ] 歡迎及首次使用引導｜Welcome and onboarding flow
- [ ] 本地使用者檔案｜Local user profile
- [ ] 過敏、禁忌及飲食偏好設定｜Allergy, restriction, and preference settings
- [ ] 互動式廚房首頁｜Interactive kitchen home screen
- [ ] 手動食材管理｜Manual pantry management
- [ ] 食材到期提醒｜Ingredient expiry reminders
- [ ] 「已經諗好」菜式搜尋｜Recipe search for users with a dish in mind
- [ ] 「唔知食乜」推薦流程｜Recommendation flow for undecided users
- [ ] 基於規則及評分的菜式排序｜Rule-based filtering and recipe ranking
- [ ] 個人化推薦理由｜Personalized recommendation explanations
- [ ] 菜式詳情｜Recipe details
- [ ] 分步煮食模式｜Step-by-step cooking mode
- [ ] 完成後回饋｜Post-cooking feedback
- [ ] 基本煮食紀錄｜Basic cooking history
- [ ] iOS 真機演示｜Demonstration on a physical iOS device

---

## 暫不納入首個版本｜Out of Scope for the First Prototype

為確保首個版本能夠穩定完成，以下功能暫不納入初期開發範圍：

To ensure that the first prototype remains achievable and stable, the following features are intentionally excluded:

- 自動辨識雪櫃內所有食材｜Automatic recognition of all refrigerator ingredients
- 即時影片煮食指導｜Real-time video cooking assistance
- 複雜的多代理 AI 系統｜Complex multi-agent AI systems
- 外賣或網上購物平台整合｜Food delivery or online shopping integrations
- 社交平台及使用者社群｜Social networking and community features
- Apple Health 或穿戴式裝置整合｜Apple Health or wearable-device integration
- 醫療診斷及個人化治療建議｜Medical diagnosis or personalized treatment advice
- 正式支付或訂閱功能｜Payment and subscription systems

---

## 推薦方式｜Recommendation Approach

首個版本計劃採用「規則篩選、評分排序及大型語言模型解釋」的混合方式。

The first prototype will use a hybrid approach combining deterministic filtering, weighted ranking, and large language model explanations.

基本流程如下：

The proposed workflow is:

1. 根據食物過敏、飲食禁忌及必要煮食工具，排除不合適的菜式；  
   Remove recipes that violate allergy, dietary, or essential equipment restrictions.

2. 根據現有食材、到期時間、預算、時間及廚藝程度計算推薦分數；  
   Rank eligible recipes according to available ingredients, expiry dates, budget, time, and cooking ability.

3. 選出最合適的候選菜式；  
   Select the most suitable recipe candidates.

4. 使用大型語言模型生成自然語言推薦理由及初學者指引；  
   Use a large language model to generate readable explanations and beginner-friendly guidance.

5. 在顯示結果前驗證輸出格式及必要的安全限制。  
   Validate the output format and relevant safety restrictions before presenting the result.

> 大型語言模型不會單獨負責過敏原判斷或其他食品安全決策。  
> The language model will not be solely responsible for allergy detection or other food-safety decisions.

---

## 暫定技術架構｜Proposed Technology Stack

### 手機應用程式｜Mobile Application

- Flutter
- Dart
- iOS
- Android（後續測試）｜Android testing at a later stage

### 後端｜Backend

- Python
- FastAPI

### 資料儲存｜Data Storage

- 初期：本地資料儲存｜Initial prototype: local storage
- 後續：PostgreSQL / Supabase｜Later stage: PostgreSQL / Supabase

### AI 與推薦｜AI and Recommendation

- 基於規則的安全篩選｜Rule-based safety filtering
- 多條件推薦評分｜Multi-constraint recipe ranking
- 大型語言模型推薦解釋｜Large language model explanations
- 結構化輸出驗證｜Structured output validation

> 技術選擇可能根據原型測試結果及團隊能力作出調整。  
> Technology choices may be adjusted according to prototype testing results and team capabilities.

---

## 項目發展階段｜Development Stages

### 階段一：產品定義與介面原型  
### Stage 1: Product Definition and Interface Prototype

- 確定目標使用者｜Define the target users
- 整理完整使用流程｜Define the complete user journey
- 建立低保真線框圖｜Create low-fidelity wireframes
- 設計視覺風格及互動式廚房首頁｜Design the visual system and interactive kitchen home screen

### 階段二：可點擊手機原型  
### Stage 2: Clickable Mobile Prototype

- 完成主要頁面｜Build the main screens
- 建立頁面導航｜Implement screen navigation
- 使用模擬資料展示完整流程｜Demonstrate the complete flow using mock data
- 在 iOS 模擬器及真機測試｜Test on an iOS simulator and physical device

### 階段三：本地功能  
### Stage 3: Local Functionality

- 保存個人偏好｜Store user preferences
- 管理食材及到期日｜Manage ingredients and expiry dates
- 建立初始菜式資料｜Create the initial recipe dataset
- 實現基礎推薦排序｜Implement basic recipe ranking

### 階段四：後端及 AI  
### Stage 4: Backend and AI Integration

- 建立 FastAPI 後端｜Build the FastAPI backend
- 連接推薦服務｜Connect the recommendation service
- 加入大型語言模型解釋｜Add large language model explanations
- 加入輸出驗證、錯誤處理及後備結果｜Add output validation, error handling, and fallback results

### 階段五：測試與演示  
### Stage 5: Testing and Demonstration

- 進行目標使用者測試｜Conduct target-user testing
- 收集意見並改善介面｜Collect feedback and improve the interface
- 修正主要問題｜Resolve major issues
- 完成演示影片及技術文件｜Prepare a demonstration video and technical documentation

---

## 評估方向｜Evaluation

本項目計劃從以下方面評估原型：

The prototype may be evaluated using:

- 推薦菜式是否符合使用者限制｜Compliance with user-defined restrictions
- 是否錯誤包含過敏原或禁忌食材｜Allergen and dietary-restriction violation rate
- 推薦菜式被接受的比例｜Recommendation acceptance rate
- 使用者作出選擇所需的時間｜Time required to select a dish
- 臨期食材的使用情況｜Use of ingredients nearing expiry
- 使用者對推薦理由的理解程度｜User understanding of recommendation explanations
- 初學者能否按照步驟完成菜式｜Beginner recipe-completion rate
- 使用者對整體操作體驗的評價｜Overall usability feedback

---

## 私隱與安全原則｜Privacy and Safety Principles

本項目涉及飲食偏好、過敏資訊及日後可能加入的健康資料，因此會遵循以下原則：

The project may process dietary preferences, allergy information, and potentially health-related data. It therefore follows these principles:

- 只收集產品功能所需的資料；  
  Collect only the data required for the product.

- 清楚說明個人資料的用途；  
  Clearly explain how personal information is used.

- 不將健康或過敏資料用於廣告；  
  Do not use health or allergy data for advertising.

- 允許使用者修改或刪除個人資料；  
  Allow users to modify or delete their personal data.

- API 密鑰只會保存在後端；  
  Store API keys only on the backend.

- 不在手機應用程式內儲存服務密鑰；  
  Do not embed service credentials in the mobile application.

- AI 生成內容不會被視為醫療或專業營養建議；  
  Do not present AI-generated content as medical or professional nutritional advice.

- 涉及過敏及食品安全的資訊會使用清晰、正式的語言表達。  
  Use clear and formal language for allergy and food-safety information.

---

## 團隊成員｜Team Members

### 颜照兴｜Jason Yan

暫定負責：

Proposed responsibilities:

- 產品規劃｜Product planning
- 系統架構｜System architecture
- 推薦邏輯｜Recommendation logic
- Python 後端｜Python backend
- AI 功能整合｜AI integration
- 技術測試及文件｜Technical testing and documentation

### 陈玉雯｜Viven Chen

暫定負責：

Proposed responsibilities:

- 手機介面開發｜Mobile interface development
- 食材管理模組｜Pantry management module
- 菜式資料整理｜Recipe data preparation
- 使用者測試｜User testing
- 介面及產品文件｜Interface and product documentation

> 目前分工為初步安排，將根據成員的實際技術能力及開發進度進一步調整。  
> These responsibilities are preliminary and may be adjusted according to each member’s demonstrated technical ability and development progress.

---

## AI 輔助開發說明｜Use of AI-Assisted Development

本項目可能使用生成式 AI 協助：

The project may use generative AI to assist with:

- 討論及整理產品需求｜Discussing and organizing product requirements
- 產生初始程式碼｜Generating initial code drafts
- 解釋錯誤訊息｜Explaining error messages
- 改善技術文件｜Improving technical documentation
- 建立測試案例｜Preparing test cases

所有納入項目的程式碼及內容均應由團隊成員審閱、測試及確認。

每位成員需要能夠解釋自己負責的主要程式碼、技術選擇、測試方法及最終結果。

All code and content included in the project should be reviewed, tested, and validated by the project team.

Each contributor should be able to explain the implementation, technical decisions, testing methods, and results of the modules for which they are responsible.

---

## 授權｜License

本項目目前僅用於學習、研究及產品原型展示。

在與所有相關成員確認程式碼所有權及後續用途前，本項目暫不提供正式的開源授權。

This project is currently intended for learning, research, and prototype demonstration purposes.

No formal open-source license will be provided until code ownership and future usage have been agreed upon by all relevant contributors.
