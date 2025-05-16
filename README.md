# bigdate
setwd("c:/r_workdata") # 필수 3가지지
Sys.setlocale("LC_ALL","Korean")
library(lubridate)

#서로 다른 데이터 타입 처리 객체
#데이터 타입이 달라도 된다
#1. 벡터와 비슷한 형태이면서 키,값 으로 저장해

l1 = list(name ="홍길동",
          addr = "서울",
          tel = "010-1111-1111",
          pay = 500
)
l1

# 특정 키만 조회하는법 $
l1$addr

#list에 요소를 추가 그리고 삭제 하는법
l1$birth = "2023"
l1$birth
l1$birth ="2024"
l1
l1$name= c("고길동","마이콜") #키에다가 값을 넣을경우 원래있는게 바낌
# 추가
l1$name[length(l1$name)+1] = "홍길동" #현재 벡터의 길이보다 뒤에 넣어줌

#삭제 값을 삭제하는법과 키를 삭제하는법

#1. value특정 값을 삭제 하는법 
l1$name[length(l1$name)-1]=NA #아 마이콜이 NA로 바뀌네
l1$name

# 2. 리스트의 키 삭제하는법!
l1
l1$birth = NULL
l1

#데이터 프레임 ! 각 컬럼 (라벨) 별로 먼저 생성후 date.frame으로 모든 컬럼 
# 컬럼별 구성
#합치기
#이 차원구조
no = c(1,2,3,4)
name = c("Apple","Banana","Peach","Graph")
price = c(500,200,100,300)
qty = c(5,2,4,7)
#+ 는 끝나지 않음
# data.frame()으로 객체를 만들면 행 번호는 기본적으로 1부터 자동으로 부여돼서 나타남
no
name
sales = data.frame(No=no, Name=name, Price=price,Qty=qty) #열컬럼에 no라는 벡터를넣음
sales

class(sales) #데이터 프레임 속성
str(sales)

#2-2 행렬로 데이터 프레임을 생성하는법 
#매트릭스는 기본적 널 만들어지기에 2차원으로 마들려고 하면 
# 행의 갯수, 행성 법칙 by=T 이걸 붙ㅇ야댐댐

sales = matrix(c(1,"Apple",500,5,
                 2,"Peach",200,2,
                 3,"Banana",700,4,
                 4,"Graph",100,7),4, by=T) #벡터를 4행으로 캐릭터형식으로
sales2= matrix(c(1,"Apple",500,5,
                 2,"Peach",200,2,
                 3,"Banana",700,4,
                 4,"Graph",100,7),4, by=T)
d1=data.frame(sales2) #컬럼에 이름 이없음 매트릭스는 기본적으로는 행과열의 이름이없음 
#데이터 프레임에는 행의 번호가있음
d1
names(d1) = c("No","Name","Price","Qty")
d1
class(d1)
#subset() 함수는 데이터프레임에서 특정 조건을 만족하는 
#행이나 열을 추출할 때 사용됩니다
#데이터 조회
sales$Name #매트릭스의 조회에서는 Name이라는게없음  그리고 매트릭스에서는 $조회 방식의차이
#데이터 프레임가능
sales
sales
#데이터 조회
sales[1,3]
sales[,2]
sales[3,]
sales
sales[c(1,3),2]

sales[,c(2,4)]
sales[,c(1:3)]
sales$Name
d1=data.frame(sales)
names(d1)=c("No","Name","Price","Qty")
sales
class(d1)
#원하는 조건만 검색 :subset() 부과 조건
sales=d1
sales
subset(sales,Qty <=5)
subset(sales,Price ==200)
subset(sales,Name=="Apple")
subset(sales,No==1)
#데이터 프레임에서 특정 컬럼만 골라내서 새로운 형태 만들기

no=c(1,2,3,4,5)
name=c("이순신","김유신","유관순","강감찬","안중근")
addr=c("서울","대전","대구","부산","광주")
tel=c(111,222,333,444,555)
hobby=c("놀","먹","자","게","멍")
mem=data.frame(No=no,Name=name,Addr=addr,Tel=tel,Hobby=hobby)
mem
mem2=subset(mem,select = c(No,Name,Tel))
mem2

mem3 = subset(mem, select=-Tel)
mem3 = subset(mem, select=-Tel)
mem3

colnames(mem3)=c("번호","이름","주소","취미")
mem3
