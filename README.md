# 🚀 GUIA COMPLETO: Publicando um Pacote Flutter no pub.dev

---

## 🧩 1. Pré-requisitos

Antes de publicar, confirme que você tem:

✅ **Conta Google** (necessária para login no pub.dev)
✅ **Dart SDK** ou **Flutter SDK** instalado (3.x+)
✅ Seu **pacote funcional e testado**
✅ Um **repositório Git público (opcional, mas recomendado)**

---

## 🗂️ 2. Estrutura esperada do pacote

O pub.dev exige alguns arquivos obrigatórios:

```
meu_pacote/
├─ lib/
│  └─ meu_pacote.dart
├─ example/
│  └─ main.dart              # exemplo funcional
├─ test/
│  └─ meu_pacote_test.dart
├─ CHANGELOG.md
├─ LICENSE
├─ README.md
└─ pubspec.yaml
```

> **Dica:** o diretório `example/` é importante — ele mostra aos usuários como usar seu pacote.

---

## ⚙️ 3. Verifique seu `pubspec.yaml`

Esse arquivo precisa estar limpo e completo. Exemplo:

```yaml
name: meu_pacote
description: SDK para integrar minha lógica em apps Flutter e Dart.
version: 1.0.0
homepage: https://github.com/seuusuario/meu_pacote
repository: https://github.com/seuusuario/meu_pacote
issue_tracker: https://github.com/seuusuario/meu_pacote/issues
documentation: https://github.com/seuusuario/meu_pacote/wiki

environment:
  sdk: ">=3.3.0 <4.0.0"
  flutter: ">=3.0.0"

dependencies:
  flutter:
    sdk: flutter

dev_dependencies:
  flutter_test:
    sdk: flutter
  lints: ^4.0.0

flutter:
  uses-material-design: false
```

⚠️ **Importante:**

* **Não use dependências locais (path:)** — o pub.dev rejeita.
* **Não deixe campos em branco**, especialmente `description`, `version` e `environment`.

---

## 🧪 4. Teste o pacote localmente

Antes de publicar, rode:

```bash
flutter pub get
flutter test
```

Tudo deve passar sem erros.
Depois simule a publicação:

```bash
dart pub publish --dry-run
```

Se aparecer:

```
Package validation passed.
```

✅ Está tudo certo para publicar.

---

## 📤 5. Fazer login no pub.dev

Execute:

```bash
dart pub login
```

Isso abrirá seu navegador e pedirá login com o Google.
Após isso, o Dart CLI vai armazenar seu token de autenticação localmente.

---

## 🌍 6. Publicar de fato

Agora publique com:

```bash
dart pub publish
```

Ele mostrará uma prévia das informações e pedirá confirmação:

```
Publishing package "meu_pacote" (1.0.0) to https://pub.dev:
Are you sure you want to publish (y/N)?
```

Digite `y` e aguarde o upload.
Em poucos segundos, você verá algo como:

```
Successfully uploaded package.
View your package at:
https://pub.dev/packages/meu_pacote
```

🎉 Parabéns! Seu pacote está **publicado oficialmente**.

---

## 🔁 7. Atualizando o pacote

Sempre que quiser publicar uma nova versão:

1. Atualize o número no `pubspec.yaml`
   (ex: de `1.0.0` para `1.0.1`)
2. Atualize o `CHANGELOG.md`
3. Rode novamente:

   ```bash
   dart pub publish --dry-run
   dart pub publish
   ```

> O pub.dev **não permite reenvio da mesma versão**, então incremente sempre (`1.0.0 → 1.0.1`).

---

## 🧾 8. Checklist antes de publicar

| Item | Verificação                            |
| ---- | -------------------------------------- |
| ✅    | README com instruções claras           |
| ✅    | CHANGELOG com histórico de versões     |
| ✅    | LICENSE válida (MIT, Apache, etc.)     |
| ✅    | Exemplo funcional em `/example`        |
| ✅    | Código formatado (`dart format .`)     |
| ✅    | Testes passando                        |
| ✅    | `pubspec.yaml` sem dependências locais |

---

## 🏷️ 9. Dicas de qualidade (score do pub.dev)

O **pub.dev** dá uma pontuação de 0–130 com base em 3 fatores:

| Categoria       | Dica para 100%                             |
| --------------- | ------------------------------------------ |
| **Pub Points**  | README, CHANGELOG, LICENSE, exemplo        |
| **Popularity**  | quanto mais downloads, melhor              |
| **Maintenance** | CI, versionamento, documentação atualizada |

💡 Use o comando:

```bash
dart pub publish --dry-run
```

para ver mensagens sobre **como melhorar sua pontuação** antes de publicar.

---

## 💡 10. Dica bônus: publicar via CI/CD (GitHub Actions)

Para automatizar a publicação (avançado):

```yaml
name: Publish to pub.dev
on:
  push:
    tags:
      - 'v*' # Exemplo: v1.0.0

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: dart-lang/setup-dart@v1
      - run: dart pub get
      - run: dart pub publish --force
        env:
          PUB_CREDENTIALS: ${{ secrets.PUB_CREDENTIALS }}
```

---

## 🧠 Resumo Final

| Etapa             | Comando                                |
| ----------------- | -------------------------------------- |
| Verificar pacotes | `dart pub publish --dry-run`           |
| Fazer login       | `dart pub login`                       |
| Publicar          | `dart pub publish`                     |
| Atualizar versão  | editar `version:` + `dart pub publish` |

