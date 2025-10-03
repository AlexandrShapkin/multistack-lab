# Multistack Lab

## 📌 Описание работы

Этот репозиторий создан как лабораторная работа для проверки подхода к работе с **монорепозиторием на GitHub** и синхронизацией отдельных его частей в разные репозитории на GitLab.  

Цель эксперимента:
* Разместить общий код разных проектов (на Go и Python) в одном монорепозитории на GitHub.
* Автоматически синхронизировать части этого монорепозитория (подкаталоги) в отдельные GitLab-репозитории.
* Настроить выполнение CI на стороне GitLab для каждого проекта отдельно.

---

## 🗂️ Структура репозитория

```
multistack-lab/
├── .github/workflows/ # GitHub Actions для синхронизации
│   ├── sync-go.yml
│   └── sync-python.yml
├── go/ # Go-проект
│   ├── main.go
│   ├── main_test.go
│   ├── go.mod
│   └── .gitlab-ci.yml
├── python/ # Python-проект
│   ├── main.py
│   ├── test_main.py
│   └── .gitlab-ci.yml
└── README.md
```

---

## ➡️ GitHub → GitLab синхронизация
- В `.github/workflows/sync-go.yml` и `.github/workflows/sync-python.yml` описаны действия GitHub Actions.
- При изменениях в соответствующей папке (`go/**` или `python/**`) запускается workflow.
- Workflow выполняет `git subtree push` и отправляет код в отдельный GitLab-репозиторий:
  - `go/` → [gitlab/.../go-multistack-lab](https://gitlab.alexandrshapkin.ru/AlexandrShapkin/go-multistack-lab)
  - `python/` → [gitlab/.../python-multistack-lab](https://gitlab.alexandrshapkin.ru/AlexandrShapkin/python-multistack-lab)


> На продолжительном отрезке времени, после размещения информации в этом репозитории, нет гарантии, что сервис GitLab по адресу https://gitlab.alexandrshapkin.ru будет доступен.

---

## 🔁 CI на стороне GitLab
- В каждом из проектов лежит свой `.gitlab-ci.yml`.
- При попадании кода в GitLab запускаются тесты:
  - Для Go — `go test ./...`
  - Для Python — `pytest`

---

## 🤔 В чем смысл
Такой подход позволяет:
- хранить все проекты в одном монорепозитории на GitHub;
- удобно делить их на подрепозитории в GitLab для отдельной разработки и CI;
- прозрачно автоматизировать процесс через `git subtree` и GitHub Actions.

---

См. также:
- [Go README](./go/README.md)
- [Python README](./python/README.md)
