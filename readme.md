# Visão Geral do Projeto

## 1.1 Propósito do Projeto

O projeto de desenvolvimento de um dashboard no Power BI foi concebido para otimizar e automatizar o processo de geração de relatórios de resultados de marketing para os clientes da Dona. Anteriormente, o processo era altamente oneroso, uma vez que exigia a criação manual dos relatórios, consumindo tempo e recursos significativos da equipe. O objetivo principal do projeto era eliminar a necessidade de trabalho manual, tornando o processo mais eficiente, preciso e escalável, para isso, foi utilizado a criação do relatório no Power BI.

## 1.2 Justificativa da Escolha do Power BI

O Power BI foi escolhido como a ferramenta de visualização de dados para este projeto por várias razões:

- **Facilidade de Uso:** O Power BI oferece uma interface intuitiva e amigável, que permite aos usuários ajustar o dashboard e design de maneira rápida e eficiente.
  
- **Conectividade com Diversas Fontes de Dados:** O Power BI possui conectores integrados para uma ampla variedade de fontes de dados, incluindo o Google Sheets, que é a fonte de dados principal deste projeto.
  
- **Capacidades de Visualização Avançadas:** O Power BI oferece uma variedade de visualizações e ferramentas de análise avançadas e altamente personalizadas, como foi neste projeto que permitem criar dashboards interativos e informativos.

## 1.3 Benefícios do Projeto

A implementação do dashboard no Power BI proporcionou uma série de benefícios significativos para a Dona e seus clientes, incluindo:

- **Redução de Custo e Tempo:** Eliminou-se a necessidade de criar manualmente os relatórios mensais que tinham tempo cerca de 20 dias para elaboração. O que é um avanço significativo e grande redução de custos associados ao processo.
  
- **Maior Precisão e Consistência:** O processo automatizado garante uma maior precisão e consistência nos relatórios, minimizando erros humanos.
  
- **Escalabilidade:** O dashboard no Power BI é facilmente escalável para lidar com um maior volume de dados e um número crescente de clientes, sem comprometer o desempenho ou a qualidade.

- **Melhoria da Tomada de Decisão:** Os visuais personalizados e interativos fornecidos pelo dashboard permitem uma análise mais detalhada e uma melhor tomada de decisão por parte dos clientes, ajudando-os a identificar tendências, padrões e oportunidades de melhoria em suas campanhas de marketing.

# Fontes de Dados

## 2.1 Fontes de Dados Utilizadas

A fonte de dados principal é um Google Sheet que contém os dados detalhados das campanhas de marketing dos clientes da empresa.

## 2.2 Processo de Extração de Dados do Google Sheet

Os dados são extraídos do Google Sheet para o Power BI por meio de um processo automatizado. Isso é facilitado pelo conector nativo do Google Sheets no Power BI, que permite que os desenvolvedores se conectem diretamente ao Google Sheet e importem os dados para o modelo de dados do Power BI.

## 2.3 Transformação dos Dados

Após a extração dos dados do Google Sheet, são aplicados processos de transformação no Power BI.

#### 2.3.1 Transformação da Aba Empresas

A **"aba Empresas"** na fonte, alimenta a tabela **dim_empresas** no Power BI, as transformações utilizadas são para alteração de tipagem e remoção de colunas sem utilização.

A **"aba Ações"** na fonte, alimenta a tabela **dim_ações** no Power BI, as transformações utilizadas nesta tabela são para pivotear de colunas para linhas os atributos da ação, remover colunas e filtrar ações que tem como valor igual a 0.

A **"aba Dados"** na fonte, alimenta a tabela **"fato_analise"** no Power BI, as transformações utilizadas nesta tabela são para remover colunas sem utilização, filtrar linhas em branco, limpar a coluna "Título" para melhorar a nuvem de palavras.

## 2.4 Cálculos e Medidas Personalizadas

Além de realizar a limpeza e transformação básica dos dados, nosso processo envolve a criação de cálculos e medidas personalizadas e avançadas. Estas medidas incluem HTML com CSS para garantir a interatividade dos elementos, objetos e componentes de acordo com as necessidades específicas de cada cliente.

As medidas personalizadas são meticulosamente organizadas na tabela **"medidas"**. Cada página tem sua própria pasta, dentro da qual todas as medidas utilizadas na respectiva página são armazenadas. No entanto, algumas medidas são universais e aplicáveis em diversas páginas. Para isso, foram agrupadas dentro da tabela **"medidas"**, na pasta **"general"**.

Nossas fórmulas DAX são elaboradas com uma variedade de condições que devem ser atendidas. Portanto, as funções DAX desempenham um papel crucial nesse processo!

# Modelagem de Dados

## 3.1 Modelo Star Schema

O projeto de dashboard no Power BI utiliza a modelagem de dados Star Schema para facilitar a análise e visualização dos resultados de marketing. Nesse modelo, as tabelas são organizadas em duas categorias principais: tabelas de dimensão e tabelas de fatos.

### 3.1.1 Tabelas de Dimensão

As tabelas de dimensão representam os diferentes atributos pelos quais os dados são analisados. As principais tabelas de dimensão utilizadas neste projeto são:

- **dim_empresas:** Esta tabela contém o cadastro de todas as empresas clientes, fornecendo informações como nome da empresa, objetivo mensal e logo das empresas.

- **dim_calendar:** Esta tabela é criada internamente no Power BI para administrar o período de análise e relacionar as tabelas de fatos. Ela contém informações sobre datas, como dia, mês e ano.

### 3.1.2 Tabelas de Fatos

As tabelas de fatos contêm métricas e medidas numéricas que são analisadas em relação às dimensões. As principais tabelas de fatos utilizadas neste projeto são:

- **fato_acoes:** Esta tabela contém o detalhamento das ações realizadas pela Dona em relação aos seus clientes. Ela inclue informações como tipo de ação e a quantidade realizada no mês.

- **fato_analise:** Esta tabela contém o detalhamento dos dados analisados e tratados pelo time de análise da Dona para informar seus clientes. Ela pode incluir informações como métricas de desempenho, temas de manchete, entre outros.

### 3.1.3 Metadado das colunas

### Tabela dim_calendar;
- date: Representa uma data especifica;
- mes_ano: Representa o mes e ano correspondentes a data;

### Tabela dim_empresas;
- id: Identificador unico da empresa;
- empresa: Nome da empresa;
- objetivo_1, objetivo_2, objetivo_3: Objetivos da empresa;
- imagem_capa_url: URL da imagem da capa relacionada a empresa;
- icon_obj_1_url, icon_obj_2_url, icon_obj_3_url: URLs dos icones relacionados aos objetivos da empresa;
- imagem_analise_url: URL da imagem relacionada a analise da empresa;
- imagem_logos_url: URL da imagem do logotipo da empresa;

### Tabela fato_acoes;
- empresa_id: Chave estrangeira que se relaciona com a tabela dim_empresas, indicando a empresa associada a ação;
- empresa: Nome da empresa;
- data: Data da ação;
- atributo: Atributo relacionado a ação;
- valor: Valor associado ao atributo;
- objetivo_periodo: Objetivo associado ao periodo da ação;
- texto_geral: Texto geral relacionado a ação do mês;
- analise_estrategica: Analise estrategica associada a ação;
- analise_estrat_tra: Analise estrategica tratada;
- texto_geral_trat: Texto geral tratado;

### Tabela fato_analise;
- empresa_id: Chave estrangeira que se relaciona com a tabela dim_empresas, indicando a empresa associada a analise;
- cliente: Cliente associado a analise;
- subcliente: Subcliente associado a analise;
- tema: Tema da analise;
- titulo: Titulo da analise;
- porta_voz: Porta-voz relacionado a analise;
- veiculo: Veiculo de midia associado a analise;
- midia: Tipo de midia;
- jornalista: Jornalista relacionado a analise;
- uf: Unidade federativa relacionada a analise;
- url: URL relacionada a analise;
- cm2: Medida relacionada a area ocupada na analise;
- valoracao: Valor associado a analise;
- alcance: Alcance da analise;
- sentimento: Sentimento relacionado a analise;
- tier: Tier associado a analise;
- origem: Origem da analise;
- protagonismo: Protagonismo associado a analise;
- tier_tier: Tier tratado;
- estado: Estado da analise;
- url_html: URL em HTML relacionada a analise;
- uf_trat: UF tratada;
- data: Data da analise;
- titulo_ajustado: Titulo ajustado da analise;

## 3.2 Relacionamentos entre Tabelas

No modelo Star Schema, as tabelas de dimensão estão relacionadas às tabelas de fatos por meio de chaves estrangeiras. Esses relacionamentos permitem que os usuários analisem e visualizem os dados de diferentes perspectivas, facilitando a compreensão dos resultados de marketing e o processo decisório.

### Desenho da Modelagem de Dados

<img src="https://i.ibb.co/pRvkJSN/project-dona.png" alt="project-dona" border="0">

# Desenvolvimento do Dashboard

Neste capítulo, é apresentado uma descrição detalhada de cada página do dashboard, destacando sua funcionalidade e importância no contexto do relatório de resultados de marketing.

## 4.1 Página Filtro

A **página Filtro** serve como ponto de controle central, permitindo a aplicação de filtros que se estendem a todas as outras páginas do dashboard. Apesar de sua importância nos bastidores, essa página permanece oculta aos olhos do cliente, mantendo a interface limpa e focada no conteúdo. Como essa página é apenas para interação, não foi utilizado recursos visuais.

## 4.2 Página Capa

A **página Capa** é a porta de entrada para o relatório, proporcionando uma primeira impressão impactante. Aqui, a logo da empresa brilha em destaque, acompanhada pelo mês de referência, estabelecendo o tom para a exploração dos dados que virão a seguir.

## 4.3 Página Objetivo

Na **página Objetivo**, delineamos os objetivos estratégicos do período em questão. Essa seção oferece uma visão clara das metas traçadas, orientando a análise dos resultados subsequentes.

## 4.4 Página Resultado 1

A **página Resultado 1** é o palco onde as ações planejadas ganham vida. Aqui, detalhamos as atividades desenvolvidas e apresentamos os resultados obtidos, proporcionando uma análise detalhada das estratégias implementadas.

## 4.5 Página Resultado 2

Na **página Resultado 2**, mergulhamos nos números e nas métricas que definem o sucesso da campanha. Destacamos os resultados alcançados em termos de alcance, quantidade e valoração, diferenciando as conquistas da assessoria das conquistas diretas do cliente.

## 4.6 Página Dashboard 1

A **página Dashboard 1** oferece uma visão panorâmica dos temas abordados e seus respectivos impactos. Aqui, exploramos os detalhes das conquistas, desde o alcance até a valoração, fornecendo insights valiosos para a estratégia futura.

## 4.7 Página Dashboard 1.1

A **página Dashboard 1.1** é reservada para uma análise mais aprofundada quando o cliente tem mais de um subcliente. Nessa seção, mergulhamos nos detalhes específicos de cada subcliente, enriquecendo a compreensão dos resultados obtidos.

## 4.8 Página Dashboard 2

Na **página Dashboard 2**, acompanhamos a evolução das matérias conquistadas mês a mês, explorando o tipo de mídia, a classificação do tier e o sentimento predominante, proporcionando uma visão abrangente do impacto da estratégia de comunicação.

## 4.9 Página Dashboard 3

A **página Dashboard 3** oferece uma perspectiva global da valoração acumulada e do alcance mensal. Aqui, destacamos os números que contam a história do sucesso da campanha, com visualizações impactantes e informativas.

## 4.10 Página Dashboard 4

Na **página Dashboard 4**, mergulhamos na geografia das matérias noticiadas, destacando o título de maior repercussão e sua participação no panorama geral. Além disso, apresentamos um ranking dos principais jornalistas, reconhecendo suas contribuições para a cobertura da campanha.

## 4.11 Página Nuvem

A **página Nuvem** é uma obra de arte textual, transformando as palavras-chave das matérias em uma nuvem de palavras envolvente e esteticamente atraente, proporcionando uma visão instantânea dos temas mais relevantes.

## 4.12 Página Destaques

A **página Destaques** ilumina a matéria de maior repercussão, destacando sua importância no cenário midiático. Aqui, celebramos o sucesso e o impacto da campanha, consolidando as conquistas alcançadas.

## 4.13 Página Análise

Na **página Análise**, reunimos todas as peças do quebra-cabeça, oferecendo um resumo detalhado das ações do fim do mês. Essa seção proporciona uma visão holística dos resultados alcançados e das lições aprendidas.

## 4.14 Página Fim

A **página Fim** marca o encerramento do relatório com estilo e elegância. Aqui, oferecemos uma despedida calorosa, reiterando os pontos-chave e preparando o terreno para futuras explorações.

# Manual de Uso

Para garantir a utilização eficiente do dashboard e a correta exportação para o formato .PDF, é imprescindível que o usuário siga os procedimentos adequados que serão detalhados neste capítulo.

## 5.1 O que não deve ser feito?

Para garantir o sucesso do processo de atualização, é crucial evitar certos pontos, tais como:

    1. Não remover uma coluna;
    2. Não renomear uma coluna, seja alterando uma letra para maiúscula ou minúscula, ou removendo um acento. Tais alterações podem desconfigurar o processamento dos dados;
    3. Não modificar o tipo de dados de uma coluna, por exemplo, inserir texto em uma linha e uma data na linha seguinte;

## 5.2 Como atualizar os dados?

Para efetuar uma atualização, é bem simples, na barra de ferramentas no meio do dashboard existe um botão "Atualizar", ao clicar irá carregar todas as tabelas e notificara com a conclusão. É importante salientar que o processo pode ser feito em qualquer página. 

### 5.2.1 Demonstrativo

<img src="https://i.ibb.co/bBHVhgH/Screenshot-3.jpg" alt="Screenshot-3" border="0">

## 5.3 Exportação em PDF

Para garantir a exportação adequada em .PDF, o usuário deve seguir os seguintes passos:

    1. Selecione o cliente e o filtro de período;
    2. Acesse a página "Destaques";
    3. Clique no botão "Veja a matéria completa";
    4. Capture a tela da imagem e insira-a na página;
    5. Em seguida, proceda com a exportação do dashboard pressionando "CTRL + P" ou navegando até "Arquivo" > "Exportar" > "Exportar em .PDF";

É importante notar que, dependendo do computador utilizado, o arquivo exportado pode apresentar erros de renderização, como imagens cortadas. Para corrigir isso, siga os passos abaixo:

    1. Abra cada página do dashboard individualmente, aguardando o carregamento completo.
    2. Após carregar todas as páginas, tente novamente realizar a exportação.

## Manutenção e Suporte

No âmbito da manutenção e suporte, é fundamental seguir as diretrizes sobre o que não deve ser feito. Caso essas regras não sejam observadas, podem surgir falhas no processo de atualização do dashboard. Para resolver tais problemas, é essencial compreender o registro de logs do erro e buscar soluções conforme as boas práticas e a documentação oficial da Microsoft sobre o Power BI. [Clique aqui para acessar a documentação](https://learn.microsoft.com/pt-br/power-bi/)

Além disso, é importante mencionar que a adição de novas colunas pode exigir suporte adicional. É possível que o Power BI tenha dificuldades em compreender e carregar corretamente essas novas colunas durante a atualização. Nesses casos, recomenda-se consultar a documentação para encontrar a solução adequada.

# Conclusão e Possíveis Melhorias

## 6.1 Conclusão

O desenvolvimento e implementação do dashboard no Power BI para geração automatizada de relatórios de resultados de marketing representam um marco significativo para a Dona e seus clientes. Ao longo deste projeto, alcançamos diversos objetivos e entregamos uma solução eficaz que proporciona benefícios tangíveis e intangíveis para todas as partes envolvidas.

O projeto não apenas simplificou e otimizou o processo de geração de relatórios, mas também elevou o nível de análise e tomada de decisão por parte dos clientes, capacitando-os a compreender e interpretar os dados de forma mais profunda e estratégica. Além disso, a automação proporcionou uma economia significativa de tempo e recursos, permitindo que a equipe se concentrasse em atividades de maior valor agregado.

## 6.2 Benefícios Alcançados

Os benefícios alcançados com a implementação do dashboard no Power BI são vastos e abrangentes. Destacamos alguns dos principais:

- **Eficiência Operacional:** A automação do processo de geração de relatórios resultou em uma significativa redução de custos e tempo, liberando recursos para outras iniciativas estratégicas.

- **Qualidade e Precisão:** A padronização e consistência dos relatórios garantem uma análise precisa e confiável dos resultados de marketing, minimizando erros e discrepâncias nos dados.

- **Tomada de Decisão Informada:** Os visuais interativos e as análises detalhadas proporcionam insights valiosos, capacitando os clientes a tomar decisões mais embasadas e estratégicas em relação às suas campanhas de marketing.

## 6.3 Possíveis Melhorias Futuras

Apesar do sucesso alcançado, reconhecemos que sempre há espaço para melhorias contínuas e inovação. Algumas áreas para possíveis melhorias futuras incluem:

- **Processo de Criação de Banco de Dados:** Explorar a criação do banco de dados para uma solução em nuvem, ou local, visando maior escalabilidade, flexibilidade e potencial de geração de valor com as informações.

- **Integração com Outras Fontes de Dados:** Expandir a conectividade do dashboard para incluir outras fontes de dados relevantes, além do Google Sheets, proporcionando uma visão mais abrangente e integrada das atividades de marketing dos clientes.

- **Implementação de Machine Learning:** Incorporar técnicas de machine learning e análise preditiva para oferecer insights mais avançados e automatizados sobre a análise das matérias, identificando tendências e padrões emergentes.

- **Customização e Personalização Adicionais:** Desenvolver recursos adicionais de customização e personalização para atender às necessidades específicas de cada cliente, permitindo a criação de relatórios ainda mais personalizados e adaptados.

## 6.4 Considerações Finais

O projeto de desenvolvimento do dashboard no Power BI representa apenas o primeiro passo de uma jornada contínua de inovação e excelência na entrega de serviços de análise e relatórios de marketing.

Contudo, este projeto demonstra que a automação e a inteligência de dados são essenciais para o sucesso no mundo moderno dos negócios, e a Dona está posicionada de forma estratégica para liderar essa transformação e oferecer soluções cada vez mais poderosas e inovadoras aos seus clientes.