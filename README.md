# UE5 Header Reorder Tool

Unreal Engine 5 프로젝트에서 `.generated.h` include를 자동으로 include 블록 마지막으로 이동시키는 도구입니다.

A tool that automatically moves `.generated.h` includes to the end of the include block in Unreal Engine 5 projects.

Unreal Engine 5 プロジェクトで `.generated.h` インクルードを自動的にインクルードブロックの最後に移動するツールです。

## 요구사항 / Requirements / 要件

- .NET 10 SDK

## 빌드 / Build / ビルド

```powershell
dotnet build
```

## 사용법 / Usage / 使用方法

```powershell
# 기본 (최근 10분 수정 파일)
# Default (files modified in last 10 minutes)
# デフォルト（過去10分以内に変更されたファイル）
dotnet run -- "D:\MyProject\MyGame"

# 전체 파일 처리
# Process all files
# 全ファイルを処理
dotnet run -- "D:\MyProject\MyGame" --all

# 미리보기 (변경 없이)
# Dry-run (preview without changes)
# ドライラン（変更なしでプレビュー）
dotnet run -- "D:\MyProject\MyGame" --all --dry-run

# 상세 출력
# Verbose output
# 詳細出力
dotnet run -- "D:\MyProject\MyGame" --all --dry-run --verbose
```

## 옵션 / Options / オプション

| 옵션 | 설명 | 기본값 |
|------|------|--------|
| `<path>` | UE5 프로젝트 경로 / Project path / プロジェクトパス | 필수 / Required / 必須 |
| `--all`, `-a` | 전체 파일 / All files / 全ファイル | `false` |
| `--minutes`, `-m` | N분 이내 파일 / Within N min / N分以内 | `10` |
| `--dry-run`, `-d` | 미리보기 / Preview / プレビュー | `false` |
| `--verbose`, `-v` | 상세 출력 / Detailed / 詳細 | `false` |

## 동작 방식 / How It Works / 動作原理

```cpp
// Before - .generated.h가 중간에 있음 (문제)
// Before - .generated.h in the middle (problem)
// 変更前 - .generated.h が途中にある（問題）
#include "MyClass.h"
#include "MyClass.generated.h"
#include "Engine.h"

// After - .generated.h가 마지막으로 이동
// After - .generated.h moved to end
// 変更後 - .generated.h が最後に移動
#include "MyClass.h"
#include "Engine.h"
#include "MyClass.generated.h"
```

## 스캔 경로 / Scan Paths / スキャン対象

- `[Project]/Source/**/*.h`
- `[Project]/Plugins/*/Source/**/*.h`

## 라이센스 / License / ライセンス

MIT
