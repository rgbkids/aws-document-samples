# 目次

## ライブストリーミング環境を作る

### nginx-rtmp-moduleを利用する (要ライセンス表記)

AWS(EC2等）自社サーバでも運営可能
例のシステム構成図
アーカイブは独自（rsyncなど）

### AWSでフルマネージドで用意する
- <a href='livestreaming/README.md'>livestreaming/README.md</a>

## プレイヤーを開発する

### HLS対応ブラウザ

- <a href='player/README.md'>player/README.md</a>

### HLS未対応対応ブラウザ

- <a href='player/README.md'>player/README.md</a>

## アーカイブを設定する

### nginx-rtmp-moduleの場合 (要ライセンス表記)

- (rsyncなどで行う)

### AWSフルマネージドの場合（S3に保存する）
 
- <a href='archive/README.md'>archive/README.md</a>

## 視聴制限

AWS CloudFrontを利用した簡易的な視聴者制限

### WAF
- https://github.com/rgbkids/balus-live-demo/tree/feature/manual/documents_other/waf

### 署名付きCookie
- <a href='signedcookie/README.md'>signedcookie/README.md</a>

## チャットを作成する

## 独自でシグナリングサーバーを用意する
メリット
プレイリスト長さを2時間にできる。これでvideo.currentTime取れる

## Firebaseを使う
https://github.com/rgbkids/balus-live-demo/tree/feature/chat_vteacher_added/firebase

# 認証
## 独自
## Firebase

## チューニング

- <a href='tuning/README.md'>tuning/README.md</a>

