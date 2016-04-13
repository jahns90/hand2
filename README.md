# Es gibt die Datensätze "Games" mit allen Spielen in den Zeilen (9 pro Spieltag) und den Spieltagen in den Spalten (34) sowie "Rating", in die die Rating veränderungen eingetragen werden mit 18 Zeilen (1 pro Team) und 35 Spalten (Wk0 als Grundlage und dann Stand nach jedem Spieltag)
# Ein Spieltag nach dem anderen! i geht also durch die 18 Teams durch
for (i in 1:18){
team<-Rating[i,"Team"]
game<-Games["Game",c(Games$Game1Home==team,Games$Game1Away==team)]
if(Games$Game1Home[i]==team){
homegame<-1}
else{
homegame<-2}
if(homegame==1){
opp<-Games[game,"Game1Away"]
}
else{
opp<-Games[game,"Game1Home"]}
winprop<-Rating[team,"Wk0"]/Rating[opp,"Wk0"]
if(Games$Game1GoalsHome[game]>Games$Game1GoalsAway[game]&homegame==1){
outcome<-2}
if(Games$Game1GoalsHome[game]>Games$Game1GoalsAway[game]&homegame==1){
outcome<-1}
if(Games$Game1GoalsHome[game]<Games$Game1GoalsAway[game]&homegame==1){
outcome<- (-1)}
if(homegame==1){
Tordiff<-Games$Game1GoalsHome[game]-Games$Game1GoalsAway[game]}
else{
Tordiff<-Games$Game1GoalsAway[game]-Games$Game1GoalsHome[game]}
Rating$Wk1[i]<-Rating$Wk0[i]+(winprop*(-1)+1)*outcome*2+Tordiff/5
print(team)
print(game)
print(homegame)
print(opp)
print(winprop)
print(outcome)
print(Tordiff)
}
