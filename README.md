# API

  ##
<p align="center">
  <a href="#problema">Problema</a> |
  <a href="#solução">Solução</a> |
  <a href="#tecnologias-utilizadas">Tecnologias Utilizadas</a> |
  <a href="#overview-técnico">Tech Overview</a> |
  <a href="#entregas">Entregas</a> |
  <a href="#saiba-mais">Saiba mais</a>
</p>

##
FATEC São José dos Campos - Professor Jessen Vidal

*Professor:* Eduardo Sakaue

Projeto elaborado para resolver o problema proposto pelo SPC, decidimos utilizar a tecnologia de inteligencia artifical para traçar perfis e recomendar produtos.

## Equipe: 

| *INTEGRANTES*         									|
|---------------------------------------------------|          
| Eduardo Kenji Higa                 |
| Eduardo Vinicius Maia								|
| Luan Matheus Satiro de Oliveira					|
| Pedro Henrique Cerqueira Fernandes (Scrum Master)	|
| Rafael Augusto Campos Plinio (PO)					|

## Problema
### Segmentação do cliente?
Possuem uma segmentação antiga (2013) que não expressa o mercado atual e é pouco utilizada internamente.
### Temos nosso mercado potencial mapeado?
Possuem ferramenta de Market Share, ampla que não possui o detalhamento do potencial financeiro ou perfil, que acaba subutilizada.
### Possuimos análise/estratégia por mercado x produto x concorrente x segmento?
A atual análise pe gerada manualmente, o projeto produzirá automação e extração dessas análises.


## Solução
### Maior detalhamento do cliente, que permitirá ações comerciais personalizadas
Usaremos um algoritmo de recomendação para o setor de vendas do SPC, que irá recomendar o produto mais adequado de acordo com o perfil de cada cliente. Foram selecionadas algumas bases para nos auxiliar nessa complementação de dados para as análises que desejamos. Realizamos uma raspagem de dados na API do twitter. Usaremos os Top Trends de regiões para auxiliar o algoritmo de recomendação.


## Tecnologias Utilizadas
* <p>
  <a href="https://www.python.org/">
  <img alt="Python" src="https://user-images.githubusercontent.com/42500368/114731807-68ebec80-9d18-11eb-8995-f5ccc064a1a5.png" height="30px" style="max-width:100%;"> </a> 
  Python                                                                                                                                           
</p>

* <p>
  <a href="https://flask.palletsprojects.com/en/1.1.x/">
  <img alt="Flask" src="https://user-images.githubusercontent.com/26223657/115167814-3121d380-a08f-11eb-93a0-285ddf1e8fac.png" height="30px" style="max-width:100%;"> </a> 
  Flask                                                                                                                                           
</p>

* <p>
  <a href="https://jinja.palletsprojects.com/en/2.10.x/api/">
  <img alt="Jinja2" src="https://user-images.githubusercontent.com/26223657/115167829-3f6fef80-a08f-11eb-8f52-7fb2e79b760a.png" height="30px"style="max-width: 100%;"> </a>
  Jinja2                                                                                                                                           
</p>

* <p>
  <a href="https://getbootstrap.com/">
  <img alt="Bootstrap" src="https://user-images.githubusercontent.com/26223657/115167815-32eb9700-a08f-11eb-92d5-d5c1d86c733c.png" height="30px"style="max-width: 100%;"> </a>
  Bootstrap                                                                                                                                           
</p>

## Overview técnico

### Google Maps API - O que é geocodificação?
Geocodificação é o processo de conversão de endereços em coordenadas geográficas (como latitude 37,423021 e longitude -122,083739), que você pode usar para colocar marcadores em um mapa ou posicionar o mapa.

A geocodificação reversa é o processo de conversão de coordenadas geográficas em um endereço legível por humanos.

Você também pode usar a API de geocodificação para localizar o endereço de um determinado ID de local.

### Parâmetros obrigatórios em uma solicitação de geocodificação reversa:

latlng - Os valores de latitude e longitude especificando o local para o qual você deseja obter o endereço mais próximo e legível.
Certifique-se de que não haja espaço entre os valores de latitude e longitude quando passados no latlng parâmetro.

(colocar print addressLatLong aqui)
Os "formatted_address"resultados não são apenas endereços postais, mas qualquer forma de nomear geograficamente um local. Por exemplo, ao geocodificar um ponto na cidade de Chicago, o ponto geocodificado pode ser denotado como um endereço de rua, como a cidade (Chicago), como seu estado (Illinois) ou como um país (Estados Unidos). Todos são "endereços" para o geocodificador. O geocodificador reverso retorna qualquer um desses tipos como resultados válidos.

### Twitter API (Análise de Sentimentos)

#### Necessário

  Python 3;
  Conta Twitter Developer;
  Projeto e App, podem ser criados na sua conta (Twitter developer);
  Bearer token (para o cadastro do seu App);
  Conta Microsoft Azure’s Text Analytics Cognitive Service e um endpoint criado (ver o guia da Microsoft para chamadas di Text Abalytics API);
  
  #### Um diretório para o projeto:
  
    mkdir how-positive-was-your-week
    cd how-positive-was-your-week
    touch week.py
    touch config.yaml

#### Configurando o config.yaml

    search_tweets_api:
      bearer_token: xxxxxxxxxxxxxxxxxxxxxxx
    azure:
      subscription_key: xxxxxxxxxxxxxxxxxxxxxxx

#### Instalar as bibliotecas Requests, PyYaML e Pandas

    import requests
    import pandas as pd
    import json
    import ast
    import yaml
    
#### Config da URL

    def create_twitter_url():
        handle = "nomeUsuarioAqui"
        max_results = 100
        mrf = "max_results={}".format(max_results)
        q = "query=from:{}".format(handle)
        url = "https://api.twitter.com/2/tweets/search/recent?{}&{}".format(
            mrf, q
        )
        return url
        
#### URL Criada Será:

    https://api.twitter.com/2/tweets/search/recent?max_results=100&query=from:nomeUsuarioAqui
    
#### Autenticação (config.yaml)

    def process_yaml():
        with open("config.yaml") as file:
            return yaml.safe_load(file)
        
Está função retorna:

    {'data': [{'id': '1272881032308629506', 'text': '@nomadaisy @kndl I just want to do deals with you'}, {'id': '1272880943687258112', 'text': '@nomadaisy @kndl I live too far away to hang responsibly with y’all 😬😭'}, {'id': '1272711045606408192', 'text': '@Babycastles https://t.co/Yfj8SJAnpG'}, {'id': '1272390182231330816', 'text': '@replylord Haha, I broke a glass in your honor today and all so I think I do read your Tweets'}, {'id': '1271810907274915840', 'text': '@replylord I like that I’m the only like here.'}, {'id': '1271435152183476225', 'text': '@Arfness @ChicagoPython @codewithbri @WeCodeDreams @agfors The video seems to be available https://t.co/GojUGdulkP'}, {'id': '1271111488024064001', 'text': 'RT @TwitterDev: Tune in tonight and watch as @jessicagarson takes us through running your favorite Python package in R. 🍿\n\nLearn how to use…'}, {'id': '1270794941892046848', 'text': 'RT @ChicagoPython: Chicago Python will be live-streaming tmrw night!\n\nOur talks:\n- How to run your favorite Python package in R by @jessica…'}, {'id': '1270485552488427521', 'text': "Speaking virtually at @ChicagoPython's __main__ meeting on Thursday night. I'll be showing how to run your favorite Python package in R. https://t.co/TnqgO80I3t"}], 'meta': {'newest_id': '1272881032308629506', 'oldest_id': '1270485552488427521', 'result_count': 9}}
    
#### Conexão com Twitter

    def twitter_auth_and_connect(bearer_token, url):
        headers = {"Authorization": "Bearer {}".format(bearer_token)}
        response = requests.request("GET", url, headers=headers)
        return response.json()

#### Configurando a main function
No final do arquivo você pode configurar a main function que será usada para chamar todas as funções que você criar. Você pode adicionar a função que você criou e chamar a função com uma condição if __name__ == "__main__"

    def main():
        url = create_twitter_url()
        
    if __name__ == "__main__":
        main()
        
#### Adicionando as variáveis url, data, bearer_token, res_json. A main function ficará:
    def main():
        url = create_twitter_url()
        data = process_yaml()
        bearer_token = create_bearer_token(data)
        res_json = twitter_auth_and_connect(bearer_token, url)
        
    if __name__ == "__main__":
        main()
        
 ## Saiba mais
  #### :bellhop_bell:  Links úteis, FAQ e Leitura:
  <a href="https://github.com/2021-FATEC-API-GRUPO-01/API/wiki/Welcome-to-the-SPC-PROJECT-wiki!"> Acesse aqui </a> para saber mais.


## Entregas

### Kick of do projeto: 
* Data: (28/02/2021 a 06/03/2021)

### Sprint 1: 
* Levantamento de requisitos
* Brainstorming
* Análises no Jupyter Notebook
* Escopo do projeto
* Data: (08/03/2021 a 28/03/2021)

### Sprint 2:
* Conclusão da coleta dos requisitos
* Estudos sobre IA
* Análise na API do Twitter
* Elaboração das bases de dados
* Data: (29/03/2021 a 04/04/2021)

### Sprint 3:
* Integração da IA com as bases de dados
* Integração da IA com o back end
* Detalhamentos dos processos técnicos
* Iniciação do front end
* Data: (26/04/2021 a 16/05/2021)

### Sprint 4:
* Deploy do Front
* Diagramação UML
* Integração do Frontend com o Backend
* Data: (17/05/2021 a 05/06/2020)

### Apresentação final:
