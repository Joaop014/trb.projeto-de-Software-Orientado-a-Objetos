# Documentação do Software

# Visão Geral
Este software implementa um sistema de enquetes com a capacidade de criar, visualizar, remover e votar em opções de enquetes. A aplicação foi construída usando o framework Spring Boot e segue uma arquitetura MVC (Model-View-Controller). Ele utiliza o padrão REST para fornecer endpoints acessíveis por meio de requisições HTTP.

# EnqueteController
Métodos
1. listAll()
Descrição: Retorna todas as enquetes cadastradas.
Endpoint: GET /enquete/all
Resposta Sucesso: 200 OK - Retorna uma lista de objetos Enquete.
Resposta Falha: 404 Not Found - Caso não existam enquetes cadastradas.
2. listEnqueteByID(Long id)
Descrição: Retorna uma enquete específica com base no ID fornecido.
Endpoint: GET /enquete/{id}
Parâmetro Path: id - ID da enquete desejada.
Resposta Sucesso: 200 OK - Retorna a enquete correspondente.
Resposta Falha: 404 Not Found - Caso a enquete com o ID especificado não seja encontrada.
3. criar(EnqueteDto enqueteDto)
Descrição: Cria uma nova enquete com base nos dados fornecidos no objeto EnqueteDto.
Endpoint: POST /enquete/novaEnquete
Corpo da Requisição: Objeto EnqueteDto contendo o nome da enquete e as opções.
Resposta Sucesso: 200 OK - Retorna a enquete recém-criada.
Resposta Falha: 400 Bad Request - Caso haja algum problema na criação da enquete.
4. deletar(Long id)
Descrição: Remove uma enquete com base no ID fornecido.
Endpoint: POST /enquete/removerEnquete/{id}
Parâmetro Path: id - ID da enquete a ser removida.
Resposta Sucesso: 200 OK - Caso a enquete seja removida com sucesso.
Resposta Falha: 404 Not Found - Caso a enquete com o ID especificado não seja encontrada.
5. adicionarOpcao(Long enqueteId, OpcaoDto dto)
Descrição: Adiciona uma nova opção a uma enquete existente.
Endpoint: POST /enquete/novaOpcao/{enqueteId}
Parâmetro Path: enqueteId - ID da enquete à qual a opção será adicionada.
Corpo da Requisição: Objeto OpcaoDto contendo o nome da nova opção.
Resposta Sucesso: 200 OK - Caso a opção seja adicionada com sucesso.
Resposta Falha: 404 Not Found - Caso a enquete com o ID especificado não seja encontrada.
6. removerOpcao(Long enqueteId, Long opcaoID)
Descrição: Remove uma opção de uma enquete existente.
Endpoint: POST /enquete/removerOpcao/{enqueteId}/{opcaoID}
Parâmetro Path: enqueteId - ID da enquete à qual a opção pertence.
Parâmetro Path: opcaoID - ID da opção a ser removida.
Resposta Sucesso: 200 OK - Retorna a enquete atualizada após a remoção da opção.
Resposta Falha: 404 Not Found - Caso a enquete ou a opção com os IDs especificados não sejam encontradas.
7. adicionarVoto(Long enqueteID, Long opcaoID)
Descrição: Adiciona um voto a uma opção de uma enquete.
Endpoint: POST /enquete/votar/{enqueteID}/{opcaoID}
Parâmetro Path: enqueteID - ID da enquete à qual a opção pertence.
Parâmetro Path: opcaoID - ID da opção que receberá o voto.
Resposta Sucesso: 200 OK - Retorna a enquete atualizada após a adição do voto.
Resposta Falha: 400 Bad Request - Caso haja algum problema na adição do voto.

##EnqueteServiceImpl

Métodos
1. findById(Long id)
Descrição: Retorna uma enquete com base no ID fornecido.
Parâmetro: id - ID da enquete desejada.
Retorno: Objeto Enquete.
Exceção: NullPointerException - Caso a enquete com o ID especificado não seja encontrada.
2. save(String nome, List<String> opcoes)
Descrição: Salva uma nova enquete com base no nome e nas opções fornecidas.
Parâmetros:
nome - Nome da enquete.
opcoes - Lista de nomes de opções.
Retorno: Objeto Enquete.
Exceção: NullPointerException - Caso haja algum problema na criação ou persistência da enquete.
3. remove(Long id)
Descrição: Remove uma enquete com base no ID fornecido.
Parâmetro: id - ID da enquete a ser removida.
Exceção: NullPointerException - Caso a enquete com o ID especificado não seja encontrada.
4. addVoto(Long enqueteID, Long opcaoId)
Descrição: Adiciona um voto a uma opção de uma enquete.
Parâmetros:
enqueteID - ID da enquete à qual a opção pertence.
opcaoId - ID da opção que receberá o voto.
Retorno: Objeto Enquete.
Exceção: NullPointerException - Caso haja algum problema na adição do voto.
5. removeOpcao(Long enqueteID, Long opcaoId)
Descrição: Remove uma opção de uma enquete.
Parâmetros:
enqueteID - ID da enquete à qual a opção pertence.
opcaoId - ID da opção a ser removida.
Retorno: Objeto Enquete.
Exceção: NullPointerException - Caso a enquete ou a opção com os IDs especificados não sejam encontradas.
6. addOpcao(Long enqueteID, OpcaoDto opcaoDto)
Descrição: Adiciona uma nova opção a uma enquete existente.
Parâmetros:
enqueteID - ID da enquete à qual a opção será adicionada.
opcaoDto - Objeto OpcaoDto contendo o nome da nova opção.
Retorno: Objeto Enquete.
Exceção: NullPointerException - Caso a enquete com o ID especificado não seja encontrada.
7. listAll()
Descrição: Retorna todas as enquetes cadastradas.
Retorno: Lista de objetos Enquete.
Entidades

# 1. Enquete

Atributos:
id - Identificador único da enquete.
nomeEnquete - Nome da enquete.
opcoes - Lista de opções associadas à enquete.

# 2. EnqueteDto

Atributos:
nome - Nome da enquete.
opcoes - Lista de opções associadas à enquete.

# 3. OpcaoDto

Atributos:
nome - Nome da opção.

# 4. Opcao

Atributos:
id - Identificador único da opção.
nome - Nome da opção.
qntVotos - Quantidade de votos recebidos pela opção.

# Repositórios

EnqueteRepository: Responsável pelo acesso aos dados das enquetes.
OpcaoRepository: Responsável pelo acesso aos dados das opções.

# Considerações Finais

Este software fornece um conjunto de APIs REST para gerenciamento de enquetes, opções e votos. Certifique-se de seguir as convenções REST ao realizar chamadas para os endpoints especificados. Além disso, as exceções NullPointerException são utilizadas para lidar com situações em que recursos não são encontrados. Certifique-se de tratar essas exceções adequadamente ao integrar ou estender este software.

