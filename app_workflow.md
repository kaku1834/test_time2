# Application Workflow

## Main Application Flow
```mermaid
graph TD
A[Start] --> B[Setup Page Config]
B --> C[Initialize Authentication]
C --> D{Auth Status?}
D -->|No| E[Show Login Error]
D -->|Yes| F[Load Data]
F --> G[Get Most Common Syuyaku]
G --> H[Filter Selection Process]
H --> H1[Brand Filter]
H1 --> H2[Region Filter]
H2 --> H3[Department Filter]
H3 --> H4[SubCategory Filter]
H4 --> H5[Syuyaku Filter]
H5 --> H6[Size Filter]
H6 --> H7[Color Filter]
H7 --> H8[SKU Filter]
H8 --> H9[Date Range Filter]
H9 --> I[Process Product Info]
I --> I1[Get Unique Product Info]
I1 --> I2[Filter for Selected Syuyaku]
I2 --> I3[Convert to Pandas]
H9 --> J[Process Summary Info]
J --> J1[Filter Accuracy Summary]
J1 --> J2[Filter Problem Summary]
I3 --> K[Display Tables]
J2 --> K
K --> L[Prepare Visualization]
L --> L1[Get Display Data]
L1 --> L2[Get Real Data]
L2 --> L3[Get Prediction Data]
L3 --> M[Get Visualization Columns]
M --> M1[Get Size Columns]
M1 --> M2[Get Color Columns]
M2 --> N[Create Dashboard]
N --> O[Display Dashboard]
O --> P[End]
classDef process fill:#f9f,stroke:#333,stroke-width:2px;
classDef decision fill:#bbf,stroke:#333,stroke-width:2px;
classDef display fill:#bfb,stroke:#333,stroke-width:2px;
class D decision;
class K,O display;
class H1,H2,H3,H4,H5,H6,H7,H8,H9 process;
class I1,I2,I3,J1,J2 process;
class L1,L2,L3,M1,M2 process;
```

## Module: auth_utils
```mermaid
graph TD
    A1[load_auth_config] --> B1[Read YAML]
    B1 --> C1[Return Config]
    
    A2[setup_authenticator] --> B2[Create Authenticator]
    B2 --> C2[Return Auth Object]
    
    A3[setup_page_config] --> B3[Configure Streamlit Page]
    
    A4[handle_authentication] --> B4{Check Auth Status}
    B4 -->|Success| C4[Show Welcome]
    B4 -->|Failed| D4[Show Error]
    B4 -->|None| E4[Show Warning]
    
    A5[initialize_authentication] --> B5[Load Config]
    B5 --> C5[Setup Auth]
    C5 --> D5[Handle Auth]
```

## Module: data_loader
```mermaid
graph TD
    A[load_data] --> B[Cache Function]
    B --> C1[Load CSV Files]
    B --> C2[Load Excel Files]
    C1 --> D[Convert Dates]
    C2 --> E[Return Data]
    D --> E
```

## Module: data_processor
```mermaid
graph TD
    A1[get_most_syuyaku] --> B1[Group by Syuyaku]
    B1 --> C1[Find Max Sales]
    C1 --> D1[Get Related Info]
    D1 --> E1[Return Values]
    
    A2[get_sorted_unique_values] --> B2[Get Unique]
    B2 --> C2[Sort Values]
    C2 --> D2[Return List]
    
    A3[filter_data_sequentially] --> B3{Check Filters}
    B3 --> C3[Apply Brand]
    C3 --> D3[Apply Region]
    D3 --> E3[Apply Department]
    E3 --> F3[Apply Date Range]
```

## Module: data_transformer
```mermaid
graph TD
    A1[process_stock_data] --> B1[Select Columns]
    B1 --> C1[Process Size]
    B1 --> D1[Process Color]
    C1 --> E1[Combine Data]
    D1 --> E1
    
    A2[process_sales_data] --> B2[Filter Country]
    B2 --> C2[Aggregate Sales]
    C2 --> D2[Join Date Info]
    
    A3[process_rate_data] --> B3[Filter Syuyaku]
    
    A4[combine_all_data] --> B4[Join Data]
    B4 --> C4[Fill Missing]
    C4 --> D4[Return Combined]
```

## Module: visualizer
```mermaid
graph TD
    A[setup_plot_style] --> B[Define Colors]
    
    C[create_dashboard_figure] --> D[Setup Figure]
    D --> E1[Plot Limited Results]
    D --> E2[Plot Holidays]
    D --> E3[Plot Temperature]
    D --> E4[Plot Sales]
    D --> E5[Plot Stock]
    D --> E6[Plot Customers]
    
    F[plot_functions] --> G1[Configure Axes]
    G1 --> H1[Set Labels]
    H1 --> I1[Add Legend]
    
    J[plot_stock] --> K1[Stack Colors]
    J --> K2[Stack Sizes]
```

Each module's workflow shows its main functions and their interactions. The diagrams use:
- Process nodes for functions
- Decision nodes for conditional logic
- Arrows to show data/control flow