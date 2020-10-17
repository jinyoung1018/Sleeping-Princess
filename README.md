## 잠자는 숲속의 공주 게임

* 잠자는 숲속의 공주 게임
  * 게임 소개
    * 조작 방법
  * 소스코드

**게임소개**

방탈 라이브러리를 이용해서 파이썬으로 만든 **숨겨진 단서**를 찾아 잠든 공주를 구하는 게임.

조작 방법: 게임을 시작하면 숨겨진 지도를 찾아서 공주의 위치를 파악할 수 있다. 공주의 위치가 파악되면 적절한 해독제로 공주를 구한다.
  
**소스코드** 

```python
from bangtal import *

setGameOption(GameOption.INVENTORY_BUTTON,False)
setGameOption(GameOption.MESSAGE_BOX_BUTTON,False)

scene1 = Scene('숲','Images/숲.png')
scene2 = Scene('공주','Images/공주배경.png')
scene3 = Scene('공주','Images/배경3.png')


startButton = Object('Images/start.png')
startButton.locate(scene1,550,360)
startButton.setScale(1.7)
startButton.show( )

tree1 = Object('Images/나무7.png')
tree1.setScale(0.5)
tree1.locate(scene1,140,120)

tree2 = Object('Images/나무5.png')
tree2.setScale(0.6)
tree2.locate(scene1,1000,110)

flashLight = Object('Images/손전등.png')
flashLight.setScale(0.1)
flashLight.locate(scene1,900,260)

tree3 = Object('Images/나무5.png')
tree3.setScale(0.3)
tree3.locate(scene1,835,220)

tree4 = Object('Images/나무5.png')
tree4.setScale(0.3)
tree4.locate(scene1,360,260)

tree5 = Object('Images/나무4.png')
tree5.setScale(0.3)
tree5.locate(scene1,460,120)

map = Object('Images/지도.png')
map.setScale(0.2)
map.locate(scene1,670,140)

yesButton = Object('Images/yes.png')
yesButton.locate(scene1,370,200)
yesButton.setScale(0.3)

noButton = Object('Images/no.png')
noButton.locate(scene1,780,200)
noButton.setScale(0.3)

question = Object('Images/질문.png')
question.locate(scene1,420,460)

map2 = Object('Images/펼친지도.png')
map2.locate(scene1,410,190)

kit = Object('Images/kit.png')
kit.locate(scene2,1100,25)
kit.setScale(0.3)

antidote1 = Object('Images/해독제1.png')
antidote1.locate(scene2,280,350)
antidote1.setScale(0.3)

antidote2 = Object('Images/해독제2.png')
antidote2.locate(scene2,600,350)
antidote2.setScale(0.3)

antidote3 = Object('Images/해독제3.png')
antidote3.locate(scene2,920,350)
antidote3.setScale(0.3)

princess = Object('Images/공주.png')
princess.locate(scene3,370,220)











def startButton_onMouseAction(x,y,action):
   showMessage('지도를 찾아서 공주님의 위치를 파악하세요!!')
   scene1.setLight(0.38)
   tree1.show( )
   startButton.hide( )
   tree2.show( )
   flashLight.show( )
   tree3.show( )
   tree4.show( )
   tree5.show( )
   

startButton.onMouseAction = startButton_onMouseAction

tree1.moved = False
def tree1_onMouseAction(x,y,action):
    if action == MouseAction.DRAG_LEFT:
        tree1.locate(scene1,80,120)
        tree1.moved = True
    elif action == MouseAction.DRAG_RIGHT:
        tree1.locate(scene1,210,120)
        tree1.moved = True
tree1.onMouseAction = tree1_onMouseAction

tree2.moved = False
def tree2_onMouseAction(x,y,action):
    if action == MouseAction.DRAG_LEFT:
        tree2.locate(scene1,940,110)
        tree2.moved = True
    elif action == MouseAction.DRAG_RIGHT:
        tree2.locate(scene1,1060,110)
        tree2.moved = True
tree2.onMouseAction = tree2_onMouseAction

tree3.moved = False
def tree3_onMouseAction(x,y,action):
    if action == MouseAction.DRAG_LEFT:
        tree3.locate(scene1,775,220)
        tree3.moved = True
    elif action == MouseAction.DRAG_RIGHT:
        tree3.locate(scene1,965,220)
        tree3.moved = True
tree3.onMouseAction = tree3_onMouseAction

tree4.moved = False
def tree4_onMouseAction(x,y,action):
    if action == MouseAction.DRAG_LEFT:
        tree4.locate(scene1,300,260)
        tree4.moved = True
    elif action == MouseAction.DRAG_RIGHT:
        tree4.locate(scene1,420,260)
        tree4.moved = True
tree4.onMouseAction = tree4_onMouseAction

tree5.moved = False
def tree5_onMouseAction(x,y,action):
    if action == MouseAction.DRAG_LEFT:
        tree5.locate(scene1,400,120)
        tree5.moved = True
    elif action == MouseAction.DRAG_RIGHT:
        tree5.locate(scene1,520,120)
        tree5.moved = True
tree5.onMouseAction = tree5_onMouseAction

def flashLight_onMouseAction(x,y,action):
    flashLight.pick( )
    question.show( ) 
    yesButton.show( )
    noButton.show( )

flashLight.onMouseAction = flashLight_onMouseAction

def yesButton_onMouseAction(x,y,action):

    scene1.setLight(1.0)
    yesButton.hide( )
    noButton.hide( )
    question.hide( )
    map.show( )
   
yesButton.onMouseAction = yesButton_onMouseAction


def noButton_onMouseAction(x,y,action):

    yesButton.hide( )
    noButton.hide( )
    question.hide( )
    
   
noButton.onMouseAction = noButton_onMouseAction


def map_onMouseAction(x,y,action):

    map.hide( )
    map2.show( )
    showMessage('목적지를 클릭하세요!!')
    
map.onMouseAction = map_onMouseAction


def map2_onMouseAction(x,y,action):
    if 323-54 < x < 323+54 and 369-54 < y < 369+54:
        scene2.enter( )
        kit.show( )
    else:
        showMessage('거기는 공주님이 없어요ㅠㅠ')
 


map2.onMouseAction = map2_onMouseAction

def kit_onMouseAction(x,y,action):
    antidote1.show( )
    antidote2.show( )
    antidote3.show( )
    showMessage("해독제를 선택하세요!!")
    
   
kit.onMouseAction = kit_onMouseAction

def antidote1_onMouseAction(x,y,action):
    princess.show( )
    
    showMessage("구해줘서 고마워요~")
    scene3.enter( )
    
   
antidote1.onMouseAction = antidote1_onMouseAction

def antidote2_onMouseAction(x,y,action):
    
    showMessage("해독제가 아니에요ㅠㅠ")
   
antidote2.onMouseAction = antidote2_onMouseAction

def antidote3_onMouseAction(x,y,action):
    
    showMessage("해독제가 아니에요ㅠㅠ")
   
antidote3.onMouseAction = antidote3_onMouseAction











startGame(scene1)


