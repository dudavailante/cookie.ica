# Controle da loja e disponibilidade

O estado da loja e o estoque ficam em `stock.json`, na raiz do site. Use os IDs do array `PRODUCTS` em `index.html` (`nutella`, `red-velvet`, `laranja-doce-de-leite` e `ninho`); os IDs identificam os sabores sem repetir nomes, preços ou descrições.

Altere `store.open` para `false` para fechar a loja ou `true` para abri-la. Quando fechada, o site mantém o cardápio e a sacola, mas bloqueia novas unidades e o envio do pedido. `store.message` é opcional: quando preenchido, aparece junto ao aviso de que a loja não está aceitando pedidos.

Para esgotar um sabor, ajuste seu `available` para `false` dentro de `products`. Para disponibilizá-lo novamente, altere para `true`. Produtos sem entrada ficam disponíveis por padrão.

O site também aceita temporariamente o formato antigo, em que os IDs dos produtos ficam diretamente na raiz do JSON; nesses arquivos, a loja é considerada aberta. Prefira o formato novo mostrado em `stock.json`. O arquivo deve continuar sendo JSON válido e usar os IDs existentes.

Teste localmente servindo a pasta do site (a leitura do estoque usa `fetch`, então não abra o HTML diretamente como `file://`):

```sh
python3 -m http.server 8000
```

Abra `http://localhost:8000`, altere e salve `stock.json` e recarregue a página. Para testar um item já na sacola, adicione-o, marque-o como esgotado e recarregue: ele será removido, a sacola será atualizada e uma mensagem explicará a alteração. A disponibilidade e o estado da loja são conferidos novamente ao adicionar unidades e ao enviar o pedido.

O site estático encaminha o pedido ao WhatsApp e não possui backend para validar pedidos recebidos. O bloqueio no `stock.json` protege a interface e seus fluxos normais, mas não impede uma mensagem enviada diretamente ao WhatsApp nem oferece validação de servidor contra requisições externas. O site busca o JSON sem usar cache do navegador e bloqueia compras se não conseguir confirmar o estoque e o estado da loja.
