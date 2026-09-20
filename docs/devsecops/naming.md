# Nomenclatura

## Arquivos e pastas

Arquivos e pastas: **inglês**, **tudo minúsculo**, palavras separadas por
**hífen**.

```
naming.md            game-library/       user-profile.ts
```

Vale para o repositório inteiro, incluindo documentação. O conteúdo dos
documentos continua em português — a regra é sobre o nome, não sobre o texto.

Nada de espaço, acento, `_` ou `camelCase` por preferência pessoal.

## Exceções

Maiúsculas e outros padrões são permitidos **quando a convenção daquele tipo
de arquivo exige**:

| Caso | Exemplo |
|---|---|
| Arquivos de raiz reconhecidos por convenção | `README.md`, `LICENSE`, `CLAUDE.md` |
| Ferramentas que esperam um nome exato | `Dockerfile`, `Makefile`, `SKILL.md` |
| Componentes em ecossistemas que usam PascalCase | `GameCard.jsx` |

O critério é sempre o mesmo: a exceção existe porque **a ferramenta ou o
ecossistema exige**, nunca por gosto. Na dúvida, minúsculo com hífen.

## Código

Identificadores — variáveis, funções, classes, tipos, tabelas, rotas — sempre
em **inglês**.

**Comentários podem ser em português.** Comentário existe para explicar, e
explicar na língua em que pensamos é mais eficaz.

### Estilo de escrita

Seguir a convenção da própria linguagem — `snake_case` em C, `camelCase` em
JavaScript, e assim por diante. Não mantemos lista nem inventamos padrão
nosso: o padrão é o que a comunidade daquela linguagem já usa.

Quando a convenção da linguagem conflitar com a regra de arquivos acima, **a
linguagem vence** — por isso `GameCard.jsx` é válido.

---

*Este documento está em `devsecops/` por ser a pasta de convenções que existe
hoje. Nomenclatura é padrão de codificação, não DevSecOps; conforme o projeto
crescer, pode mudar para uma pasta onde faça mais sentido.*
