**What are data visualizations and why are they important?**

Data visualizations are visual representations of information and data. They are the fastest way to condense data and share information with stakeholders.

**What are the different types of data visualization goals?**

- **Explore:** As you're initially exploring and analyzing your data, you’ll create data visualizations to better understand what is happening in the data. These visualizations are part of your discovery process and are used to make sense of the large quantity of numbers and text found within datasets.
    
- **Explain:** Once you've made discoveries in your data, you’ll want to use data visualizations to help explain your insights to others. These data visualizations can help make large, complicated, or abstract insights easier to understand for your stakeholders. You should almost always use data visualizations to explain your insights.
    
- **Exhibit:** This is the type of data visualization that takes on more of an art form and does not always adopt all the general data viz best practices. Many times with this type of data viz, the design is prioritized over the clarity/simplicity around communicating insights.
    

**What is Tableau Public?**

Tableau Public is a free platform that allows you to create and share data visualizations. It is very similar to Tableau Desktop, with the main difference being cost and privacy. Tableau Public is free, but all work that is performed is saved to the Tableau community page.

**How does Tableau compare with Excel?**

The primary purpose of Tableau is for exploring data and creating/sharing data visualizations. While it has the ability to perform other tasks, such as manipulating data, if a substantial amount of work needs to be done before creating data visualizations, then other tools, such as Excel, should be used. Spreadsheet software (e.g., Excel) surpasses Tableau’s capabilities when it comes to things tasks such as data wrangling and multi-layered calculations.

**What is typically involved in preparing data in Tableau?**

- Renaming fields
    
- Hiding fields
    
- Pivoting fields
    
- Updating data types
    
- Splitting fields
    

**What are some of the common types of dirty data?**

- **Invalid values:** E.g., negative values in an _Age_ field
    
- **Incorrect values:** E.g., outdated information
    
- **Inconsistent data:** E.g., “Monday,” “monday,” “Mon,” and “M” in a _Day of Week_ field
    
- **Inconsistent data types:** E.g., “8” (numerical) and “eight” (text) listed in an _Hours Slept_ field
    
- **Duplicate values:** E.g., multiple votes from the same person
    
- **Missing/Incomplete values:** E.g., first names in a _Full Name_ field
    

**How are data fields classified in Tableau?**

Fields are automatically classified as **discrete** or **continuous**. 

- **Discrete:** Individually separate and distinct. When a discrete field is plotted, there are gaps between each point of data — signifying that each point of data is separate from the whole. Discrete fields are blue.
    
- **Continuous**: Forming an unbroken whole; without interruption. When a continuous field is plotted on a line graph, the line is unbroken. Continuous fields are green.
    

**What are the different data types in Tableau?**

- **String (text):** Can include letters, symbols, and numbers
    
- **Date:** E.g., 2/11/2005
    
- **Date & Time:** E.g., 2/11/2005 11:45:00 AM
    
- **Numerical:** Numbers only, with or without a decimal
    
- **Boolean:** Values that are either "True" or "False"
    
- **Geographic:** Countries, zip codes, etc.
    

**Does Tableau automatically assign a data type to each field?**

Yes, but each field should be carefully checked since data types can be incorrectly assigned. For example, if you have a field of zip codes, Tableau may process that field as a _numerical_ data type when it should instead be _geographic_.

**What is the difference between a data source and a Tableau data source?**

A data source is the location and container of the data you choose to access when you use Tableau. This could be a spreadsheet in Excel/Google Sheets, a text file, or a PDF, among other file types. Data sources can hold multiple tables or sheets of data.

A _Tableau_ data source is the link between Tableau and the data. The Tableau data source contains any edits, connections, joins, and other manipulations you have made to the data source _in_ Tableau.

In the data source page of Tableau, the data source information can be found in the left pane and the Tableau data source is found on the right side, within the canvas, metadata grid, and data grid.

**What is the difference between joins, unions, and relationships?**

- A join is a horizontal connection between two or more tables. When joining tables, there must be at least one common field with shared values between the tables.
    
- A union is a vertical connection between two tables. For a union to happen properly, the fields within both tables must match.
    
- A relationship does not physically connect tables, unlike joins and unions. Instead, Tableau describes a relationship as a "contract" between tables. They are similar to joins, but Tableau will automatically select the join type based on the fields used in the visualization.
    

**What is the difference between cross-database joins and data blends?**

- Cross-database joins connect multiple data sources within a single Tableau data source.
    
- Data blends combine multiple Tableau data sources.
    
- The major difference is _when_ aggregation occurs. Data blends aggregate _before_ combining, whereas joins combine and _then_ aggregate.