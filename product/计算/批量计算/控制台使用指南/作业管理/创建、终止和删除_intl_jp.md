## ジョブの作成

ジョブの説明については、[名詞の説明](https://cloud.tencent.com/document/product/599/10396)の「ジョブ」を参照してください。[Batchコンソール]()を通してジョブを作成できます。

1. [Batchコンソール]()にログインします。まだBatchサービスを有効化していない場合は、Batchコンソールのホームページに関連する指示を参照してください。

2. 左側のナビゲーションバーの「ジョブ」オプションをクリックし、目標地域を選択して【新規作成】ボタンをクリックします。
![1](https://main.qcloudimg.com/raw/ee1ae2a02fa59c956086c8dd4290fb07.png)

3. ジョブの基本情報を構成します。

![2](https://main.qcloudimg.com/raw/8b563fe289624c4ce90fffac08b4f708.png)

4. 「タスクフロー」の左側にあるタスクテンプレートを選択し、マウスを動かしてタスクを右側のキャンバスに配置し、アンカーをドラッグアンドドロップして接続を確立します。

 ![3](https://main.qcloudimg.com/raw/2d57e9a9e558ae2af35c2e6ea272afc6.png)

5. 「タスクフロー」の右側にある「タスク詳細」を開き、正しいことを確認したら、【完了】ボタンをクリックします。
   + ジョブタスクフローでは、各タスクはタスクテンプレートに基づいてカスタマイズされます。
   + 右側の「タスク情報」オプションを開き、あるタスクを選択して、該当タスクの一部分の構成を編集することができます。編集操作はタスクテンプレートには影響しません。
   
   ![4](https://main.qcloudimg.com/raw/871a36decb2a133a169473cd2f9cd227.png)
   
## ジョブ終了
特定の条件下でジョブの実行を終了することができます。終了に関する説明については、APIドキュメント[タスクインスタンスの終了](https://intl.cloud.tencent.com/document/product/599/12688)を参照してください。

## ジョブ削除
ジョブが最終状態のSUCCEEDまたはFAILED状態にあるときは、ジョブリストからジョブを削除できます。

![5](https://main.qcloudimg.com/raw/f7d584bde4cc8654eca12e394e01c458.png)




