# Jogo do 31

Web app multijogador (um anfitrião cria a mesa, os outros entram com um código de 4 letras). Abre no browser do telemóvel.

## Regras

1. Cada jogador escolhe em segredo um número de 1 a 31 (vários podem escolher o mesmo).
2. À vez, na ordem da mesa, cada um pede um número que ainda não tenha saído — e nunca o seu.
3. Se alguém pedir o teu número, ficas livre e sais da roda.
4. Não há posições: só conta quem fica no fim. O último que sobrar paga.
5. Se os que restam tiverem todos o mesmo número, o jogo acaba logo e pagam todos (ninguém o pode pedir).

## Anfitrião

- Cria a mesa e partilha o código.
- Ordena os jogadores (▲▼) pelos lugares à mesa, escolhe quem começa (▶) e inicia o jogo.
- Pode remover jogadores (✕) e passar a vez de quem estiver desligado.
- No fim, recomeça (mesma ordem, escolhendo quem começa) ou volta à sala de espera.

## Técnico

- `index.html` único, sem build. Publicar via GitHub Pages (`.nojekyll` incluído).
- Tempo real via MQTT sobre WebSocket em brokers públicos (EMQX, HiveMQ, Mosquitto), em paralelo; MQTT.js embutido.
- O anfitrião é autoritativo: guarda o estado, valida as jogadas e envia a cada jogador apenas o seu número secreto
  (os dos outros só são revelados quando saem ou no fim). Estado do anfitrião guardado em `localStorage` (botão "Retomar mesa").
- `?broker=ws://host:porta` troca os brokers (útil para testes com um broker local).
