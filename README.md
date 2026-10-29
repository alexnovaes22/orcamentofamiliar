# Orçamento da Família

Orçamento mensal no formato da planilha (Previsto e Real), com os dados sincronizados no Firebase (plano gratuito) e criptografados no navegador antes de serem enviados.

## Publicar no GitHub Pages
1. Envie `index.html`, `README.md` e `.gitignore` para um repositório.
2. Em *Settings → Pages*, escolha a branch `main` e a pasta raiz.
3. Acesse `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`.
4. No Firebase, confira se `SEU-USUARIO.github.io` está em Authentication → Configurações → Domínios autorizados.

## Primeiro acesso
Entre com o e-mail e a senha cadastrados no Firebase. Como a conta ainda não tem dados, o sistema pede o **código de primeiro acesso**, que carrega os dados de 2026 e os grava na nuvem, criptografados com a sua senha. Isso acontece uma única vez.

## Segurança
- A configuração do Firebase no código não é secreta: ela só identifica o projeto.
- Quem protege os dados são as regras do Firestore (cada conta acessa só o próprio cofre) e a criptografia AES-256 feita no navegador. No banco fica apenas texto cifrado.
- **Se esquecer a senha:** "Esqueci minha senha" cria uma senha nova, mas os dados continuam protegidos pela antiga, que o sistema pede uma vez. Sem a senha antiga, só um backup em Excel recupera os dados.

## Regras do Firestore
As regras completas estão no arquivo `firestore.rules`. Cole no Firebase (Firestore Database → Regras → Publicar) sempre que ele mudar.

### Versão anterior (antes da aba Faturas)
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /cofres/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

## Uso
- **Mês:** escolha o mês, alterne entre Previsto e Real e digite os valores. Cada alteração é salva na nuvem, e o status aparece no topo.
- **Ano:** resumo mês a mês, acumulado e gráficos.
- **Backup e conta:** Excel (cópia extra e impressão), PDFs, restauração e troca de senha.

## Aba Faturas
- Importe os PDFs das faturas (Santander, Banco do Brasil, Caixa e Porto) no mês em que elas vencem.
- Use o PDF original baixado do app ou do site do banco. Cópias feitas com "Imprimir como PDF" viram imagem e não podem ser lidas.
- A leitura do PDF acontece no navegador. Só os lançamentos já organizados vão para o Firebase, criptografados.
- O tipo de cada compra é sugerido automaticamente. Ao corrigir um tipo, o sistema aprende o estabelecimento.
- "Enviar para o orçamento" leva os totais por tipo para o Real do mês, sem os gastos de terceiros.

## Pasta lib
As bibliotecas (Firebase, leitor de PDF, Excel, PDF e gráficos) ficam na pasta `lib/` do próprio repositório, em versões fixas. O sistema não carrega código de nenhum servidor externo.

## Primeiro acesso
O código de primeiro acesso foi removido: os dados já estão na nuvem. Em um aparelho novo, basta entrar com e-mail e senha. Se algum dia o cofre precisar ser recriado, use "Usar um backup .xlsx".
