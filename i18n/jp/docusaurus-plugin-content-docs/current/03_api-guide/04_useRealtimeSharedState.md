---
sidebar_position: 4
---

# useRealtimeSharedState

本メソッドは、Reactの`useState`のように使えてt、状態の変化をサーバに送り同じURLを見ているすべてのユーザにその状態を共有することができます。

```tsx
const [state, setState] = useRealtimeSharedState({color:"red", number:3}, "slideState") 
```

`useRealtimeSharedState`は第一引数にdefault値、第二引数にactionIdを指定します。
actionIdは同一URL内で一意になっていれば任意の文字列で問題ありません。

本メソッドは1つの変数と1つの関数をペアとした配列を返します。
`useState`と同じように、１つ目の返り値が状態を格納し、２つ目の返り値を使って状態を更新します。

URLとactionIdをペアにして、値をサーバに送信し管理します。

## 初回レンダリング時
初回レンダリング時にサーバから最新の値を取得します。取得できなかった場合はdefault値を採用します。

## 値の更新時
更新があると同じURLを見ている全ユーザに最新の値を配信します。

