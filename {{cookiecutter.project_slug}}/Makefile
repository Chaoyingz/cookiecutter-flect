path = src/{{cookiecutter.project_slug}}

.PHONY: install
install:
	rye sync
	rye install pre-commit -f
	pre-commit install

.PHONY: format
format:
	rye run ruff check --fix-only $(path) tests
	rye run ruff format $(path) tests

.PHONY: lint
lint:
	rye run ruff check $(path) tests
	rye run ruff format --check $(path) tests
{%- if cookiecutter.enable_type_checking -%}

.PHONY: typecheck
typecheck:
	rye run pyright

{%- endif %}
.PHONY: test
test:
	rye run coverage run -m pytest

.PHONY: dev
dev:
	export PYTHONPATH=src && rye run uvicorn src.{{cookiecutter.project_slug}}.main:app --reload