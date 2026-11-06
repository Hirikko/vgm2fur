# vgm2fur

Aplicativo CLI desenvolvido em Python que permite converter arquivos VGM em módulos do Furnace Tracker (`.fur`).

> [!WARNING] **Versão original descontinuada:** a partir de abril de 2026, o desenvolvedor original declarou esta versão abandonada e sem previsão de suporte.

> Este repositório é um fork independente, mantido com o objetivo de dar continuidade ao projeto e expandir suas funcionalidades.

## Instalação

**Pré-requisitos:**

- Python 3.10 ou superior.

**Etapas de instalação:**

1. Baixe o arquivo wheel da versão desejada na seção de Releases.
2. Instale o arquivo utilizando `pip` ou `pipx`.

Instalação com `pip`:

bash

```
pip install <caminho-para-o-arquivo-wheel>
```

Ou com `pipx`:

bash

```
pipx install <caminho-para-o-arquivo-wheel>
```

Após a instalação, será possível executar `vgm2fur` diretamente pelo terminal.

### Desinstalação

Com `pip`:

bash

```
pip uninstall vgm2fur
```

Ou com `pipx`:

bash

```
pipx uninstall vgm2fur
```

Utilize o comando correspondente à ferramenta usada durante a instalação.

## Utilização

Suponha que você tenha um arquivo VGM chamado `input.vgm` e queira convertê-lo para `output.fur`.

Execute:

bash

```
vgm2fur input.vgm -o output.fur
```

Alternativamente, você pode simplesmente executar:

bash

```
vgm2fur file.vgm
```

Nesse caso, o programa converterá automaticamente `file.vgm` para `file.fur`.

O arquivo VGM de entrada pode estar compactado (`.vgz`) ou descompactado (`.vgm`).

### Opções disponíveis

Você pode adicionar uma ou mais das seguintes opções ao comando.

`iii` representa um valor inteiro e `fff` representa um valor de ponto flutuante.

|Opção|Descrição|
|---|---|
|`--pattern-length=iii`|Define o comprimento dos padrões (patterns) do Furnace, em linhas. Padrão: 128.|
|`--row-duration=fff`|Define a duração de uma linha do Furnace, em amostras (1 amostra = 1/44100 segundo).|
|`--playback-rate=fff`|Define a taxa de reprodução em Hz (quantas linhas serão reproduzidas por segundo).|
|`--skip-samples=iii`|Ignora as primeiras `iii` amostras antes de iniciar a conversão. Útil para eliminar o silêncio inicial.|
|`--ym2612-volume=fff`|Define o volume do chip YM2612. Padrão: 1.|
|`--sn76489-volume=fff`|Define o volume do chip SN76489. Padrão: 1.|
|`--no-latch`|Desativa o mecanismo de retenção de frequência (frequency latching) do YM2612. Pode ser necessário quando algumas notas FM desaparecem no módulo gerado.|

## Conversão em lote

O vgm2fur permite converter arquivos individualmente através da linha de comando.  
Para automatizar a conversão de vários arquivos de uma só vez, disponibilizamos o script `vgm2furs.sh`.

Esse script percorre todos os arquivos `.vgm` presentes no diretório atual e gera automaticamente um módulo `.fur` correspondente para cada arquivo.

### Script `vgm2furs.sh`

bash

```
#!/bin/bash

for file in *.vgm; do
    [ -e "$file" ] || continue

    output="${file%.vgm}.fur"

    echo "Convertendo: $file -> $output"

    vgm2fur "$file" -o "$output"
done

echo "Todas as conversões foram concluídas!"
```

### Como utilizar

1. Coloque o script `vgm2furs.sh` na pasta que contém os arquivos VGM.
2. Conceda permissão de execução:

bash

```
chmod +x vgm2furs.sh
```

3. Execute:

bash

```
./vgm2furs.sh
```

Os módulos `.fur` serão gerados automaticamente na mesma pasta dos arquivos VGM.

**Observação:** o script automatiza a execução individual do conversor para cada arquivo. A conversão em lote é feita pelo próprio script, não por um recurso nativo do vgm2fur.

## Limitações

Atualmente, a versão original oferece suporte apenas a módulos VGM do SEGA Genesis (YM2612 + SN76489), com as seguintes limitações:

- DAC/PCM possui suporte parcial.
- CSM não é suportado. O programa encerrará a execução com um erro caso encontre esse recurso.

O suporte a outros chips e sistemas depende de futuras implementações.

## Desenvolvimento futuro (Mensagem do criador original)

Atualmente estou trabalhando, de forma privada, em uma nova versão do vgm2fur, que deverá ser mais sustentável e extensível a longo prazo. O objetivo é finalmente oferecer suporte completo e sem bugs ao DAC do YM2612 e, posteriormente, provavelmente adicionar suporte a outros chips.

Infelizmente, pelo que parece, ainda serão necessários mais um ou dois anos de trabalho para que essa nova versão alcance o mesmo nível de funcionalidades da versão atual.

Este projeto foi desenvolvido em um ritmo bastante acelerado durante um longo período de férias. Não acredito que consiga dedicar novamente tanto tempo livre ao desenvolvimento adequado deste projeto sem comprometer o desenvolvimento de outros projetos interessantes e inspiradores que também gostaria de realizar.

Se alguém conseguir criar sua própria versão do vgm2fur e torná-la melhor que a minha, ficarei muito feliz em deixar essa responsabilidade para outra pessoa. Aliás, provavelmente até contribuirei com o projeto, porque gosto muito dele.

Mas, até que isso aconteça, posso prometer que continuarei dedicando pelo menos uma hora por semana ao vgm2fur. ❤️

## Continuidade do projeto e contribuições (Fork)

Este repositório é um fork independente, mantido por mim, com o objetivo de dar continuidade ao legado do desenvolvedor original e preservar o excelente trabalho realizado na criação do vgm2fur.

Minha intenção é manter o projeto vivo, ampliar suas funcionalidades e expandir o suporte a diferentes chips de áudio e sistemas.

Gostaria também de convidar outros desenvolvedores, músicos e entusiastas a participarem dessa iniciativa!

Contribuições são muito bem-vindas, especialmente para:

- Desenvolver novos módulos de conversão para diferentes chips de áudio.
- Adicionar suporte a mais sistemas e plataformas de videogames.
- Melhorar a precisão das conversões e a reprodução das características originais de cada chip.
- Corrigir bugs e aprimorar os módulos existentes.
- Expandir a compatibilidade com diferentes formatos e recursos de áudio.
- Melhorar a documentação, os testes e a manutenção do projeto.

O objetivo é construir uma ferramenta cada vez mais completa, capaz de converter músicas de diferentes sistemas e plataformas para módulos do Furnace Tracker, preservando suas características sonoras com a maior fidelidade possível.

Toda contribuição, seja com código, testes, documentação, sugestões ou ideias, será muito bem-vinda.

**Vamos continuar esse legado juntos! ❤️**

## Agradecimentos

Um agradecimento especial ao desenvolvedor original (Alexander Shokhin) pela criação do vgm2fur e por todo o trabalho que tornou este projeto possível.

Este fork busca reconhecer e preservar esse trabalho, dando continuidade ao desenvolvimento e abrindo espaço para que mais pessoas possam contribuir com sua evolução.
