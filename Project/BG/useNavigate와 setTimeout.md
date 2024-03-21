💕 구현해야 하는 것 :
이전 페이지에서 나왔던 카드목록을 받아와서 그 중 하나를 보여줘야 함, 그런데 사용자가 짝지카드를 선택지에서 골라야 해서 짝을 맞추어 넘겨받아야 함.

<br>

어떻게 구현할까 생각해보았는데,

리스트 안의 리스트로 만들어야 하나 ? => 취소 ❣ 생각해보니 그냥 사용 목록에 따라 인덱스를 이용하면 됨. 이럴 때마다 알고리즘 푸는 것이 도움이 되는 것 같당 ㅋㅋ

리스트 랜덤순서로 그림카드나 숫자카드가 나옴 -> 짝지인 카드 맞추기 (인덱스 이용)
선택지 카드 목록 : 전체카드 9개 랜덤 출몰 + 짝지카드(인덱스가 같은 카드)

### 이동하기

useNavigate import함

```
import { useLocation, useNavigate } from "react-router-dom";
const navigate = useNavigate();

navigate("/game/guess", {
          state: { step: step },
          usedNumberCards: usedNumberCards,
          usedPictureCards: usedPictureCards,
        });
```

다음 페이지에서 화면에 나온 카드가 나타나도록 같이 넘겨줌

그런데 마지막 카드가 보이기 전에 다음 페이지로 이동되었다.
그래서 setTimeout함수를 사용해줌 !

```
setTimeout(() => {
        navigate("/game/guess", {
          state: { step: step },
          usedNumberCards: usedNumberCards,
          usedPictureCards: usedPictureCards,
        });
      }, 3000); // 3초 후에 이동
    }
```

setTimeout() :자바스크립트의 함수, 첫번째 매개함수는 실행할 함수이고 두번째 매개함수는 함수 실행 전 기다려야 할 시간
