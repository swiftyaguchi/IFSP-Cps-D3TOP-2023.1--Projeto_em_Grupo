# IFSP - Campus Campinas
**Pós-graduação em Ciência de Dados**<br>
**Disciplina D3TOP/2023 – Tópicos em Ciência de Dados**


Projeto em Grupo - Parte 1 e 2

“Exercício de análise do projetos de leis municipais da Câmara de Vereadores de Campinas usando técnicas de NLP/ML”

Junho/2023

Professor: Samuel Martins (samuel.martins@ifsp.edu.br) <br>
Aluno: Swift Motoo Yaguchi - CP301665X <br>



# Descrição e motivação do problema

Apesar de serem representantes eleitos pela população, pouco se sabe sobre a produção legislativa dos vereadores de Campinas, produção esta que a midia noticia esporadicamente, com interesses jornalísticos muitas vezes buscando sensacionalismo, e não avaliando a qualidade das propostas de leis produzidas pelos vereadores em seu conjunto.

Campinas tem 33 vereadores, que produzem anualmente centenas de projetos de lei com diversas finalidades, e que são debatidas nas reuniões regulares da Câmara Municipal, sendo que algumas são aprovadas tornando-se leis que irão inflenciar a vida da população da cidade, positiva ou negativamente.

É interessante observar que, além dos 33 vereadores, o Prefeito de Campinas envia também dezenas de projetos de lei à Câmara Municipal sendo que o peso destes para influenciar a vida da população é muito maior, positiva ou negativamente.

A Câmara Muncipal é o espaço onde estes projetos de lei são debatidos e avaliados pelos vereadores, eleitos democraticamente para serem os representantes da população para esta avaliação de toda produção legislativa, seguindo um processo legislativo inicial de avaliação onde participam dezenas de técnicos especialistas da própria Câmara Municipal e Comissões especiais compostas pelos vereadores com apoio de suas equipes de assessores, bem como audiências públicas onde a população tem oportunidade de se manifestar a favor ou contra.

Este processo legislativo é onde o texto dos projetos de lei são avaliados, textos que trazem em seu conteúdo benefícios para a população da cidade, ou não.

Este projeto é um exercício de análise dos projetos de leis municipais da Câmara Municipal de Campinas usando técnicas de NLP e ML para tentar identificar se um texto de projeto de lei pode ser benéfico para a população da cidade.


# Descrição da base de dados

Para este projeto foi montada uma base de dados de projetos de lei da Câmara Municipal de Campinas do ano de 2019, antes da última eleição municipal, e portanto não devendo ter intenção de crítica ou influência à Câmara Municipal em seu mandato corrente.

Há vários tipos de projetos de lei, com finalidades diferentes, e para este projeto foi escolhido o conjunto de PLO's (Projetos de Lei Ordinárias), que são as mais comuns e em quantidade maior. Como referência, o Regimento Interno da Câmara Muncipal descreve os vários tipos de projetos de lei (https://www.campinas.sp.leg.br/atividade-legislativa/regimento-interno).

A base de dados foi montada num arquivo no fromato csv e contém os seguintes campos:

* Texto: texto completo do PLO
* Ementa: resumo do PLO
* Vereador: autor do PLO
* Data: data de apresentação do PLO
* Nota: uma avaliação pessoal do texto do PLO
* isUtil: se o PLO é útil para a cidade ou não (1 ou 0)

O conjunto de Projetos de Leis foi extraído do site da Câmara Muncipal de Campinas
(https://www.campinas.sp.leg.br/atividade-legislativa/producao-legislativa), selecionando o período de 01/01/2019 a 31/12/2019 e PLO como tipo de matéria.

Os PLOs estão disponíveis apenas no formalto pdf e a extração do texto foi feita manualmente, ora utilizando a ferramenta pdftotext da biblioteca pyhton, ora utlizando conversor de pdf para word. Em tempo, recentemente tenho tido diiculdades com as bibliotecas python para extração de texto em arquivos pdf, que não tem mais funcionado, com versões "deprecated", talvez numa tendência de monetização. Convém esclarecer que leis municipais já promulgadas tem seus textos em sites diversos em formato html, inclusivre da Prefeitura de Campinas, que podem ser extraidos com bibliotecas python como beautfulsoup. Projetos de Lei, quando aprovados na Câmara Municipal, são promulgados pelo Prefeito e tornam-se leis municipais.

Os critérios pessoais utilizados para avaliar cada PLO foram os seguintes:

1. Lei reduz custos para a cidade, fiscaliza executivo, combate corrupção <br>
2. Lei melhora a educação, saúde, transporte, segurança, habitação na cidade <br>
3. Lei reduz burocracia na cidade, diminui controle do Estado <br>
4. Lei permite criar empregos ou incentiva empreendedores <br>
5. Lei com benefício real para a cidade de alguma outra forma <br>
6. Lei aumenta custos para a cidade, interfere alçada de outro órgão ou legislação anterior <br>
7. Lei aumenta privilégios apenas para uma parcela menor da cidade <br>
8. Lei prejudica a cidade com aumento de burocracia ou controle do Estado <br>
9. Lei de nome de ruas, praças, e homenagens <br>
10. Lei de datas comemorativas <br>
11. Lei de placas e informativos mas sem atuar na causa e sem benefício real para a cidade <br>
12. Lei  de programas e cursos na rede escolar, sem real benefício para a cidade <br>
13. Lei  de proibições e penalizações sem interação com órgãos fiscalizadores competentes ou sem real benefício para a cidade <br>
14. Lei  sem benefício adicional real para a cidade <br>

Para a rotulação da coluna __isUtil__ considerei como 1 os PLOs de avaliação 1 a 5, e como 0 os restantes de avaliação 6 a 14.

Convém observar que esta rotulação do isUtil pode ser redefinida de acordo com opiniões de cada pessoa com seus critérios de cidadania responsável, podendo dar resultados diferentes, o que é perfeitamente normal numa democracia.



# Objetivo de negócio ou científico associado ao problema

Tendo em vista o processo legislativo descrito acima que envolve muito tempo e uma 
quantidade grande de pessoas para avaliar um projeto de lei, que essencialmente é um texto em 
sua grande maioria, o objetivo deste projeto é buscar otimizar este processo legislativo com 
técnicas de NLP e ML. <br>
Abaixo estão as justificativas para a relevância desse tema:<br>

Importância Social:<br>
1. Transparência Legislativa: A avaliação automatizada de projetos de lei proporciona maior 
transparência no processo legislativo, permitindo que os cidadãos compreendam melhor o 
conteúdo e os impactos das propostas em discussão. Isso fortalece a participação cidadã e a 
democracia, pois promove o engajamento informado dos indivíduos na formulação de políticas 
públicas.<br>
2. Eficiência e Agilidade: A automatização da avaliação de projetos de lei permite uma análise 
mais rápida e precisa, otimizando o trabalho dos legisladores, pesquisadores e demais agentes 
envolvidos na análise legislativa. Isso contribui para a eficiência do processo legislativo, 
agilizando a tramitação de propostas e facilitando a tomada de decisões embasadas em 
evidências.<br>

Importância Científica:<br>
1. Avanços em Processamento de Linguagem Natural: A aplicação de técnicas de NLP na 
análise de projetos de lei impulsiona o desenvolvimento de métodos e algoritmos mais 
sofisticados nessa área. Isso contribui para o avanço do conhecimento científico em NLP, 
abrindo caminho para novas aplicações em diversos domínios.<br>
2. Integração de Dados Legislativos: A avaliação automatizada de projetos de lei permite a 
integração de grandes volumes de dados legislativos, promovendo a construção de bases de 
dados robustas e acessíveis. Essas bases de dados podem ser valiosas para pesquisadores, 
permitindo estudos longitudinais, análises comparativas e a identificação de tendências 
legislativas ao longo do tempo.<br>

Importância Tecnológica:<br>
1. Desenvolvimento de Ferramentas e Sistemas: A pesquisa na avaliação de projetos de lei 
utilizando NLP e ML impulsiona o desenvolvimento de ferramentas e sistemas especializados. 
Essas soluções tecnológicas podem ser utilizadas não apenas para a análise legislativa, mas 
também em outras áreas que requerem processamento e análise de textos jurídicos, como 
escritórios de advocacia, departamentos jurídicos e instituições de pesquisa.<br>
2. Integração com Outras Tecnologias: A combinação de técnicas de NLP e ML com outras 
tecnologias emergentes, como Inteligência Artificial, Big Data e Análise de Redes Sociais, pode 
potencializar ainda mais a análise de projetos de lei. Essas integrações podem revelar insights 
complexos, padrões ocultos e relações entre leis, contribuindo para uma análise legislativa mais 
abrangente e abordagens inovadoras na formulação de políticas públicas.<br>
Portanto, a avaliação de projetos de lei utilizando técnicas de NLP e ML desempenha um papel 
crucial na promoção da transparência, eficiência, avanço científico e desenvolvimento 
tecnológico. Essa abordagem tem o potencial de impactar positivamente a sociedade.


**Para este projeto utilizei como base códigos da disciplina D3TOP e do curso online de AWS Sagmaker/ ML - Lab 2.1**

# Arquitetura AWS para este Projeto

Apresento aqui de forma breve a arquititura AWS utilizada para este projeto:

- o desenvolvimento do modelo é feito em Sagemaker e um endpoint de acesso ao modelo é criado <br>
- o modelo é colocado em produção através do AWS Lambda e API Gateway <br>
- Usuário envia dado de teste remotamente usando URL definida pelo API Gateway para o modelo<br>
- ASW Sagemaker processa os dados recebidos contra o modelo e retona a resposta ao usuário<br>

!![How to build ML Archtecture with AWS Sagemaker + Lambda + API Gateway Hands-on Tutorial](https://github.com/swiftyaguchi/IFSP-Cps-D3TOP-2023.1--Projeto_em_Grupo/assets/96662865/dfa99d5c-d00d-475e-8cea-e7138a0b2efd)
