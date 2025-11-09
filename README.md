# 🧠 Lifestyle and Health Risk Prediction using Decision Tree (R)

## 📋 Overview  
This project predicts a person’s **health risk level** based on their **age**, **sleep duration**, and **profession** using a **Decision Tree Classifier** in R.  
The goal is to explore how lifestyle habits influence overall health and to create a simple, interpretable model for early risk detection.

---

## 🧰 Tools & Libraries Used
- **R Programming Language**
- `rpart` → Decision Tree modeling  
- `rpart.plot` → Tree visualization  
- `caret` → Data partitioning and accuracy evaluation  



View(Lifestyle_and_Health_Risk)
LHR <- Lifestyle_and_Health_Risk

# Select columns
Health <- LHR[, c("age", "sleep", "profession", "health_risk")]

# Convert categorical columns into factors
LHR$profession <- as.factor(LHR$profession)
LHR$health_risk <- as.factor(LHR$health_risk)
library(caret)

train_index <- createDataPartition(LHR$health_risk, p = 0.60, list = FALSE)
train_data <- LHR[train_index, ]
test_data  <- LHR[-train_index, ]

library(caret)

train_index <- createDataPartition(LHR$health_risk, p = 0.60, list = FALSE)
train_data <- LHR[train_index, ]
test_data  <- LHR[-train_index, ]

library(rpart)
library(rpart.plot)

model <- rpart(health_risk ~ ., data = train_data)
rpart.plot(model)

pred <- predict(model, test_data, type = "class")

library(caret)
con  <- confusionMatrix(pred, test_data$health_risk)
acc  <- con$overall["Accuracy"]

print(con)
print(acc)

