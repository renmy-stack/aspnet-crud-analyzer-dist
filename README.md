# CRUD Mapping Analyzer — 配布

ASP.NET Web Forms（`*.aspx.vb` / 型付きDataSet `*.xsd` / `*.aspx`）アプリ、および
**通常のSQL / SQL Server T-SQL / Oracle PL/SQL** のソースファイルを静的解析し、
**「どのファイルが・どのテーブルに・どのCRUD操作（Create / Read / Update / Delete）をしているか」**
をマトリクス（CSV / Excel / HTML）として出力するツールの配布用リポジトリです。

> このリポジトリは **exe の配布専用** です。ソースコードは非公開リポジトリで管理しています。

## ダウンロード

最新版はこちら 👉 **[Releases](../../releases/latest)** から `crud-analyzer-gui.exe` をダウンロード

- Windows 64bit / **インストール不要**（Python も不要）
- exe をダブルクリックで起動

## 使い方

1. `crud-analyzer-gui.exe` をダブルクリックで起動
2. 「解析対象」で対象アプリのフォルダを選ぶ
3. **「▶ 解析する」** を押す
4. 「マトリクス / テーブル別 / テーブル集計 / 明細 / 診断」タブで結果をその場で確認（並べ替え・絞り込み・行詳細）
5. **「🌐 HTMLを開く」** で単一HTMLレポートをブラウザ表示。結果は CSV / Excel でも出力されます（外部通信は一切なし・完全ローカル動作）

## 主な機能

- インラインSQL / StringBuilder構築 / xsd CommandText / .aspx DataSource を解析
- **通常SQL / SQL Server T-SQL / Oracle PL/SQL の `.sql` 系ファイルも解析**
  （対象拡張子: `.sql` `.pks` `.pkb` `.pls` `.prc` `.fnc` `.trg` ほか。判定は拡張子でなく中身で行うため、
  PL/SQL が `.sql` で置かれていても、標準SQL・T-SQL・PL/SQL が混在していても自動で解釈します）
- **テーブル中心ビュー**：「テーブル別」＝このテーブルを触る全ファイル一覧（影響範囲調査）／
  「テーブル集計」＝触られている数の多い順（ホットスポット＝密結合の発見）
- **単一HTMLレポート `crud_report.html`**：Excel不要・**完全オフライン**でブラウザ閲覧。ホットスポット棒グラフ、
  ソート/絞り込み可能な各表、依存グラフ（Mermaidソース）を1ファイルに同梱
- **ストアド定義からテーブル追跡**：`CREATE PROCEDURE/FUNCTION` の定義が解析対象にあれば、
  `EXEC` 呼び出しを proc が実際に触るテーブルへ展開し呼び出し元に紐付け（`via-proc`）
- TableAdapter 経由の間接CRUDも紐付け
- テーブルを特定できなかった箇所の「取りこぼし診断」レポート
- 外部送信なし。解析対象のソースは手元から一切出ません

### 再ビルド不要の現場調整（設定ファイル）

解析対象フォルダ直下に `crud_config.json` を置くと、**exe を変えずに**挙動を調整できます（すべて任意）。

- `exclude` … 解析から除外するファイル（自動生成Designer / obj / Tests など）
- `table_aliases` … テーブル名の名寄せ（表記ゆれの統合）
- `extra_stopwords` … テーブル名として扱わない語を追加
- `sql_extensions_extra` … 解析するSQL拡張子を追加

### 対応する方言の主なポイント

- 識別子: `[角括弧]`(T-SQL) と `"ダブルクォート"`(Oracle) の両対応（スペース入りも可）
- 既定スキーマ `dbo.`(T-SQL) は除去、Oracle のスキーマ（`hr.` 等）は保持
- T-SQL の `GO` バッチ区切り、`MERGE … USING` の源テーブル（Read）を認識
- 動的SQL（`EXECUTE IMMEDIATE` でテーブル名が変数）は推定せず診断レポートに列挙

## 動作環境

Windows 10 / 11（64bit）。追加のランタイム不要。
