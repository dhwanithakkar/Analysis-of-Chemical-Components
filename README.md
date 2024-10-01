# Analysis of Chemical components

## Problem Statement

The process of selecting new cosmetic products can be both daunting and anxiety inducing, particularly for individuals who experience skin sensitivities or reactions to 
unfamiliar items. The fear of adverse reactions to new products often complicates the 
decision-making process. Despite the availability of ingredient information on product 
labels, the technical complexity of these lists often leaves consumers feeling 
overwhelmed and uncertain. 

This project report addresses these challenges by proposing the use of data science to 
create a content-based recommendation system aimed at predicting which cosmetic 
products may be suitable for individual users based on their specific needs.

## Dataset

We focus on processing the ingredient lists of 1,472 cosmetics from Sephora. Our data encompasses six product categories featuring various brands.
1) moisturizers
2) cleansers
3) face masks
4) eye creams
5) treatments
6) sun protection

Furthermore, we recognize five different skin types: 
1) combination
2) dry
3) normal
4) oily
5) sensitive

For each cosmetic product that matches the skin type, we have 1 listed in that skin type section.
We have a detailed ingredient list for each product and also their prices, rank.



Below is a snapshot of the dataset for better understanding.

![7](https://github.com/user-attachments/assets/f03c8cda-15f7-4982-873f-29d5a88065ed)



### Steps followed 

Data Cleaning and Processing
- Step 1 : Skim the file before attempting to load it into memory: this will give you more insight into what columns are required and which ones can be discarded.
- Step 2 : Import all the necessary libraries and load the dataset into Jupyter Nootbook, dataset is a CSV file.
- Step 3 : In this project we will focus on moisturizers for those with dry skin. Filter the dataset to focus specifically on moisturizers suitable for dry skin.
- Step 4 : Reset index 

![1](https://github.com/user-attachments/assets/07768f01-5fad-41e3-ba50-c5bd454797c9)


Tokenization/Bag of Words and Creating Dictionary
- Step 4 : Tokenize ingredient lists to prepare data for analysis. We will break down the ingredient lists into individual tokens.
- Step 5 : After splitting them into tokens, we'll make a binary bag of words. Then we will create a dictionary with the tokens, ingredient_idx, which will have the following format:

{ "ingredient": index value, … }

This consists of 2231 ingredients in total.

![2](https://github.com/user-attachments/assets/aac8ea41-9f9b-4219-b0a0-17ccb6510a87)


Initializing Document-Term Matrix (DTM):

- Step 6 : Here each cosmetic product will correspond to a document, and each chemical composition will correspond to a term. This means we can think of the matrix as a “cosmetic-ingredient” matrix. 
- Step 7 : To create this matrix, we'll first make an empty matrix filled with zeros. The length of the matrix is the total number of cosmetic products in the data. The width of the matrix is the total number of ingredients. 
- Step 8 : Before we can fill the matrix, we create a function to count the tokens (i.e., an ingredients list) for each row. Our end goal is to fill the matrix with 1 or 0: if an ingredient is in a cosmetic, the value is 1. If not, it remains 0. We will name this function 'oh_encoder'.

![3](https://github.com/user-attachments/assets/7043cb82-49ea-4d77-9d4d-a6d3a0cf0cb6)

![4](https://github.com/user-attachments/assets/61ee5fab-5aba-49dc-9490-bdbdc9af45fb)

    
Dimension reduction with t-SNE and plotting with Bokeh:

T-distributed Stochastic Neighbor Embedding (t-SNE) is a nonlinear dimensionality reduction technique that is well-suited for embedding high-dimensional data for visualization in a low-dimensional space of two or three dimensions. 

- Step 9 :  The dimensions of the existing matrix is (190, 2231), which means there are 2231 features in our data. For visualization, we should downsize this into two dimensions. We'll use t-SNE for reducing the dimension of the data here.

- Step 10 :  With the t-SNE values, we can plot all our items on the coordinate plane. 
- Step 11 : Add a hover tool that allows to check the information of each item whenever the cursor is directly over it.
- Step 12 : We'll add tooltips with each product's name, brand, price, and rank (i.e., rating).

![5](https://github.com/user-attachments/assets/7897b269-ee7e-4ba4-8117-fc37fb05a36b)


Each point on the plot represents a different cosmetic item, with the spacing 
between the points reflecting their similarities in composition. Items that are 
positioned close to one another indicate that they share similar characteristics or 
ingredients, while those that are farther apart suggest greater differences in their 
formulations. This visualization enables users to compare various cosmetic items 
intuitively, making it accessible even for those without a background in chemistry. 
By analyzing the proximity of the points, one can quickly identify which products 
may have comparable qualities, facilitating informed decision-making in product 
selection.

We can easily compare both the products in terms of its price, rank and ingredients.


**EXAMPLE 1:**
‘Color Control Cushion Compact Broad-Spectrum SPF 50+’ and ‘BB Cushion 
Hydra Radiance SPF 50’. For instance, if we determine that the product from 
Laneige isn’t suitable for our skin type, the plot will also suggest that the ‘Color 
Control Cushion Compact Broad-Spectrum SPF 50+’ from Amorepacific could be 
a similarly poor option, given that it shares almost the same ingredient 
composition. This insight allows us to make more informed decisions about 
potential products to avoid.
![6](https://github.com/user-attachments/assets/b66b5b1e-ce35-4258-9246-29b09154700a)

Moreover, if we are interested in delving deeper into the specifics of each 
ingredient, we have the capability to print out a detailed list of the ingredients for 
any product we choose.
![8](https://github.com/user-attachments/assets/9b5f5a59-17a0-4222-9545-b70fd6032f00)

**EXAMPLE 2:**
Let’s take a closer look at a few cosmetic products, all of which are represented at 
the same point on the scatter plot. This alignment indicates that these products 
share identical ingredient compositions. If an individual wants to maintain the effectiveness of their skincare routine without the hefty price tag, they could consider opting for more 
economical alternatives like 'Hope in a Jar' or 'Miraculous Anti-Aging Miracle 
Worker,' both offered by Philosophy. These alternatives not only provide a similar 
formulation but also deliver comparable results at a fraction of the cost.

![9](https://github.com/user-attachments/assets/374236e4-72e4-4bd2-887e-b03743543d2c)
