# Python Subproject

Этот каталог содержит пример небольшого проекта на Python, который является частью монорепозитория [multistack-lab](https://github.com/AlexandrShapkin/multistack-lab).  

## Содержание
- `main.py` — простая программа с функцией `add(a, b)` и примером использования.
- `test_main.py` — минимальный тест для функции `add`.
- `.gitlab-ci.yml` — конфигурация GitLab CI для запуска тестов.

## CI
В GitLab настроен pipeline:
```yaml
stages:
  - test

python-test:
  image: python:3.12
  stage: test
  script:
    - pip install pytest
    - pytest -v
```

Таким образом, при каждой синхронизации из GitHub в GitLab запускается тестирование.

```bash
python main.py
# Hello from Python, 2+3= 5

pytest -v
# test_main.py::test_add PASSED
```