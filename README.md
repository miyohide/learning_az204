# AZ-204試験勉強メモ

## Service Busのトピックフィルター

- bool値フィルター
    - すべての着信メッセージがサブスクリプションに選択される（true）、あるいは受信メッセージのいずれもサブスクリプションに選択されない（false）のいずれか
- SQLフィルター
    - 受信メッセージのユーザー定義のプロパティとシステムプロパティに対して、ブローカーで評価されるSQL
- 相関関係フィルター
    - 受信メッセージのユーザー及びシステムプロパティの一つ以上と照合される条件セット。

できる限り相関関係フィルターを利用する

see. https://docs.microsoft.com/ja-jp/azure/service-bus-messaging/topic-filters

## Azure StorageのBLOB層の設定をRESTで行う

PUTメソッドを使って`comp=tier`というクエリ文字列を投げる。

see. https://docs.microsoft.com/ja-jp/rest/api/storageservices/set-blob-tier

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

## Application Insightsでの機能

- Funnels
    - ユーザーに対する洞察を取得し、手順ごとのコンバージョンレートを監視する
    - 製品の購入に最も頻繁に関連するユーザーがアクセスしたページ
- Impact
    - 読み込み時間とその他のプロパティがアプリの様々な部分のコンバージョン率に及ぼす影響について分析する
- Retention
    - アプリに戻るユーザーの数、およびそのユーザーが特定のタスクを実行したり目標を達成したりする頻度を分析する
- User Flows
    - ユーザーがサイトのページ間および機能間をどのように移動しているかを目を見てわかるようにする。以下の疑問の答えを得るのに役立つ。
        - ユーザーは対象サイトのページから他のサイトにどのように移動しているのか
        - ユーザーは対象サイトのページで何をクリックしているのか
        - 対象サイト内でユーザーが他のサイトに移動するのが最も多い場所はどこか
        - ユーザーが同じ操作を何回も繰り返している場所があるか

- Users
    - どれぐらいの人がアプリを使い、どれぐらいの人がそのページを見たかを知る

## Event Hubs Capture

- 選択したAzure Blob StorageまたはAzure Data Lake Storageアカウント内のEvent Hubsのストリーミングデータを自動的にキャプチャするもの。
- ファイル名は`https://<storageaccount>.blob.core.windows.net/<container>/<namespace>/<eventhub>/<partitionid>/<year>/<month>/<day>/<hour>/<minute>/<second>.avro`になる

## Azure Cosmos DBにサポートされているAPI

- MongoDB
    - ドキュメント指向データベースのMongoDBのAPIと互換なもの
- Table
    - 既存のAzure Tableストレージアプリにプレミアム機能を提供するために構築されたキー値データベース
- Gremlin
    - グラフデータを格納及び操作するために使用する
- Cassandra
    - キー・バリュー型データストアを提供する分散データベース管理システムであるCassandraのAPIと互換なもの
- SQL
    - SQLクエリに根ざしたクエリ機能を提供。JavaScriptおよびJSONネイティブAPI。

## App Serviceでのアプリの診断ログの有効化

see. https://docs.microsoft.com/ja-jp/azure/app-service/troubleshoot-diagnostic-logs

## B2B Logic Appsの構築を開始するための手順

1. 統合アカウントを作成する
2. パートナー、契約、その他の成果物を追加する
3. ロジックアプリの作成
4. ロジックアプリを統合アカウントにリンクする
5. 成果物を含むロジックアプリをビルドする

## カスタムコネクタの作成

1. ユーザーのAPIを作成し、安全を確保する
2. ユーザーのAPIの説明をし、コネクタを規定する
3. ユーザーのコネクタを使用する
4. ユーザーのコネクタを共有する（オプション）
5. ユーザーのコネクタを保証する（オプション）

## Azure ADのアプリマニフェスト

Azure ADの属性を設定するファイル。ポータルでできない項目があるのでこのファイルで設定する。

see. https://docs.microsoft.com/ja-jp/azure/active-directory/develop/reference-app-manifest

- allowPublicClient
- oauth2AllowImplicitFlow
    - OAuth2.0暗黙的フローアクセストークンを要求できるかどうか。SPAなどで利用。

## Azure ADに登録できる「アプリ」「リソース」「API制限」の解説

see. https://jpazureid.github.io/blog/azure-active-directory/oauth2-application-resource-and-api-permissions/

## 機密クライアントとパブリッククライアント

Microsoft認証ライブラリ（MSAL）では、機密クライアントとパブリッククライアントの2種類のクライアントが定義されている。

- 機密クライアントは、サーバー（Webアプリ、WebAPIアプリ、サービス／デーモンアプリ）で実行されるアプリ。クライアントIDはWebブラウザを通じて公開されるが、シークレットはバックチャンネルでのみ渡され直接公開されない。`ConfidentialClientApplication`クラスを使用する。
- パブリッククライアントは、デバイス、デスクトップコンピューター、またはWebブラウザで実行されるアプリ。安全にアプリケーションシークレットを保持することは信頼されていないので、ユーザーの代理でWebAPIにのみアクセスする。`PublicClientApplication`クラスを使用する。

こんな感じで実装。

```csharp
IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(clientId)
    .WithClientSecret(clientSecret)
    .WithRedirectUri("https://foobar.net")
    .build();
```

機密クライアントのみに存在する装飾子として

- `.WithCertificate`
- `.WithClientSecret`

がある。

## Azure CDNのキャッシュ動作の設定

- キャッシュのバイパス
    - キャッシュを行わず、もともと指定されているキャッシュディレクティブヘッダーを無視する
- オーバーライド
    - もともと指定されているキャッシュ期間を無視し、代わりに指定したキャッシュ期間を使う。これは、`cache-control`の`no-cache`をオーバーライドしない。
- 存在しない場合に設定
    - キャッシュディレクティブヘッダーがもともと指定されていた場合はそれにしたが、指定されていなかった場合は、設定したキャッシュ期間を使う。

see. https://docs.microsoft.com/ja-jp/azure/cdn/cdn-caching-rules

キャッシュディレクティブヘッダーについては、以下を参照のこと。

https://docs.microsoft.com/ja-jp/azure/cdn/cdn-how-caching-works#cache-directive-headers
