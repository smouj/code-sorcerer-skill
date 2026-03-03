name: code-sorcerer
description: Writes and debugs complex code with mystical precision
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

Writes and debugs complex code with mystical precision. Code Sorcerer combines static analysis, runtime debugging, and security scanning to produce production-grade code that's both performant and secure.

## Purpose

Solve real-world coding challenges that require deep technical expertise:

- **Debug complex memory corruption** in C/C++ multithreaded applications (use-after-free, race conditions)
- **Optimize performance bottlenecks** in Python data pipelines (CPU profiling, memory optimization, async refactoring)
- **Generate secure API integrations** with proper authentication, input validation, and error handling
- **Rewrite legacy spaghetti code** into clean, tested, typed modules (Python to Typer, JS to TS)
- **Implement complex algorithms** (graph traversal, crypto primitives, compression) with correctness guarantees
- **Hardening against injection attacks** (SQLi, XSS, command injection) in web applications
- **Diagnose and fix deadlocks** in concurrent systems with thread sanitizer and lock ordering analysis

## Scope

### Commands

`cast-spell` - Core code generation/debugging engine. Accepts natural language prompts with code context.

```bash
cast-spell --prompt "Refactor this function to use async/await and add error handling" \
           --input src/utils.py:45-78 \
           --output src/utils_async.py \
           --languages python \
           --security-level high \
           --test-coverage 0.9
```

`inspect-aura` - Static analysis and code quality assessment. Scans codebase for vulnerabilities, code smells, and complexity.

```bash
inspect-aura --path ./src \
             --checks all \
             --exclude tests,docs \
             --format sarif \
             --output reports/aura.sarif
```

`optimize-flow` - Performance optimization wizard. Profiles code and suggests/applies optimizations.

```bash
optimize-flow --target src/api/server.py \
              --profile cpu,memory \
              --optimize loops,io \
              --benchmark before/after \
              --iterations 1000
```

`shield-ward` - Security hardening. Injects validation, sanitization, and secure defaults.

```bash
shield-ward --component auth/login.py \
            --inject csrf,xss,sqli \
            --framework django \
            --output hardened/auth/
```

`trace-mana` - Runtime debugging and trace generation. Attaches to process, logs execution flow.

```bash
trace-mana --pid 12345 \
           --trace syscalls,network \
           --duration 30s \
           --output traces/mana_$(date +%s).json
```

`run-ritual` - Execute test suites with enhanced coverage and mutation testing.

```bash
run-ritual --suite integration \
           --coverage-threshold 0.85 \
           --mutation-test \
           --fail-fast \
           --parallel 4
```

`revert-changes` - Undo Code Sorcerer modifications using git or backup manifest.

```bash
revert-changes --manifest .code_sorcerer_manifest.json \
               --revert-all \
               --backup-before-revert
```

## Work Process

### 1. Preparation

Load context and configuration:

```bash
export CODE_SORCERER_DEBUG=1
export CODE_SORCERER_OPT_LEVEL=aggressive
export CODE_SORCERER_SECURITY_LEVEL=high
```

Read `.codesorcerer.yaml` config (if present) for project-specific rules.

### 2. Spell Casting (cast-spell)

**Step A**: Parse prompt and extract intent using NLP classification.

**Step B**: Load relevant files from provided `--input` specs.

**Step C**: Run AST parsing to understand code structure before modification.

**Step D**: Generate modified code with type checking (mypy) and linting (pylint) in memory.

**Step E**: Write output with backup of original: `file.ext.sorcery_backup_TIMESTAMP`.

**Step F**: Update manifest `.code_sorcerer_manifest.json` with operation details.

**Step G**: Run unit tests (if available) to verify no breakage.

Example flow:
```bash
cast-spell \
  --prompt "Fix the memory leak in this function and add proper cleanup" \
  --input src/memory_utils.c:120-145 \
  --output src/memory_utils_fixed.c \
  --languages c \
  --security-level high \
  --test-coverage 0.95
```

Internal steps:
1. Extracts lines 120-145 from `src/memory_utils.c`
2. Analyzes with clang-tidy for memory issues
3. Generates fixed version with proper `free()` calls and error handling
4. Validates with `valgrind --leak-check=full` on test binary
5. Writes output and backup
6. Logs to `~/.openclaw/logs/code_sorcerer_YYYY-MM-DD.log`

### 3. Aura Inspection (inspect-aura)

**Step A**: Build comprehensive AST for target path.

**Step B**: Run checks in sequence:
- Bandit (security)
- Semgrep (pattern matching)
- Pylint (code quality)
- Mypy (type checking)
- Radon (complexity)
- Custom rules from `rules/sorcery_rules.yaml`

**Step C**: Aggregate findings with severity scoring.

**Step D**: Generate report in requested format.

**Step E**: Suggest fixes with confidence scores.

### 4. Optimization Flow (optimize-flow)

**Step A**: Create baseline benchmark using `pytest-benchmark` or custom harness.

**Step B**: Profile target with appropriate tool:
- Python: `cProfile`, `py-spy`, `memory_profiler`
- C/C++: `perf`, `valgrind --tool=callgrind`
- Node: `--inspect`, `clinic.js`

**Step C**: Identify hotspots (top 5 functions consuming >70% time or memory).

**Step D**: Apply algorithmic improvements (O(n²) → O(n log n), memoization, vectorization).

**Step E**: Re-run benchmark and compare.

**Step F**: Generate report with metrics:
- Speedup factor
- Memory reduction percentage
- Regression warnings

### 5. Security Shield (shield-ward)

**Step A**: Detect framework from project files (package.json, requirements.txt, etc).

**Step B**: Map security controls to framework conventions.

**Step C**: For each `--inject` tag:
- CSRF: Add token verification middleware
- XSS: Escape template variables, add CSP headers
- SQLi: Replace raw queries with parameterized ORM calls
- CMD injection: Validate/sanitize shell inputs, use subprocess with list args

**Step D**: Generate diff of security additions.

**Step E**: Run security tests (OWASP ZAP baseline, custom exploit tests).

**Step F**: Output hardened code with annotations explaining each protection.

### 6. Trace Mana (trace-mana)

**Step A**: Attach to target PID with `ptrace` (Linux) or `dtrace` (BSD/macOS).

**Step B**: Configure tracepoints (syscalls, network, file I/O, signal handling).

**Step C**: Capture for `--duration` or until Ctrl+C.

**Step D**: Post-process trace to build call tree and bottleneck analysis.

**Step E**: Generate flame graph (`flamegraph.pl`) and I/O timeline.

**Step F**: Suggest fixes for slow syscalls, blocking calls, retry storms.

### 7. Run Ritual (run-ritual)

**Step A**: Detect test framework:
- Python: pytest, unittest, nose2
- JavaScript: jest, mocha, vitest
- Rust: cargo test
- Go: go test

**Step B**: Execute with coverage collection (`pytest --cov`, `jest --coverage`).

**Step C**: Run mutation testing (`mutmut`, `stryker`) if `--mutation-test` enabled.

**Step D**: Parallelize test execution (xargs -P, pytest-xdist).

**Step E**: Generate JUnit XML and coverage HTML reports.

**Step F**: Fail if thresholds not met.

### 8. Rollback (revert-changes)

**Step A**: Read manifest `.code_sorcerer_manifest.json` which contains:
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

**Step B**: For each operation, restore backup if exists:
```bash
if [ -f "$backup_file" ]; then
  mv "$backup_file" "$original_file"
fi
```

**Step C**: Alternatively, use git if `--git-revert`:
```bash
git revert <commit_hash> --no-edit
```

**Step D**: Clean manifest entries as they're reverted.

**Step E**: Generate rollback report with list of restored files.

## Golden Rules

1. **Never modify without backup**: Every file changed gets timestamped `.sorcery_backup_*` AND git commit if repo detected.
2. **Type safety mandatory**: Generated code must pass `mypy --strict` with 0 errors. If language lacks typing (JS), add JSDoc annotations.
3. **Security first**: Default `--security-level` is `medium`. Any `high` level must pass `bandit -x tests` with no high-severity findings.
4. **Tests required**: If project has test suite, `cast-spell` must run tests post-modification. If tests fail, revert automatically.
5. **Minimal diff**: Only change what's necessary. Preserve formatting (use `black` for Python, `prettier` for JS, but respect original style first).
6. **No magic strings**: Hardcoded credentials, URLs, or secrets trigger rejection. Use environment variables or config files.
7. **Complexity penalty**: Functions exceeding cyclomatic complexity 15 must be split. `radon cc` enforces this.
8. **Error handling hygiene**: All I/O operations must have try/except (or equivalent) with logging. No bare `except Exception:` without re-raise or proper handling.
9. **Performance baselines**: `optimize-flow` requires benchmark run before and after. Speedup must exceed 5% to consider change.
10. **Documentation requirement**: Every new public function/class gets docstring with args, returns, raises, examples.

## Examples

**Example 1: Fix memory leak in C code**

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

Backup created: `src/http_parser.c.sorcery_backup_20260303_143022`

Manifest entry:
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

**Example 2: Optimize Python data processing**

User input:
```bash
optimize-flow \
  --target src/etl/transform.py \
  --profile cpu,memory \
  --optimize loops,io \
  --benchmark before/after
```

Output report:
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

**Example 3: Security hardening for Flask API**

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

Added CSP headers, HTTPS enforcement, HSTS via Talisman configuration in `create_app()`.

**Example 4: Trace deadlock**

User input:
```bash
trace-mana \
  --pid 28471 \
  --trace futex,network \
  --duration 20s \
  --output traces/deadlock_analysis.json
```

Output summary:
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

## Dependencies

System packages (Debian/Ubuntu):
```bash
apt-get install -y python3-pip python3-venv gcc gdb valgrind \
  clang-tidy clang-format pkg-config libssl-dev
```

Python packages (auto-installed by sorcery.sh if missing):
```bash
pip install pylint mypy black bandit semgrep pytest pytest-cov \
  memory_profiler py-spy radon mutmut flask-wtf flask-talisman
```

Optional (for specific languages):
- Node.js 18+ (for JS/TS optimization)
- Rust toolchain (for Rust code analysis)
- Go compiler (for Go profiling)

Runtime environment variables:
```bash
CODE_SORCERER_HOME="/opt/openclaw/skills/code-sorcerer"
CODE_SORCERER_CACHE="$HOME/.cache/code_sorcerer"
CODE_SORCERER_LOG_LEVEL="INFO"  # DEBUG, INFO, WARN, ERROR
CODE_SORCERER_MAX_CONCURRENT=4    # parallel operations
CODE_SORCERER_GIT_INTEGRATION=1  # auto-commit changes
CODE_SORCERER_BACKUP_RETENTION_DAYS=30
```

Project-local config (`.codesorcerer.yaml`):
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
  hot_threshold: 0.1  # 10% runtime to optimize
  max_iterations: 3
formatting:
  python: black
  javascript: Prettier
  c: clang-format
```

## Verification

After any `cast-spell`:

1. Check backup exists: `ls -l file.py.sorcery_backup_*`
2. Verify syntax: `python3 -m py_compile file.py`
3. Run type check: `mypy file.py`
4. Run lint: `pylint file.py`
5. Execute tests: `pytest tests/ -xvs`
6. Review diff: `git diff --no-index file.py.sorcery_backup_* file.py`

After `optimize-flow`:

1. Confirm benchmark: `cat reports/benchmark_before_after.json`
2. Check no new complexity: `radon cc file.py`
3. Run full test suite: `pytest --tb=short`

After `shield-ward`:

1. Run security scan: `bandit -r hardened/`
2. Test with OWASP ZAP (if available): `zap-baseline.py -t http://localhost:8000`
3. Verify authentication still works: manual smoke test

After `inspect-aura`:

1. Review SARIF report: `cat reports/aura.sarif | jq '.runs[0].results[] | select(.level=="error")'`
2. Ensure no critical vulnerabilities remain

## Troubleshooting

**Issue**: `cast-spell` fails with "AST parsing error"
**Fix**: Ensure input file encoding is UTF-8. Run `file -I filename` to check. Convert with `iconv` if needed.

**Issue**: Valgrind reports memory leaks in "fixed" code
**Fix**: Check for false positives from system libraries. Use `--trace-children=yes` if forks involved. Suppress known libs with `--suppressions=valgrind.supp`.

**Issue**: Optimization slows down code
**Fix**: Benchmarking artifact (cold start). Warm up functions before measuring. Use `perf stat -e cache-misses` to check for cache thrashing introduced by vectorization.

**Issue**: Security shield breaks runtime
**Fix**: Likely CSRF token missing in AJAX requests. Ensure frontend sends `X-CSRFToken` header. Check Talisman/CORS settings.

**Issue**: Trace-mana permission denied
**Fix**: Run as root or with `sudo ptrace` capability: `sudo setcap cap_sys_ptrace=eip $(which code-sorcerer)`.

**Issue**: Manifest corruption prevents rollback
**Fix**: Restore from git: `git checkout -- <file>` or use backup file directly if present: `mv file.ext.sorcery_backup_TIMESTAMP file.ext`.

**Issue**: High CPU usage during analysis
**Fix**: Limit concurrency: `export CODE_SORCERER_MAX_CONCURRENT=2`. Exclude large directories: add to `.codesorcerer.yaml` exclude_paths.

**Issue**: mypy false errors on third-party stubs
**Fix**: Generate stubs: `stubgen -m external_lib -o .`. Or add `# type: ignore` inline with explanatory comment.

## Rollback Commands

**Complete rollback of all Code Sorcerer operations in current repo**:
```bash
code-sorcerer revert --all --manifest .code_sorcerer_manifest.json
```

**Rollback specific operation by timestamp**:
```bash
code-sorcerer revert --timestamp 2026-03-03T14:30:22Z --manifest .code_sorcerer_manifest.json
```

**Restore from git if commit was created**:
```bash
git log --grep="[Code Sorcerer]" --oneline
git revert <commit_hash> --no-edit
```

**Manual rollback using backups**:
```bash
# Find all backups
find . -name "*.sorcery_backup_*" -type f

# Restore one
mv src/utils.py.sorcery_backup_20260303_142215 src/utils.py

# Restore all in directory
find src/ -name "*.sorcery_backup_*" -exec sh -c 'mv "$1" "${1%.sorcery_backup_*}"' _ {} \;
```

**Clean manifest after manual restore**:
```bash
jq 'del(.operations[] | select(.timestamp=="2026-03-03T14:30:22Z"))' \
  .code_sorcerer_manifest.json > tmp.json && mv tmp.json .code_sorcerer_manifest.json
```

## Support

Logs: `~/.openclaw/logs/code_sorcerer_*.log`
Reports: `reports/sorcery_YYYY-MM-DD/`
Documentation: `https://kilo.ai/docs/skills/code-sorcerer`
Issue tracker: `https://github.com/Kilo-Org/kilocode/issues/new?template=code_sorcerer.yaml`
```