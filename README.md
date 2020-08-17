# manual-angular
for me


### ng-if
```html
<div ng-if="pickingItem.hapPoChk == 1">
합포
</div>
<div ng-if="pickingItem.hapPoChk != 1">
단포
</div>
```

### 길게누를경우 onhold longclick
```html

<button on-hold="onHold()"> </button>
        // 사용자 길게누를 경우
        $scope.onHold = function () {
            $scope.selectMinusAlertPopup('누적집계', '직전 집계로 되돌리시겠습니까?');
        }

    // 선택 팝업창 - 데이터의 누계감소
    $scope.selectMinusAlertPopup = function (titleTxt, messageTxt) {

        var storageName = 'ngStorage-ebgEntryCheckedChanged';
        var changed = JSON.parse(localStorage.getItem(storageName));

        var myPopup = $ionicPopup.show({
            template: messageTxt,
            title: titleTxt,
            scope: $scope,
            buttons: [
                {
                    text: '<b>확인</b>',
                    type: 'button-positive',
                    // 확인
                    onTap: function (e) {

                        // 화면에 변화가 없다면
                        if (changed === null || changed === undefined || changed === 'false' || $scope.arrClicked.length == 0) {
                            $scope.completeAlertPopup("알림", "집계감소할 항목이 없습니다.");
                        }
                        else {
                            // 버튼을 누를때마다, stack에 추가한다
                            // stack을 감소시키면서, 집계값을 감소한다.
                            $scope.restoreClicked();

                            // 닫기
                            myPopup.close();
                            e.preventDefault();

                        }
                    }
                },
                { text: '취소' }
            ]
        });
        // 취소
        myPopup.then(function (res) {
        });
    };

```
