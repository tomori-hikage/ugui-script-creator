# ugui-script-creator

ugui-script-creatorはuGUIをスクリプトで構築するためのAssetです

## 導入方法

ugui-script-creator.unitypackageをプロジェクトにインポートしてください
UICreator.csを直接プロジェクトにインポートしていただいても問題ありません

## 使用方法

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

![実行結果](https://github.com/tomoriaki/ugui-script-creator/blob/readme_images/Images/ss.png)

## 配布ライセンス

MIT / X11ライセンスで公開いたします

## 使用ライセンス

ugui-script-creatorはUnity-Technologies / UIをベースに作成しています
[Copyright (c) 2014-2015, Unity Technologies](https://bitbucket.org/Unity-Technologies/ui/src/0155c39e05ca5d7dcc97d9974256ef83bc122586/LICENSE?at=5.2&fileviewer=file-view-default)
