# AgentHub Admin Panel Design Specification (SPECS.md Equivalency)

This specification defines the visual hierarchy, state machines, component styling, and section-by-section behavioral requirements for the AgentHub Admin Panel.

## Component Inventory (Reusable UI Library)

### 1. Sidebar Navigation
- **Visuals**: A persistent, fixed-width column on the left (or left-drawer layout for tablet views). Heavy dark border/fill in dark mode; clean light-grey boundary in light mode. Displays the "AgentHub" logo, brand mark, and a vertical list of the 6 core sections.
- **Interactive States**: Displays an "active" indicator (e.g., solid accent background block and contrasting text color) representing the currently selected section. 

### 2. Metric Card
- **Visuals**: Solid background panel with rounded corners (`rounded-xl`), subtle outer border (`border border-slate-200 dark:border-slate-800`), and a small soft shadow. Includes:
  - An icon container with an accent background tinted to match the metric's semantic context.
  - A small, muted label.
  - A large, bold numeric readout.
- **Behavior**: Static preview metrics.

### 3. Action Dropdown (The "⋮" Menu)
- **Visuals**: A small absolute-positioned menu that overlays adjacent content, styled with list options, hover states, and clear boundaries.
- **Behavior**: Clicking the trigger (`⋮` button) toggles the dropdown visible/invisible. Only one dropdown can be open at a time globally. Clicking anywhere outside the open dropdown's container automatically closes it.

### 4. Modal Overlays
- **Visuals**: A semi-transparent dark backdrop filling 100% of the screen height and width (`backdrop-blur-sm bg-slate-900/50`). Centered over the screen is the modal body.
- **Behavior**: Opens when "View detail" or "Configure" is selected. Closes when clicking the explicit close button (typically an "X" or "Close" button) or when clicking anywhere directly on the backdrop outside the modal dialog box.

### 5. Collapsible List (Skills List)
- **Visuals**: A hidden or compact list box container with an action trigger button showing a caret icon (▼/▲).
- **Behavior**: Clicking the trigger toggles the list open/closed. Uses CSS transition rules (`transition-all duration-300 max-h-0 overflow-hidden` changing to an explicit `max-h-96`) to guarantee a smooth dynamic layout transition.

### 6. Badges & Indicators
- **Visuals**: Small, low-contrast pill-shaped badges (`px-2.5 py-0.5 rounded-full text-xs font-semibold`). Colors indicate status dynamically (e.g., green for Active/Resolved, amber for Inactive/Warn, red for Failing/Error).

---

## Section-by-Section Specifications (Minimum 3 Specs per Section)

### 1. Dashboard View
1. **Metric Grid Layout**: Four distinct, responsive metric cards arranged in a 2x2 grid on medium screens and 1x4 on large screens, detailing:
   - **Total Revenue (Month)**: Indigo theme.
   - **Discount/Coupon Losses**: Amber theme.
   - **Active Agents**: Emerald theme.
   - **Failing Agents**: Rose theme.
2. **Weekly Activity Chart Area**: A full-width placeholder area below the metric grid with a distinctive dashed border (`border-dashed border-2 border-slate-300 dark:border-slate-700`), a clean SVG graphic visualization representing a line/bar chart, and a centered description label.
3. **Recent Events Ticker**: A miniature timeline feed showing recent actions or operational states of agents.

### 2. User Management View
1. **Interactive Table**: A dense table listing at least 5 hardcoded users with columns for `Name`, `Email Address`, `Subscription Plan` (Pro, Standard, Enterprise), and `Status` (Active, Suspended).
2. **Dynamic Detail Modal**: Choosing "View detail" from the row action dropdown opens a modal containing comprehensive user records, complete with a placeholder user avatar, user registration date, lifetime value (LTV), and last login IP.
3. **Delete Action Guard**: Selecting "Delete" triggers a browser-native confirmation alert (`confirm()`) or mock visual confirmation toast.

### 3. Agent Management View
1. **Agent Overview Cards/List**: A catalog listing at least 4 registered agents detailing: agent name, owner (the renting company user), current status badge (Active, Inactive, Failing), and their skill lists.
2. **Animated Collapsible Skills**: Associated capabilities (e.g., "Web Crawler", "Outlook Writer") are collapsed by default. Clicking the caret button expands the panel downward with a smooth visual transition.
3. **Prompt Configuration Drawer**: Selecting "Configure" opens a modal displaying the agent's exact system instructions in an editable HTML `<textarea>` element, allowing mock prompt engineering.

### 4. Skills Catalog View
1. **Context Banner**: A prominent panel explanation box at the top explaining the precise architecture of "Skills" inside the AgentHub infrastructure (how capabilities map to dynamic tool definitions).
2. **Skill Detail Grid**: At least 4 distinct skill blocks containing: Skill Name, short description, status tag, and an indicator count showing the exact number of agents using this skill.
3. **Dynamic Skills Modal**: "View detail" displays deep schema properties such as expected JSON input schemas and API parameters required.

### 5. Agent Contracts View
1. **Financial Ledger Table**: A tracking matrix of at least 4 active and historical billing agreements showing: Client, Rented Agent, Contracted Skills summary list, Contract Validity Dates, and total amount paid.
2. **Detailed Itemized Invoices**: Choosing "View detail" displays an interactive invoice breakdown modal highlighting individual subscription skill costs (e.g., "Base Rate: $150", "Browsing Skill: $50") and billing frequencies.
3. **Filter and Search State**: Visual mock dropdown controls for filtering contracts by "Active" versus "Expired" status.

### 6. Error Log View
1. **System Log Stream**: A real-time style log displaying at least 6 hardcoded error events. Columns: `Timestamp`, `Agent Name`, `Severity/Error Type Badge` (Critical, Warning, Info), and `Brief Message`.
2. **Traceback Modal**: Choosing "View detail" loads a modal visualizing a code-style stack trace inside a container block, ideal for debugging.
3. **Resolve Action Trigger**: Clicking "Mark as resolved" visualizes a state change by converting the severity badge to a green "Resolved" state and striking through the message.

---

## Acceptance Criteria
1. **Unified SPA Engine**: Moving between pages replaces the content in the main viewport container without triggering a full page reload, while preserving application configurations.
2. **Theme Switcher**: Clicking the Sun/Moon toggle in the header adds or removes the `.dark` class on the main root container. The dark mode state persists across section views.
3. **Dropdown Boundaries**: Clicking inside a dropdown opens it; clicking outside or on a different dropdown closes it.
4. **Modal Escapes**: Every modal remains closable by clicking the external backdrop container as well as an explicit close trigger button.
5. **Fluid Collapsibles**: Agent details and skill cards expand and collapse using CSS transitions without abrupt visual jumps.
6. **Unified Data Integrity**: The exact same agent name (e.g., "SupportBot Pro") must consistently propagate across Agent Management, Contracts, and the Error Logs to maintain realistic mock-data consistency.