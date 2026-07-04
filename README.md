# Data Storytelling: Interactive Order Performance Dashboard

## 📌 Project Overview
This repository contains **Project 4** of the **DecodeLabs Industrial Training Kit (Batch 2026)**. In enterprise operations, data visualization must move beyond basic charting to become a strategic engine for decision-making. [cite_start]The objective of this project is to implement a high-impact, low-noise **Power BI Dashboard** that transforms 1,200 transactional records into an executive data story readable within seconds[cite: 1647, 1648, 1653].

[cite_start]Following the three professional roles of data visualization—**The Architect** (matching chart choices to business logic), **The Editor** (maximizing the data-ink ratio), and **The Storyteller** (structuring insights around business narratives)—the dashboard isolates an operational leak worth over **\$519K** and provides a clear, data-driven hypothesis for revenue recovery[cite: 1654, 1655, 1656, 1657, 1701].

---

## 🎨 Dashboard Design Philosophies & UI Constraints
[cite_start]To prevent information overflow, the report implements a strict **"One Page, One Core Message"** architecture across four beautifully styled report views[cite: 1663]:
* [cite_start]**Zero Baseline Integrity:** Every bar and line chart starts its value axis at a absolute zero to prevent visual distortion[cite: 1797].
* [cite_start]**Legend Elimination:** All legends were removed and replaced with direct data labels to optimize the data-ink ratio[cite: 1656, 1695, 1799].
* [cite_start]**Spotlight Color Palette:** The visual theme is limited to 5 distinct hues (navy ink, muted grey background context, and a single intentional accent color matching the narrative beat of each page—**Blue** for growth, **Red** for operational risk, and **Green** for tactical resolution)[cite: 1795, 1813].
* [cite_start]**Anti-Chartjunk Policy:** Avoided all 3D distortions, pie charts over 3 slices, heavy structural borders, or decorative gridlines[cite: 1656, 1729, 1799].

---

## 🏛️ The Dashboard Narrative Structure (SCR Framework)

### 📈 Page 1: The Situation (Theme Accent: Blue)
* [cite_start]**Executive Focus:** Framing baseline growth limits and category performance layout[cite: 1691, 1813].
* [cite_start]**Action Title:** *"Revenue reached \$1.26M across 1,200 orders, but quarterly growth has cooled since its 2023 peak"*[cite: 1667].
* [cite_start]**Chart Choices:** A continuous timeline **Line Chart** captures quarterly sales velocity, paired with a **Horizontal Bar Chart** ranking product lines descending[cite: 1694, 1695].
* [cite_start]**Core Insights:** The business hit an all-time revenue high of **\$145.6K in Q2 2023** but has since decelerated by **29% down to \$128.3K by Q2 2025**[cite: 1696, 1805]. [cite_start]`Chair` and `Printer` dominate catalog revenue shares, while `Phone` yields the lowest baseline income[cite: 1697].

### 🚨 Page 2: The Complication (Theme Accent: Red)
* [cite_start]**Executive Focus:** Unmasking the primary bottleneck hiding within transaction states[cite: 1726, 1813].
* [cite_start]**Action Title:** *"41% of all orders are Cancelled or Returned – \$520K in order value never converts to kept revenue"*[cite: 1701].
* [cite_start]**Chart Choices:** A descriptive **Horizontal Bar Chart** ranking fulfillment states, and an operational comparison bar chart isolating performance by settlement method[cite: 1726, 1729].
* [cite_start]**Core Insights:** Only a minor **19.2%** of transactional orders reach final `Delivered` status[cite: 1731, 1807]. [cite_start]Combined, `Cancelled` (20.8%) and `Returned` (20.6%) completely outweigh every single completed order status[cite: 1731]. [cite_start]This friction rate hovers uniformly between **41% and 44%** across four of five payment types—with **Online Payment** emerging as a major positive anomaly at just **35.3%**[cite: 1732, 1807].

### 🟩 Page 3: The Resolution (Theme Accent: Green)
* [cite_start]**Executive Focus:** Modeling financial recovery values via targeted process optimization[cite: 1758, 1813].
* [cite_start]**Action Title:** *"Matching every payment method to Online's 35.3% failure rate could recover ~\$73K in order value"*[cite: 1735].
* [cite_start]**Chart Choices:** A targeted benchmark visualization applying a **Constant Reference Line** drawn at the 35.3% Online failure rate floor to immediately visualize efficiency gaps[cite: 1758, 1761].
* [cite_start]**Core Insights:** By establishing a clear checkout optimization strategy (e.g., small fee waivers, automated digital wallet prompts, or faster refund promises) to shift volume toward Online payment methods, the company can actively attempt to close the **6.1-point failure gap**[cite: 1743, 1757, 1808]. [cite_start]Successfully matching this benchmark would save an estimated **\$73,200 in order value**, shifting it straight into completed revenue—a **14% reduction in total capital drain**[cite: 1763, 1808].

### 📊 Page 4: Channel Detail (Supporting View)
* [cite_start]**Executive Focus:** Providing a granular marketing attribution breakdown to look at specific growth levers[cite: 1786].
* [cite_start]**Action Title:** *"Instagram drives the most total revenue, but Facebook customers spend the most per order"*[cite: 1766].
* [cite_start]**Core Insights:** All five core customer acquisition channels perform within a tight velocity band[cite: 1787]. [cite_start]**Instagram** leads absolute transactional revenue volume at **\$275.3K**, whereas **Facebook** fields premium individual customer value averaging **\$1,098 per transaction**[cite: 1787].

---

## 🛠️ Data Modeling & DAX Formulation
[cite_start]The business intelligence metrics driving this dashboard are programmatically compiled within Power BI using custom **Data Analysis Expressions (DAX)** built directly on top of the verified dataset[cite: 1812]:

* **Gross Enterprise Revenue:**
    ```dax
    Total Revenue = SUM(Orders[TotalPrice])
    ```
* **Pipeline Failure Velocity:**
    ```dax
    Failed Order Rate = 
    DIVIDE(
        CALCULATE(COUNT(Orders[OrderID]), Orders[OrderStatus] IN {"Cancelled", "Returned"}),
        COUNT(Orders[OrderID]),
        0
    )
    ```
* **Online Checkout Failure Anchor:**
    ```dax
    Online Failure Rate = 
    CALCULATE(
        [Failed Order Rate], 
        Orders[PaymentMethod] = "Online"
    )
    ```
* **Projected Recovery Model:**
    ```dax
    Projected Recovery Value = 
    SUMX(
        FILTER(Orders, Orders[PaymentMethod] <> "Online"),
        Orders[TotalPrice] * ([Failed Order Rate] - [Online Failure Rate])
    )
    ```

---

## 🏁 Verification Check against Requirements
[cite_start]Every visualization component is strictly cross-validated against the original Project 4 task criteria[cite: 1789]:
* [cite_start][x] **Appropriate Visual Selection:** Replaced generic pie charts with clean horizontal bar charts to elegantly show multi-categorical dimensions (5+ steps)[cite: 1729, 1793].
* [cite_start][x] **Action-Oriented Titles:** Eliminated lazy titles like "Revenue over Time" and replaced them with punchy, insight-driven analytical headlines[cite: 1657, 1667, 1701, 1735, 1766].
* [cite_start][x] **Executive Decision Support:** Designed around explicit **"So What?"** text recommendations right inside the interface layout[cite: 1756, 1762].

---

## 📂 Repository Layout
