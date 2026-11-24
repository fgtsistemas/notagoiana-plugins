---
name: notas-fiscais
description: Emitir, consultar e cancelar NFS-e (nota fiscal de serviço) pelo NotaGoiana. Use quando o usuário pedir para emitir uma nota, ver o faturamento, achar uma nota ou um tomador, mandar o link do PDF ao cliente ou cancelar uma nota.
---

# Notas fiscais pelo NotaGoiana

O conector `notagoiana` dá acesso às empresas que o usuário acessa no NotaGoiana. Responda em português do Brasil.

## Emitir

1. Sem o `empresa_id`, comece por `listar_empresas`.
2. Ache o tomador com `buscar_tomadores` (nome, CPF/CNPJ ou e-mail). CNPJ novo também serve: o sistema busca na Receita.
3. `preparar_nota` cria o rascunho com o valor, o tomador e o serviço. Para "igual à do mês passado", ache a nota com
   `buscar_notas` e passe o id em `nota_referencia_id`.
4. Se o usuário pediu para emitir, chame `emitir_rascunho` com o id do rascunho logo em seguida. Se ele só pediu para
   preparar ou conferir, mostre a prévia (tomador, serviço, valor, ISS e competência) e espere o "pode emitir".
5. Depois de emitida, informe o número da NFS-e. `link_da_nota` dá a página com o PDF e o XML para mandar ao cliente.

Pergunte antes só quando faltar um dado (empresa, tomador, valor ou serviço). A competência só muda se o usuário disser.

## Consultar

- `faturamento`: total do período, notas, canceladas, ISS e os maiores tomadores.
- `buscar_notas`, `detalhes_da_nota` e `listar_rascunhos`.

## Cancelar

`cancelar_nota` com o motivo dito pelo usuário (15 a 255 caracteres) e o código: 1 = erro na emissão, 2 = serviço não
prestado, 9 = outros.

## Quando algo é recusado

As recusas vêm com a mesma mensagem da tela do sistema (plano vencido, certificado, empresa fora do acesso). Explique a
mensagem ao usuário com as palavras dela, sem tentar contornar.
