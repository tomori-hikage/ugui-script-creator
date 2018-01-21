# ugui-script-creator

## Description

ugui-script-creatorはuGUIをスクリプトで構築するためのAssetです

※ 独自のスプライトを使用する場合やエディタ実行のみで使用する場合はResources/ugui-script-creatorフォルダを削除していただいても問題ありません

## Demo

![実行結果](https://github.com/tomoriaki/ugui-script-creator/blob/readme_images/Images/result2.gif)

## Installation

ugui-script-creator.unitypackageをプロジェクトにインポートしてください

## Usage

```csharp
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.UI.Utility;


public class Example : MonoBehaviour
{
    #region event
    private void Start()
    {
        // EventSystemが存在しない場合一緒に生成します
        Canvas canvas = UICreator.CreateCanvas();


        // キャンバスの子としてテキストを生成する
        Text text = UICreator.CreateText(canvas.gameObject);
        text.rectTransform.localPosition = Vector3.left * 140f;
        text.text = "Hello World!!";
        text.alignment = TextAnchor.MiddleCenter;
        text.color = Color.green;

        // オブジェクト名やコンポーネントの初期値を設定する
        Dropdown dropdown = UICreator.CreateDropdown(canvas.gameObject, "Gender", "性別");
        dropdown.GetComponent<RectTransform>().localPosition = Vector3.right * 140f;
        dropdown.options.Clear();
        dropdown.options.Add(new Dropdown.OptionData { text = "男性" });
        dropdown.options.Add(new Dropdown.OptionData { text = "女性" });
    }
    #endregion
}
```

![実行結果](https://github.com/tomoriaki/ugui-script-creator/blob/readme_images/Images/result1.png)

```csharp
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.UI.Utility;
using UniRx;


public class Example : MonoBehaviour
{
    #region event
    private void Start()
    {
        Canvas canvas = UICreator.CreateCanvas();


        Button button = UICreator.CreateButton(canvas.gameObject, "Random", "ランダム");
        button.GetComponent<RectTransform>().localPosition = Vector3.left * 140f;
        button.OnClickAsObservable()
            .Subscribe(_ => Camera.main.backgroundColor = new Color(Random.Range(0f, 1f), Random.Range(0f, 1f), Random.Range(0f, 1f)));

        Image image = UICreator.CreateImage(canvas.gameObject, "Background");
        image.rectTransform.localPosition = Vector3.right * 140f;
        image.color = new Color(250f / 255f, 120f / 255f, 255f / 255f);
        Toggle toggle = UICreator.CreateToggle(image.gameObject, "Interactable", "Interactable");
        toggle.GetComponent<RectTransform>().localPosition = Vector3.right * 30f;

        toggle.OnValueChangedAsObservable()
            .Subscribe(interactable => button.interactable = interactable);
    }
    #endregion
}
```

![実行結果](https://github.com/tomoriaki/ugui-script-creator/blob/readme_images/Images/result2.gif)

## Reference

| メソッド名 | 機能 | 備考 |
|:-----------|:-----------|:-----------|
| CreateCanvas | Canvasを生成する | EventSystemがシーン上に存在しない場合は生成する |
| CreateEventSystem | EventSystemを生成する |  |
| CreatePanel | Panelを生成する |  |
| CreateButton | Buttonを生成する |  |
| CreateText | Textを生成する |  |
| CreateImage | Imageを生成する |  |
| CreateRawImage | RawImageを生成する |  |
| CreateSlider | Sliderを生成する |  |
| CreateToggle | Toggleを生成する |  |
| CreateInputField | InputFieldを生成する |  |
| CreateDropdown | Dropdownを生成する |  |
| CreateScrollView | ScrollViewを生成する |  |

## Author

[Twitter: @tomoriaki](https://twitter.com/tomoriaki)
[Qiita: @tomoriaki](https://qiita.com/tomoriaki)

## Distribution License

[MIT](https://github.com/tomoriaki/ugui-script-creator/blob/master/LICENSE)

## Use License

ugui-script-creatorはUnity-Technologies / UIをベースに作成しています

[Copyright (c) 2014-2015, Unity Technologies](https://bitbucket.org/Unity-Technologies/ui/src/0155c39e05ca5d7dcc97d9974256ef83bc122586/LICENSE?at=5.2&fileviewer=file-view-default)
