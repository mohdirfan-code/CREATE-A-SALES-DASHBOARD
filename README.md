# CREATE-A-SALES-DASHBOARD

*COMPANY*: CODTECH IT SOLUTIONS

*NAME*: MOHD IRFAN

*INTERN ID*: CT08WY57

*DOMAIN*: POWER BI

*DURATION*: 8 WEEKS

*MENTOR*: NEELA SANTHOSH KUMAR

## Task 1: Sales Dashboard in Power BI
# Overview
The goal of this task was to provide a clear overview of sales trends, customer segments, and product performance using various Power BI visualizations. This dashboard enables business decision-makers to analyze sales patterns effectively and make data-driven decisions.
The dataset used for this analysis contained sales data, customer information, product categories, order details, and geographical data. By transforming this data into meaningful visual representations, the dashboard helps identify profitable segments, track sales trends over time, and examine regional sales performance. Additionally, I incorporated a Date Slicer, allowing users to filter sales data dynamically based on specific time periods.

# Dashboard Components and Insights
1. Sales by Segment (Pie Chart)
The pie chart represents the sales distribution across different customer segments: Consumer, Corporate, and Home Office. This visualization helps identify the largest revenue-generating segment and understand which customer group contributes most to the total sales.
From the analysis, it is clear that some segments perform better than others. Understanding these variations allows businesses to optimize marketing strategies and focus on high-value customer groups.

2. Sales by Order Date (Line Chart)
The line chart showcases the trend of total sales over time based on the Order Date. This visualization helps identify seasonal sales patterns, growth trends, and fluctuations in revenue. By analyzing this data, businesses can anticipate peak sales periods, adjust inventory, and plan sales strategies accordingly.

3. Sales by Sub-Category (Bar Chart)
The bar chart displays the sales performance of various product sub-categories. This helps in identifying top-performing and underperforming products. Businesses can use this insight to make informed decisions regarding product promotions, inventory management, and future product investments.
For example, if a particular category is consistently underperforming, the company can analyze the reasons behind it—whether due to low demand, high competition, or pricing issues—and take corrective actions.

4. Sales by State (Map Visualization)
The map visualization provides a geographic representation of sales across different states. This allows businesses to analyze regional sales performance, identify high-revenue areas, and target potential markets for expansion.
Geographical insights are crucial for understanding how location influences sales. If certain states have significantly lower sales, businesses can adjust their marketing efforts to boost performance in those regions.

5. Sales by Region (Donut Chart)
The donut chart compares sales across different regions (East, West, Central, and South). This visualization helps in regional performance comparison and enables businesses to focus on high-revenue areas while improving strategies for underperforming regions.

6. Date Slicer (Interactive Filtering)
One of the most important features added to the dashboard is the Date Slicer. This allows users to filter sales data based on specific time periods. By selecting different date ranges, users can analyze trends over time and observe changes in sales patterns during specific months or years.

# Conclusion
This Sales Analysis Dashboard successfully provides a comprehensive view of sales trends using interactive Power BI visualizations. By analyzing different dimensions of sales—such as customer segments, product categories, regional sales, and time-based trends—this dashboard enables businesses to identify opportunities for growth, optimize sales strategies, and improve decision-making.

## OUTPUT : ![Image](https://github.com/user-attachments/assets/9df1259d-1f3c-49fc-a343-0385fc642937)





graph TD
    subgraph "Phase 1: Data Foundation & Splitting"
        A["<b>Start:</b> <br> Imbalanced Pestopia Dataset <br> (55,914 Images, 132 Classes)"] --> B{Stratified 80-10-10 Split};
        B --> C["Training Set <br> (44,731 Images)"];
        B --> D["Validation Set <br> (5,591 Images)"];
        B --> E["Test Set <br> (5,592 Images)"];
    end

    subgraph "Phase 2: Preprocessing & Augmentation"
        C --> F["<b>Training Data Pipeline:</b> <br> - Apply `RandAugment` <br>   (Solves Overfitting) <br> - Resize to 224x224 <br> - ToTensor & Normalize"];
        D & E --> G["<b>Validation/Test Pipeline:</b> <br> - Resize to 224x224 <br> - ToTensor & Normalize"];
        F --> H[Training DataLoader];
        G --> I[Validation DataLoader];
    end

    subgraph "Phase 3: SOTA Model & Training Recipe"
        J["<b>Model Architecture:</b> <br> ConvNeXt-Tiny <br> (Pre-trained on ImageNet-21k)"]
        
        subgraph "LLRD Strategy"
            direction LR
            J1["Stem <br> (Slowest LR)"] --> J2["Stage 1-2 <br> (Slow LR)"] --> J3["Stage 3 <br> (Medium LR)"] --> J4["Stage 4 <br> (Fast LR)"] --> J5["Head <br> (Fastest LR)"];
        end

        K["<b>Loss Function:</b> <br> Class-Balanced Focal Loss <br> (Handles Imbalance & Hard Cases)"]
        L["<b>Optimizer & Scheduler:</b> <br> - AdamW Optimizer <br> - Cosine Annealing LR"]
    end
    
    subgraph "Phase 4: Training & Validation Loop (30 Epochs)"
        M{Start Epoch} --> N[Train model on one batch];
        N --> O[Calculate Loss & Backpropagate];
        O --> P{End of Training Batches?};
        P -- Yes --> Q[Evaluate model on Validation Set];
        Q --> R{Is Val Accuracy > Best Accuracy?};
        R -- Yes --> S[Save Best Model Weights];
        R -- No --> T[End Epoch];
        S --> T;
        P -- No --> N;
        T --> U{All Epochs Done?};
        U -- No --> M;
    end
    
    subgraph "Phase 5: Final Evaluation on Unseen Data"
        V[Load Best Saved Model] --> W[Make Predictions on Test Set];
        W --> X["<b>Calculate Final Metrics:</b> <br> - Top-1 Accuracy: 74.52% <br> - Top-3 Accuracy: 90.31% <br> - Top-5 Accuracy: 94.19%"];
        X --> Y["<b>End:</b> <br> Final Trained Model"];
    end

    %% Connections
    H --> M;
    I --> M;
    J --> J1;
    L --> M;
    K --> M;
    U -- Yes --> V;
