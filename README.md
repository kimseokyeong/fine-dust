# fine-dust
Concentration of fine dust by country


install.packages("rvest")

library(rvest)

library(tidyverse)

 

url = "https://www.airkorea.or.kr/web/contents/contentView/?pMENU_NO=127&cntnts_no=4"

html = read_html(url)

table = html %>% html_nodes("table") %>% html_nodes("td") %>% html_text()

table = table[-c(1,37,73,109,145,181,217,253)]

 

df = as.data.frame(matrix(table , nrow=40 , ncol=7 , byrow = TRUE))

year = rep(2018:2011,c(5,5,5,5,5,5,5,5))

df = cbind(year, df)

colnames(df) = c("year","지역","미세먼지","초미세먼지","이산화질소", "아산황가스","연평균오존","최고연평균오존")

 

 

#1.

ggplot(data = df , aes(x=지역, y=미세먼지)) + geom_point(aes(color = 지역),size = 4) +

  ggtitle("나라별 미세먼지수치 비교") 

 

 

#2.

ggplot(data = df , aes(x =  지역 , y = 연평균오존)) + 

  geom_bar(stat = "identity" , fill="dark blue") + coord_flip() +

  ggtitle("나라별 연평균오존 비교") + theme(title = element_text(color="black" , size=30) ,

  axis.title.x=element_text(size=20)) 
