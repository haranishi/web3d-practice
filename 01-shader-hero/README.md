# 練習01 — シェーダーグラデ・ヒーロー

Three.js + 自作GLSL（simplex noise + fbm + cosine palette）で、Stripe/Linear系の
「動くメッシュグラデ・ヒーロー」を作る最初の練習。3Dモデル不要・ビルド不要。

## 動かし方
`index.html` を**ダブルクリックしてブラウザで開くだけ**（CDNのThree.jsを読むのでネット接続が要る）。
ローカルサーバーで開きたいなら：
```
cd ~/web3d-practice/01-shader-hero
python3 -m http.server 8080   # → http://localhost:8080
```

## ここで学べること（07・08・09ノートに対応）
- ShaderMaterial の配線、vertex/fragment、uniform（uTime/uMouse）
- **simplex noise → fbm**（有機的な動きの土台 = 07ノート）
- **cosine palette** での配色、vignette、grain
- **色管理**（outputColorSpace / toneMapping の判断 = 08ノート）
- マウスの**慣性追従**（lerp = 09ノート）、prefers-reduced-motion対応

## ✍️ 改造課題（写経→改造→自作 の「改造」フェーズ）
まず数字を1つずつ触って、何が起きるか body で覚える：
1. `palette()` の `d = vec3(0.30,0.20,0.55)` を変える → 配色が激変（自分のブランド色に）
2. `float t = uTime * 0.08;` の係数 → 速さ
3. `fbm` のループ回数 `i<5` → ディテール量（重さも増える）
4. `uv*1.5` の倍率 → 模様のスケール
5. `grain * 0.04` → 粒子感の強さ
6. マウス追従 `lerp(targetMouse, 0.05)` の 0.05 → 重さ（小さいほどヌルッと）

## 次の一手（できたら）
- スクロールで色/速度が変わる（GSAP ScrollTrigger or Lenis = 02ノート）
- テキストを SplitText で1文字ずつ出す
- 板を3D化して頂点ディスプレイスメント（07ノート課題7）

→ 詳細とロードマップは Obsidian `02_notes/Web制作_3D表現/11_練習01_シェーダーグラデヒーロー.md`
