# Go Subproject

Этот каталог содержит пример небольшого проекта на Go, который является частью монорепозитория [multistack-lab](https://github.com/AlexandrShapkin/multistack-lab).  

## Содержание
- `main.go` — простая программа с функцией `Add(a, b int)` и примером использования.
- `main_test.go` — минимальный тест для функции `Add`.
- `go.mod` — модульные настройки Go.
- `.gitlab-ci.yml` — конфигурация GitLab CI для запуска тестов.

## CI
В GitLab настроен pipeline:
```yaml
stages:
  - test

go-test:
  image: golang:1.22
  stage: test
  script:
    - go test ./...
```

Таким образом, при каждой синхронизации из GitHub в GitLab запускается тестирование.

## Пример запуска локально
```bash
go run main.go
# Hello from Go, 2+3= 5

go test ./...
# ok  	command-line-arguments	0.XXXs
```