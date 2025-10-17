# GameBallMQTTandHTTP
servidor MQTT, e trẽs clientes jogadores. Você deverá determinar somente para essa parte de criação de partida, como cada jogador irá Publicar ou Assinar tópicos no servidor MQTT visando o gerenciamento da criação de partida.  O jogo (partida iniciada) continua com a comunicação baseada em objetos. 
Atividade Prática 4
SISTEMAS DISTRIBUÍDOS

Agora iremos incrementar o jogo de bolas da última atividade prática. Para isso, utilizaremos o estilo arquitetônico baseado em eventos: https://github.com/Garrocho/sistemas_distribuidos/tree/main/eventos. 

Basicamente, iremos desenvolver a mecânica de criação de partida. Você pode utilizar o jogo Dota 2 de exemplo. Veja como irá funcionar na imagem a seguir:



Nesse caso, teremos então o servidor MQTT, e trẽs clientes jogadores. Você deverá determinar somente para essa parte de criação de partida, como cada jogador irá Publicar ou Assinar tópicos no servidor MQTT visando o gerenciamento da criação de partida.

O jogo (partida iniciada) continua com a comunicação baseada em objetos. O jogo quando iniciar, cada jogador deverá ter uma posição específica, não podendo ser uma posição igual à versão anterior do jogo, para isso, veja o exemplo de posicionamento de jogadores na Tela 4.


# matchmaker_simple.py (MQTT)
# =============================
# Coordenador de criação de partida — **bem simples**
# - Agrupa 3 jogadores.
# - Envia convite individual e espera 10s por ACEITE.
# - Se todos aceitarem, publica START com posições iniciais (não 0,0).
# - Se alguém recusar ou der timeout, publica CANCEL e todos voltam a procurar.
#
# Tópicos (simples):
# Cliente -> Servidor
# mm/find {"player": "Nome"}
# mm/cancel {"player": "Nome"}
# mm/accept/<match_id> {"player": "Nome", "ok": true|false}
# Servidor -> Cliente(s)
# mm/invite/<player> {"match_id": str, "players": ["A","B","C"], "timeout": 10}
# mm/start/<match_id> {"spawns": {"A": [x,y], ...}}
# mm/cancel/<match_id> {"reason": "timeout"|"cancel"}
#
# Uso:
# python matchmaker_simple.py --broker 127.0.0.1 --port 1883
