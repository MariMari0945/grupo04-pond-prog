# Grupo 4

## Casos de Testes


| Nº  | Tipo    | Descrição do Teste                                                              | Resultado Obtido                                | Observações                                      |
| --- | ------- | ------------------------------------------------------------------------------- | ----------------------------------------------- | ------------------------------------------------ |
| 1   | SHA-256 | Hash de string simples ("Hello, World!")                                       | dffd6021bb2bd5b0af676290809ec3a53191dd81c7f70a4b28688a362182986f   | Todas as vezes testadas foi originado o mesmo Hash        |
| 2   | AES-256 | Hash de string simples ("Hello, World!")                                  | 3uuVedkDqKkrDWcRfd5BdQ==  /  yT7MbXl5lYbK/jTAoCCisw==  / ...              | Todas as vezes testadas apresentaram Hashs difertes                          |
| 3   | SHA-256 | Hash de string vazia                                      | e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855              | Surpreende ao apresentar hash próprio e sempre o mesmo hash          |
| 4   | AES-256 | Hash de string vazia                                                           | IFfzNBIRuEHPMxorcDp/zQ==  /  7Pl4UV2Cjka0kgyybBa0OQ==  / ...   | Surpreende ao apresentar hash e ser hashs distintos |
| 5   | SHA-256 | Descriptografia do ciphertext do 1º teste ("Hello, World!")                  |  Null          | A Função não é reversivel e não pode ser Descriptografada dessa forma                          |
| 6   | AES-256 | Descriptografia do ciphertext do 2º teste ("Hello, World!") usando a key              | Hello, World!                           | Reversibilidade comprovada com a Key               |
| 7   | AES-256 | Criptografia de "Hello, World!" utilizando chave fixa e IV aleatório           | Ciphertexts diferentes a cada execução                        | A utilização de IV aleatório garante maior segurança, mesmo com chave constante. |
| 8   | AES-256 | Tentativa de criptografia com chave de tamanho incorreto                       | Erro lançado: chave inválida                     | Tratamento de exceção implementado               |
| 9   | AES-256 | Criptografia e descriptografia de uma string extensa (mais de 1024 caracteres)   | Texto original recuperado integralmente                       | Não importa o tamanho da String ela poderá ser criptografada e recuperada |
| 10  | AES-256 | Comparação entre os modos de operação CBC e ECB utilizando a mesma entrada     | CBC: ciphertext varia com IV; ECB: ciphertext é determinístico  | O modo CBC é preferível, pois evita a exposição de padrões presentes no texto cifrado |

## Explicação

### Método Utilizado

&emsp;No caso de testes da criptografia por SHA-256, foi empregada a biblioteca hashlib para gerar hashes a partir de diferentes entradas – tanto para strings simples quanto para casos especiais, como entradas vazias. Por ser uma função unidirecional, também testamos a impossibilidade de reverter o hash para o valor original.

Para o AES-256, foram realizados testes de criptografia e descriptografia utilizando bibliotecas de criptografia: Crypto.Cipher e Crypto.Util.Padding. As operações foram testadas com parâmetros variados, como:

- Uso de chave e IV (vetor de inicialização) fixos versus IV aleatórios;
- Teste de reversibilidade, onde o texto cifrado é convertido de volta para o texto original mediante o uso correto da chave;
- Criptografia de dados extensos para verificar o funcionamento do padding e a correta divisão em blocos;
- Comparação entre modos de operação (CBC e ECB), demonstrando a importância de escolher um modo mais seguro.

### Insights Obtidos

A criptografia SHA-256 é uma excelente critografia para finalidades que demandam de uma irreversabilidade sem contar com auxilio de uma chave. Apesar desse ponto, ela sempre apresenta os mesmo resultados ao se imputar um mesmo valor, o que pode demonstrar uma vulnerabilidade dela em certas aplicações. Já a criptografia AES-256 possui a chave que permite essa reversabilidade da mensagem trazendo para diversos contextos, como o da blockchain, possibilidades de comunicação e descriptografia de mensagens por chave. Ainda sim vale lembrar a vulnerabilidade de alguém descobrir a chave o que possibilitaria ela de verificar todas as mensagens e descriptografalas também.