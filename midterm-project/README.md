# Exploratory Data Analysis Project - Manufacturing Industry Database

The dataset for this project is located [here](Manufacturing_Industry_Database.csv) and the detailed explanations of the variables in the dataset can be found [here](./mfc_desc.md). The data set is the NBER-CES Manufacturing Industry Database, containing the annual data from the United States manufacturing sector for the period from 1958 to 2018. The data set page provides all the information needed to become familiar with the variables and how they were collected or calculated.

Your goal in this project is to use this data set and develop a Python notebook, containing the codes and texts, focused on exploratory data analysis. The main goal should be to perform an exploratory data analysis with all the steps required. 

## Important: Integrated Analysis and Narrative Development

**The tasks listed below should NOT be done as separate, disconnected sections.** Instead, think of your analysis as telling a story or developing a narrative about the US manufacturing sector. Use these tasks as tools to explore questions and build your narrative. For example:

- You might clean a subset of the data, perform grouping and statistical analysis, then use data visualization and correlation analysis together to explore a specific question or theme.
- Then, you might select another subset of variables, clean them, and use a combination of these tools to develop another part of your narrative.
- You could perform grouping first, then use those grouped results for correlation analysis and/or data visualization.

**Focus on the analysis and the "story" you are trying to tell** rather than treating each task as a checklist item. The goal is to create an integrated, coherent exploration of the data that uses these techniques in combination to answer interesting questions about manufacturing trends in the US.

## Project Tasks

Following is a list of tasks that you should incorporate into your analysis and their corresponding weights in the project grade:

- **Data Cleaning & Handling Missing Data (20 points):**  
  **This project is iterative in nature.** The complete dataset contains many columns and there are likely many missing values throughout the entire dataset. You are **NOT** expected to clean the entire dataset at once. Instead, you should explore the dataset first, identify the specific columns that are relevant to each part of your analysis, and then focus your data cleaning efforts on only those subsets of columns. **Important: The subset of columns you select may differ for different analyses.** For example, you might need to select and clean one set of columns for your correlation analysis, and a different set of columns for your data visualization tasks. Similarly, your grouping analysis might require yet another subset of variables. **This means you will likely perform data cleaning and missing value handling multiple times throughout your notebook, each time focusing on the specific variables needed for that particular analysis.** This iterative approach allows you to focus on meaningful analysis rather than attempting to clean an entire large dataset upfront. For each subset of data you work with, make sure there are no missing values in your chosen variables, or handle them appropriately. Further, ensure that everything is in the correct format. Removing all the rows with missing values with no investigation is not a proper way of handling missing data.

- **Descriptive Statistics (10 points):**  
  Calculate and report the basic statistics for the variables of your interests. Remember, every statistical calculation and reported value needs to be explained in text cells. If you are calculating the statistics for specific variables, explain what they are representing and what they tell us about the data.

- **Data Visualisation (25 points):**  
  Use data visualization techniques you learned in the course to investigate the various aspects of the data. Look for interesting relationships and/or plots that can convey your messages or help you investigate the answer to a possible question you might have and think the data can help you to answer. Using graphs and plots, you should be communicating something specific maybe about a trend or some type of relationship between variables. The plots should not be the goal. Use them to make a point or investigate a possible question in mind. All graphs should be properly labeled, properly sized, and sufficiently explained if they are representing a special trend.

- **Grouping (10 points):**  
  Use grouping to look at various aspects of the data. For instance, use grouping as a tool in combination with other tools, if you can, to look at various industries, years, or employment numbers based on other variables in the data set.

- **Correlation Analysis (10 points):**  
  Perform sets of correlation analysis between different variables in the dataset. You might need to combine grouping and correlation analysis to look at a specific aspect of the data. Remember to clearly explain the outcome of your correlation analysis.

- **Insights and Interpretations (15 points):**  
  Every correlation analysis, data visualization, and grouping should come with some explanations and possible insights about what to make of the results and how can it give us some information about the status of manufacturing in the US.

- **Overall Quality of the Notebook and Analysis (10 points):**  
  Make sure the notebook is well organized. It has a title, sections, and subsections. Make sure that text cells and code cells are logically ordered and organized, and the explanations and comments are clear.


**Remember**, you are doing exploratory data analysis, so explore and analyze the data! Try to ask questions and use the data to answer those questions using the tools and methods you have learned. Show your work step-by-step with comments in your code lines and texts between the code cells in the notebook environment. One possible option to find some interesting information from this data is to look at different trends and explore their possible relations with historical events. Your submission should be a Python notebook with all of the texts, codes, comments, and results.

## Submission

Your final submission will be a Python notebook (.ipynb file). When creating your notebook:

- Make sure the notebook is well-organized and it includes the codes and the outputs.
- Make sure your name is in the notebook, preferably as a text in your notebook.
- Make sure you do not print very large chunks of data and variables with so much data. They just make your code unclean and hard to understand. They also mostly serve no purpose.
- Use proper variable names that help anyone reading your code understand what each variable might be representing.
- Once you are done writing your code, your notebook most probably includes code cells that you used for experimenting with some functions or testing some code lines. Organize your notebook and clean it up. Remove those unneeded sections/cells, restart the kernel, and then run the notebook from the beginning. Then submit the notebook with the results.
- Keep the length of code lines in your code short. Break the long lines into multiple lines.