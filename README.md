# Data-Visualization_1
```
 library(ggplot2)
                  library(dplyr)
                  library(tidyr)
                  
                  # Read data
                  
                  gene_counts <- read.delim("C:/Users/lenovo/Desktop/WheatNLR/Data/1_thesis_data/1_yield/Orthofinder_results/Results_Apr24_5/Orthogroups/Orthogroups.GeneCount.tsv", sep = "\t")
                  
                  # Calculate total genes per species
                  species_columns <- setdiff(colnames(gene_counts), c("Orthogroup", "Total", "yield_known"))
                  total_counts <- colSums(gene_counts[, species_columns], na.rm = TRUE)
                  
                  # Convert to data frame for ggplot
                  plot_data <- data.frame(
                    Species = names(total_counts),
                    TotalGenes = as.numeric(total_counts)
                  )
                  
                  # Create bar plot
                  ggplot(plot_data, aes(x = reorder(Species, -TotalGenes), y = TotalGenes, fill = Species)) +
                    geom_col() +
                    geom_text(aes(label = TotalGenes), vjust = -0.3, size = 3) +
                    labs(title = "Total Gene Counts by Species",
                         x = "Species",
                         y = "Total Gene Count") +
                    theme_minimal() +
                    theme(axis.text.x = element_text(angle = 45, hjust = 1),
                          legend.position = "none") +
                    scale_fill_viridis_d()        
                  ```
                  
                  
                  
                  
                  
                  
   ```               
                  
                  # Pivot data to long format
                  long_data <- gene_counts %>%
                    select(-Total, -yield_known) %>%
                    pivot_longer(cols = -Orthogroup, names_to = "Species", values_to = "Count")
                  
                  # Create faceted plots
                  ggplot(long_data, aes(x = Orthogroup, y = Count)) +
                    geom_col(fill = "red") +
                    facet_wrap(~ Species, scales = "free_y") +
                    labs(title = "Gene Counts per Orthogroup by Species",
                         x = "Orthogroup",
                         y = "Gene Count") +
                    theme_minimal() +
                    theme(axis.text.x = element_blank(),
                          axis.ticks.x = element_blank())
                          ```
