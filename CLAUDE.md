# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## デプロイ先

https://shutakawakami616.github.io/task-board/

`main` ブランチへのpushをトリガーに `.github/workflows/deploy.yml` が自動でビルド・デプロイする(GitHub Actions → GitHub Pages)。

## 技術スタック

- React 19 + TypeScript
- Vite 8(ビルド・開発サーバー)。`base` は `/task-board/`(GitHub Pagesのリポジトリ名に合わせて設定)
- oxlint(Lint)
- スタイリングはプレーンCSS(CSS Modulesやライブラリは未導入)。`src/index.css` にCSS変数(`--text` / `--bg` / `--accent` など)を定義し、ライト/ダークモードは `prefers-color-scheme` で切り替え
- 状態管理はReactの `useState` のみ。タスクは `localStorage`(キー: `task-board:tasks`)に永続化

## 命名規約

- コンポーネントファイルはPascalCase + `.tsx`(例: `TaskItem.tsx`)、対応するスタイルは同名の `.css`(例: `App.css`)
- 型定義は `src/types.ts` に集約し、`interface` 名はPascalCase(例: `Task`)
- CSSクラス名はBEM(`ブロック__エレメント`、`ブロック--モディファイア`)。例: `.task-item`、`.task-item__label`、`.task-item--completed`

## Git運用ルール

- コードに変更を加えたら、その都度コミットしてGitHubにプッシュすること。変更をローカルに溜め込まない。
- コミット前に `git status` / `git diff` で差分を確認し、意図した変更のみが含まれていることを確認する。
- コミットメッセージは変更内容が分かるように簡潔に書く。
- push前にリモートの最新状態を確認し、必要であれば取り込んでからプッシュする。
