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

## Azure Container Registory

### Dockerイメージをビルドしてpushする

`az acr build`を実行すると、Dockerイメージをビルドして、その後Azure Container Registoryにpushする。具体的なコマンドは以下のとおり。

```
az acr build --image イメージ名 --registry レジストリ名 --file Dockerfile .
```

### システム割り当てマネージドIDの割り当て方

VM作成時は`--assign-identity`をつける

```
az vm create --resource-group rg --name vmname --image win2016datacenter --assign-identity --admin-username azureuser --admin-password myPassword1
```

既存のVMで有効にする場合は`az vm identity assign`を実行する

```
az vm identity assign -g rg -n vmname
```

see. https://docs.microsoft.com/ja-jp/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm

### ユーザーが割り当てたマネージドIDの割り当て方

最初に`az identity create`でユーザー割り当てIDを作成する。

```
az identity create -g rg -n myUserAssignedId
```

VM作成時は作成したIDを`--assign-identity`にて指定する。

```
az vm create --resource-group rg --name vmname --image win2016datacenter --assign-identity myUserAssignedId --admin-username azureuser --admin-password myPassword1
```

既存のVMでは`az vm identity assign`を実行する。

```
az vm identity assign -g rg -n vmname --identities myUserAssignedId
```

see. https://docs.microsoft.com/ja-jp/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm

## Azureで一般化されたVMイメージを作成する

Windowsでは`Sysprep`を使って、Linuxでは`waagent`を使用する。

see. https://docs.microsoft.com/ja-jp/azure/virtual-machines/windows/capture-image-resource

see. https://docs.microsoft.com/ja-jp/azure/virtual-machines/linux/capture-image

## Azure App ServiceにおけるTLS相互認証の構成

- ASP.NETの場合は`HttpRequest.ClientCertificate`プロパティを使用
- その他は`X-ARR-ClientCert`HTTPヘッダを使用

see. https://docs.microsoft.com/ja-jp/azure/app-service/app-service-web-configure-tls-mutual-auth

## Azure Storageにおける読み取り要求の高可用性

デフォルトは`PrimaryOnly`。高可用性を求めるのであれば要変更。

see. https://docs.microsoft.com/ja-jp/azure/storage/common/geo-redundant-design#read-requests

## Azure Storage キュートService Busキューとの比較

FIFOや自動重複検出が求められるのであればService Busキュー。その他は以下URLを参照。

see. https://docs.microsoft.com/ja-jp/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted

## CosmosDBのリソース階層

以下の階層となっている。

- データベースアカウント
    - データベース
        - コンテナー
            - アイテム
            - ストアドプロシージャ
            - ユーザー定義機能
            - トリガー

## API Managementのrate-limitとquotaとの違い

- `rate-limit`は短期間の制限。
- `quota`は長期間。`renewal-period`は`3600`以上

## Azure App Serviceでのアプリの診断ログの有効化

Azure Monitorにログを送信することも可能。

see. https://docs.microsoft.com/ja-jp/azure/app-service/troubleshoot-diagnostic-logs

## Azure Container Instancesを作成する

PowerShellの場合、`New-AzContainerGroup`を使用する

## Azure Functionsのエラー処理と再試行

BLOB Storage/Queue Storage/Service Busにはトリガーソースでの再試行をサポートしている。BLOB Storage/Queue Storageは最大5回、Service Busは最大10回再試行される。

see. https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-bindings-error-pages?tabs=csharp

## ASP.NET Core向けのDockerイメージ

- `dotnet/core/sdk`はビルド用
- `dotnet/core/aspnet`は実行用

see. https://docs.microsoft.com/ja-jp/aspnet/core/host-and-deploy/docker/building-net-docker-images?view=aspnetcore-5.0

## Web AppsにCORSの設定を行う

```
az webapp cors add -g myRG -n myApp --allowed-origins https://myapps.com
```

see. https://docs.microsoft.com/en-us/cli/azure/webapp/cors?view=azure-cli-latest

## Event Grid / Event Hubs / Service Busの違い

- publish - subscribeモデルが実装できるのはEvent GridとService Bus
- Service BusはFIFOのサポートやduplicate detectionがある
- Event HubsはEvent Hubs CaptureでBlob StorageやData Lake Storageにイベントをキャプチャできる

see. https://docs.microsoft.com/ja-jp/azure/event-grid/compare-messaging-services
