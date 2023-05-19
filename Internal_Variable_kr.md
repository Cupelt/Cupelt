# 내부 변수
다음 트리거에는 내부 변수가 존재합니다.
- [Click/Walk Trigger](https://github.com/TriggerReactor/TriggerReactor/wiki/Click-and-Walk-Triggers_kr#click-%ED%8A%B8%EB%A6%AC%EA%B1%B0)
- [Command Trigger](https://github.com/TriggerReactor/TriggerReactor/wiki/Command-Trigger_kr#%EB%82%B4%EB%B6%80-%EB%B3%80%EC%88%98)
- [Area Trigger](https://github.com/TriggerReactor/TriggerReactor/wiki/Area-Trigger_kr#%EB%82%B4%EB%B6%80-%EB%B3%80%EC%88%98-%EB%AA%A9%EB%A1%9D)
- Custom Trigger
    |변수 종류|변수 타입|설명|
    |:------|:------|:------:|
    |event|Event|Custom Trigger에 지정된 이벤트에 대한 정보를 가집니다.|
    |player|[Player](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/entity/Player.html)?|Custom Trigger에 지정된 이벤트가 *'플레이어'* 대한 정보를 가지고 있다면, 플레이어를 반환합니다.</br></br>단, 제3자 플러그인의 커스텀 이벤트에서 따로 player(이벤트 실행자) 변수를 필요로 하는 경우가 있습니다.</br>이 경우에는 기존의 Player타입의 player내부변수가 그 플러그인이 원하는 타입의 변수로 덮어 씌워 집니다.|
    |entity|[Entity](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/entity/Entity.html)?|Custom Trigger에 지정된 이벤트가 *'엔티티'* 대한 정보를 가지고 있다면, 플레이어를 반환합니다.|
    |block|[Block](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/block/Block.html)?|Custom Trigger에 지정된 이벤트가 *'블록'* 대한 정보를 가지고 있다면, 플레이어를 반환합니다.|
    
    '?' 는 정보가 없을때, [null](https://github.com/TriggerReactor/TriggerReactor/wiki/Variables_kr#null) 을 반환하는 변수라는 의미입니다.
- [Inventory Trigger](https://github.com/TriggerReactor/TriggerReactor/wiki/Inventory-Trigger_kr#%EB%82%B4%EB%B6%80-%EB%B3%80%EC%88%98-%EB%AA%A9%EB%A1%9D)
- [Repeat Trigger](https://github.com/TriggerReactor/TriggerReactor/wiki/Repeating-Trigger_kr#%EB%82%B4%EB%B6%80-%EB%B3%80%EC%88%98-%EB%AA%A9%EB%A1%9D)

이런 내부변수는, 따로 사용자가 지정하지 않아도 사용가능한 특수한 변수입니다. 예를 들어보겠습니다.

다음 코드는 CommandTrigger에서 작성된 코드입니다.
```
#MESSAGE player
```
다른 변수였다면, 지정되지 않아서 [null](https://github.com/TriggerReactor/TriggerReactor/wiki/Variables_kr#null)이 출력되었겠지만, 변수안에 값이 있어, player가 정상적으로 출력되는걸 볼 수 있습니다.

그렇기 때문에 CommandTrigger에서, `./명령어 테스트` 같은 명령어를 구현하고자 할 때, 다음과 같이 구현할 수 있습니다.
```
IF argslength == 1 //명령어를 입력했을 때, 지정된 값보다 큰 배열을 가져오려고 할 때 발생하는 오류를 막기위한 조건문
  IF args[0] == "테스트" // "./명령어 테스트" 에서 '테스트' 를 가져와서 판별하는 조건문
    #MESSAGE "테스트가 완료되었습니다!"
  ENDIF
ENDIF
```

## player 변수
**player 변수**는 트리거에서 특별한 변수입니다.
이 변수는 트리거 내에서 뿐만 아니라 Placeholder와 Executor 내에서도 사용됩니다.
즉, 자신의 트리거 구문에서 player 변수를 수정하면, 대상 정보를 필요로 하는Placeholder(이를테면 $playername) 와 Executor(이를테면 #MESSAGE) 에서는 이 변수의 변경을 수용하여 대상자가 변경됩니다.

CustomTrigger과 RepeatingTrigger과 같이, player 변수가 자동으로 정의되지 않는 경우가 있는 트리거에서는 이 player 변수를 지정해줌으로써 대상 정보를 필요로 하는 Executor과 Placeholder을 사용할 수 있게 됩니다.

예를 들어,

    player = player("MidnightSugar")
    #MESSAGE "제 이름은MidnightSugar 입니다!"
    player = player("wysohn")
    #MESSAGE "제 이름은 wysohn 입니다!"

위 구문은 처음으로 MidnightSugar에게 메시지를 보내고, player 변수의 대상자를 wysohn으로 변경함으로써 두 번째로 wysohn에게 보낼 것입니다.

위와 같은 특징을 이용하여, 개별반복(foreach) 형식의 반복문에서 활용하면 모든 온라인 플레이어에게 메시지를 보내는 구문을 더 간단하게 할 수 있습니다.

    FOR player = getPlayers()
        #MESSAGE "이 메시지는 모든 플레이어에게 보내집니다."
    ENDFOR
