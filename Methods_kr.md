트리거 리액터를 이용 하면 자바의 메소드에 **직접** 액세스가 가능해집니다. 이 말은 즉 스크립트 내에서 불가능 한 것이 없다는 것 입니다.

하지만 메소드를 이용 하시려면 기본적인 자바 지식이 조금 필요합니다. 이 글에서는 조금의 기본 지식을 배워서 스크립트 내에서 사용 가능하게 될 수 있게 도와줄 내용들이 있습니다.

## 메소드란 무엇인가?

**메소드** 라는것은 자바에서 *"함수"* 를 말하는 것 입니다.</br>
여기서 함수란, 어떤한 값이 들어가면 어떤 값이 나오는게 함수입니다.

![Function](https://github.com/Cupelt/Cupelt/assets/57065968/bc2c8d55-2577-45d4-afcc-81f328aab44e)

## Javadoc 읽기
메소드를 완벽하게 활용하려면 Javadoc 을 읽고 이해 할 수 있어야합니다.</br>
먼저 [CommandTrigger 내부 변수](https://github.com/TriggerReactor/TriggerReactor/wiki/Command-Trigger_kr#%EB%82%B4%EB%B6%80-%EB%B3%80%EC%88%98)의 [Player](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/entity/Player.html)를 살펴 보겠습니다.

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
