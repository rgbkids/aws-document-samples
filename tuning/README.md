# 性能改善

## 遅延関連

1. AWS Elemental MediaPackage -> Channels -> {チャンネル名} -> Add/edit endpoints

- Segment duration (sec)  
1秒-2秒に設定（バッファの設定です。この値を小さくすると遅延時間が短くなりますが、再生が不安定になります）
- Live playlist window duration (sec)  
Segment duration × 3 程度に設定（m3u8ファイルに記録する全tsファイルの合計再生時間です。Segment durationが1秒なら、3秒を設定すると、3つのtsファイルが記録されます）

2. CloudFront Distributions -> {Distribution名} -> 各Path Pattern を選択 -> Edit  

- Object Caching: Customize
- Minimum TTL: 1
- Maximum TTL: 1
- Default TTL: 1

キャッシュの時間を短くしたらCloudFrontの利用価値は？  
→大量のリクエスト（tsファイルは1-2秒なので、ユーザからかなりのリクエストがくる。下記：制限引き上げのリクエストと関連）を捌くため。


## 画質関連

AWS Elemental MediaLive -> Channels -> Details -> Actions/Edit -> Output groups -> 各Outputの設定

- Rate Control  
    - Rate Control Mode：VBRに変更  
高解像度を扱う場合は、VBR（可変ビットレート）のほうが、同容量のCBR（固定ビットレート）よりも高品質になり、処理も早くなります。  
    - Bitrate：5000000(デフォルト)→適宜変更（最低は1000。動作確認であれば最低値でも可）（帯域と調整する必要あり。下記：制限引き上げのリクエストと関連）

- Additional settings  
    - Max Bitrate：適宜変更(最低は1000。動作確認であれば最低値でも可)を入力  


# 制限引き上げのリクエスト

AWSサービスの制限（公式）  
https://docs.aws.amazon.com/ja_jp/general/latest/gr/aws_service_limits.html
  
例えば「1秒あたりの最大同時視聴者数 × ビットレート(画質)」の値がCloudFrontの転送レート上限40Gbpsを超える場合、引き上げ申請が必要になります。  
引き上げ申請なしであれば「ビットレート5-10MBで同時視聴者数1,000人」くらいが安全圏だと思います。  
（本番前に、AWSさんにイベント実施日と想定視聴者数等を連絡したほうが良いと思います。帯域の確保など、相談に乗ってくれると思います）
  
## CloudFront の制限

- ディストリビューションごとのデータ転送レート: 40 Gbps  
- 1 秒あたり、ディストリビューションあたりのリクエスト: 100,000
- AWSに上限引き上げのリクエストをする場合
https://docs.aws.amazon.com/ja_jp/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html

## Lambda@Edge の制限

- 1 秒あたりのリクエスト: 10,000 
- 同時実行数: 1,000 - 3,000(米国東部：バージニア北部)
- AWSに上限引き上げのリクエストをする場合
https://docs.aws.amazon.com/ja_jp/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html#limits-lambda-at-edge

## AWS Elemental MediaPackage の制限

- アカウントあたりの最大チャネル: 30  
https://docs.aws.amazon.com/ja_jp/general/latest/gr/aws_service_limits.html#limits_mediapackage
- AWSに上限引き上げのリクエストをする場合  
https://console.aws.amazon.com/support/home
