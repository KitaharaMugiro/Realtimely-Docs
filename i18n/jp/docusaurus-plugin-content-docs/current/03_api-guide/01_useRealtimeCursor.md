---
sidebar_position: 1
---

# useRealtimeCursor
本メソッドが実施することは以下になります

* マウスの動きを監視し、clientX, clinentYをstateに保存する
* 500msのインターバルで、URL, clientX, clientY, ユーザ情報(ランダムに振られた名前、アバター、色)をサーバに送ります
* WebSocketでサーバ上で同一のURLに該当する他のユーザの情報が追加された場合、それを取得します
* 他のユーザのまとめてリストで保持し、画面上に描画する関数を定義します

本メソッドは２つの関数を返します。
* `onMouseMove`
* `renderCursors`

## onMouseMove
この関数はマウスイベントを処理する関数になっています。
全画面をカバーしているルートに近い要素にonMouseMoveに当ててください。

```tsx
<div onMouseMove={onMouseMove}>
```

## renderCursors
リアルタイムに取得したマウスの位置情報とユーザ情報(ランダムに振られた名前、アバター、色)を描画する関数になっています。

```tsx
return (
  <div>
    {renderCursors()}
  </div>
);
```

`renderCursors`の引数にカーソルのカスタムビューを生成する関数を入れることができます。

```tsx
const customView = (param: CustomCursorViewParameter) => {
    return (<CursorEye userInfo={param.userInfo} />)
}

return (
  <div>
    {renderCursors(customView)}
  </div>
);
```

## カスタム情報を付与してカスタムビューを描画する
`useRealtimeCursor`の第二引数にString形式でカスタムの情報を付与することができる。
この情報を付与すると、`CustomCursorViewParameter`の`customInfo`にその情報へアクセスが可能になるため、カスタムビューを作成する際にその情報を利用することができる。

```tsx
const [customUserInfo, setCustomeUserInfo] = useState({ name: "", id: "" })
const { onMouseMove, renderCursors } = useRealtimeCursor(100, JSON.stringify(customUserInfo))

useEffect(() => {
    const id = uuidv4()
    const name = id.substring(0, 5)
    setCustomeUserInfo({ name, id })
}, [])

/**カスタムビューを設定したい場合 */
const customView = (param: CustomCursorViewParameter) => {
    console.log({ customInfo: param.customInfo })
    return (<Cursor userInfo={param.userInfo} />)
}
```


## delete time
ユーザがオフラインになると、サーバへデータが送られなくなります。
各データにはサーバで振り分けたdelete timeが設定されており、`useRealtimeCursor`ではdelete timeを超えたデータは取り除きます。
delete timeは１０秒で固定しております。
この設定値を変えたい場合は、[自分でバックエンドを構築する](/docs/how-it-works/self-backend)を参照ください。

