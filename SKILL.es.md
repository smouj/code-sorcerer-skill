name: code-sorcerer
description: Escribe y depura código complejo con precisión mística
version: 2.1.0
author: OpenClaw Dev Team
requires:
  - python3 >= 3.9
  - gcc >= 10.0
  - gdb
  - valgrind
  - pylint
  - mypy
  - black
  - pytest
  - bandit
  - semgrep
provides:
  - cast-spell
  - inspect-aura
  - optimize-flow
  - shield-ward
  - trace-mana
  - run-ritual
  - revert-changes
tags:
  - magic
  - debugging
  - optimization
  - spells
  - security
  - performance
entrypoint: /opt/openclaw/skills/code-sorcerer/bin/sorcery.sh
```


# Code Sorcerer

Escribe y depura código complejo con precisión mística. Code Sorcerer combina análisis estático, depuración en tiempo de ejecución y escaneo de seguridad para producir código de producción que sea tanto performante como seguro.

## Purpose

Resolver desafíos de codificación del mundo real que requieren experiencia técnica profunda:

- **Depurar corrupción de memoria compleja** en aplicaciones C/C++ multihilo (use-after-free, condiciones de carrera)
- **Optimizar cuellos de botella de rendimiento** en pipelines de datos Python (perfilado CPU, optimización memoria, refactoring async)
- **Generar integraciones de API seguras** con autenticación, validación de entrada y manejo de errores apropiados
- **Reescribir código legacy spaghettizado** en módulos limpios, probados y tipados (Python a Typer, JS a TS)
- **Implementar algoritmos complejos** (recorrido de grafos, primitivas criptográficas, compresión) con garantías de corrección
- **Endurecimiento contra ataques de inyección** (SQLi, XSS, inyección de comandos) en aplicaciones web
- **Diagnosticar y corregir deadlocks** en sistemas concurrentes con sanitizador de hilos y análisis de orden de locks

## Alcance

### Commands

`cast-spell` - Motor principal de generación/depuración de código. Acepta prompts en lenguaje natural con contexto de código.

```bash
cast-spell --prompt "Refactor this function to use async/await and add error handling" \
           --input src/utils.py:45-78 \
           --output src/utils_async.py \
           --languages python \
           --security-level high \
           --test-coverage 0.9
```

`inspect-aura` - Evaluación de análisis estático y calidad de código. Escanea codebase en busca de vulnerabilidades, code smells y complejidad.

```bash
inspect-aura --path ./src \
             --checks all \
             --exclude tests,docs \
             --format sarif \
             --output reports/aura.sarif
```

`optimize-flow` - Hechicero de optimización de rendimiento. Perfila código y sugiere/aplica optimizaciones.

```bash
optimize-flow --target src/api/server.py \
              --profile cpu,memory \
              --optimize loops,io \
              --benchmark before/after \
              --iterations 1000
```

`shield-ward` - Endurecimiento de seguridad. Inyecta validación, sanitización y valores seguros por defecto.

```bash
shield-ward --component auth/login.py \
            --inject csrf,xss,sqli \
            --framework django \
            --output hardened/auth/
```

`trace-mana` - Depuración en tiempo de ejecución y generación de trazas. Se conecta al proceso, registra flujo de ejecución.

```bash
trace-mana --pid 12345 \
           --trace syscalls,network \
           --duration 30s \
           --output traces/mana_$(date +%s).json
```

`run-ritual` - Ejecuta suites de pruebas con cobertura mejorada y mutación testing.

```bash
run-ritual --suite integration \
           --coverage-threshold 0.85 \
           --mutation-test \
           --fail-fast \
           --parallel 4
```

`revert-changes` - Deshace modificaciones de Code Sorcerer usando git o manifiesto de backup.

```bash
revert-changes --manifest .code_sorcerer_manifest.json \
               --revert-all \
               --backup-before-revert
```

## Proceso de Trabajo

### 1. Preparation

Cargar contexto y configuración:

```bash
export CODE_SORCERER_DEBUG=1
export CODE_SORCERER_OPT_LEVEL=aggressive
export CODE_SORCERER_SECURITY_LEVEL=high
```

Leer config `.codesorcerer.yaml` (si existe) para reglas específicas del proyecto.

### 2. Spell Casting (cast-spell)

**Paso A**: Parsear prompt y extraer intención usando clasificación NLP.

**Paso B**: Cargar archivos relevantes de las especificaciones `--input` proporcionadas.

**Paso C**: Ejecutar parseo AST para entender estructura del código antes de modificación.

**Paso D**: Generar código modificado con type checking (mypy) y linting (pylint) en memoria.

**Paso E**: Escribir output con backup del original: `file.ext.sorcery_backup_TIMESTAMP`.

**Paso F**: Actualizar manifiesto `.code_sorcerer_manifest.json` con detalles de la operación.

**Paso G**: Ejecutar unit tests (si están disponibles) para verificar que no haya breakage.

Ejemplo de flujo:
```bash
cast-spell \
  --prompt "Fix the memory leak in this function and add proper cleanup" \
  --input src/memory_utils.c:120-145 \
  --output src/memory_utils_fixed.c \
  --languages c \
  --security-level high \
  --test-coverage 0.95
```

Pasos internos:
1. Extrae líneas 120-145 de `src/memory_utils.c`
2. Analiza con clang-tidy buscando problemas de memoria
3. Genera versión corregida con llamadas `free()` apropiadas y manejo de errores
4. Valida con `valgrind --leak-check=full` en binario de prueba
5. Escribe output y backup
6. Registra en `~/.openclaw/logs/code_sorcerer_YYYY-MM-DD.log`

### 3. Aura Inspection (inspect-aura)

**Paso A**: Construir AST completo para la ruta objetivo.

**Paso B**: Ejecutar checks en secuencia:
- Bandit (seguridad)
- Semgrep (pattern matching)
- Pylint (calidad de código)
- Mypy (type checking)
- Radon (complejidad)
- Reglas personalizadas de `rules/sorcery_rules.yaml`

**Paso C**: Agregar hallazgos con puntuación de severidad.

**Paso D**: Generar reporte en formato solicitado.

**Paso E**: Sugerir fixes con puntuaciones de confianza.

### 4. Optimization Flow (optimize-flow)

**Paso A**: Crear benchmark base usando `pytest-benchmark` o harness personalizado.

**Paso B**: Perfilar objetivo con herramienta apropiada:
- Python: `cProfile`, `py-spy`, `memory_profiler`
- C/C++: `perf`, `valgrind --tool=callgrind`
- Node: `--inspect`, `clinic.js`

**Paso C**: Identificar hotspots (top 5 funciones que consumen >70% tiempo o memoria).

**Paso D**: Aplicar mejoras algorítmicas (O(n²) → O(n log n), memoización, vectorización).

**Paso E**: Re-ejecutar benchmark y comparar.

**Paso F**: Generar reporte con métricas:
- Factor de aceleración
- Porcentaje de reducción de memoria
- Advertencias de regresión

### 5. Security Shield (shield-ward)

**Paso A**: Detectar framework desde archivos del proyecto (package.json, requirements.txt, etc).

**Paso B**: Mapear controles de seguridad a convenciones del framework.

**Paso C**: Para cada tag `--inject`:
- CSRF: Añadir middleware de verificación de tokens
- XSS: Escapar variables de template, añadir headers CSP
- SQLi: Reemplazar queries raw con llamadas ORM parametrizadas
- CMD injection: Validar/sanitizar inputs de shell, usar subprocess con args como lista

**Paso D**: Generar diff de adiciones de seguridad.

**Paso E**: Ejecutar tests de seguridad (OWASP ZAP baseline, custom exploit tests).

**Paso F**: Output código endurecido con anotaciones explicando cada protección.

### 6. Trace Mana (trace-mana)

**Paso A**: Conectar al PID objetivo con `ptrace` (Linux) o `dtrace` (BSD/macOS).

**Paso B**: Configurar tracepoints (syscalls, network, file I/O, signal handling).

**Paso C**: Capturar por `--duration` o hasta Ctrl+C.

**Paso D**: Post-procesar traza para construir call tree y análisis de cuellos de botella.

**Paso E**: Generar flame graph (`flamegraph.pl`) y timeline de I/O.

**Paso F**: Sugerir fixes para syscalls lentos, llamadas bloqueantes, tormentas de retry.

### 7. Run Ritual (run-ritual)

**Paso A**: Detectar framework de pruebas:
- Python: pytest, unittest, nose2
- JavaScript: jest, mocha, vitest
- Rust: cargo test
- Go: go test

**Paso B**: Ejecutar con recolección de cobertura (`pytest --cov`, `jest --coverage`).

**Paso C**: Ejecutar mutación testing (`mutmut`, `stryker`) si `--mutation-test` habilitado.

**Paso D**: Paralelizar ejecución de pruebas (xargs -P, pytest-xdist).

**Paso E**: Generar reportes JUnit XML y HTML de cobertura.

**Paso F**: Fallar si umbrales no cumplidos.

### 8. Rollback (revert-changes)

**Paso A**: Leer manifiesto `.code_sorcerer_manifest.json` que contiene:
```json
{
  "operations": [
    {
      "timestamp": "2026-03-03T14:22:15Z",
      "prompt": "refactor login",
      "input_file": "src/auth/login.py",
      "output_file": "src/auth/login_async.py",
      "backup_file": "src/auth/login.py.sorcery_backup_20260303_142215",
      "command": "cast-spell",
      "git_commit": "abc123"
    }
  ]
}
```

**Paso B**: Para cada operación, restaurar backup si existe:
```bash
if [ -f "$backup_file" ]; then
  mv "$backup_file" "$original_file"
fi
```

**Paso C**: Alternativamente, usar git si `--git-revert`:
```bash
git revert <commit_hash> --no-edit
```

**Paso D**: Limpiar entradas de manifiesto según se revierten.

**Paso E**: Generar reporte de rollback con lista de archivos restaurados.

## Reglas de Oro

1. **Nunca modificar sin backup**: Cada archivo modificado obtiene `.sorcery_backup_*` con timestamp Y commit git si repo detectado.
2. **Type safety obligatorio**: Código generado debe pasar `mypy --strict` con 0 errores. Si el lenguaje no tiene tipado (JS), añadir anotaciones JSDoc.
3. **Seguridad primero**: `--security-level` por defecto es `medium`. Cualquier nivel `high` debe pasar `bandit -x tests` sin hallazgos de severidad alta.
4. **Tests requeridos**: Si el proyecto tiene suite de tests, `cast-spell` debe ejecutar tests post-modificación. Si tests fallan, revertir automáticamente.
5. **Diff mínimo**: Solo cambiar lo necesario. Preservar formato (usar `black` para Python, `prettier` para JS, pero respetar estilo original primero).
6. **No magic strings**: Credenciales hardcodeadas, URLs o secretos trigger rechazo. Usar variables de entorno o archivos de config.
7. **Penalidad de complejidad**: Funciones que excedan complejidad ciclomática 15 deben dividirse. `radon cc` lo hace cumplir.
8. **Hygiene de manejo de errores**: Todas las operaciones de I/O deben tener try/except (o equivalente) con logging. No hay `except Exception:` sin re-raise o manejo apropiado.
9. **Baseline de rendimiento**: `optimize-flow` requiere benchmark antes y después. Aceleración debe superar 5% para considerar cambio.
10. **Requisito de documentación**: Cada función/clase pública nueva obtiene docstring con args, returns, raises, ejemplos.

## Ejemplos

**Ejemplo 1: Fix memory leak en código C**

User input:
```bash
cast-spell \
  --prompt "Fix memory leaks: malloc without free on error paths" \
  --input src/http_parser.c:200-250 \
  --languages c \
  --security-level high
```

Output (`src/http_parser_fixed.c`):
```c
// Added proper cleanup on error paths
// Original lines 200-250 had 3 malloc calls without corresponding free in error handlers

int parse_http_request(const char *data, size_t len) {
    request_t *req = malloc(sizeof(request_t));
    if (!req) return -1;

    header_t *headers = malloc(MAX_HEADERS * sizeof(header_t));
    if (!headers) {
        free(req);  // FIXED: was missing
        return -1;
    }

    // ... parsing logic ...

    if (parse_failed) {
        free(headers);  // FIXED: was missing
        free(req);
        return -1;
    }

    // success path
    req->headers = headers;
    return 0;
}
```

Backup creado: `src/http_parser.c.sorcery_backup_20260303_143022`

Entrada de manifiesto:
```json
{
  "operation": "cast-spell",
  "timestamp": "2026-03-03T14:30:22Z",
  "prompt": "Fix memory leaks: malloc without free on error paths",
  "files_modified": ["src/http_parser_fixed.c"],
  "backups_created": ["src/http_parser.c.sorcery_backup_20260303_143022"],
  "validation": "valgrind --leak-check=full ./test_parser => 0 leaks"
}
```

**Ejemplo 2: Optimizar procesamiento de datos Python**

User input:
```bash
optimize-flow \
  --target src/etl/transform.py \
  --profile cpu,memory \
  --optimize loops,io \
  --benchmark before/after
```

Reporte output:
```
=== Optimization Report ===
Target: src/etl/transform.py:process_data()
Baseline: 12.4s CPU, 145MB memory
After: 3.1s CPU, 42MB memory
Speedup: 4.0x (75% faster)
Memory reduction: 71%

Changes applied:
1. Replaced nested for loops with vectorized numpy operations (process_rows)
2. Switched list accumulation to generator pattern (stream_records)
3. Replaced pandas.read_csv(chunksize=1000) with dtype specification (reduced memory 55%)
4. Added @lru_cache to expensive lookup function (cache hits: 89%)

Validation:
- pytest tests/test_transform.py -k test_process_data passed (100% coverage)
- No regressions: output checksum matches golden file (sha256: abc123...)
---

Run: pytest -xvs tests/test_transform.py
```

**Ejemplo 3: Security hardening para Flask API**

User input:
```bash
shield-ward \
  --component app/api.py \
  --inject csrf,xss,sqli \
  --framework flask \
  --output hardened/
```

Output (`hardened/app_api.py`):
```python
from flask_wtf import FlaskForm, CSRFProtect
from flask_talisman import Talisman
from werkzeug.security import generate_password_hash, check_password_hash
import html

csrf = CSRFProtect()
talisman = Talisman()

class LoginForm(FlaskForm):
    username = StringField('Username', validators=[DataRequired(), Length(max=80)])
    password = PasswordField('Password', validators=[DataRequired()])

@app.route('/login', methods=['POST'])
@csrf.protect()
def login():
    form = LoginForm()
    if not form.validate_on_submit():
        return jsonify({'error': 'Invalid input'}), 400
    
    # SQLi protection: use parameterized query
    user = db.session.execute(
        text("SELECT * FROM users WHERE username = :username"),
        {'username': form.username.data}
    ).fetchone()
    
    # XSS protection: escape output
    display_name = html.escape(user.display_name) if user else ''
    
    # Check password with constant-time comparison
    if not check_password_hash(user.password_hash, form.password.data):
        return jsonify({'error': 'Invalid credentials'}), 401
    
    return jsonify({
        'name': display_name,
        'token': create_token(user.id)
    })
```

Añadidos headers CSP, HTTPS enforcement, HSTS via configuración Talisman en `create_app()`.

**Ejemplo 4: Trace deadlock**

User input:
```bash
trace-mana \
  --pid 28471 \
  --trace futex,network \
  --duration 20s \
  --output traces/deadlock_analysis.json
```

Resumen output:
```
=== Trace Analysis ===
PID: 28471
Duration: 20.3s
Events captured: 1,247,311

Futex wait chain detected (possible deadlock):
Thread 0x7f9a1c (main):
  futex_wait(0x7f9a1c, 0x1) at worker.c:347
  -> blocked on mutex A

Thread 0x7f9a2d (pool-2):
  futex_wait(0x7f9a2d, 0x1) at worker.c:347
  -> blocked on mutex B
  -> holds mutex A (lock_order: A->B)

Thread 0x7f9a3e (pool-3):
  futex_wait(0x7f9a3e, 0x1) at worker.c:347
  -> blocked on mutex A
  -> holds mutex B (lock_order: B->A)

DEADLOCK DETECTED: Circular wait (A->B->A)

Recommendation:
- Enforce global lock ordering: always acquire mutex A before mutex B
- File: src/worker.c:310-340

Flame graph saved: traces/flamegraph_28471.svg
```

## Dependencias

Paquetes del sistema (Debian/Ubuntu):
```bash
apt-get install -y python3-pip python3-venv gcc gdb valgrind \
  clang-tidy clang-format pkg-config libssl-dev
```

Paquetes Python (auto-instalados por sorcery.sh si faltan):
```bash
pip install pylint mypy black bandit semgrep pytest pytest-cov \
  memory_profiler py-spy radon mutmut flask-wtf flask-talisman
```

Opcionales (para lenguajes específicos):
- Node.js 18+ (para optimización JS/TS)
- Rust toolchain (para análisis de código Rust)
- Go compiler (para profiling de Go)

Variables de entorno de runtime:
```bash
CODE_SORCERER_HOME="/opt/openclaw/skills/code-sorcerer"
CODE_SORCERER_CACHE="$HOME/.cache/code_sorcerer"
CODE_SORCERER_LOG_LEVEL="INFO"  # DEBUG, INFO, WARN, ERROR
CODE_SORCERER_MAX_CONCURRENT=4    # operaciones paralelas
CODE_SORCERER_GIT_INTEGRATION=1  # auto-commit cambios
CODE_SORCERER_BACKUP_RETENTION_DAYS=30
```

Configuración proyecto-local (`.codesorcerer.yaml`):
```yaml
exclude_paths:
  - "node_modules"
  - "venv"
  - "dist"
  - "build"
  - "*.min.js"
security:
  enable_bandit: true
  enable_semgrep: true
  custom_rules: "security/rules.yaml"
testing:
  framework: pytest
  coverage_target: 0.90
  run_mutation: false
optimization:
  hot_threshold: 0.1  # 10% runtime para optimizar
  max_iterations: 3
formatting:
  python: black
  javascript: Prettier
  c: clang-format
```

## Verificación

Después de cualquier `cast-spell`:

1. Verificar backup existe: `ls -l file.py.sorcery_backup_*`
2. Verificar sintaxis: `python3 -m py_compile file.py`
3. Ejecutar type check: `mypy file.py`
4. Ejecutar lint: `pylint file.py`
5. Ejecutar tests: `pytest tests/ -xvs`
6. Revisar diff: `git diff --no-index file.py.sorcery_backup_* file.py`

Después de `optimize-flow`:

1. Confirmar benchmark: `cat reports/benchmark_before_after.json`
2. Verificar no nueva complejidad: `radon cc file.py`
3. Ejecutar suite completa: `pytest --tb=short`

Después de `shield-ward`:

1. Ejecutar security scan: `bandit -r hardened/`
2. Test con OWASP ZAP (si disponible): `zap-baseline.py -t http://localhost:8000`
3. Verificar authentication sigue funcionando: manual smoke test

Después de `inspect-aura`:

1. Revisar SARIF report: `cat reports/aura.sarif | jq '.runs[0].results[] | select(.level=="error")'`
2. Asegurar no hay vulnerabilidades críticas restantes

## Solución de Problemas

**Problema**: `cast-spell` falla con "AST parsing error"
**Solución**: Asegurar que archivo de entrada encoding es UTF-8. Ejecutar `file -I filename` para verificar. Convertir con `iconv` si es necesario.

**Problema**: Valgrind reporta memory leaks en código "corregido"
**Solución**: Buscar falsos positivos de librerías del sistema. Usar `--trace-children=yes` si hay forks involved. Suprimir librerías conocidas con `--suppressions=valgrind.supp`.

**Problema**: Optimización hace más lento el código
**Solución**: Artefacto de benchmarking (cold start). Calentar funciones antes de medir. Usar `perf stat -e cache-misses` para buscar cache thrashing introducido por vectorización.

**Problema**: Security shield rompe runtime
**Solución**: Probablemente token CSRF faltando en peticiones AJAX. Asegurar que frontend envía header `X-CSRFToken`. Verificar config Talisman/CORS.

**Problema**: Trace-mana permission denied
**Solución**: Ejecutar como root o con capability `sudo ptrace`: `sudo setcap cap_sys_ptrace=eip $(which code-sorcerer)`.

**Problema**: Corrupción de manifiesto previene rollback
**Solución**: Restaurar desde git: `git checkout -- <file>` o usar archivo backup directamente si está presente: `mv file.ext.sorcery_backup_TIMESTAMP file.ext`.

**Problema**: Alto CPU usage durante análisis
**Solución**: Limitar concurrencia: `export CODE_SORCERER_MAX_CONCURRENT=2`. Excluir directorios grandes: añadir a `.codesorcerer.yaml` exclude_paths.

**Problema**: mypy falsos errores en stubs de terceros
**Solución**: Generar stubs: `stubgen -m external_lib -o .`. O añadir `# type: ignore` inline con comentario explicativo.

## Comandos de Rollback

**Rollback completo de todas las operaciones de Code Sorcerer en repo actual**:
```bash
code-sorcerer revert --all --manifest .code_sorcerer_manifest.json
```

**Rollback operación específica por timestamp**:
```bash
code-sorcerer revert --timestamp 2026-03-03T14:30:22Z --manifest .code_sorcerer_manifest.json
```

**Restaurar desde git si se creó commit**:
```bash
git log --grep="[Code Sorcerer]" --oneline
git revert <commit_hash> --no-edit
```

**Rollback manual usando backups**:
```bash
# Encontrar todos los backups
find . -name "*.sorcery_backup_*" -type f

# Restaurar uno
mv src/utils.py.sorcery_backup_20260303_142215 src/utils.py

# Restaurar todos en directorio
find src/ -name "*.sorcery_backup_*" -exec sh -c 'mv "$1" "${1%.sorcery_backup_*}"' _ {} \;
```

**Limpiar manifiesto después de restore manual**:
```bash
jq 'del(.operations[] | select(.timestamp=="2026-03-03T14:30:22Z"))' \
  .code_sorcerer_manifest.json > tmp.json && mv tmp.json .code_sorcerer_manifest.json
```

## Soporte

Logs: `~/.openclaw/logs/code_sorcerer_*.log`
Reportes: `reports/sorcery_YYYY-MM-DD/`
Documentación: `https://kilo.ai/docs/skills/code-sorcerer`
Issue tracker: `https://github.com/Kilo-Org/kilocode/issues/new?template=code_sorcerer.yaml`
```