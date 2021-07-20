﻿# モジュール 3 - ソース ファイルに関するデータ エンジニアリングの考慮事項

このラボでは、ひとりまたはグループで20分間、以下の情報を読むよう講師から指示されます。その後、質問に答え、要件に基づいて見つけた結果を教室内で発表します。 

## チームのホワイトボード アクティビティ

ワイド・ワールド・インポーターズ (WWI) は、売上トランザクションを Oracle データベースのテーブルからデータ レイクにコピーするパイプラインを構築する計画です。

**要件**

* データをコピーするパイプラインは、スケジュールに基づいて毎日 1 回実行されます。
* 同社は、この生データを取り込み、最小限の変換を適用したいと考えています。
* データ レイクには常にオリジナル データのコピーが含まれ、ダウンストリーム処理で計算や変換エラーが発生しても、常にオリジナルから再計算できるようにします。
* また、選択したファイル形式がなるべく広範囲の業界標準ツールで使用できることを確認し、データの調査と処理を行うツールが限定されるファイル形式は避けることを希望しています。
* フォルダー構造は、このタイプのデータの典型的な探索と分析クエリで使用できるものでなくてはなりません。  

**データの例**

WWI からはデータの例として以下が提供されました。データの*最も*代表的な行を選択したものと想定されます。

|SaleKey|CityKey|CustomerKey|BillToCustomerKey|StockItemKey|DeliveryDateKey|SalespersonKey|WWIInvoiceID|Description|Package|Quantity|UnitPrice|TaxRate|TotalExcludingTax|TaxAmount|Profit|TotalIncludingTax|TotalDryItems|TotalChillerItems|LineageKey
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- 
|294018|98706|0|0|25|2012/01/04|156|57894|Black and orange, handle with care despatch tape 48mmx75m|Each|144|3.70|15.000|532.80|79.92|345.60|612.72|144|0|14
|294019|98706|0|0|216|2012/01/04|156|57894|USB, food flash drive - sushi roll|Each|5|32.00|15.000|160.00|24.00|100.00|184.00|5|0|14
|294020|98706|0|0|168|2012/01/04|156|57894|IT joke mug - keyboard not found � press F1 to continue (White)|Each|10|13.00|15.000|130.00|19.50|85.00|149.50|10|0|14
|294021|98706|0|0|100|2012/01/04|156|57894|Dinosaur battery-powered slippers (Green) L|Each|4|32.00|15.000|128.00|19.20|96.00|147.20|4|0|14

## ホワイトボード

イベント用のホワイトボードを開きます。 「アクティビティ 1」 のエリアに以下の課題に対する答えを書き込んでください。

*以下の課題はすでにホワイトボードのテンプレートに含まれています。*

課題

1. 生データでは、どのファイル形式を使用すべきですか? このファイル形式を推奨するのはなぜですか? その理由を 2 つ以上挙げてください。

2. WWI は、データセットをディスクにシリアル化する際、どの特定の設定を使用する必要がありますか (特に`Description`フィールドに注意してください)? これを提案するのはなぜですか?

3. 階層型ファイル システムでの使用を推奨するフォルダー構造を図示してください。必ずファイル システムとフォルダーを指摘し、各レイヤー (ファイル システム、フォルダー、ファイル) の名前の由来を説明してください。

4. 使用しているフォルダー構造は、このタイプのデータで典型的な探究的および分析的クエリのパフォーマンスをどのようにサポートしますか?

5. WWI はこのデータを機密とみなします。競合他社がこれを手に入れると、取り返しのつかない危害が発生する可能性があるためです。どのようにしてデータ レイクをデプロイし、データ レイクのエンドポイントへのアクセスを保護するのか図示してください。必ずデータが Azure Synapse Analytics Workspace とデータ レイク間でどのように流れるのか、また、なぜこれによって WWI の要件に対応できるのか説明してください。パレットのアイコンを使用してソリューションを図示してください。

6. WWI は、売上データへのどのような変更も当年度のみで行い、許可のあるユーザー全員がデータ全体でクエリを実行できるようにしたいと考えています。以前に WWI に推奨していたフォルダー構造に関し、これをRBAC と ACL を使用して達成するにはどうすればよいですか? 2020年の初めと終わりにどのようなアクションを取る必要があるのか説明してください。ここに示されているパレットを使い、セキュリティ グループ、組み込まれている役割、アクセス許可を図示してください。