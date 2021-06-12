---
title: "Workflow Comparison"
output:
  pdf_document: default
  html_notebook: default
---
# Load Libraries
```{r}
library(ShortRead)
library(qckitfastq)
library(ggplot2)
library(ggpubr)
library(dplyr)
library(ggthemes)
library(tidyverse)
```

# Load Data
![[Section_5.4_ Cumulative_Coverage_Change.jpg]]
### Set paths
```{r}
graph_path=("C:/Users/voro/OneDrive/9_Studium/MasterThesis/R_scripts/Graphs")
EPI2ME_QC_D4_Path=("EPI2ME_Data_Reports/basecalling_1d_barcode-v1_D4.csv")
EPI2ME_QC_D5_Path=("EPI2ME_Data_Reports/basecalling_1d_barcode-v1_D5.csv")
EPI2ME_Tax_D4_Path=("EPI2ME_Data_Reports/classification_16s_barcode-v1_D4.csv")
EPI2ME_Tax_D5_Path=("EPI2ME_Data_Reports/classification_16s_barcode-v1_D5.csv")
Demultiplexing_qcat_D4_Path=("Workflow_Data_Reports/D4/demultiplexing_qcat_tax_wf_comp_01/")
Demultiplexing_qcat_D4_List=list.files(Demultiplexing_qcat_D4_Path,pattern = ".fastq")
Demultiplexing_qcat_D5_Path=("Workflow_Data_Reports/D5/demultiplexing_qcat_tax_wf_comp_01/")
Demultiplexing_qcat_D5_List=list.files(Demultiplexing_qcat_D5_Path,pattern = ".fastq")
Filter_Nanofilt_D4_Path=("Workflow_Data_Reports/D4/filter_trim_nanofilt_tax_wf_comp_01/")
Filter_Nanofilt_D4_List=list.files(Filter_Nanofilt_D4_Path,pattern = ".fastq")
Filter_Nanofilt_D5_Path=("Workflow_Data_Reports/D5/filter_trim_nanofilt_tax_wf_comp_01/")
Filter_Nanofilt_D5_List=list.files(Filter_Nanofilt_D5_Path,pattern = ".fastq")
Kraken2_Classification_D4_Path=("Workflow_Data_Reports/D4/classification_kraken2_nanofilt_tax_wf_comp_01/")
Kraken2_Classification_D5_Path=("Workflow_Data_Reports/D5/classification_kraken2_nanofilt_tax_wf_comp_01/")
Kraken2_Report_D4_Path=("Workflow_Data_Reports/D4/r_kraken2_report_nanofilt_tax_wf_comp_01/")
Kraken2_Report_D5_Path=("Workflow_Data_Reports/D5/r_kraken2_report_nanofilt_tax_wf_comp_01/")

graph_path=("Graphs/")
```
### Load EPI2ME files
```{r,message=FALSE}
library(readr)
EPI2ME_QC_D4 <- read_csv(EPI2ME_QC_D4_Path)
EPI2ME_QC_D5 <- read_csv(EPI2ME_QC_D5_Path)
EPI2ME_Tax_D4 <- read_csv(EPI2ME_Tax_D4_Path)
EPI2ME_Tax_D5 <- read_csv(EPI2ME_Tax_D5_Path)
```

# Comparison EPI2ME Fastq 16S vs. Kraken2 Workflow
### Get total read amounts
#### Use of the ShortRead library (works)
The total amount of reads for D4 before and after filtering with POND Workflow
```{r}
read_count_df=countFastq(Demultiplexing_qcat_D4_Path)
sum(read_count_df$records)
read_count_df=countFastq(Filter_Nanofilt_D4_Path)
sum(read_count_df$records)
```
The total amount of reads for D5 before and after filtering with POND Workflow
```{r}
read_count_df=countFastq(Demultiplexing_qcat_D5_Path)
sum(read_count_df$records)
read_count_df=countFastq(Filter_Nanofilt_D5_Path)
sum(read_count_df$records)
```
### Plot Read quality
#### NanoR (not working)
```{r}
# NanoR need to have summary file and others

# Glist<-NanoPrepareG(DataFastq=Demultiplexing_qcat_D4_Path)
# Passed FASTQ: 25
# Error in file.path(DataSummary) : 
#   argument "DataSummary" is missing, with no default
```
#### MinIONQC (not working)
```{r}
# MinIONQC also needs summary file
```
#### qckitfastq (works)
Plot the read quality of the D4 before and after filtering by length and quality
```{r,fig.width = 8, fig.height = 6}
# First the bifile is create with the bash command("cats *.fastq > bigfile.fastq)
# Load the aggregated fastq files (bigfile)
curr_fastq_path=paste(Demultiplexing_qcat_D4_Path,"bigfile/bigfile.fastq",sep = "")
quality_dataframe_1 <- per_read_quality(curr_fastq_path)
curr_fastq_path=paste(Filter_Nanofilt_D4_Path,"/bigfile/bigfile.fastq",sep = "")
quality_dataframe_2 <- per_read_quality(curr_fastq_path)

# Put the filtered and unfiltered dataframes into one
quality_dataframe_1$read="unfiltered"
quality_dataframe_2$read="filtered"
prq=rbind(quality_dataframe_1,quality_dataframe_2)
prq$read=as.factor(prq$read)
colnames(prq)=c("filter_criteria","sequence_mean")

# Define names for the plot
title="Read quality of D4"
xlabel="Mean quality score [-]"
ylabel="Read frequency [-]"
legendlabel="Filter criteria"
filename="Section_5.3_ Read_Quality_D4.jpg"

# Define the data and order of the color filling
q=ggplot(prq,aes(x=sequence_mean,  fill = reorder(filter_criteria, desc(filter_criteria))))+
  # Define it to be a histogram plot with specific binwidth
  geom_histogram(position="identity",binwidth=0.1)+
  # Set a theme
  theme_tufte() + 
  # Define formatting and load defined texts
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.y = element_text(size=14,margin = margin(t = 0, r = 20, b = 0, l = 0)),
        axis.title.x = element_text(size=14,margin = margin(t = 20, r = 0, b = 0, l = 0)))+
  xlab(xlabel) +
  ylab(ylabel) +
  guides(fill = guide_legend(title = legendlabel))
# Set a color scheme
q=q+scale_fill_manual(values=c("#d1495b","#00798c"))
# Annotate the title
q=annotate_figure(q,top = text_grob(title, color = "black", face = "bold", size = 16))
# Save and print the plot
ggsave(plot = q, width = 8, height = 6, dpi = 300, filename = filename, path = graph_path)
```
Show Graph
```{r}
q
```


Plot the read quality of the D5 before and after filtering by length and quality
```{r,fig.width = 8, fig.height = 6}
# First the bifile is create with the bash command("cats *.fastq > bigfile.fastq)
# Load the aggregated fastq files (bigfile)
curr_fastq_path=paste(Demultiplexing_qcat_D5_Path,"bigfile/bigfile.fastq",sep = "")
quality_dataframe_1 <- per_read_quality(curr_fastq_path)
curr_fastq_path=paste(Filter_Nanofilt_D5_Path,"/bigfile/bigfile.fastq",sep = "")
quality_dataframe_2 <- per_read_quality(curr_fastq_path)

# Put the filtered and unfiltered dataframes into one
quality_dataframe_1$read="unfiltered"
quality_dataframe_2$read="filtered"
prq=rbind(quality_dataframe_1,quality_dataframe_2)
prq$read=as.factor(prq$read)
colnames(prq)=c("filter_criteria","sequence_mean")

# Define names for the plot
title="Read quality of D5"
xlabel="Mean quality score [-]"
ylabel="Read frequency [-]"
legendlabel="Filter criteria"
filename="Section_5.3_ Read_Quality_D5.jpg"

# Define the data and order of the color filling
q=ggplot(prq,aes(x=sequence_mean,  fill = reorder(filter_criteria, desc(filter_criteria))))+
  # Define it to be a histogram plot with specific binwidth
  geom_histogram(position="identity",binwidth=0.1)+
  # Set a theme
  theme_tufte() + 
  # Define formatting and load defined texts
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.y = element_text(size=14,margin = margin(t = 0, r = 20, b = 0, l = 0)),

        axis.title.x = element_text(size=14,margin = margin(t = 20, r = 0, b = 0, l = 0)))+
  xlab(xlabel) +
  ylab(ylabel) +
  guides(fill = guide_legend(title = legendlabel))
# Set a color scheme
q=q+scale_fill_manual(values=c("#d1495b","#00798c"))
# Annotate the title
q=annotate_figure(q,top = text_grob(title, color = "black", face = "bold", size = 16))
# Save and print the plot
ggsave(plot = q, width = 8, height = 6, dpi = 300, filename = filename, path = graph_path)
```
Show Graph
```{r}
q
```
### Plot Read length distribution
Read Length Distribution for D4
```{r,fig.width = 8, fig.height = 6}
# for loading single fastq file it is not working
# fseq <- seqTools::fastqq(fastq_path)

# Create a dataframe to which the read length counts can be added
store_dataframe_1=data.frame( matrix(0, ncol = 2, nrow = 10000))
# Read lengths up 10000 can be stored
colnames(store_dataframe_1)=c("read_length","num_reads")
store_dataframe_1$read_length=seq(1,10000)

for (i in Demultiplexing_qcat_D4_List){
  fastq_path=paste(Demultiplexing_qcat_D4_Path,i,sep = "")
  # print(fastq_path)
  sink("nul")
  fseq <- seqTools::fastqq(fastq_path)
  sink()
  read_len <- read_length(fseq)
  # print(sum(read_len$num_reads))
  
  zero=numeric(abs(nrow(store_dataframe_1)-nrow(read_len)))
  col_add=c(read_len$num_reads,zero)
  store_dataframe_1$num_reads=store_dataframe_1$num_read+col_add
}
# Create a dataframe to which the read length counts can be added
store_dataframe_2=data.frame( matrix(0, ncol = 2, nrow = 10000))
# Read lengths up 10000 can be stored
colnames(store_dataframe_2)=c("read_length","num_reads")
store_dataframe_2$read_length=seq(1,10000)

for (i in Filter_Nanofilt_D4_List){
  fastq_path=paste(Filter_Nanofilt_D4_Path,i,sep = "")
  # print(fastq_path)
  sink("nul")
  fseq <- seqTools::fastqq(fastq_path)
  sink()
  read_len <- read_length(fseq)
  # print(sum(read_len$num_reads))
  
  zero=numeric(abs(nrow(store_dataframe_2)-nrow(read_len)))
  col_add=c(read_len$num_reads,zero)
  store_dataframe_2$num_reads=store_dataframe_2$num_read+col_add
}


# Not all of the reads were loaded, print 
read_count_df=countFastq(Demultiplexing_qcat_D4_Path)
sum(read_count_df$records)
sum(store_dataframe_1$num_reads)
read_count_df=countFastq(Filter_Nanofilt_D4_Path)
sum(read_count_df$records)
sum(store_dataframe_2$num_reads)

# Create filter criteria and store them in one dataframe
store_dataframe_1$filter_criteria="unfiltered"
store_dataframe_2$filter_criteria="filtered"
store_dataframe=rbind(store_dataframe_1,store_dataframe_2)

title="Readlength_Distribution of D4"
xlabel="Read length [bp]"
ylabel="Read frequency [-]"
legendlabel="Filter criteria"
filename="Section_5.3_Read_Length_Distribution_D4.jpg"

q=ggplot(store_dataframe, aes(y=num_reads, x=read_length,  fill = reorder(filter_criteria, desc(filter_criteria)))) + 
  geom_bar(stat = 'identity')+
  xlim(0, 2500)+
  theme_tufte() +
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.y = element_text(size=14,margin = margin(t = 0, r = 20, b = 0, l = 0)),
        axis.title.x = element_text(size=14,margin = margin(t = 20, r = 0, b = 0, l = 0)))+
  xlab(xlabel) +
  ylab(ylabel) +
  guides(fill = guide_legend(title = legendlabel))
q=q+scale_fill_manual(values=c("#d1495b","#00798c"))
q=annotate_figure(q,top = text_grob(title, color = "black", face = "bold", size = 16))
ggsave(plot = q, width = 8, height = 6, dpi = 300, filename = filename, path = graph_path)
```
Show Graph
```{r}
q
```
Read Length Distribution for D5
```{r,fig.width = 8, fig.height = 6}
# for loading single fastq file it is not working
# fseq <- seqTools::fastqq(fastq_path)

# Create a dataframe to which the read length counts can be added
store_dataframe_1=data.frame( matrix(0, ncol = 2, nrow = 10000))
# Read lengths up 10000 can be stored
colnames(store_dataframe_1)=c("read_length","num_reads")
store_dataframe_1$read_length=seq(1,10000)

for (i in Demultiplexing_qcat_D5_List){
  fastq_path=paste(Demultiplexing_qcat_D4_Path,i,sep = "")
  # print(fastq_path)
  sink("nul")
  fseq <- seqTools::fastqq(fastq_path)
  sink()
  read_len <- read_length(fseq)
  # print(sum(read_len$num_reads))
  
  zero=numeric(abs(nrow(store_dataframe_1)-nrow(read_len)))
  col_add=c(read_len$num_reads,zero)
  store_dataframe_1$num_reads=store_dataframe_1$num_read+col_add
}
# Create a dataframe to which the read length counts can be added
store_dataframe_2=data.frame( matrix(0, ncol = 2, nrow = 10000))
# Read lengths up 10000 can be stored
colnames(store_dataframe_2)=c("read_length","num_reads")
store_dataframe_2$read_length=seq(1,10000)

for (i in Filter_Nanofilt_D5_List){
  fastq_path=paste(Filter_Nanofilt_D5_Path,i,sep = "")
  # print(fastq_path)
  sink("nul")
  fseq <- seqTools::fastqq(fastq_path)
  sink()
  read_len <- read_length(fseq)
  # print(sum(read_len$num_reads))
  
  zero=numeric(abs(nrow(store_dataframe_2)-nrow(read_len)))
  col_add=c(read_len$num_reads,zero)
  store_dataframe_2$num_reads=store_dataframe_2$num_read+col_add
}


# Not all of the reads were loaded, print 
read_count_df=countFastq(Demultiplexing_qcat_D5_Path)
sum(read_count_df$records)
sum(store_dataframe_1$num_reads)
read_count_df=countFastq(Filter_Nanofilt_D5_Path)
sum(read_count_df$records)
sum(store_dataframe_2$num_reads)

# Create filter criteria and store them in one dataframe
store_dataframe_1$filter_criteria="unfiltered"
store_dataframe_2$filter_criteria="filtered"
store_dataframe=rbind(store_dataframe_1,store_dataframe_2)

title="Readlength_Distribution of D5"
xlabel="Read length [bp]"
ylabel="Read frequency [-]"
legendlabel="Filter criteria"
filename="Section_5.3_Read_Length_Distribution_D5.jpg"

q=ggplot(store_dataframe, aes(y=num_reads, x=read_length,  fill = reorder(filter_criteria, desc(filter_criteria)))) + 
  geom_bar(stat = 'identity')+
  xlim(0, 2500)+
  theme_tufte() +
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.y = element_text(size=14,margin = margin(t = 0, r = 20, b = 0, l = 0)),
        axis.title.x = element_text(size=14,margin = margin(t = 20, r = 0, b = 0, l = 0)))+
  xlab(xlabel) +
  ylab(ylabel) +
  guides(fill = guide_legend(title = legendlabel))
q=q+scale_fill_manual(values=c("#d1495b","#00798c"))
q=annotate_figure(q,top = text_grob(title, color = "black", face = "bold", size = 16))
ggsave(plot = q, width = 8, height = 6, dpi = 300, filename = filename, path = graph_path)
```
Show Graph
```{r}
q
```
### Compare Barcode Read Counts
Compare Read Counts of EPI2ME vs Workflow for D4
```{r,fig.width = 10, fig.height = 5}

# EPI2ME Barcode Counts
EPI2ME_QC_D4$barcode[is.na(EPI2ME_QC_D4$barcode)] <- "none"
EPI2ME_QC_D4_counts=as.data.frame(table(EPI2ME_QC_D4$barcode))
EPI2ME_QC_D4_counts$workflow="EPI2ME"
colnames(EPI2ME_QC_D4_counts)=c("barcode","counts","workflow")


# Workflow Barcode Counts
Workflow_QC_D4_counts=as.data.frame(unique(Demultiplexing_qcat_D4_List))
colnames(Workflow_QC_D4_counts)="barcode"
Workflow_QC_D4_counts$counts=0
for (i in Workflow_QC_D4_counts$barcode){
  fastq_path=paste(Demultiplexing_qcat_D4_Path,i,sep = "")
  current_count=countFastq(fastq_path)
  # print(current_count$records)
  Workflow_QC_D4_counts$counts[which(Workflow_QC_D4_counts$barcode==i)]=current_count$records
}
Workflow_QC_D4_counts$workflow="POND"
Workflow_QC_D4_counts$barcode=str_remove(Workflow_QC_D4_counts$barcode, ".fastq")

#Create one dataframe
barcode_comp=rbind(EPI2ME_QC_D4_counts,Workflow_QC_D4_counts)

title="Barcode read frequency of D4"
xlabel="Barcode [-]"
ylabel="Read frequency [-]"
legendlabel="Type of Workflow"
filename="Section_5.3_Barcode_Read_Frequency_D4.jpg"

q=ggplot(data = barcode_comp, aes(x = barcode, y = counts, fill = workflow),) +
geom_bar(position = position_dodge(width = 0.8), stat = "identity", width = 0.75)+
   geom_text(aes(label=counts), position = position_dodge(width = 1),size=3,hjust=-0.1,vjust=0.2,angle=90)+
  ylim(0, 30000)+
  theme_tufte() +
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.y = element_text(size=14,margin = margin(t = 0, r = 20, b = 0, l = 0)),
        axis.title.x = element_text(size=14,margin = margin(t = 20, r = 0, b = 0, l = 0)),
        axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))+
  xlab(xlabel) +
  ylab(ylabel) +
  guides(fill = guide_legend(title = legendlabel))
q=q + scale_fill_manual(values=c("#d1495b","#00798c"))
q=annotate_figure(q,top = text_grob(title, color = "black", face = "bold", size = 16))
ggsave(plot = q, width = 10, height = 5, dpi = 300, filename = filename, path = graph_path)
```
Show Graph
```{r}
q
```
Compare Read Counts of EPI2ME vs Workflow for D5
```{r,fig.width = 10, fig.height = 5}
# EPI2ME Barcode Counts
EPI2ME_QC_D5$barcode[is.na(EPI2ME_QC_D5$barcode)] <- "none"
EPI2ME_QC_D5_counts=as.data.frame(table(EPI2ME_QC_D5$barcode))
EPI2ME_QC_D5_counts$workflow="EPI2ME"
colnames(EPI2ME_QC_D5_counts)=c("barcode","counts","workflow")


# Workflow Barcode Counts
Workflow_QC_D5_counts=as.data.frame(unique(Demultiplexing_qcat_D5_List))
colnames(Workflow_QC_D5_counts)="barcode"
Workflow_QC_D5_counts$counts=0
for (i in Workflow_QC_D5_counts$barcode){
  fastq_path=paste(Demultiplexing_qcat_D5_Path,i,sep = "")
  current_count=countFastq(fastq_path)
  # print(current_count$records)
  Workflow_QC_D5_counts$counts[which(Workflow_QC_D5_counts$barcode==i)]=current_count$records
}
Workflow_QC_D5_counts$workflow="POND"
Workflow_QC_D5_counts$barcode=str_remove(Workflow_QC_D5_counts$barcode, ".fastq")

#Create one dataframe
barcode_comp=rbind(EPI2ME_QC_D5_counts,Workflow_QC_D5_counts)

title="Barcode read frequancy of D5"
xlabel="Barcode [-]"
ylabel="Read frequency [-]"
legendlabel="Type of Workflow"
filename="Section_5.3_Barcode_Read_Frequency_D5.jpg"

q=ggplot(data = barcode_comp, aes(x = barcode, y = counts, fill = workflow),) +
geom_bar(position = position_dodge(width = 0.8), stat = "identity", width = 0.75)+
   geom_text(aes(label=counts), position = position_dodge(width = 1),size=3,hjust=-0.1,vjust=0.2,angle=90)+
  ylim(0, 60000)+
  theme_tufte() +
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.y = element_text(size=14,margin = margin(t = 0, r = 20, b = 0, l = 0)),
        axis.title.x = element_text(size=14,margin = margin(t = 20, r = 0, b = 0, l = 0)),
        axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))+
  xlab(xlabel) +
  ylab(ylabel) +
  guides(fill = guide_legend(title = legendlabel))
q=q + scale_fill_manual(values=c("#d1495b","#00798c"))
q=annotate_figure(q,top = text_grob(title, color = "black", face = "bold", size = 16))
ggsave(plot = q, width = 10, height = 5, dpi = 300, filename = filename, path = graph_path)
```
Show Graph
```{r}
q
```
### Classification Comparison
The read classification success on the rank of species is plotted of EPI2ME against Workflow
```{r, fig.width = 8, fig.height = 6}
# Load the kraken2 report files for D4
filenames <- list.files(path=Kraken2_Report_D4_Path,pattern = "REPORT")
# Store the filenames in shortened form (BCXX)
T0_IDs <- substr(filenames,1,4)
# Create empty list
T0_df_list=list()
for (i in 1:length(filenames)){
  # Get the sample name of the barcode
  # sample_name=as.character(sample_id$sample_id[which(sample_id$barcode_t_0==substr(filenames[i],1,4))])
  sample_name=substr(filenames[i],1,4)
  # Check that the sample_name exitst
  if (length(sample_name)!=0){
    # Create the load path
    load_path=paste(Kraken2_Report_D4_Path,filenames[i], sep = "")
    # Store the df in the list
    df=read.csv(load_path, header=TRUE)
    # df=read_delim(load_path,"\t", escape_double = FALSE, col_names = FALSE,trim_ws = TRUE)
    # Add the df to the list with the corresponding sample name
    T0_df_list[[sample_name]]<- df
    # Print whats going on
    print(paste(substr(filenames[i],1,4),sample_name,sep = " --> "))
  }
}
# Put all of the barcode dataframes form the list into one dataframe
D4_Total_Kraken2_Report <- bind_rows(T0_df_list, .id = "column_label")
# Adapt colnames
colnames(D4_Total_Kraken2_Report)[1]<-"barcode"
colnames(D4_Total_Kraken2_Report)[2]<-"level"
#_______________________________________________________________________________

# Load the kraken2 report files for D5
filenames <- list.files(path=Kraken2_Report_D5_Path,pattern = "REPORT")
# Store the filenames in shortened form (BCXX)
T1_IDs <- substr(filenames,1,4)
# Create empty list
T1_df_list=list()
for (i in 1:length(filenames)){
  # Get the sample name of the barcode
  # sample_name=as.character(sample_id$sample_id[which(sample_id$barcode_t_0==substr(filenames[i],1,4))])
  sample_name=substr(filenames[i],1,4)
  # Check that the sample_name exitst
  if (length(sample_name)!=0){
    # Create the load path
    load_path=paste(Kraken2_Report_D5_Path,filenames[i], sep = "")
    # Store the df in the list
    df=read.csv(load_path, header=TRUE)
    # df=read_delim(load_path,"\t", escape_double = FALSE, col_names = FALSE,trim_ws = TRUE)
    # Add the df to the list with the corresponding sample name
    T1_df_list[[sample_name]]<- df
    # Print whats going on
    print(paste(substr(filenames[i],1,4),sample_name,sep = " --> "))
  }
}
# Put all of the barcode dataframes form the list into one dataframe
D5_Total_Kraken2_Report <- bind_rows(T1_df_list, .id = "column_label")
# Adapt colnames
colnames(D5_Total_Kraken2_Report)[1]<-"barcode"
colnames(D5_Total_Kraken2_Report)[2]<-"level"
#_______________________________________________________________________________

# EPI2ME Data D4
# Exchange NA with none
EPI2ME_Tax_D4$barcode[is.na(EPI2ME_Tax_D4$barcode)] <- "none"
# Subset the dataframe
df1=as.data.frame(table(EPI2ME_Tax_D4$exit_status,EPI2ME_Tax_D4$barcode))
# Remove the "Error" parameter
df1=df1[df1$Var1!="Error",]   
# Add Column with the name of the workflow and the Dataset
df1$workflow="EPI2ME_D4"
# Rename Columns
colnames(df1)=c("classification","barcode","readnum","workflow_type")
# Change column type
df1$classification=as.character(df1$classification)
# Harmonize dataset
df1$classification[which(df1$classification=="Classification successful")]<-"classified"
# Harmonize dataset
df1$classification[which(df1$classification=="Unclassified")]<-"unclassified"
# Change column type
df1$barcode=as.character(df1$barcode)
#_______________________________________________________________________________

# POND D4 Data
df2=data.frame()
for (i in unique(D4_Total_Kraken2_Report$barcode)){
  # Get the total read number for the current barcode
  total_read_num=D4_Total_Kraken2_Report$total_read_number[which(D4_Total_Kraken2_Report$barcode==i)][1]
  # Get the percentage amount of classifed reads at the species level
  species_rank_perc=D4_Total_Kraken2_Report$s_cov_perc[which(D4_Total_Kraken2_Report$barcode==i)][1]
  # Calculat the number of classified reads
  num_classified_reads=total_read_num*species_rank_perc/100
  # Calculat the number of unclassified reads
  num_unclassified_reads=total_read_num-total_read_num*species_rank_perc/100
  # Define column and store them in new dataframe
  c1=c("classified",i,num_classified_reads)
  c2=c("unclassified",i, num_unclassified_reads)
  df2=rbind(df2,c1)
  df2=rbind(df2,c2)
}
# Add Column with the name of the workflow and the Dataset
df2$workflow="POND_D4"
# Rename Columns
colnames(df2)=c("classification","barcode","readnum","workflow_type")
# Harmonize data type
df2$readnum=round(as.numeric(df2$readnum))

#_______________________________________________________________________________

# EPI2ME Data D5
EPI2ME_Tax_D5$barcode[is.na(EPI2ME_Tax_D5$barcode)] <- "none"
df3=as.data.frame(table(EPI2ME_Tax_D5$exit_status,EPI2ME_Tax_D5$barcode))
df3=df3[df3$Var1!="Error",]   
df3$workflow="EPI2ME_D5"
colnames(df3)=c("classification","barcode","readnum","workflow_type")
df3$classification=as.character(df3$classification)
df3$classification[which(df3$classification=="Classification successful")]<-"classified"
df3$classification[which(df3$classification=="Unclassified")]<-"unclassified"
df3$barcode=as.character(df3$barcode)
#_______________________________________________________________________________

# POND D5 Data
df4=data.frame()
for (i in unique(D5_Total_Kraken2_Report$barcode)){
  total_read_num=D5_Total_Kraken2_Report$total_read_number[which(D5_Total_Kraken2_Report$barcode==i)][1]
  species_rank_perc=D5_Total_Kraken2_Report$s_cov_perc[which(D5_Total_Kraken2_Report$barcode==i)][1]
  num_classified_reads=total_read_num*species_rank_perc/100
  num_unclassified_reads=total_read_num-total_read_num*species_rank_perc/100
  c1=c("classified",i,num_classified_reads)
  c2=c("unclassified",i, num_unclassified_reads)
  df4=rbind(df4,c1)
  df4=rbind(df4,c2)
}
df4$workflow="POND_D5"
colnames(df4)=c("classification","barcode","readnum","workflow_type")
df4$readnum=round(as.numeric(df4$readnum))
#_______________________________________________________________________________

# Combine all datasets for plotting
data=rbind(df1,df2,df3,df4)

#_______________________________________________________________________________

# Compute specific parameters

# Classification numbers
sum(data$readnum[which(data$workflow_type=="EPI2ME_D4" & data$classification=="classified")]) /
sum(data$readnum[which(data$workflow_type=="EPI2ME_D4")]) * 100

sum(data$readnum[which(data$workflow_type=="EPI2ME_D5" & data$classification=="classified")]) /
sum(data$readnum[which(data$workflow_type=="EPI2ME_D5")]) * 100

sum(data$readnum[which(data$workflow_type=="POND_D4" & data$classification=="classified")]) /
sum(data$readnum[which(data$workflow_type=="POND_D4")]) * 100

sum(data$readnum[which(data$workflow_type=="POND_D5" & data$classification=="classified")]) /
sum(data$readnum[which(data$workflow_type=="POND_D5")]) * 100

#_______________________________________________________________________________

title=paste("Species Level Classification Comparison")
xlabel="Workflow and Dataset [-]"
ylabel="Number of Reads [-]"
legendlabel="Classification"
filename="Section_5.3_Species_Level_Classification_Comparison.jpg"

q=ggplot(data, aes(x = workflow_type, y = readnum, fill=reorder(classification, desc(classification)))) + 
  geom_bar(stat = "identity", width=0.4)+
  theme_tufte() +
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.y = element_text(size=14,margin = margin(t = 0, r = 20, b = 0, l = 0)),
        axis.title.x = element_text(size=14,margin = margin(t = 20, r = 0, b = 0, l = 0)),
        axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))+
  xlab(xlabel) +
  ylab(ylabel) +
  guides(fill = guide_legend(title = legendlabel))
q=q + scale_fill_manual(values=c("#d1495b","#00798c"))
q=annotate_figure(q,top = text_grob(title, color = "black", face = "bold", size = 16))
ggsave(plot = q, width = 8, height = 6, dpi = 300, filename = filename, path = graph_path)
```
Show Graph
```{r}
q
```
### Species Abundance Comparison
The classified species is comapred based on its ambundance
- Abundance Graphs
- Pavian Graph
```{r}
Barcode = "BC01"
topx=10

BC_EPI2ME_Tax_D4=as.data.frame(table(EPI2ME_Tax_D4$species[which(EPI2ME_Tax_D4$barcode==Barcode)]))
colnames(BC_EPI2ME_Tax_D4)=c("species_name", "read_freq")
BC_EPI2ME_Tax_D4$workflow="EPI2ME_D4"

BC_EPI2ME_Tax_D5=as.data.frame(table(EPI2ME_Tax_D5$species[which(EPI2ME_Tax_D5$barcode==Barcode)]))
colnames(BC_EPI2ME_Tax_D5)=c("species_name", "read_freq")
BC_EPI2ME_Tax_D5$workflow="EPI2ME_D5"

load_path=paste(Kraken2_Classification_D4_Path, Barcode,".fastq_REPORT", sep = "")
BC_POND_Tax_D4=read_delim(load_path,"\t", escape_double = FALSE, col_names = FALSE, trim_ws = TRUE)
BC_POND_Tax_D4=BC_POND_Tax_D4[which(BC_POND_Tax_D4$X4=="S"),]
BC_POND_Tax_D4=as.data.frame(cbind(BC_POND_Tax_D4$X6, BC_POND_Tax_D4$X3))
colnames(BC_POND_Tax_D4)=c( "species_name","read_freq")
BC_POND_Tax_D4$workflow="POND_D4"
BC_POND_Tax_D4$read_freq=as.numeric(BC_POND_Tax_D4$read_freq)

load_path=paste(Kraken2_Classification_D5_Path, Barcode,".fastq_REPORT", sep = "")
BC_POND_Tax_D5=read_delim(load_path,"\t", escape_double = FALSE, col_names = FALSE, trim_ws = TRUE)
BC_POND_Tax_D5=BC_POND_Tax_D5[which(BC_POND_Tax_D5$X4=="S"),]
BC_POND_Tax_D5=as.data.frame(cbind(BC_POND_Tax_D5$X6, BC_POND_Tax_D5$X3))
colnames(BC_POND_Tax_D5)=c( "species_name","read_freq")
BC_POND_Tax_D5$workflow="POND_D5"
BC_POND_Tax_D5$read_freq=as.numeric(BC_POND_Tax_D5$read_freq)

# Create percentage Abundance
BC_EPI2ME_Tax_D4$read_freq=BC_EPI2ME_Tax_D4$read_freq/sum(BC_EPI2ME_Tax_D4$read_freq)*100 
BC_EPI2ME_Tax_D5$read_freq=BC_EPI2ME_Tax_D5$read_freq/sum(BC_EPI2ME_Tax_D5$read_freq)*100 
BC_POND_Tax_D4$read_freq=BC_POND_Tax_D4$read_freq/sum(BC_POND_Tax_D4$read_freq)*100 
BC_POND_Tax_D5$read_freq=BC_POND_Tax_D5$read_freq/sum(BC_POND_Tax_D5$read_freq)*100 

# Order the dataframes and only take top 10 abundance
BC_EPI2ME_Tax_D4<-BC_EPI2ME_Tax_D4[order(BC_EPI2ME_Tax_D4$read_freq, decreasing = TRUE),]
BC_EPI2ME_Tax_D4=head(BC_EPI2ME_Tax_D4,topx)

BC_EPI2ME_Tax_D5<-BC_EPI2ME_Tax_D5[order(BC_EPI2ME_Tax_D5$read_freq, decreasing = TRUE),]
BC_EPI2ME_Tax_D5=head(BC_EPI2ME_Tax_D5,topx)

BC_POND_Tax_D4<-BC_POND_Tax_D4[order(BC_POND_Tax_D4$read_freq, decreasing = TRUE),]
BC_POND_Tax_D4=head(BC_POND_Tax_D4,topx)

BC_POND_Tax_D5<-BC_POND_Tax_D5[order(BC_POND_Tax_D5$read_freq, decreasing = TRUE),]
BC_POND_Tax_D5=head(BC_POND_Tax_D5,topx)


# Combine all datasets for plotting
data=rbind(BC_EPI2ME_Tax_D4,BC_POND_Tax_D4,BC_EPI2ME_Tax_D5,BC_POND_Tax_D5)
  
# Define title and filename
title=paste("Species Level Abundance Comparison D4 ", "(", Barcode, ")", sep = "")
xlabel="Workflow and Dataset [-]"
ylabel="Percentage of Abundance [%]"
legendlabel="Species Name"
filename=paste("Section_5.3_Species_Level_Abundance_Comparison_D4_",Barcode,".jpg", sep = "")

plot_sample_1 <- ggplot(data=BC_EPI2ME_Tax_D4, aes(x=workflow , y=read_freq, fill=reorder(species_name, desc(read_freq)))) +
  geom_bar(stat = "identity") + coord_polar("y", start=0)+
  theme_tufte() +
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.x = element_text(size=14,margin = margin(t = -20, r = 0, b = 0, l = 0)),
        axis.text = element_blank())+
  guides(fill = guide_legend(title = "Species")) +
  ylab(ylabel) +
  xlab(NULL) +
  scale_fill_brewer(palette="RdBu") +
  geom_text(aes(label = round(read_freq, 1), x = 1.3), 
            position = position_stack(vjust = 0.5),color = "white",size=4)

plot_sample_2 <- ggplot(data=BC_POND_Tax_D4, aes(x=workflow , y=read_freq, fill=reorder(species_name, desc(read_freq)))) +
  geom_bar(stat = "identity") + coord_polar("y", start=0)+
  theme_tufte() +
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.x = element_text(size=14,margin = margin(t = -20, r = 0, b = 0, l = 0)),
        legend.position = "left",
        axis.text = element_blank())+
  guides(fill = guide_legend(title = "Species")) +
  ylab(ylabel) +
  xlab(NULL) +
  scale_fill_brewer(palette="RdBu") +
  geom_text(aes(label = round(read_freq, 1), x = 1.3), 
            position = position_stack(vjust = 0.5),color = "white",size=4)

q=ggplot <- ggarrange(plot_sample_1, plot_sample_2,ncol = 1, nrow = 2,labels = c("EPI2ME", "POND"),vjust=3)
q=annotate_figure(q,top = text_grob(title, color = "black", face = "bold", size = 16))
ggsave(plot = q, width = 8, height = 8, dpi = 300, filename = filename, path = graph_path)
```
Print the Graph
```{r,fig.width = 8, fig.height = 8}
print(q)
```
```{r}
topx=10

BC_EPI2ME_Tax_D4=as.data.frame(table(EPI2ME_Tax_D4$genus[which(EPI2ME_Tax_D4$barcode==Barcode)]))
colnames(BC_EPI2ME_Tax_D4)=c("genus_name", "read_freq")
BC_EPI2ME_Tax_D4$workflow="EPI2ME_D4"

BC_EPI2ME_Tax_D5=as.data.frame(table(EPI2ME_Tax_D5$genus[which(EPI2ME_Tax_D5$barcode==Barcode)]))
colnames(BC_EPI2ME_Tax_D5)=c("genus_name", "read_freq")
BC_EPI2ME_Tax_D5$workflow="EPI2ME_D5"

load_path=paste(Kraken2_Classification_D4_Path, Barcode,".fastq_REPORT", sep = "")
BC_POND_Tax_D4=read_delim(load_path,"\t", escape_double = FALSE, col_names = FALSE, trim_ws = TRUE)
BC_POND_Tax_D4=BC_POND_Tax_D4[which(BC_POND_Tax_D4$X4=="G"),]
BC_POND_Tax_D4=as.data.frame(cbind(BC_POND_Tax_D4$X6, BC_POND_Tax_D4$X3))
colnames(BC_POND_Tax_D4)=c( "genus_name","read_freq")
BC_POND_Tax_D4$workflow="POND_D4"
BC_POND_Tax_D4$read_freq=as.numeric(BC_POND_Tax_D4$read_freq)

load_path=paste(Kraken2_Classification_D5_Path, Barcode,".fastq_REPORT", sep = "")
BC_POND_Tax_D5=read_delim(load_path,"\t", escape_double = FALSE, col_names = FALSE, trim_ws = TRUE)
BC_POND_Tax_D5=BC_POND_Tax_D5[which(BC_POND_Tax_D5$X4=="G"),]
BC_POND_Tax_D5=as.data.frame(cbind(BC_POND_Tax_D5$X6, BC_POND_Tax_D5$X3))
colnames(BC_POND_Tax_D5)=c( "genus_name","read_freq")
BC_POND_Tax_D5$workflow="POND_D5"
BC_POND_Tax_D5$read_freq=as.numeric(BC_POND_Tax_D5$read_freq)

# Create percentage Abundance
BC_EPI2ME_Tax_D4$read_freq=BC_EPI2ME_Tax_D4$read_freq/sum(BC_EPI2ME_Tax_D4$read_freq)*100 
BC_EPI2ME_Tax_D5$read_freq=BC_EPI2ME_Tax_D5$read_freq/sum(BC_EPI2ME_Tax_D5$read_freq)*100 
BC_POND_Tax_D4$read_freq=BC_POND_Tax_D4$read_freq/sum(BC_POND_Tax_D4$read_freq)*100 
BC_POND_Tax_D5$read_freq=BC_POND_Tax_D5$read_freq/sum(BC_POND_Tax_D5$read_freq)*100 

# Order the dataframes and only take top 10 abundance
BC_EPI2ME_Tax_D4<-BC_EPI2ME_Tax_D4[order(BC_EPI2ME_Tax_D4$read_freq, decreasing = TRUE),]
BC_EPI2ME_Tax_D4=head(BC_EPI2ME_Tax_D4,topx)

BC_EPI2ME_Tax_D5<-BC_EPI2ME_Tax_D5[order(BC_EPI2ME_Tax_D5$read_freq, decreasing = TRUE),]
BC_EPI2ME_Tax_D5=head(BC_EPI2ME_Tax_D5,topx)

BC_POND_Tax_D4<-BC_POND_Tax_D4[order(BC_POND_Tax_D4$read_freq, decreasing = TRUE),]
BC_POND_Tax_D4=head(BC_POND_Tax_D4,topx)

BC_POND_Tax_D5<-BC_POND_Tax_D5[order(BC_POND_Tax_D5$read_freq, decreasing = TRUE),]
BC_POND_Tax_D5=head(BC_POND_Tax_D5,topx)

# Define title and filename
title=paste("Genus Level Abundance Comparison D4 ", "(", Barcode, ")", sep = "")
xlabel="Workflow and Dataset [-]"
ylabel="Percentage of Abundance [%]"
legendlabel="Genus Name"

filename=paste("Section_5.3_Genus_Level_Abundance_Comparison_D4_",Barcode,".jpg", sep = "")

plot_sample_1 <- ggplot(data=BC_EPI2ME_Tax_D4, aes(x=workflow , y=read_freq, fill=reorder(genus_name, desc(read_freq)))) +
  geom_bar(stat = "identity") + coord_polar("y", start=0)+
  theme_tufte() +
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.x = element_text(size=14,margin = margin(t = -20, r = 0, b = 0, l = 0)),
        axis.text = element_blank())+
  guides(fill = guide_legend(title = "Genus")) +
  ylab(ylabel) +
  xlab(NULL) +
  scale_fill_brewer(palette="RdBu") +
  geom_text(aes(label = round(read_freq, 1), x = 1.3), 
            position = position_stack(vjust = 0.5),color = "white",size=4)

plot_sample_2 <- ggplot(data=BC_POND_Tax_D4, aes(x=workflow , y=read_freq, fill=reorder(genus_name, desc(read_freq)))) +
  geom_bar(stat = "identity") + coord_polar("y", start=0)+
  theme_tufte() +
  theme(plot.title = element_text(color="Black", size=12, face="bold")) +
  theme(axis.title.x = element_text(size=14,margin = margin(t = -20, r = 0, b = 0, l = 0)),
        legend.position = "left",
        axis.text = element_blank())+
  guides(fill = guide_legend(title = "Genus")) +
  ylab(ylabel) +
  xlab(NULL) +
  scale_fill_brewer(palette="RdBu") +
  geom_text(aes(label = round(read_freq, 1), x = 1.3), 
            position = position_stack(vjust = 0.5),color = "white",size=4)

q=ggplot <- ggarrange(plot_sample_1, plot_sample_2,ncol = 1, nrow = 2,labels = c("EPI2ME", "POND"),vjust=3)
q=annotate_figure(q,top = text_grob(title, color = "black", face = "bold", size = 16))
ggsave(plot = q, width = 8, height = 8, dpi = 300, filename = filename, path = graph_path)
```
Print the Graph
```{r,fig.width = 8, fig.height = 8}
q
```










