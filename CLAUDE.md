# 技術スタック・開発ルール(poem-runo)

このリポジトリ、および関連プロジェクト(`open-runo`/`open-web-server`/
`aruaru-db`/`aruaru-web`/`open-raid-z`)で開発・保守を行う際は、以下を基本方針とする。
作業ドライブは `F:\open-runo`(E:ドライブは2026-07-10に消失、以後Fが実体)。
この節は [`open-raid-z`](https://github.com/aon-co-jp/open-raid-z) の
`CLAUDE.md` を正本とし、各プロジェクトへコピーして同期する。

**poem-runo とは**: `open-runo`(Rust + Poem 製 GraphQL Federation
プラットフォーム)を正本として `F:\open-runo\open-runo` から `git clone` した
後継リポジトリ(https://github.com/aon-co-jp/poem-runo)。REST API の乱立と
WunderGraph Cosmo 有料版への依存を断つという open-runo の目的を、Poem
フレームワークとの統合をリポジトリ名として明示する形で引き継ぎ、発展させる。
履歴は open-runo のものをそのまま保持しているため、両リポジトリのコミット
ログは 2026-07-10 の分岐点まで共通。今後の開発は poem-runo 側を主軸に進める。

## フロントエンド

- **Tauri**(メインフレームワーク): https://v2.tauri.app/ | https://github.com/tauri-apps/tauri
- HTML5 / CSS3
- **TypeScript**: 必要最低限・最小限の範囲に留める(ロジックはRust側に置き、
  TypeScript側はDOM操作・`invoke()`呼び出し等の薄い配線のみとする方針)
- **Bootstrap**

## バックエンド・コア

- **Rust**(メイン言語): https://www.rust-lang.org/ja/ | https://github.com/rust-lang/rust
- **Poem**(Webフレームワーク): https://docs.rs/poem/latest/poem/ | https://github.com/poem-web/poem

## API設計思想(参考・概念のみ)

- **VersionLess API**という考え方を参考にする(WunderGraphのブログ/podcast参照)。
- **WunderGraph Cosmo**: あくまで**参考・着想元としてのみ**参照する。
  **実装には絶対に使用しない**。https://github.com/wundergraph/cosmo

## 関連プロジェクト

- **poem-runo**(このリポジトリ。open-runo の後継。GraphQL Federation /
  API Gateway / AI-native routing platform): https://github.com/aon-co-jp/poem-runo
- **open-runo**(分岐元。引き続き独自にメンテナンスされる場合がある):
  https://github.com/aon-co-jp/open-runo
- **open-web-server**: https://github.com/aon-co-jp/open-web-server
- **aruaru-db**: https://github.com/aon-co-jp/aruaru-db
- **aruaru-web**: https://github.com/aon-co-jp/aruaru-web
- **open-raid-z**(開発ルールの正本): https://github.com/aon-co-jp/open-raid-z
- **rs-to-readme**: https://github.com/aon-co-jp/rs-to-readme

## 運用ルール

- **開発中はこの`CLAUDE.md`を、コード変更のコミット/pushと必ず一緒に
  push する**(内容を更新した場合はもちろん、変更が無い場合も他の変更と
  一緒にコミット対象へ含めておくこと)。
- 実装で迷った場合や、API仕様の詳細確認が必要な場合は、学習データからの
  推測より公式ドキュメント(上記URL)を優先して参照する。
- 作業ドライブが変わった場合は、この節を更新し、関連プロジェクトの
  引き継ぎ資料にも変更の経緯を記録すること。

## 現状(このリポジトリ固有)

- `cargo check --workspace` / `cargo test --workspace --no-run` は成功する
  (15クレート構成、テストコンパイル済み)。todo!()/unimplemented!()マーカーなし。
- README多言語版は `README-<言語>.md` 形式で日本語・英語・中国語簡体字・
  韓国語・スペイン語・フランス語・ドイツ語・イタリア語・ロシア語・
  アラビア語の10言語が揃っている。

## HANDOFF(直近の自動実行パス)

- **2026-07-10 20:30 poem-runo 発足**: `open-runo` を正本として
  `F:\open-runo\open-runo` から `git clone` し、リモートを
  `https://github.com/aon-co-jp/poem-runo.git` に付け替えて push、
  `poem-runo` リポジトリを発足させた(履歴は open-runo と共通)。
  無人自動開発を 2026-07-11 12:00 まで継続する運用中。21:30 に安全のため
  push、21:40 前後で利用制限のリセットが想定されるが、回復後は
  scheduled task 経由でこの CLAUDE.md の HANDOFF を読み、続きから開発を
  再開すること。次回パスがまず行うべきこと: (1) このリポジトリ固有の
  README.md 冒頭を poem-runo 向けに書き換え(open-runo からの fork/継承
  である旨を明記)、(2) `cargo check --workspace` で現状ビルドが壊れて
  いないことを確認、(3) `docs/HANDOFF.md` の次点候補から実装を1つ進める、
  (4) 作業ごとに commit して `git push origin main` する。
  次回パス実行時は毎回この項目を上書き更新し、進捗と次にやることを
  明記すること(セッションを跨いで記憶が引き継がれないため)。

- **2026-07-10 (open-runo 側)**: 定時の自律メンテナンスパス。`cargo check --workspace` /
  `cargo test --workspace --no-run` は変更前から成功済みを確認(ビルド破損なし)。
  `todo!()`/`unimplemented!()`/フェイクデータを返すスタブ関数は見つからず
  (実装は本当に完了している)。README-Japan.md と README-English.md が
  Phase A 以前の古い「ビジョン文書」のまま放置されており、実際の実装
  (15クレート・176テスト・自己学習AI・KeyGuardian・DUAL DATABASE・
  VersionlessAPI 等)と矛盾していた(例: 英語版は「設計・開発初期段階」
  「License TBD」「外部LLMプロバイダへのルーティング」と記載)ため、
  ルートの `README.md`(正しい最新情報)を基準に両ファイルを修正した:
  README-Japan.md はルート README.md の内容をそのまま反映、
  README-English.md は他8言語版と同じ構成(機能比較表・open-runo限定機能・
  クイックスタート・15クレート構成)の正確な英語版に書き換えた。
  他8言語版(中/韓/西/仏/独/伊/露/アラビア語)は内容確認済みで正確、変更不要。
  次回パスへの引き継ぎ: 特に緊急の課題は残っていない。次点候補は
  `docs/HANDOFF.md` の「次セッション候補」(Google Drive API 直接統合、
  FederatedBackend の TOML 設定化など)。

## API 方針: REST 全廃・gRPC / Connect へ (2026-11-04)

### 日本語
- **REST は全廃する。新しい API は REST で作らない。** ブラウザや `curl` から呼ぶ API は **Connect の単純呼び出し**(`POST /<パッケージ>.<Service>/<Method>`、`content-type: application/json`、本文は JSON)、サービス間は **gRPC / gRPC-web**(RPoem の管理API `open_runo.admin.v1.Admin` と同じ流儀)。ストリーミングは、必要になってから。
- **既存の REST は、触るときに順に移す。** 移したら旧 REST の経路は消す。移行が終わるまで残るが、**新規には追加しない**。
- **JSON は RS-JSON に統一**する(読み込みは `from_str_secure` / `parse_secure` でサイズ・深さ・重複キーの上限つき、書き出しは `rust_json::fast`)。ブラウザの WASM に `prost` は入れない(サイズが増えるため)。
- **例外(自分たちの API ではなく、相手の規格が決めているもの)**: ACME、OAuth/OIDC のコールバック、第三者(GitHub など)からの Webhook、ヘルスチェック、静的ファイル配信、OTLP など。これらは規格どおりの HTTP を受ける。
- 参考実装: `RPoem`(`open_runo.admin.v1.Admin`)、`open-easy-web`(`server/src/connect.rs`、`proto/open_easy_web/admin/v1/admin.proto`)。
- ※ このリポジトリのコードが既に方針どおりかどうかは、各リポジトリの現状による。この節は方針の記録であり、コードの変更を意味しない。

### English
- **REST is being abolished. New APIs are not built as REST.** APIs called from browsers or `curl` use **Connect unary calls** (`POST /<package>.<Service>/<Method>`, `content-type: application/json`, JSON body); service-to-service calls use **gRPC / gRPC-web** (the same style as RPoem's admin API `open_runo.admin.v1.Admin`). Streaming only when it is actually needed.
- **Existing REST endpoints are migrated one by one, when they are touched.** The old REST route is removed once migrated. Until migration is finished they remain, but **no new ones are added**.
- **JSON is unified on RS-JSON**: reading with `from_str_secure` / `parse_secure` (size, depth and duplicate-key limits), writing with `rust_json::fast`. `prost` is not put into browser WASM (it would grow the binary).
- **Exceptions (shapes dictated by someone else's standard, not our own API)**: ACME, OAuth/OIDC callbacks, webhooks from third parties (e.g. GitHub), health checks, static file serving, OTLP, and so on. These accept plain HTTP as the standard requires.
- Reference implementations: `RPoem` (`open_runo.admin.v1.Admin`) and `open-easy-web` (`server/src/connect.rs`, `proto/open_easy_web/admin/v1/admin.proto`).
- Note: whether the code in a given repository already follows this policy depends on that repository. This section records the policy; it does not mean the code has been changed.

### Deutsch (KI-Übersetzung, noch nicht von Muttersprachlern geprüft)
- **REST wird abgeschafft. Neue APIs werden nicht als REST gebaut.** APIs, die aus dem Browser oder mit `curl` aufgerufen werden, nutzen **Connect-Unary-Aufrufe** (`POST /<Paket>.<Service>/<Methode>`, `content-type: application/json`, JSON-Body); zwischen Diensten gilt **gRPC / gRPC-web** (wie bei der Admin-API von RPoem, `open_runo.admin.v1.Admin`). Streaming erst, wenn es wirklich nötig ist.
- **Bestehende REST-Endpunkte werden einzeln migriert, sobald man sie anfasst.** Nach der Migration wird die alte REST-Route entfernt. Bis dahin bleiben sie bestehen, es werden aber **keine neuen hinzugefügt**.
- **JSON wird auf RS-JSON vereinheitlicht**: Lesen mit `from_str_secure` / `parse_secure` (Grenzen für Größe, Tiefe und doppelte Schlüssel), Schreiben mit `rust_json::fast`. `prost` kommt nicht in Browser-WASM (die Datei würde größer).
- **Ausnahmen (Formate, die ein fremder Standard vorgibt, nicht unsere eigene API)**: ACME, OAuth/OIDC-Callbacks, Webhooks von Dritten (z. B. GitHub), Health-Checks, statische Dateien, OTLP usw. Diese nehmen schlichtes HTTP entgegen, wie es der Standard verlangt.
- Referenzimplementierungen: `RPoem` (`open_runo.admin.v1.Admin`) und `open-easy-web` (`server/src/connect.rs`, `proto/open_easy_web/admin/v1/admin.proto`).
- Hinweis: Ob der Code eines Repositorys diese Richtlinie schon befolgt, hängt vom jeweiligen Repository ab. Dieser Abschnitt hält die Richtlinie fest; er bedeutet nicht, dass der Code bereits geändert wurde.

### Русский (машинный перевод, носителями языка ещё не проверен)
- **REST полностью отменяется. Новые API не создаются как REST.** API, вызываемые из браузера или через `curl`, используют **унарные вызовы Connect** (`POST /<пакет>.<Service>/<Method>`, `content-type: application/json`, тело — JSON); между сервисами — **gRPC / gRPC-web** (так же, как административный API RPoem, `open_runo.admin.v1.Admin`). Потоковая передача — только когда она действительно нужна.
- **Существующие REST-эндпоинты переносятся по одному, когда до них доходят руки.** После переноса старый REST-маршрут удаляется. До завершения переноса они остаются, но **новые не добавляются**.
- **JSON унифицируется на RS-JSON**: чтение через `from_str_secure` / `parse_secure` (ограничения на размер, глубину и повторяющиеся ключи), запись через `rust_json::fast`. `prost` не добавляется в браузерный WASM (размер вырос бы).
- **Исключения (форматы, заданные чужим стандартом, а не наш собственный API)**: ACME, обратные вызовы OAuth/OIDC, вебхуки сторонних сервисов (например, GitHub), проверки работоспособности, раздача статических файлов, OTLP и т. п. Они принимают обычный HTTP, как требует стандарт.
- Эталонные реализации: `RPoem` (`open_runo.admin.v1.Admin`) и `open-easy-web` (`server/src/connect.rs`, `proto/open_easy_web/admin/v1/admin.proto`).
- Примечание: соответствует ли код конкретного репозитория этой политике, зависит от самого репозитория. Этот раздел фиксирует политику и не означает, что код уже изменён.
