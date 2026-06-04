# CRUD Mapping Analyzer — 配布

ASP.NET Web Forms（`*.aspx.vb` / 型付きDataSet `*.xsd` / `*.aspx`）アプリを静的解析し、
**「どのファイルが・どのテーブルに・どのCRUD操作（Create / Read / Update / Delete）をしているか」**
をマトリクス（CSV / Excel）として出力するツールの配布用リポジトリです。

> このリポジトリは **exe の配布専用** です。ソースコードは非公開リポジトリで管理しています。

## ダウンロード

最新版はこちら 👉 **[Releases](../../releases/latest)** から `crud-analyzer-gui.exe` をダウンロード

- Windows 64bit / **インストール不要**（Python も不要）
- exe をダブルクリックで起動

## 使い方

1. `crud-analyzer-gui.exe` をダブルクリックで起動
2. 「解析対象」で対象アプリのフォルダを選ぶ
3. **「▶ 解析する」** を押す
4. 「マトリクス / 明細 / 診断」タブで結果をその場で確認（並べ替え・絞り込み・行詳細）
5. 結果は CSV / Excel でも出力されます（外部通信は一切なし・完全ローカル動作）

## 主な機能

- インラインSQL / StringBuilder構築 / xsd CommandText / .aspx DataSource を解析
- TableAdapter 経由の間接CRUDも紐付け
- テーブルを特定できなかった箇所の「取りこぼし診断」レポート
- 外部送信なし。解析対象のソースは手元から一切出ません

## 動作環境

Windows 10 / 11（64bit）。追加のランタイム不要。
