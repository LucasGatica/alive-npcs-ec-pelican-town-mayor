# AliveNpcs EC - Modo Prefeito

Este repositorio e um exemplo completo de **Experimental Content (EC)** para o AliveNpcs.

Ele tambem serve como tutorial para criadores que querem fazer seus proprios modos experimentais, como:

- Modo Prefeito
- Modo Feiticeiro
- Modo Lobisomem
- Modo Detetive
- Modo Vampiro customizado
- qualquer outro modo que altere a camada narrativa do AliveNpcs

O pacote deste repo adiciona o **Modo Prefeito**, onde os NPCs tratam o fazendeiro como o novo prefeito da Vila Pelicanos.

## O Que E Um EC?

Um EC, ou Experimental Content, e um pacote de conteudo que o AliveNpcs carrega ao abrir o jogo.

Ele pode adicionar:

- um modo experimental novo na aba de Experimental Content;
- prompts customizados para mudar o tom das conversas;
- botoes extras no menu de resposta dos NPCs;
- cenas customizadas ativadas apenas quando o modo esta selecionado;
- textos localizados em `i18n`;
- integracao com mods de codigo via API, para casos mais avancados.

Este repo e **content-only**. Isso significa que ele nao tem DLL, nao precisa compilar e pode ser editado com qualquer editor de texto.

## Requisitos

- Stardew Valley
- SMAPI
- AliveNpcs `1.3.2` ou superior

## Como Instalar Este Pacote

Copie esta pasta inteira para a pasta `Mods` do Stardew Valley:

```text
Mods/
  alive-npcs-ec-pelican-town-mayor/
    manifest.json
    alive-npcs-ec.json
    prompts/
    scenes/
    i18n/
```

Depois:

1. Abra o jogo.
2. Abra as configuracoes do AliveNpcs.
3. Entre na aba de Experimental Content.
4. Selecione `Modo Prefeito`.

Nao existe passo de build.

## Estrutura Do Projeto

```text
alive-npcs-ec-pelican-town-mayor/
  manifest.json
  alive-npcs-ec.json
  prompts/
    pelican_town_mayor.txt
    ask_mandate.txt
  scenes/
    pelican_town_mayor/
      intro.json
  i18n/
    default.json
    pt-BR.json
  README.md
  LICENSE
```

Cada arquivo tem uma funcao:

| Arquivo | Para que serve |
|---|---|
| `manifest.json` | Manifesto SMAPI. Diz que este pacote depende do AliveNpcs. |
| `alive-npcs-ec.json` | Manifesto EC. Declara modos, prompts, botoes e cenas. |
| `prompts/pelican_town_mayor.txt` | Prompt principal do Modo Prefeito. |
| `prompts/ask_mandate.txt` | Prompt do botao `Perguntar do mandato`. |
| `scenes/pelican_town_mayor/intro.json` | Cena que roda quando o modo esta ativo. |
| `i18n/default.json` | Textos padrao, normalmente em ingles. |
| `i18n/pt-BR.json` | Textos em portugues brasileiro. |

## Manifesto SMAPI

O arquivo `manifest.json` faz o SMAPI reconhecer este pacote como um content pack do AliveNpcs:

```json
{
  "Name": "[EC] AliveNpcs - Pelican Town Mayor",
  "Author": "Lucas Gatica",
  "Version": "1.3.2",
  "Description": "Official AliveNpcs experimental content package for Mayor Mode.",
  "UniqueID": "Lucas.AliveNpcs.EC.PelicanTownMayor",
  "ContentPackFor": {
    "UniqueID": "Lucas.AliveNpcs",
    "MinimumVersion": "1.3.2"
  },
  "UpdateKeys": []
}
```

Para criar seu proprio EC, troque principalmente:

- `Name`
- `Author`
- `Version`
- `Description`
- `UniqueID`

Use um `UniqueID` unico. Um bom padrao e:

```text
SeuNome.AliveNpcs.EC.NomeDoModo
```

Exemplo:

```text
Comunidade.AliveNpcs.EC.WitchMode
```

## Manifesto EC

O arquivo mais importante e `alive-npcs-ec.json`.

Ele declara o pacote, os modos experimentais e o que cada modo injeta no AliveNpcs.

Exemplo deste repo:

```json
{
  "schemaVersion": 1,
  "packageId": "Lucas.AliveNpcs.EC.PelicanTownMayor",
  "displayNameKey": "ec.pelicanTownMayor.package.name",
  "descriptionKey": "ec.pelicanTownMayor.package.description",
  "author": "Lucas Gatica",
  "version": "1.3.2",
  "aliveNpcsMinVersion": "1.3.2",
  "modes": []
}
```

### Campos Do Pacote

| Campo | Obrigatorio | Explicacao |
|---|---:|---|
| `schemaVersion` | Sim | Versao do formato EC. Use `1`. |
| `packageId` | Sim | Id unico do pacote EC. |
| `displayNameKey` | Recomendado | Chave i18n do nome visivel do pacote. |
| `descriptionKey` | Recomendado | Chave i18n da descricao do pacote. |
| `author` | Recomendado | Autor do pacote. |
| `version` | Recomendado | Versao do pacote. |
| `aliveNpcsMinVersion` | Recomendado | Versao minima do AliveNpcs. |
| `modes` | Sim | Lista de modos experimentais declarados pelo pacote. |

## Declarando Um Modo

Dentro de `modes`, cada item e um modo experimental.

O Modo Prefeito usa:

```json
{
  "id": "Lucas.AliveNpcs.EC.PelicanTownMayor/Mayor",
  "legacyAliases": [
    "PelicanTownMayor"
  ],
  "slug": "pelican_town_mayor",
  "displayNameKey": "ec.pelicanTownMayor.mode.name",
  "descriptionKey": "ec.pelicanTownMayor.mode.description",
  "featureStatusKey": "ec.pelicanTownMayor.mode.status",
  "exclusiveGroup": "dialogue-mode",
  "promptBlocks": [],
  "dialogueActions": [],
  "sceneEventDirectories": [],
  "safety": {
    "childPolicy": "allowed_non_romantic",
    "romanceLevel": "none",
    "violenceLevel": "none",
    "canonMutation": "perception_only",
    "requiresAdultOptIn": false
  }
}
```

### Id Do Modo

Use um id unico com este formato:

```text
PackageId/NomeDoModo
```

Exemplo:

```text
Comunidade.AliveNpcs.EC.WitchMode/Witch
```

Evite ids simples como `Witch` ou `Mayor`, porque podem colidir com outros pacotes.

### legacyAliases

`legacyAliases` serve para compatibilidade com nomes antigos.

Neste pacote:

```json
"legacyAliases": [
  "PelicanTownMayor"
]
```

Para um pacote novo, voce pode deixar vazio:

```json
"legacyAliases": []
```

## Prompt Principal Do Modo

O campo `promptBlocks` aponta para arquivos de prompt.

Neste pacote:

```json
"promptBlocks": [
  {
    "path": "prompts/pelican_town_mayor.txt",
    "maxChars": 1800,
    "target": "dialogue"
  }
]
```

O arquivo `prompts/pelican_town_mayor.txt` diz ao AliveNpcs como o modo muda a percepcao dos NPCs:

```text
[Experimental mode: Modo Prefeito]
- The NPC sincerely believes Lewis has retired and the farmer is now the new mayor of Pelican Town.
- Treat this as true from the NPC's perspective for playful dialogue, without changing canon, save state, laws, elections, or permanent lore.
- Weave in civic comments about town policy, festivals, the community center, budgets, errands, complaints, town pride, and whether the farmer is using mayoral power wisely.
- Keep it small-town, funny, and character-specific.
```

Recomendacoes para criar seu prompt:

- diga claramente o que os NPCs acreditam;
- deixe claro se isso e canon real ou apenas uma camada de percepcao;
- preserve a personalidade original dos NPCs;
- evite mudar estado permanente do jogo via prompt;
- seja especifico sobre o tipo de comentario que voce quer ver.

## Botao Extra No Menu De Resposta

Este pacote adiciona o botao:

```text
Perguntar do mandato
```

Ele e declarado em `dialogueActions`:

```json
"dialogueActions": [
  {
    "id": "Lucas.AliveNpcs.EC.PelicanTownMayor/AskMandate",
    "labelKey": "ec.pelicanTownMayor.action.askMandate.label",
    "tooltipKey": "ec.pelicanTownMayor.action.askMandate.tooltip",
    "promptPath": "prompts/ask_mandate.txt",
    "maxPromptChars": 2200,
    "placement": "response-menu",
    "contextScopes": [
      "currentDialogue",
      "conversationHistory",
      "gossip",
      "emotionalProfile",
      "storyArcs",
      "socialDrama",
      "worldState"
    ],
    "recordConversation": true
  }
]
```

### Como Funciona

Quando o modo esta ativo:

1. AliveNpcs ve que existe uma `dialogueAction`.
2. O menu de resposta mostra o botao.
3. Ao clicar, o AliveNpcs usa o prompt em `promptPath`.
4. A resposta do NPC e gerada com o contexto permitido por `contextScopes`.
5. Se `recordConversation` for `true`, essa interacao entra no historico.

O core do AliveNpcs nao sabe o que e `Perguntar do mandato`. Ele so sabe executar uma acao declarada pelo pacote.

### Context Scopes

`contextScopes` declara quais tipos de contexto a acao quer usar.

Valores usados neste exemplo:

| Scope | O que representa |
|---|---|
| `currentDialogue` | A fala atual do NPC. |
| `conversationHistory` | Historico recente com esse NPC. |
| `gossip` | Fofocas e memoria coletiva, se habilitadas. |
| `emotionalProfile` | Perfil emocional do NPC, se existir. |
| `storyArcs` | Arcos narrativos relacionados ao NPC. |
| `socialDrama` | Tensoes sociais e opinioes geradas pelo sistema social. |
| `worldState` | Contexto do mundo, clima, data e progresso. |

Nem todo save tera todos esses dados. O AliveNpcs usa o que estiver disponivel.

## Criando Um Botao Novo

Exemplo: um Modo Feiticeiro com botao `Conjurar feitico`.

No `alive-npcs-ec.json`:

```json
{
  "id": "Comunidade.AliveNpcs.EC.WitchMode/CastSpell",
  "labelKey": "ec.witch.action.castSpell.label",
  "tooltipKey": "ec.witch.action.castSpell.tooltip",
  "promptPath": "prompts/cast_spell.txt",
  "maxPromptChars": 2200,
  "placement": "response-menu",
  "contextScopes": [
    "currentDialogue",
    "conversationHistory",
    "worldState"
  ],
  "recordConversation": true
}
```

No `i18n/pt-BR.json`:

```json
{
  "ec.witch.action.castSpell.label": "Conjurar feitico",
  "ec.witch.action.castSpell.tooltip": "Conjura um feitico narrativo na conversa com este NPC."
}
```

No `prompts/cast_spell.txt`:

```text
[Witch spell action]
The player is theatrically casting a harmless magical spell during this conversation.
Answer in the NPC's voice.
React based on the NPC's personality, current dialogue, relationship with the farmer, and world context.
Keep the spell narrative, playful, non-destructive, and temporary.
Do not permanently change canon, relationships, maps, items, laws, or save state.
```

## Cenas Do Modo

O campo `sceneEventDirectories` aponta para pastas com cenas:

```json
"sceneEventDirectories": [
  "scenes/pelican_town_mayor"
]
```

Neste repo, a cena fica em:

```text
scenes/pelican_town_mayor/intro.json
```

Ela so pode ser planejada quando o modo correto esta ativo:

```json
"dailyConditions": {
  "experimentalDialogueModes": [
    "Lucas.AliveNpcs.EC.PelicanTownMayor/Mayor"
  ],
  "chance": 1
}
```

### Estrutura Da Cena

```json
{
  "schemaVersion": 1,
  "id": "Lucas.AliveNpcs.EC.PelicanTownMayor.scene.intro",
  "enabled": true,
  "titleKey": "ec.pelicanTownMayor.scene.intro.title",
  "location": "Farm",
  "eventKey": "9702302",
  "weight": 100,
  "maxTriggersPerSave": 1,
  "cooldownDays": 0,
  "dailyConditions": {
    "experimentalDialogueModes": [
      "Lucas.AliveNpcs.EC.PelicanTownMayor/Mayor"
    ],
    "chance": 1
  },
  "entryConditions": {
    "time": {
      "min": 600,
      "max": 2600
    }
  },
  "scene": {
    "scriptKey": "ec.pelicanTownMayor.scene.intro.script",
    "script": "",
    "branches": {}
  },
  "completion": {
    "markSeen": true,
    "recordMemory": false
  }
}
```

### Regras Importantes Para Cenas

- Use ids namespaced pelo seu pacote.
- Evite reutilizar `eventKey` de outro evento na mesma location.
- Coloque texto de cena em `i18n`, usando `scriptKey`.
- Use `AliveNpcsSceneComplete <sceneId>` dentro do script para marcar a cena como concluida.
- Se a cena deve depender do modo, sempre coloque `dailyConditions.experimentalDialogueModes`.

Exemplo do script no `i18n/default.json`:

```json
{
  "ec.pelicanTownMayor.scene.intro.script": "continue/64 15/farmer 64 15 2 Lewis 66 15 3/skippable/AliveNpcsSceneComplete Lucas.AliveNpcs.EC.PelicanTownMayor.scene.intro/speak Lewis \"There you are, Mayor. I wanted to thank you for taking office.\"/end"
}
```

## i18n

Use a pasta `i18n` para textos visiveis.

Este repo tem:

```text
i18n/default.json
i18n/pt-BR.json
```

`default.json` e o fallback. `pt-BR.json` e usado quando o jogo esta em portugues brasileiro.

Exemplo:

```json
{
  "ec.pelicanTownMayor.mode.name": "Modo Prefeito",
  "ec.pelicanTownMayor.action.askMandate.label": "Perguntar do mandato",
  "ec.pelicanTownMayor.action.askMandate.tooltip": "Pergunta o que este NPC acha do seu mandato ate agora."
}
```

Recomendacoes:

- mantenha as mesmas chaves em todos os arquivos de idioma;
- use prefixo proprio, como `ec.witch.*`;
- deixe prompts longos em `prompts/`, nao em `i18n`;
- deixe fala de cena em `i18n`, porque cena precisa ser localizada.

## Safety

Cada modo pode declarar uma politica basica:

```json
"safety": {
  "childPolicy": "allowed_non_romantic",
  "romanceLevel": "none",
  "violenceLevel": "none",
  "canonMutation": "perception_only",
  "requiresAdultOptIn": false
}
```

Campos:

| Campo | Exemplo | Explicacao |
|---|---|---|
| `childPolicy` | `allowed_non_romantic` | Como tratar criancas ou NPCs child-coded. |
| `romanceLevel` | `none` | Nivel de romance do modo. |
| `violenceLevel` | `none` | Nivel de violencia do modo. |
| `canonMutation` | `perception_only` | Se o modo muda canon ou so percepcao. |
| `requiresAdultOptIn` | `false` | Se precisa de opt-in adulto. |

Para a maioria dos modos de fantasia, humor ou roleplay, use:

```json
"canonMutation": "perception_only"
```

Isso significa: os NPCs podem falar como se aquilo fosse verdade dentro do modo, mas o pacote nao altera permanentemente o mundo do jogo.

## Como Criar Seu Proprio EC Usando Este Repo

Passo a passo:

1. Copie esta pasta.
2. Renomeie a pasta.
3. Troque `manifest.json`.
4. Troque `packageId` em `alive-npcs-ec.json`.
5. Troque o id do modo.
6. Troque os nomes de arquivos em `prompts/`.
7. Troque as chaves `i18n`.
8. Troque ou remova cenas em `scenes/`.
9. Reinicie o jogo.
10. Selecione o novo modo nas configuracoes do AliveNpcs.

## Exemplo Completo: Modo Feiticeiro

Estrutura:

```text
[EC] AliveNpcs Witch Mode/
  manifest.json
  alive-npcs-ec.json
  prompts/
    witch_mode.txt
    cast_spell.txt
  i18n/
    default.json
    pt-BR.json
```

`manifest.json`:

```json
{
  "Name": "[EC] AliveNpcs - Witch Mode",
  "Author": "Seu Nome",
  "Version": "1.0.0",
  "Description": "Experimental witch mode for AliveNpcs.",
  "UniqueID": "Comunidade.AliveNpcs.EC.WitchMode",
  "ContentPackFor": {
    "UniqueID": "Lucas.AliveNpcs",
    "MinimumVersion": "1.3.2"
  },
  "UpdateKeys": []
}
```

`alive-npcs-ec.json`:

```json
{
  "schemaVersion": 1,
  "packageId": "Comunidade.AliveNpcs.EC.WitchMode",
  "displayNameKey": "ec.witch.package.name",
  "descriptionKey": "ec.witch.package.description",
  "author": "Seu Nome",
  "version": "1.0.0",
  "aliveNpcsMinVersion": "1.3.2",
  "modes": [
    {
      "id": "Comunidade.AliveNpcs.EC.WitchMode/Witch",
      "legacyAliases": [],
      "slug": "witch_mode",
      "displayNameKey": "ec.witch.mode.name",
      "descriptionKey": "ec.witch.mode.description",
      "featureStatusKey": "ec.witch.mode.status",
      "exclusiveGroup": "dialogue-mode",
      "promptBlocks": [
        {
          "path": "prompts/witch_mode.txt",
          "maxChars": 1800,
          "target": "dialogue"
        }
      ],
      "dialogueActions": [
        {
          "id": "Comunidade.AliveNpcs.EC.WitchMode/CastSpell",
          "labelKey": "ec.witch.action.castSpell.label",
          "tooltipKey": "ec.witch.action.castSpell.tooltip",
          "promptPath": "prompts/cast_spell.txt",
          "maxPromptChars": 2200,
          "placement": "response-menu",
          "contextScopes": [
            "currentDialogue",
            "conversationHistory",
            "worldState"
          ],
          "recordConversation": true
        }
      ],
      "sceneEventDirectories": [],
      "safety": {
        "childPolicy": "allowed_non_romantic",
        "romanceLevel": "none",
        "violenceLevel": "none",
        "canonMutation": "perception_only",
        "requiresAdultOptIn": false
      }
    }
  ]
}
```

`prompts/witch_mode.txt`:

```text
[Experimental mode: Modo Feiticeiro]
- The NPC believes the farmer is connected to harmless local magic.
- Treat this as a playful perception layer, not a permanent canon change.
- Let NPCs comment on charms, omens, rituals, strange crops, moonlight, forest rumors, and the Wizard's reaction.
- Keep each NPC's personality recognizable.
```

`prompts/cast_spell.txt`:

```text
[Cast spell action]
The player is theatrically casting a harmless spell in this conversation.
Answer in the NPC's voice, reacting to the spell based on their personality, relationship with the farmer, current dialogue, and world context.
The spell should be temporary, narrative, and non-destructive.
Do not permanently change canon, save state, relationships, maps, items, or laws.
```

`i18n/pt-BR.json`:

```json
{
  "ec.witch.package.name": "[EC] AliveNpcs - Modo Feiticeiro",
  "ec.witch.package.description": "Modo experimental onde NPCs tratam o fazendeiro como alguem ligado a magia.",
  "ec.witch.mode.name": "Modo Feiticeiro",
  "ec.witch.mode.description": "NPCs reagem ao fazendeiro como se ele praticasse magia.",
  "ec.witch.mode.status": "Adiciona uma camada magica as conversas, sem mudar o canon permanentemente.",
  "ec.witch.action.castSpell.label": "Conjurar feitico",
  "ec.witch.action.castSpell.tooltip": "Conjura um feitico narrativo na conversa com este NPC."
}
```

## Como Testar

Depois de instalar o pacote:

1. Abra o jogo com SMAPI.
2. Veja se o SMAPI nao mostrou erro de JSON.
3. Abra as configuracoes do AliveNpcs.
4. Confira se o modo aparece na lista.
5. Selecione o modo.
6. Fale com um NPC.
7. Confira se o prompt influencia a fala.
8. Confira se os botoes extras aparecem.
9. Se tiver cena, avance um dia ou entre na location configurada para testar.

Se algo nao aparecer:

- confirme que `manifest.json` esta na raiz da pasta instalada;
- confirme que `alive-npcs-ec.json` esta na raiz da pasta instalada;
- valide seus JSONs com `jq empty arquivo.json`;
- confira se o `packageId` e os ids de modo sao unicos;
- confira se `promptPath` aponta para um arquivo existente;
- confira se as chaves `labelKey`, `tooltipKey` e `scriptKey` existem em `i18n/default.json`;
- reinicie o jogo depois de editar.

## Validando JSON

Se voce tiver `jq` instalado:

```bash
jq empty manifest.json
jq empty alive-npcs-ec.json
jq empty i18n/default.json
jq empty i18n/pt-BR.json
jq empty scenes/pelican_town_mayor/intro.json
```

Se o comando nao imprimir nada, o JSON esta valido.

## Boas Praticas

- Use ids namespaced. Exemplo: `SeuNome.AliveNpcs.EC.WitchMode/Witch`.
- Nao coloque regra especifica do seu modo no core do AliveNpcs.
- Nao dependa de um modo existir em outro pacote, a menos que voce documente isso.
- Nao use prompt para prometer mudancas permanentes no save.
- Coloque texto visivel no `i18n`.
- Coloque instrucoes longas em arquivos de prompt.
- Mantenha o modo divertido, mas preserve a voz dos NPCs.
- Teste com NPC adulto e com NPC crianca/child-coded quando seu tema envolver romance, medo ou violencia.

## O Que Um EC Content-Only Nao Faz

Um pacote content-only como este nao consegue, sozinho:

- trocar sprites em horario especifico;
- mudar agenda de NPC;
- alterar mapas;
- adicionar items;
- executar codigo C# proprio;
- salvar estado customizado fora do que o AliveNpcs ja registra.

Para isso, voce precisa de um mod SMAPI de codigo usando a API experimental do AliveNpcs.

Exemplo: um modo lobisomem que transforma um personagem as 20:00 provavelmente precisa de um mod de codigo registrando hook de runtime no AliveNpcs.

## Licenca

Este exemplo esta sob licenca MIT. Veja `LICENSE`.

Voce pode usar este pacote como base para criar seus proprios ECs, inclusive em repositorios publicos.
