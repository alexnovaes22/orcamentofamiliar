# Orçamento da Família

Sistema de orçamento familiar com dados no Firebase, criptografados no navegador antes de serem enviados.

## Telas
- **Início:** resultado do mês, alerta dos próximos 3 meses (com avaliação da previsão: otimista, realista ou conservadora), avisos e diagnóstico de para onde vai o dinheiro.
- **Rendas**, em três blocos:
  1. **Renda principal:** holerites em PDF (SEED, NEAD, Unopar), Renda Renata, 13º e férias. É a base para medir o peso das dívidas.
  2. **Renda complementar:** bolsas, estágio, bicos. Conta no mês, mas é temporária e pode ter data para acabar.
  3. **Reserva (poupança):** retiradas ajudam a fechar o mês, mas não são renda; valores guardados não são gasto.
- **Gastos:** Cartões (faturas em PDF), Contas fixas e Outros gastos.
- **Planejamento:** os próximos 12 meses, calculados sozinhos. A meta de gastos do dia a dia é opcional.
- **Backup:** Excel (também serve para restaurar), PDF do mês e do ano, troca de senha.

## Instalação
Envie para o GitHub o `index.html` e a pasta `lib`. Cole o conteúdo de `firestore.rules` no Firebase (Firestore Database → Regras → Publicar) se ainda não tiver feito.

## Segurança
- PDFs de faturas e holerites são lidos no navegador e não são enviados a lugar nenhum.
- CPF, endereço e número completo do cartão não são guardados.
- Tudo o que vai para o Firebase é criptografado com a sua senha.
- As bibliotecas ficam na pasta `lib/`, sem carregar código de servidores externos.
- Excel e PDF baixados não são criptografados: guarde-os em pasta pessoal, nunca no GitHub.
