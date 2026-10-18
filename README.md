<p align="center">
  <img src="docs/icone.png" width="88" alt="">
</p>
<h1 align="center">Carteiro SBW</h1>
<p align="center">
  As NFS-e e a Nota de Débito da semana, num e-mail para cada franqueado Subway.<br>
  Programa interno do Contas a Receber da ZAMP.
</p>
<p align="center">
  <a href="https://github.com/HenioSampaio/carteiro-sbw-versoes/releases/latest/download/CarteiroSBW.exe"><img alt="Baixar o CarteiroSBW.exe" src="https://img.shields.io/badge/Baixar-CarteiroSBW.exe-15803d?style=for-the-badge&logo=windows11&logoColor=white"></a>
  <a href="https://github.com/HenioSampaio/carteiro-sbw-versoes/releases/latest"><img alt="Versão mais nova" src="https://img.shields.io/github/v/release/HenioSampaio/carteiro-sbw-versoes?style=for-the-badge&label=vers%C3%A3o&color=0f766e"></a>
  <img alt="Windows 10 e 11" src="https://img.shields.io/badge/Windows-10%20%7C%2011-0078D4?style=for-the-badge">
</p>

<p align="center"><img src="docs/tela-arquivos.png" width="860" alt="Carteiro SBW, passo 1: arquivos da semana"></p>

## O que ele faz

- **Gera a Nota de Débito** de cada loja em PDF (o SAP não emite), com os valores da ZFRANQ_002.
- **Junta as NFS-e** que o SAP exporta e avisa se falta alguma.
- **Monta um e-mail por grupo de franqueado** (ou por loja), com a tabela dos documentos e o vencimento.
- **Envia** pela conta Microsoft ou pelo Outlook, com prévia, teste, pausa e controle para nunca mandar a mesma nota duas vezes.

## Instalar

1. Baixe o **CarteiroSBW.exe** pelo botão acima.
2. Clique com o botão direito no arquivo → **Propriedades** → marque **Desbloquear** → **OK**.
3. Abra. Se aparecer *"O Windows protegeu o computador"*, clique em **Mais informações → Executar assim mesmo**.
4. Na primeira vez, o programa pede a **licença** (enviada pelo responsável) e a **pasta do Carteiro** (ele procura sozinho no OneDrive).

Não precisa instalar Python nem mais nada. Depois, para atualizar, basta o botão **Atualizar** dentro do programa.

## Toda semana, em 5 passos

```mermaid
flowchart TB
    subgraph E["📥 1 - ENTRADA · você coloca os arquivos da semana"]
        direction LR
        Z["ZFRANQ_002<br/>valores e documentos"]
        S["Store Database<br/>grupos e e-mails"]
        K["KNA1<br/>CNPJ e endereço"]
        N["PDFs das NFS-e<br/>exportados do SAP"]
    end
    subgraph W["⚙️ o Carteiro faz"]
        direction LR
        P["<b>Prévia</b><br/>gera as NDs e<br/>monta os e-mails"] --> C["<b>Conferir</b><br/>totais e alertas"] --> T["<b>Teste</b><br/>só para você"] --> V["<b>Envio</b><br/>Microsoft ou Outlook"]
    end
    subgraph G["🗂️ fica guardado"]
        direction LR
        O[("2 - SAIDA<br/>NFS-e + ND de cada cliente")]
        F[("enviados.csv<br/>nunca envia 2 vezes")]
    end
    E --> W --> G

    classDef passo fill:#15803d,stroke:#0f5f2c,color:#fff
    classDef arquivo fill:#f1f5f9,stroke:#94a3b8,color:#0f172a
    classDef guarda fill:#fef3c7,stroke:#d97706,color:#78350f
    class P,C,T,V passo
    class Z,S,K,N arquivo
    class O,F guarda
```

| | Passo | O que acontece |
|:-:|---|---|
| 1 | **Arquivos da semana** | Você coloca a ZFRANQ_002, a Store Database, a KNA1 e os PDFs das NFS-e na pasta de entrada. O programa reconhece cada arquivo pelo conteúdo. |
| 2 | **Prévia** | Gera as NDs, junta as NFS-e de cada loja, saneia os e-mails da Store Database e monta os e-mails. Nada é enviado. |
| 3 | **Conferir** | A lista de e-mails, com totais, alertas e o detalhe de cada um. |
| 4 | **Teste** | Alguns e-mails só para você, para ver como chegam. |
| 5 | **Envio** | Envia aos franqueados, com pausa, retomada e relatório no fim. |

<!-- NOVIDADES:INICIO -->
## Novidades da versão 3.3

<sub>18/10/2026</sub>

- A pasta compartilhada guarda só os dados: o código do programa saiu dela, e a tela vem sempre de dentro do CarteiroSBW.exe (ninguém muda a tela de todos sem querer).
<!-- NOVIDADES:FIM -->

O histórico completo está em [Releases](https://github.com/HenioSampaio/carteiro-sbw-versoes/releases) e na tela **Novidades** do programa.

<p align="center"><img src="docs/tela-novidades.png" width="760" alt="Tela de Novidades do Carteiro SBW"></p>

## Perguntas frequentes

<details>
<summary><b>Apaguei o programa e baixei de novo. Perco a licença?</b></summary>
<br>
Não. A licença fica no seu usuário do Windows, não no arquivo. Basta abrir o programa novo.
</details>

<details>
<summary><b>O Windows ou o navegador bloqueou o arquivo.</b></summary>
<br>
O programa não tem assinatura digital de empresa, então o Windows desconfia de arquivos baixados. Faça o passo do <b>Desbloquear</b> (Instalar, item 2). Quem atualiza pelo botão dentro do programa não vê esse aviso.
</details>

<details>
<summary><b>Posso usar em outro computador?</b></summary>
<br>
Sim. A licença vale para o seu usuário da empresa, em qualquer computador em que você entre com ele.
</details>

<details>
<summary><b>Como o programa se atualiza?</b></summary>
<br>
Ele consulta o <code>versao.json</code> deste repositório. Quando há versão nova, baixa o <code>CarteiroSBW.exe</code>, confere o SHA-256 e só então troca o arquivo e reabre.
</details>

## Segurança e privacidade

- Este repositório tem só o programa compilado e o `versao.json`. Nenhuma planilha, nota, e-mail de cliente ou senha.
- O programa só abre com licença emitida pelo responsável, assinada digitalmente (Ed25519) e ligada ao usuário do Windows. Licenças podem ser revogadas.
- A senha ou o login Microsoft ficam protegidos no seu usuário do Windows, nunca em arquivo.
- Cada versão é conferida pelo SHA-256 antes de ser instalada.

<p align="center"><sub>Uso interno · ZAMP III S.A. · código-fonte em repositório privado</sub></p>
