# ANN-Bathymetry-Extraction-Model

#At first the program should read the .txt file with the points that is going to be trainned and the other one that is going to be use to make the prediction. In this example is used the file with the sections spaced 500 meters.

train<-read.table("./train500.txt", sep = ";", header = TRUE)
prediction<-read.table("./pred.txt", sep = ";", header = TRUE)

#Trainning the ANN and printing
print(nn500 <- neuralnet(Z_Normalized ~ RED_N + NIR_N, data=train, hidden=3, rep=100, err.fct="sse", linear.output=TRUE))

plot(nn500)

#Doing the prediction for the "prediction" points
pred_ANN_500 <- predict(nn500,"prediction")

#Exporting the results for a .txt file

write.table(pred_ANN_500, file = "pred_ANN_500.txt", row.names = TRUE, sep = ";", dec = ",")


