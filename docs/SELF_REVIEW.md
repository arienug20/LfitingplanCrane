# Self-review paket dokumentasi A0

## Pendahuluan dan tujuan

Review mencakup seluruh paket Markdown: struktur, tautan lokal, ID, dependency graph, status awal, kontrak,
benchmark, batas allowlist, dan kesiapan handoff. Ini bukan test aplikasi atau review independen engineering.

## Dasar dan persamaan pemeriksaan

78 task = 13 kelompok × 6 task. Status awal 1 READY + 77 TODO + 0 DONE = 78.
File Markdown: 24 dokumen inti/kontrak/engineering/runbook + 78 card + task index + self-review = 104.
Angka benchmark diperiksa ulang secara independen dengan operasi aritmetika SI, bukan fungsi aplikasi yang belum dibuat.
Referensi engineering dan edisi: [register standar](engineering/standards-register.md).

## Analisis dan temuan sebelum koreksi

| No | Lokasi | Kutipan (salah/kurang) | Jenis masalah | Penjelasan | Rekomendasi (teks benar) |
|---|---|---|---|---|---|
| 1 | TND-006, prasyarat versi awal | "[TND-005](tasks/TND-005.md), [RIG-005](tasks/RIG-005.md), [MOD-006](tasks/MOD-006.md)" | Logika dependensi | Task mengubah entry point yang juga ditulis SGL-006, tetapi belum memiliki dependensi langsung/serial terhadapnya. | "Prasyarat: TND-005, RIG-005, MOD-006, SGL-006. Integrasi tandem memperluas evaluator single yang sudah terverifikasi." |
| 2 | Task UI, allowlist versi awal | "src/ui/crane/ChartTableEditor.tsx" | Format/struktur task | Komponen baru saja belum cukup agar alur dapat dicapai melalui workspace. File integrasi shell belum dialokasikan. | "Allowlist UI mencakup file fitur dan src/ui/shell/Workspace.tsx khusus wiring. Shared integration file hanya diubah satu integrator pada satu waktu." |
| 3 | CAT-006, acceptance versi awal | "B-CHART10m→10000kg;9m unsupported." | Format/struktur | Notasi rapat menyulitkan pembacaan angka dan unit untuk executor. | "B-CHART: radius 10 m → kapasitas 10000 kg; radius 9 m → unsupported." |
| 4 | HANDOFF dan pemeriksaan tautan awal | "Pemeriksaan paket: lihat self-review; hasil hanya berlaku untuk dokumentasi." | Format/struktur | File SELF_REVIEW.md belum tersedia pada pemeriksaan pertama sehingga tautan belum dapat dibuka. | "Pemeriksaan paket: lihat docs/SELF_REVIEW.md yang mencatat temuan, koreksi, dan hasil pemeriksaan dokumentasi. Hasil tidak menyatakan aplikasi telah diuji." |

Koreksi 1–3 sudah diterapkan pada task index/card. Koreksi 4 dipenuhi melalui dokumen ini dan pemeriksaan ulang tautan.

## Bukti pemeriksaan otomatis

Status: PASS — pemeriksaan dokumentasi, bukan pengujian aplikasi.
Hasil: 104 file Markdown; 78 task; 165 edge dependensi tanpa siklus; status 1 READY/77 TODO/0 DONE;
1018 tautan lokal valid pada pemeriksaan sebelum lampiran validator; 74 command test targeted cocok dengan allowlist.
Command pemeriksaan dokumentasi: `python3 /tmp/validate_liftplan_docs.py`.
Validator membaca seluruh Markdown dari filesystem, membandingkan card/index, menelusuri DAG dan tautan lokal,
memeriksa allowlist/test command, serta memastikan proyek belum berisi source aplikasi. Script sementara berada di luar proyek.
Pemeriksaan benchmark: operasi aritmetika independen pada B-UNIT, B-SINGLE, B-FACTOR, B-NET, B-TANDEM, B-RIG, B-MAT.
Tidak ada npm install, build, unit test aplikasi, E2E aplikasi, Git commit, push, atau deploy yang dijalankan.

## Kesimpulan dan rekomendasi

Paket ini adalah instruksi sebelum coding; task aplikasi tetap 0 DONE. Setelah final validation lolos, mulai dengan FND-001
hanya ketika coding diotorisasi. G-STD-01, G-CAT-01 dan G-POL-01 tetap terbuka; metadata publik dan benchmark sintetis tidak menutupnya.

## Lampiran — validator baseline yang dapat dijalankan ulang

Script di bawah hanya memeriksa baseline dokumentasi sebelum coding: 78 task, 0 DONE, dan belum ada source aplikasi.
Setelah coding dimulai, ubah baseline pemeriksaan melalui amendment; kegagalan asumsi awal bukan otomatis bug aplikasi.
Jalankan dari root proyek dengan Python3. Tidak membutuhkan package, network, atau file sementara dari sesi sebelumnya.

```bash
python3 - <<'PY'
from pathlib import Path
text = Path("docs/SELF_REVIEW.md").read_text(encoding="utf-8")
code = text.split("<!-- VALIDATOR_SOURCE -->\n```python\n", 1)[1].split("\n```", 1)[0]
exec(compile(code, "documentation-validator", "exec"))
PY
```

<!-- VALIDATOR_SOURCE -->
```python
from pathlib import Path
from collections import Counter
import re, json, hashlib

root = Path.cwd().resolve()
docs = {p.relative_to(root).as_posix(): p.read_text(encoding='utf-8') for p in root.rglob('*.md')}
groups = 'FND MOD PRJ SITE CAT SGL RIG TND SIM CLR REV OUT VAL'.split()
expected = {f'{g}-{i:03}' for g in groups for i in range(1,7)}
errors = []
cards = {Path(p).stem: t for p,t in docs.items() if p.startswith('docs/tasks/')}
if set(cards) != expected: errors.append(('task IDs', sorted(expected-set(cards)), sorted(set(cards)-expected)))
required = ['Tujuan','Prasyarat dan gate','Bacaan wajib','Kondisi awal','Batas pekerjaan','File yang boleh diubah',
            'Kontrak input/output','Langkah implementasi','Acceptance criteria dan test cases','Perintah verifikasi','Bukti penyelesaian','Handoff']
dependencies = {}
allowlists = {}
test_paths = []
for tid, text in cards.items():
    for heading in required:
        if f'## {heading}\n' not in text: errors.append((tid,'missing section',heading))
    if text.count('- [ ] ') < 5: errors.append((tid,'acceptance count'))
    depsec = text.split('## Prasyarat dan gate\n',1)[1].split('\n## ',1)[0]
    deps = re.findall(r'\[([A-Z]+-\d{3})\]\(',depsec)
    dependencies[tid] = deps
    if any(d not in expected or d==tid for d in deps): errors.append((tid,'invalid dependency',deps))
    allowsec = text.split('## File yang boleh diubah\n',1)[1].split('\n## ',1)[0]
    files = re.findall(r'^- `([^`]+)`',allowsec,re.M)
    allowlists[tid] = files
    if not files: errors.append((tid,'no allowlist'))
    for p in files:
        if p.startswith('/') or '..' in Path(p).parts: errors.append((tid,'unsafe allowlist',p))
    commands = text.split('## Perintah verifikasi\n',1)[1].split('\n## ',1)[0]
    targeted = re.findall(r'npm run test:(?:unit|e2e) -- ([^\s`]+)',commands)
    for p in targeted:
        test_paths.append(p)
        if p not in files: errors.append((tid,'targeted test outside allowlist',p))
    if tid not in ('FND-001','FND-002','FND-006','VAL-006') and not targeted: errors.append((tid,'no targeted test'))
    if 'Belum ada implementasi atau test aplikasi yang dijalankan.' not in text: errors.append((tid,'misleading initial evidence'))

visiting=set(); visited=set(); order=[]
def visit(tid):
    if tid in visiting:
        errors.append(('cycle',tid)); return
    if tid in visited: return
    visiting.add(tid)
    for d in dependencies.get(tid,[]): visit(d)
    visiting.remove(tid); visited.add(tid); order.append(tid)
for tid in sorted(expected): visit(tid)

index=docs['docs/TASK_INDEX.md']; index_rows={}
for line in index.splitlines():
    if not re.match(r'^\| \[[A-Z]+-\d{3} — ',line): continue
    columns=[s.strip() for s in line.split('|')[1:-1]]
    tid=re.search(r'\[([A-Z]+-\d{3})',columns[0]).group(1)
    if tid in index_rows: errors.append(('duplicate index',tid))
    index_rows[tid]=columns
    ideps=re.findall(r'\[([A-Z]+-\d{3})\]',columns[1])
    if ideps != dependencies.get(tid,[]): errors.append((tid,'index/card dependency mismatch',ideps,dependencies.get(tid)))
if set(index_rows)!=expected: errors.append(('index/card ID mismatch',sorted(set(index_rows)^expected)))
statuses=Counter(c[2] for c in index_rows.values())
if statuses != Counter({'TODO':77,'READY':1}): errors.append(('initial statuses',dict(statuses)))
if index_rows.get('FND-001',[None,None,None])[2]!='READY': errors.append(('bootstrap not ready',))

broken=[]; local_count=0
for rel,text in docs.items():
    for label,target in re.findall(r'\[([^\]]+)\]\(([^)]+)\)',text):
        if target.startswith(('http://','https://','mailto:')): continue
        path=target.split('#',1)[0]
        if not path: continue
        local_count+=1
        dest=(root/rel).parent/path
        if not dest.is_file(): broken.append((rel,target))
if broken: errors.append(('broken local links',broken))

allfiles=[p for p in root.rglob('*') if p.is_file() and '.git' not in p.relative_to(root).parts]
unexpected=[str(p.relative_to(root)) for p in allfiles if p.suffix!='.md' and p.name!='.write-test']
if unexpected: errors.append(('non-document files in project',unexpected))
if len(docs)!=104: errors.append(('markdown count',len(docs)))

def ancestors(tid):
    acc=set()
    def collect(n):
        for d in dependencies.get(n,[]):
            if d not in acc: acc.add(d); collect(d)
    collect(tid); return acc
# Same engine entrypoint must have a serial dependency; shared UI files have an explicit integration lock.
if 'SGL-006' not in ancestors('TND-006'): errors.append(('SGL/TND shared evaluator unordered',))
if 'CAT-002' in ancestors('CAT-006'): errors.append(('fixture evaluator wrongly blocked by real catalog',))
if 'CAT-002' not in ancestors('VAL-006'): errors.append(('release does not wait real catalog',))
arch=docs['docs/ARCHITECTURE.md']
for cmd in ('test:unit','test:e2e','npm run check','npm run build','npm run verify'):
    if cmd not in arch: errors.append(('undocumented command',cmd))

max_card=max((len(t.split()),tid) for tid,t in cards.items())
report={'markdown_files':len(docs),'tasks':len(cards),'groups':{g:sum(t.startswith(g+'-') for t in cards) for g in groups},
        'initial_statuses':dict(statuses),'dependency_edges':sum(map(len,dependencies.values())),
        'dag_visited':len(visited),'local_links_checked':local_count,'targeted_test_commands':len(test_paths),
        'largest_task_words':max_card,'bytes':sum(len(t.encode()) for t in docs.values()),'errors':errors}
print(json.dumps(report,ensure_ascii=False,indent=2))
raise SystemExit(1 if errors else 0)

```
