# Parent Repository

> **Source of truth** — tüm core kod burada yaşar.

## Nasıl Çalışır?

`main` branch'e push yapıldığında `.github/workflows/notify-children.yml` workflow'u tetiklenir ve tanımlı child repository'lere `repository_dispatch` event'i gönderir.

## Kurulum

### 1. Secret Tanımla

Repository Settings → Secrets → Actions → **New repository secret**:

| Secret | Açıklama |
|---|---|
| `CHILD_REPOS_PAT` | Child repo'lara dispatch gönderebilmek için `repo` scope'lu Personal Access Token |

### 2. Child Repo Listesini Güncelle

`.github/workflows/notify-children.yml` dosyasında `CHILD_REPOS` environment variable'ını düzenle:

```yaml
env:
  CHILD_REPOS: |
    owner/child-repo-1
    owner/child-repo-2
```

### 3. Push ve İzle

```bash
git add .
git commit -m "feat: update core logic"
git push origin main
# → GitHub Actions child repo'lara dispatch gönderecek
```

## Dosya Yapısı

```
parent/
├── .github/
│   └── workflows/
│       └── notify-children.yml
├── src/
│   └── core.py
└── README.md
```
