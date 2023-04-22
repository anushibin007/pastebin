# SPA Assignment 1 Guide

!!! warning

	All the steps mentioned here are based on how I approached the assignment. I would anyone who is reading this to properly read the instructions given by the faculty and discuss the same in the group to see if my approach is in line with what the professor has given. THis guide was written to primarily help those that have no idea about the Databrick, etc.

## Subject & Subject Code

Stream Processing and Analytics (S2-22 SSZG556)

## Questions

Question Summary: http://taxila-aws.bits-pilani.ac.in/mod/forum/discuss.php?d=57989

- Part A - 10 M
	- Analyzing and evaluating Streaming Framework / Platform
- Part B - 25 M
	- Using given problem statement and dataset, you need to use databricks platform and run ML experiements using Pyspark ML library and showcase

## Video Guide

Check this video for a guide on how to solve the the assignment: https://youtu.be/cJ-rLnizaFw

Feel free to comment in the video if you have any doubts. Or contact me in the WhatsApp group. I will try to explain as much as I know.

## Links & Important Code Blocks

### Links

- Binary Classification Databricks Sample - https://docs.databricks.com/_extras/notebooks/source/binary-classification.html
- DataBricks - https://community.cloud.databricks.com/
- G7 Demo on Databricks - https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/6374943227371516/1151767014322707/8298046428141319/latest.html

### Code Blocks

``` python title="Reading Data from DBFS"
dataset = spark.read.format("csv").schema(schema).option("header", "true").load("/FileStore/data.csv")
```

## Related

- [[Assignments Post Mid Sem]]