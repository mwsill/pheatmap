pheatmap
========

A package for drawing pretty heatmaps in R. The ordinary heatmap function in R has several drawbacks when it comes to producing publication quality heatmaps. It is hard to produce pictures with consistent text, cell and overall sizes and shapes. The function pheatmap tries to alleviate the problems by offering more fine grained control over heatmap dimensions and appearance.

```{r}
library(devtools)                  
install_github('mwsill/pheatmap')

# Create test matrix
test = matrix(rnorm(200), 20, 10)
test[1:10, seq(1, 10, 2)] = test[1:10, seq(1, 10, 2)] + 3
test[11:20, seq(2, 10, 2)] = test[11:20, seq(2, 10, 2)] + 2
test[15:20, seq(2, 10, 2)] = test[15:20, seq(2, 10, 2)] + 4
colnames(test) = paste("Test", 1:10, sep = "")
rownames(test) = paste("Gene", 1:20, sep = "")
# Generate annotations for rows and columns
annotation_col = data.frame(
                    CellType = factor(rep(c("CT1", "CT2"), 5)),
                    Time = 1:5
                )
rownames(annotation_col) = paste("Test", 1:10, sep = "")

annotation_row = data.frame(
                    GeneClass = factor(rep(c("Path1", "Path2", "Path3"), c(10, 4, 6)))
                )
rownames(annotation_row) = paste("Gene", 1:20, sep = "")

#perform external column clustering by hclust
colclus <- hclust(dist(t(test)))

# Display row and color annotations
pheatmap(test, annotation_col = annotation_col,cols_dendro=colclus)
```