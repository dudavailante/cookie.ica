# Controle de disponibilidade

O estoque fica em `stock.json`, na raiz do site. Use os IDs do array `PRODUCTS` em `index.html` (`nutella`, `red-velvet`, `laranja-doce-de-leite` e `ninho`); os IDs identificam os sabores sem repetir nomes, preços ou descrições.

Para esgotar um sabor, adicione uma entrada com `available` igual a `false`:

```json
{
  "red-velvet": { "available": false },
  "nutella": { "available": false }
}
```

Para disponibilizá-lo novamente, altere para `true` ou remova sua entrada. Sabores sem entrada ficam disponíveis por padrão. O arquivo deve continuar sendo JSON válido e usar os IDs existentes.

Teste localmente servindo a pasta do site (a leitura do estoque usa `fetch`, então não abra o HTML diretamente como `file://`):

```sh
python3 -m http.server 8000
```

Abra `http://localhost:8000`, altere e salve `stock.json` e recarregue a página. Para testar um item já na sacola, adicione-o, marque-o como esgotado e recarregue: ele será removido, a sacola será atualizada e uma mensagem explicará a alteração. A disponibilidade também é conferida novamente ao adicionar unidades e ao enviar o pedido.

Quando revisar a alteração, faça commit e push de `stock.json` para o GitHub. O deploy estático existente do Netlify publica o arquivo junto com o site; não é necessário configurar uma pipeline nova. O site busca o JSON sem usar cache do navegador e bloqueia compras se não conseguir confirmar o estoque.
