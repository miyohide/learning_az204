# AZ-204試験勉強メモ

## Service Busのフィルター

- bool値フィルター
- SQLフィルター
- 相関関係フィルター

see. https://docs.microsoft.com/ja-jp/azure/service-bus-messaging/topic-filters

## Azure StorageのBLOB層の設定をRESTで行う

PUTメソッドを使って`comp=tier`というクエリ文字列を投げる。

see. https://docs.microsoft.com/ja-jp/rest/api/storageservices/set-blob-tier

## Azure ADのアプリケーションマニフェスト

see. https://docs.microsoft.com/ja-jp/azure/active-directory/develop/reference-app-manifest

## AzureリソースのマネージドID

see. https://docs.microsoft.com/ja-jp/azure/active-directory/managed-identities-azure-resources/overview

## Azure API Managementのポリシー

see. https://docs.microsoft.com/en-us/azure/api-management/api-management-access-restriction-policies

## Durable Functionsの一般的なアプリケーションパターン

- 関数チェーン
    - 関数のシーケンスが特定の順序で実行される
- ファンアウト／ファンイン
    - 複数の関数を並列に実行し、すべての関数が終了するのを待つ
- 非同期HTTP API
    - 外部クライアントとの間の実行時間の長い操作の状態を調整する。HTTPエンドポイントで実行時間の長いアクションをトリガーする。
- モニター
    - ワークフロー内の繰り返しプロセス。特定の条件が満たされるまでポーリングする
- 人による操作
    - 途中で人による操作を挟むパターン
- アグリゲーター
    - ある期間のイベントデータを1つのアドレス可能なエンティティに集計することに関連する。通常のステートレス関数で実装すると同時実行制御が大きな課題となるが、単一の関数として実装できることがメリット。

see. https://docs.microsoft.com/ja-jp/azure/azure-functions/durable/durable-functions-overview
