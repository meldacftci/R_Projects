# R Data Analysis Projects | Data Cleaning & Visualization
This repository contains data analysis projects using R.
I analyze datasets, clean them, and apply statistical techniques.
###📌 Included Analyses:
✔ Data Cleaning
✔ Exploratory Data Analysis (EDA)
✔ Statistical Summaries
✔ Data Visualization (ggplot2)
### Libraries Used:
-dplyr
-ggplot2
-readODS
> install.packages("readODS")
WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

https://cran.rstudio.com/bin/windows/Rtools/
also installing the dependency ‘minty’

URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/minty_0.0.5.zip' deneniyor
Content type 'application/zip' length 592603 bytes (578 KB)
downloaded 578 KB

URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/readODS_2.3.2.zip' deneniyor
Content type 'application/zip' length 491915 bytes (480 KB)
downloaded 480 KB

package ‘minty’ successfully unpacked and MD5 sums checked
package ‘readODS’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
	C:\Users\hp\AppData\Local\Temp\RtmpkB11UY\downloaded_packages
> library(readODS)
> data7 <-read_ods("C:/Users/hp/Desktop/R-Giris-Seviyesi-Egitimi-main/dataexample.ods.ods")
Hata: file does not exist
> data7 <-read_ods("C:/Users/hp/Desktop/dataexample.ods")
> head(data7)
# A tibble: 6 × 6
  OrderDate Region  Rep     Item   Units Total 
  <chr>     <chr>   <chr>   <chr>  <dbl> <chr> 
1 1.06.2024 East    Jones   Pencil    95 189.05
2 1/23/2024 Central Kivell  Binder    50 999.50
3 2.09.2024 Central Jardine Pencil    36 179.64
4 2/26/2024 Central Gill    Pen       27 539.73
5 3/15/2024 West    Sorvino Pencil    56 167.44
6 4.01.2024 East    Jones   Binder    60 299.40
> str(data7)
tibble [43 × 6] (S3: tbl_df/tbl/data.frame)
 $ OrderDate: chr [1:43] "1.06.2024" "1/23/2024" "2.09.2024" "2/26/2024" ...
 $ Region   : chr [1:43] "East" "Central" "Central" "Central" ...
 $ Rep      : chr [1:43] "Jones" "Kivell" "Jardine" "Gill" ...
 $ Item     : chr [1:43] "Pencil" "Binder" "Pencil" "Pen" ...
 $ Units    : num [1:43] 95 50 36 27 56 60 75 90 32 60 ...
 $ Total    : chr [1:43] "189.05" "999.50" "179.64" "539.73" ...
> sum(is.na(data7))
[1] 0
> summary(data7)
  OrderDate            Region         
 Length:43          Length:43         
 Class :character   Class :character  
 Mode  :character   Mode  :character  
                                      
                                      
                                      
     Rep                Item          
 Length:43          Length:43         
 Class :character   Class :character  
 Mode  :character   Mode  :character  
                                      
                                      
                                      
     Units          Total          
 Min.   : 2.00   Length:43         
 1st Qu.:27.50   Class :character  
 Median :53.00   Mode  :character  
 Mean   :49.33                     
 3rd Qu.:74.50                     
 Max.   :96.00                     
> mean(data7$Units, na.rm= TRUE)
[1] 49.32558
> median(data7$Units, na.rm= TRUE)
[1] 53
> sd(data7$Units, na.rm= TRUE)
[1] 30.07825
> table(data7$Units)

 2  3  4  5  7 11 14 15 16 27 28 29 32 35 36 42 
 1  1  1  1  2  1  1  1  1  1  2  1  1  1  1  1 
46 50 53 55 56 57 60 62 64 66 67 74 75 76 80 81 
 1  2  1  1  1  1  2  1  1  1  1  1  1  1  1  1 
87 90 94 95 96 
 1  2  1  1  2 
> prop.table(table(data7$Units))

         2          3          4          5 
0.02325581 0.02325581 0.02325581 0.02325581 
         7         11         14         15 
0.04651163 0.02325581 0.02325581 0.02325581 
        16         27         28         29 
0.02325581 0.02325581 0.04651163 0.02325581 
        32         35         36         42 
0.02325581 0.02325581 0.02325581 0.02325581 
        46         50         53         55 
0.02325581 0.04651163 0.02325581 0.02325581 
        56         57         60         62 
0.02325581 0.02325581 0.04651163 0.02325581 
        64         66         67         74 
0.02325581 0.02325581 0.02325581 0.02325581 
        75         76         80         81 
0.02325581 0.02325581 0.02325581 0.02325581 
        87         90         94         95 
0.02325581 0.04651163 0.02325581 0.02325581 
        96 
0.04651163 
> library(dplyr)
> data7_filter <- data7 %>% filter(data7$Units > 45)
> head(data7_filter)
# A tibble: 6 × 6
  OrderDate Region  Rep     Item   Units Total 
  <chr>     <chr>   <chr>   <chr>  <dbl> <chr> 
1 1.06.2024 East    Jones   Pencil    95 189.05
2 1/23/2024 Central Kivell  Binder    50 999.50
3 3/15/2024 West    Sorvino Pencil    56 167.44
4 4.01.2024 East    Jones   Binder    60 299.40
5 4/18/2024 Central Andrews Pencil    75 149.25
6 5.05.2024 Central Jardine Pencil    90 449.10
>   count(data7$Total)
Error in UseMethod("count") : 
  'count' için uygulanabilir bir metod yok ("character" sınıfının bir nesnesine uygulanan)
>   median(data7$Total, na.rm= TRUE)
[1] "299.40"
> group_by(data7$Total) %>% 
+   summarise(mean(data7$Total, na.rm= TRUE))
Error in UseMethod("group_by") : 
  'group_by' için uygulanabilir bir metod yok ("character" sınıfının bir nesnesine uygulanan)
> library(ggplot2)
> ggplot(data7, aes(data7$Units))
Uyarı mesajları:
Use of `data7$Units` is discouraged.
ℹ Use `Units` instead. 
> View(data7)
> ggplot(data7, aes(x=data7$Units, y= data7$Total))+ 
+   geom_point(fill="skyblue",color="black", size= 19, shape=16)
Uyarı mesajları:
1: Use of `data7$Units` is discouraged.
ℹ Use `Units` instead. 
2: Use of `data7$Total` is discouraged.
ℹ Use `Total` instead. 
> ggplot(data7, aes(y= Rep))+
+   geom_boxplot(fill="red", color="black")+
+   labs(title = "kutu grafigi", y="degerler")
> data7$Total <- as.numeric(data7$Total)
Uyarı mesajları:
Zorlamadan dolayı ortaya çıkan NAs
# I used gsub() function to replace all commas in the column of Total with an empty string.
> data7$Total <- gsub(",","", data7$Total)
 # I used gsub() function to replace all spaces in the column of Total with an empty string.  
> data7$Total <- gsub(" ", "", data7$Total)
# I used gsub() function to replace all characters in the colunn of Total that are not 0-9 digits or a period with an empty string. This is because the column may contain other characters besides numeric values (e.g., letters, symbols, etc.). R cannot interpret these characters as numbers, so they need to be removed.
> data7$Total <- gsub("[^0-9.]", "", data7$Total)
# After cleaning data from what blocks it to be arithmetic operations, I described the column as numeric by using as.numeric() function.
> data7$Total <- as.numeric(data7$Total)
> mean(data7$Total, na.rm = TRUE)
[1] 478.068
> ggplot(data7, aes(x= Units))+
+   geom_histogram(binwidth =10, fill="blue", color="black")+ 
+   labs(title="units dagilimi", x="units", y="frekans")
> ggplot(data7, aes(x= Total))+
+   geom_histogram(Units= 10, fill="pink", color="purple")+
+   labs(title= "total dagilimi", x=Total, y"units")
Hata: unexpected string constant içinde:
"  geom_histogram(Units= 10, fill="pink", color="purple")+
  labs(title= "total dagilimi", x=Total, y"units""
> ggplot(data7, aes(x= Total))+
+   geom_histogram(Units= 10, fill="pink", color="purple")+
+   labs(title= "total dagilimi", x="total", y"units")
Hata: unexpected string constant içinde:
"  geom_histogram(Units= 10, fill="pink", color="purple")+
  labs(title= "total dagilimi", x="total", y"units""
> ggplot(data7, aes(x = Total)) +
+   geom_histogram(binwidth = 10, fill = "pink", color = "purple") +
+   labs(title = "Total Dağılımı", x = "Total", y = "Units")
Uyarı mesajları:
Removed 2 rows containing non-finite outside
the scale range (`stat_bin()`). 
> data7 %>%
+   group_by(Region) %>%
+   summarise(Avg_Units = mean(Units, na.rm= TRUE))
# A tibble: 3 × 2
  Region  Avg_Units
  <chr>       <dbl>
1 Central      50.0
2 East         53.2
3 West         38.5
> head(avg_units)
Hata: 'avg_units' nesnesi bulunamadı
> head(Avg_Units)
Hata: 'Avg_Units' nesnesi bulunamadı
> summary_table <- data7 %>%
+   group_by(Region) %>%
+   summarise(Avg_Units= mean(Units, na.rm= TRUE))
> head(Avg_Units)
Hata: 'Avg_Units' nesnesi bulunamadı
> head(summary_table)
# A tibble: 3 × 2
  Region  Avg_Units
  <chr>       <dbl>
1 Central      50.0
2 East         53.2
3 West         38.5
> data7 %>%
+   group_by(data$Rep) %>%
+   summarise(Avg_Rep =mean(na.rm =TRUE))
Error in `group_by()`:
ℹ In argument: `data$Rep`.
Caused by error in `data$Rep`:
! 'closure' tipi nesne alt küme yapılamaz
Run `rlang::last_trace()` to see where the error occurred.
> data7 %>%
+   group_by(Rep) %>%
+   summarise(Avg_Rep =mean(na.rm =TRUE))
Error in `summarise()`:
ℹ In argument: `Avg_Rep = mean(na.rm =
  TRUE)`.
ℹ In group 1: `Rep = "Andrews"`.
Caused by error in `mean.default()`:
! varsayılanı olmayan "x" argümanı yok
Run `rlang::last_trace()` to see where the error occurred.
> data7 %>%
+   group_by(Rep) %>%
+   summarise(Avg_Rep =mean(Rep, na.rm =TRUE))
# A tibble: 11 × 2
   Rep      Avg_Rep
   <chr>      <dbl>
 1 Andrews       NA
 2 Gill          NA
 3 Howard        NA
 4 Jardine       NA
 5 Jones         NA
 6 Kivell        NA
 7 Morgan        NA
 8 Parent        NA
 9 Smith         NA
10 Sorvino       NA
11 Thompson      NA
Uyarı mesajları:
There were 11 warnings in `summarise()`.
The first warning was:
ℹ In argument: `Avg_Rep = mean(Rep, na.rm =
  TRUE)`.
ℹ In group 1: `Rep = "Andrews"`.
Caused by warning in `mean.default()`:
! argument is not numeric or logical: returning NA
ℹ Run dplyr::last_dplyr_warnings() to see the
  10 remaining warnings. 
> data7 %>% 
+   group_by(Rep) %>%
+   summarise(Count_Rep = n())
# A tibble: 11 × 2
   Rep      Count_Rep
   <chr>        <int>
 1 Andrews          4
 2 Gill             5
 3 Howard           2
 4 Jardine          5
 5 Jones            8
 6 Kivell           4
 7 Morgan           3
 8 Parent           3
 9 Smith            3
10 Sorvino          4
11 Thompson         2
> data7 <- data7 %>%
+   arrange(data7$Rep)
> head(data7$Rep)
[1] "Andrews" "Andrews" "Andrews" "Andrews"
[5] "Gill"    "Gill"   
> totally_sold <- data7 %>%
+   group_by(Rep) %>%
+   summarise(totally_sold = summary_dataSles, na.rm= TRUE)
Error in `summarise()`:
ℹ In argument: `totally_sold =
  summary_dataSles`.
ℹ In group 1: `Rep = "Andrews"`.
Caused by error:
! 'summary_dataSles' nesnesi bulunamadı
Run `rlang::last_trace()` to see where the error occurred.
> totally_sold <- data7 %>%
+   group_by(Rep) %>%
+   summarise(Totally_Sold = sum(Sales, na.rm= TRUE))
Error in `summarise()`:
ℹ In argument: `Totally_Sold =
  sum(Sales, na.rm = TRUE)`.
ℹ In group 1: `Rep = "Andrews"`.
Caused by error:
! 'Sales' nesnesi bulunamadı
Run `rlang::last_trace()` to see where the error occurred.
> totally_sold <- data7 %>%
+   group_by(Rep) %>%
+   summarise(Totally_Sold = sum(Item, na.rm= TRUE))
Error in `summarise()`:
ℹ In argument: `Totally_Sold = sum(Item,
  na.rm = TRUE)`.
ℹ In group 1: `Rep = "Andrews"`.
Caused by error in `sum()`:
! argümanın geçersiz 'type' (character)
Run `rlang::last_trace()` to see where the error occurred.
> totally_sold <- data7 %>%
+   group_by(Rep) %>%
+   summarise(Totally_Sold = sum(Total, na.rm= TRUE))
> ordered_sold <- totally_sold %>%
+   arrange(desc(Totally_Sold))
> head(ordered_sold)
# A tibble: 6 × 2
  Rep     Totally_Sold
  <chr>          <dbl>
1 Kivell         3109.
2 Parent         3102.
3 Jardine        2812.
4 Jones          2363.
5 Gill           1741.
6 Smith          1641.
> ggplot(data7, aes(x="Rep", y="Item"))+
+   geom_point(fill="skyblue",color="black", size= 19, shape=16)
Uyarı mesajları:
In geom_point(fill = "skyblue", color = "black", size = 19, shape = 16) :
  All aesthetics have length 1, but the data has
43 rows.
ℹ Please consider using `annotate()` or provide
  this layer with data containing a single row.
> ggplot(data7, aes(x= Rep, y= Item))+
+   geom_point(fill="skyblue", color="black",size= 19, shape= 16)
> summarise(Avg_Sales= mean(Total, na.rm=TRUE))
Hata: 'Total' nesnesi bulunamadı
> summarise(Avg_Sales= mean(Unit, na.rm=TRUE))
Hata: 'Unit' nesnesi bulunamadı
> head(data7)
# A tibble: 6 × 6
  OrderDate  Region Rep   Item  Units Total
  <chr>      <chr>  <chr> <chr> <dbl> <dbl>
1 4/18/2024  Centr… Andr… Penc…    75  149.
2 4.10.2025  Centr… Andr… Penc…    66  131.
3 10/31/2025 Centr… Andr… Penc…    14   NA 
4 12/21/2025 Centr… Andr… Bind…    28  140.
5 2/26/2024  Centr… Gill  Pen      27  540.
6 1/15/2025  Centr… Gill  Bind…    46  414.
> summarise(Avg_Sales= mean(Units, na.rm=TRUE))
Hata: 'Units' nesnesi bulunamadı
> data7 %>%
+   group_by(Region) %>%
+   summarise(Avg_Sales = mean(Units, na.rm= TRUE)) %>%
+   arrange(desc(Avg_Sales))
# A tibble: 3 × 2
  Region  Avg_Sales
  <chr>       <dbl>
1 East         53.2
2 Central      50.0
3 West         38.5
> data7 %>% 
+   group_by(Rep) %>%
+   summarise(Total_Sales= sum(Total, nar.rm= TRUE)) %>%
+   arrange(desc(Total_Sales))%>%
+   head(5)
# A tibble: 5 × 2
  Rep     Total_Sales
  <chr>         <dbl>
1 Kivell        3110.
2 Parent        3103.
3 Jardine       2813.
4 Jones         2364.
5 Smith         1642.
> ggplot(data7, aes(x= Total))+
+   geom_histogram(binwidth = 100, fill="blue", color="black")+
+   labs(title = "toplam satislarin dagilimi", x="satis miktari", y="frekans")
Uyarı mesajları:
Removed 2 rows containing non-finite
outside the scale range (`stat_bin()`). 
> ggplot(data7, aes(x= Units))+
+   geom_boxplot(fill="pink", color="black, ")+
+   labs(title = "kutu grafigi", y="degerler")
Error in `geom_boxplot()`:
! Problem while converting geom to
  grob.
ℹ Error occurred in the 1st layer.
Caused by error:
! Unknown colour name: black, 
Run `rlang::last_trace()` to see where the error occurred.
> ggplot(data7, aes(x = Units)) +
+   geom_boxplot(fill = "pink", color = "black") +
+   labs(title = "Kutu Grafiği", y = "Değerler")
> summarise( data7, mean(Total)
+ mean_total <- data7 %>%
Hata: unexpected symbol içinde:
"summarise( data7, mean(Total)
mean_total"
> mean_total <- data7 %>%
+   summarise(ortalama = mean(Total, na.rm = TRUE))
> print(mean_total)
# A tibble: 1 × 1
  ortalama
     <dbl>
1     478.
> median_total <- data7%>%
+   summarise(medyan = median(Total,na.rm=TRUE))
> print(median_total)
# A tibble: 1 × 1
  medyan
   <dbl>
1   300.
