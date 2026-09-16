# Aula 03 — Refatoração REST da EscolaApi

## Comparativo antes/depois

| # | Anti-padrão | Antes | Depois |
|---|-------------|-------|--------|
| 1 | Verbo na URI | `POST /deletarAluno?id=2` → 200 texto | `DELETE /api/v1/alunos/1` → 204 |
| 2 | Status errado | `GET /getAlunoPorId/9999` → 204 vazio | `GET /api/v1/alunos/9999` → 404 ProblemDetails |
| 3 | Aninhamento 4+ níveis | `/escola/cursos/.../matriculas/1` | `/api/v1/alunos/2/matriculas` |
| 4 | Sem versionamento | `/getAlunos` | `/api/v1/alunos` |
| 5 | Sem paginação | 120 alunos, 34,5 KB | 10 alunos, 3,03 KB + metadados |
| 6 | Erro HTML 500 | HTML com status 500 | JSON ProblemDetails com 404 |

## Resultado

- `EscolaController.cs` removido.
- `AlunosController.cs` criado em `api/v1/alunos`.
- Todos os 6 anti-padrões corrigidos.
- `[JsonIgnore]` adicionado em `Matricula.Aluno` para evitar ciclo de serialização.