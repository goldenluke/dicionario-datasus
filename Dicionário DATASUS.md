```toc
```

# Dicionário de Variáveis e Guia de Análise para o Sistema de Informações sobre Nascidos Vivos (SINASC)

## Introdução: O SINASC como Pilar da Saúde Materno-Infantil no Brasil

O Sistema de Informações sobre Nascidos Vivos (SINASC), implantado oficialmente pelo Ministério da Saúde a partir de 1990, representa uma das mais importantes e robustas fontes de dados para a vigilância em saúde no Brasil.1 Sua criação foi um marco para a saúde pública nacional, estabelecendo um mecanismo padronizado para a coleta de informações epidemiológicas sobre todos os nascimentos ocorridos no território nacional. O objetivo primordial do sistema é fornecer subsídios essenciais para o planejamento, monitoramento e avaliação de políticas públicas, especialmente aquelas voltadas à saúde materno-infantil, permitindo conhecer o perfil dos nascidos vivos, as condições da gestação e do parto, e as características sociodemográficas das mães.3

A pedra angular do SINASC é a Declaração de Nascido Vivo (DNV), um documento-fonte padronizado cujo preenchimento é obrigatório para todos os nascidos vivos no país, sejam eles de partos hospitalares ou domiciliares.2 A DNV possui um duplo caráter de fundamental importância: primeiramente, é um instrumento epidemiológico que alimenta o sistema com dados vitais; em segundo lugar, tem valor jurídico, sendo o documento hábil e necessário para a lavratura da Certidão de Nascimento nos Cartórios de Registro Civil.8 O formulário, pré-numerado e distribuído em três vias autocopiativas pelo Ministério da Saúde, garante a padronização da coleta em escala nacional.3

A governança do SINASC é descentralizada e tripartite, envolvendo as esferas municipal, estadual e federal, o que reflete a própria organização do Sistema Único de Saúde (SUS).10 O fluxo da informação inicia-se com o preenchimento da DNV nos estabelecimentos de saúde (hospitais, maternidades) ou, em casos de partos domiciliares, nos cartórios. Esses dados são então digitados nos sistemas de informação municipais, que os consolidam e os enviam para as Secretarias Estaduais de Saúde. Estas, por sua vez, realizam uma nova consolidação e enviam a base de dados estadual para o nível federal, onde é gerenciada pela Secretaria de Vigilância em Saúde e Ambiente (SVSA/MS) e disponibilizada publicamente através do Departamento de Informática do SUS (DATASUS).3

Este relatório foi elaborado com o propósito de servir como um dicionário de dados exaustivo e um guia analítico para as 61 variáveis que compõem os microdados do SINASC. O objetivo é capacitar pesquisadores, epidemiologistas, gestores de saúde e cientistas de dados a utilizar esta rica fonte de informação com a máxima precisão, rigor metodológico e criticidade, desvendando não apenas o significado de cada campo, mas também seu potencial analítico e suas limitações intrínsecas.

## Seção 1: Dicionário Detalhado das Variáveis do SINASC

Nesta seção, cada uma das 61 variáveis do dataset do SINASC é descrita em detalhes. As variáveis foram agrupadas por afinidade temática para facilitar a consulta e a compreensão de suas inter-relações.

### 1.1 Variáveis de Identificação e Controle do Sistema

Este grupo de variáveis corresponde a metadados gerados pelo próprio sistema de informação. Embora não sejam tipicamente utilizadas em análises epidemiológicas diretas, são cruciais para a auditoria, gestão da qualidade e rastreabilidade dos dados, permitindo compreender o fluxo e o processamento de cada registro.

- **ORIGEM**: Identifica o sistema ou a origem do banco de dados do qual o registro provém. É uma variável de controle interno do DATASUS.
    
    - **Descrição**: Indica a fonte do processamento do registro (e.g., sistema de entrada municipal, consolidação estadual, base federal).
        
    - **Valores Possíveis**: Códigos numéricos ou textuais que podem variar entre diferentes extrações e versões do sistema.10
        
- **NUMEROLOTE**: Número do lote de envio dos dados.
    
    - **Descrição**: Identifica o conjunto (lote) de registros que foi transmitido da esfera municipal ou estadual para a base nacional. É essencial para rastrear a origem e o momento do processamento de um grupo de registros.10
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **VERSAOSIST**: Versão do software SINASC utilizado para a digitação do registro.
    
    - **Descrição**: Indica a versão do sistema de entrada de dados. Esta informação é relevante para análises históricas, pois mudanças na versão do sistema podem implicar alterações nas regras de validação, na interface de entrada ou na estrutura do banco de dados.10
        
    - **Valores Possíveis**: Texto (e.g., '3.2.02', '3.2.03').
        
- **DTCADASTRO**: Data de cadastro do registro no sistema local.
    
    - **Descrição**: Corresponde à data em que a DNV foi digitada no sistema de informação, no nível municipal ou do estabelecimento de saúde.
        
    - **Valores Possíveis**: Data no formato DDMMAAAA.
        
- **DTRECEBIM**: Data de recebimento do registro no nível central.
    
    - **Descrição**: Data em que o registro foi recebido e processado na base de dados nacional do DATASUS. Em alguns contextos, pode também representar a data da última atualização daquele registro específico.15
        
    - **Valores Possíveis**: Data no formato DDMMAAAA.
        
- **DIFDATA**: Diferença, em dias, entre a data do nascimento e a data do recebimento original.
    
    - **Descrição**: Calculada como `$DTNASC - DTRECORIGA$`. Esta variável é um indicador fundamental da oportunidade do sistema de vigilância, medindo o tempo decorrido entre a ocorrência do evento (nascimento) e seu registro oficial na base de dados. Valores elevados podem indicar atrasos no fluxo da informação.15
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **DTRECORIGA**: Data de recebimento original da Declaração de Nascido Vivo.
    
    - **Descrição**: Campo de referência utilizado para o cálculo da variável `DIFDATA`. Representa a data em que a DNV foi recebida originalmente para processamento.15
        
    - **Valores Possíveis**: Data no formato DDMMAAAA.
        
- **STDNEPIDEM**: Status da DNV Epidemiológica.
    
    - **Descrição**: Indica se o registro provém de uma "Declaração de Nascido Vivo Epidemiológica". Este tipo de DNV é um instrumento utilizado para a coleta de dados de nascimentos conhecidos tardiamente pelo sistema de saúde, como em casos de crianças que faleceram no primeiro ano de vida sem que uma DNV tivesse sido emitida no momento do nascimento. É uma ferramenta crucial para a vigilância do óbito infantil e para a correção da subnotificação de nascimentos.17
        
    - **Valores Possíveis**: `1` (Sim), `0` (Não).
        
- **STDNNOVA**: Status da "DN Nova".
    
    - **Descrição**: Indica se o registro foi preenchido utilizando o novo modelo da Declaração de Nascido Vivo. Esta variável é particularmente relevante para marcar a transição ocorrida a partir de 2011, quando o formulário da DNV foi significativamente alterado, com a inclusão de novas variáveis e a modificação na forma de coleta de outras, como a escolaridade materna.15
        
    - **Valores Possíveis**: `1` (Sim), `0` (Não).
        
- **CONTADOR**: Variável sequencial de contagem.
    
    - **Descrição**: Geralmente um identificador numérico sequencial de registro, gerado durante a extração ou processamento dos dados. Sua função é primariamente de controle interno do banco de dados.
        
    - **Valores Possíveis**: Numérico sequencial.
        

### 1.2 Variáveis de Localização e Estabelecimento de Saúde

Essas variáveis são fundamentais para a epidemiologia e a gestão em saúde, pois permitem a georreferenciação dos eventos e a vinculação dos nascimentos a estabelecimentos de saúde específicos. São a base para análises espaciais, avaliação de acesso a serviços e cálculo de indicadores municipais, estaduais e regionais.

- **CODESTAB**: Código do Estabelecimento de Saúde.
    
    - **Descrição**: Código numérico único que identifica o estabelecimento de saúde (hospital, maternidade, etc.) onde ocorreu o parto, conforme o Cadastro Nacional de Estabelecimentos de Saúde (CNES). Esta variável é extremamente poderosa, pois permite o linkage (cruzamento) com a base de dados do CNES para obter informações detalhadas sobre a unidade de saúde, como sua natureza jurídica (pública, privada), tipo de gestão (municipal, estadual), número de leitos obstétricos e de UTI neonatal, e os tipos de serviços oferecidos.20
        
    - **Valores Possíveis**: Código numérico de 7 dígitos.
        
- **CODMUNNASC**: Código do Município de Nascimento.
    
    - **Descrição**: Código oficial do município onde ocorreu o nascimento, seguindo a tabela de codificação do Instituto Brasileiro de Geografia e Estatística (IBGE).
        
    - **Valores Possíveis**: Código numérico de 6 dígitos. Os dois primeiros dígitos identificam a Unidade da Federação (UF).23
        
- **CODMUNRES**: Código do Município de Residência da Mãe.
    
    - **Descrição**: Código IBGE do município onde a mãe reside. Esta é a variável padrão para o cálculo da vasta maioria dos indicadores de saúde materno-infantil (e.g., taxa de mortalidade infantil, cobertura de pré-natal). A análise por residência, em vez de ocorrência, permite avaliar a situação de saúde da população de um determinado território, corrigindo as distorções causadas pelo deslocamento de gestantes para municípios com maior oferta de serviços de saúde.14
        
    - **Valores Possíveis**: Código numérico de 6 dígitos.
        
- **CODPAISRES**: Código do País de Residência da Mãe.
    
    - **Descrição**: Código que identifica o país de residência da mãe, com base em tabela padronizada pelo DATASUS. É particularmente relevante para estudos sobre saúde de populações migrantes e para a vigilância de eventos de saúde em residentes de outros países que tiveram filhos no Brasil.
        
    - **Valores Possíveis**: Códigos numéricos. O código para o Brasil é `10`.26
        
- **LOCNASC**: Local de Ocorrência do Nascimento.
    
    - **Descrição**: Classifica o local onde o parto ocorreu. É uma variável crucial para monitorar a proporção de partos institucionais versus domiciliares e para identificar nascimentos que ocorrem em condições potencialmente mais arriscadas, fora de estabelecimentos de saúde.8
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Hospital
            
        - `2`: Outro Estabelecimento de Saúde (e.g., Unidade Básica de Saúde, ambulância)
            
        - `3`: Domicílio
            
        - `4`: Outros (e.g., via pública, veículo)
            
        - `5`: Aldeia Indígena
            
        - `9`: Ignorado
            

### 1.3 Variáveis do Recém-Nascido

Este grupo contém as informações vitais, antropométricas e clínicas do recém-nascido, coletadas logo após o nascimento. São a base para a construção de indicadores-chave de saúde neonatal e para a vigilância de agravos.

- **DTNASC**: Data do Nascimento.
    
    - **Descrição**: Data de ocorrência do nascimento.
        
    - **Valores Possíveis**: Data no formato DDMMAAAA.
        
- **HORANASC**: Hora do Nascimento.
    
    - **Descrição**: Hora de ocorrência do nascimento, no formato 24 horas.
        
    - **Valores Possíveis**: Hora no formato HHMM (e.g., 1430 para 14h30).
        
- **SEXO**: Sexo do Recém-Nascido.
    
    - **Descrição**: Sexo biologicamente definido ao nascer.
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Masculino
            
        - `2`: Feminino
            
        - `9`: Ignorado (em modelos mais antigos)
            
        - `0`: Indefinido (em modelos mais recentes da DNV).8
            
- **APGAR1**: Índice de Apgar no 1º Minuto.
    
    - **Descrição**: Pontuação que avalia a vitalidade do recém-nascido no primeiro minuto de vida, baseada em cinco critérios (frequência cardíaca, esforço respiratório, tônus muscular, irritabilidade reflexa e cor da pele). Cada critério recebe uma nota de 0 a 2, totalizando um escore de 0 a 10. Um escore baixo no primeiro minuto é um indicativo da necessidade de manobras de reanimação neonatal.28
        
    - **Valores Possíveis**: Numérico inteiro de 0 a 10.
        
- **APGAR5**: Índice de Apgar no 5º Minuto.
    
    - **Descrição**: Reavaliação do Índice de Apgar no quinto minuto de vida. É considerado um indicador mais robusto da condição do neonato e possui maior valor prognóstico para a sobrevivência neonatal do que o Apgar de 1º minuto. Escores persistentemente baixos (abaixo de 7) no quinto minuto estão associados a um maior risco de asfixia perinatal e complicações neurológicas, embora não seja, isoladamente, um preditor de sequelas a longo prazo.30
        
    - **Valores Possíveis**: Numérico inteiro de 0 a 10.
        
- **RACACOR**: Raça/Cor do Recém-Nascido.
    
    - **Descrição**: Raça ou cor do recém-nascido, conforme declarada pela mãe. Nos modelos mais recentes da DNV (a partir de 2011), esta variável foi substituída pela `RACACORMAE`, pois a raça/cor da mãe é considerada um marcador socioeconômico mais relevante e estável para análises de iniquidades em saúde.19
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Branca
            
        - `2`: Preta
            
        - `3`: Amarela
            
        - `4`: Parda
            
        - `5`: Indígena
            
        - `9`: Ignorado
            
- **PESO**: Peso ao Nascer.
    
    - **Descrição**: Peso do recém-nascido, aferido em gramas. Esta é uma das variáveis mais importantes do SINASC, sendo fundamental para a identificação de recém-nascidos de Baixo Peso ao Nascer (BPN), definido pela OMS como peso inferior a 2.500 gramas. O BPN é um dos mais fortes preditores de mortalidade infantil e de morbidades neonatais.33
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **IDANOMAL**: Identificação de Anomalia Congênita.
    
    - **Descrição**: Variável dicotômica que indica se foi detectada alguma anomalia congênita no recém-nascido no momento do exame físico após o parto.
        
    - **Valores Possíveis (Codificados)**: `1` (Sim), `2` (Não), `9` (Ignorado). Em algumas versões do sistema, pode ser `S` (Sim) ou `N` (Não).
        
- **CODANOMAL**: Código da Anomalia Congênita.
    
    - **Descrição**: Se `IDANOMAL` for "Sim", este campo deve conter o código da anomalia congênita identificada, conforme a Classificação Estatística Internacional de Doenças e Problemas Relacionados com a Saúde, 10ª revisão (CID-10). O campo pode conter um código CID-10 ou uma descrição textual da anomalia. A qualidade desta variável é crucial para a vigilância de defeitos congênitos, como ficou evidente durante a emergência de saúde pública causada pelo vírus Zika, onde o SINASC se tornou uma ferramenta essencial para monitorar os casos de microcefalia (código Q02 da CID-10) e outras manifestações da Síndrome Congênita associada ao Zika (SCZ).35
        
    - **Valores Possíveis**: Código alfanumérico da CID-10 ou texto descritivo.
        

### 1.4 Variáveis da Mãe

Este conjunto de variáveis descreve o perfil sociodemográfico, a naturalidade e a história reprodutiva da mãe, sendo essencial para estudos sobre os determinantes sociais da saúde e as iniquidades nos desfechos materno-infantis.

#### 1.4.1 Dados Sociodemográficos

- **IDADEMAE**: Idade da Mãe.
    
    - **Descrição**: Idade da mãe em anos completos na data do parto. É uma variável fundamental para a análise de risco, pois a gestação nos extremos da vida reprodutiva (adolescência, <20 anos; e idade materna avançada, ≥35 anos) está associada a um maior risco de desfechos adversos tanto para a mãe quanto para o recém-nascido.38
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **DTNASCMAE**: Data de Nascimento da Mãe.
    
    - **Descrição**: Data de nascimento completa da mãe. Permite o cálculo preciso da idade materna e a verificação de consistência com o campo `IDADEMAE`.
        
    - **Valores Possíveis**: Data no formato DDMMAAAA.
        
- **ESTCIVMAE**: Estado Civil/Situação Conjugal da Mãe.
    
    - **Descrição**: Situação conjugal da mãe, autodeclarada. É frequentemente utilizada como um proxy para a rede de apoio social e familiar da gestante.8
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Solteira
            
        - `2`: Casada
            
        - `3`: Viúva
            
        - `4`: Separada judicialmente/Divorciada
            
        - `5`: União estável
            
        - `9`: Ignorado
            
- **ESCMAE**: Escolaridade da Mãe (modelo antigo).
    
    - **Descrição**: Nível de instrução da mãe, em anos de estudo concluídos, conforme o modelo da DNV vigente até 2010.
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Nenhuma
            
        - `2`: 1 a 3 anos de estudo
            
        - `3`: 4 a 7 anos de estudo
            
        - `4`: 8 a 11 anos de estudo
            
        - `5`: 12 anos e mais de estudo
            
        - `9`: Ignorado
            
- **ESCMAE2010**: Escolaridade da Mãe (modelo novo, a partir de 2011).
    
    - **Descrição**: Nível de instrução da mãe, classificado por níveis de ensino, conforme o modelo da DNV implementado a partir de 2011. Esta mudança tornou a variável mais alinhada com as classificações educacionais do país.15
        
    - **Valores Possíveis (Codificados)**:
        
        - `0`: Sem escolaridade
            
        - `1`: Ensino Fundamental I (1ª a 4ª série)
            
        - `2`: Ensino Fundamental II (5ª a 8ª série)
            
        - `3`: Ensino Médio
            
        - `4`: Ensino Superior incompleto
            
        - `5`: Ensino Superior completo
            
        - `9`: Ignorado
            
- **ESCMAEAGR1**: Escolaridade da Mãe Agrupada.
    
    - **Descrição**: Trata-se de uma variável derivada, provavelmente criada pelo DATASUS ou por plataformas de dados para agregar as categorias de escolaridade em faixas mais amplas ou para harmonizar os diferentes formatos de coleta (`ESCMAE` e `ESCMAE2010`) ao longo do tempo.
        
    - **Valores Possíveis**: Códigos numéricos para faixas de escolaridade (e.g., 0-3 anos, 4-7 anos, 8-11 anos, 12+ anos). A especificação exata pode variar dependendo da fonte da extração dos dados.
        
- **SERIESCMAE**: Série Escolar da Mãe.
    
    - **Descrição**: Complementa a variável `ESCMAE2010`, especificando a última série concluída pela mãe dentro dos níveis de ensino Fundamental e Médio.
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **CODOCUPMAE**: Código da Ocupação da Mãe.
    
    - **Descrição**: Código da ocupação habitual da mãe, com base na Classificação Brasileira de Ocupações (CBO). Permite análises sobre a relação entre o tipo de trabalho materno, exposição a riscos ocupacionais e desfechos gestacionais. No entanto, esta variável frequentemente apresenta alta taxa de preenchimento incompleto ou genérico.17
        
    - **Valores Possíveis**: Código numérico de 4 ou 6 dígitos da CBO.
        
- **RACACORMAE**: Raça/Cor da Mãe.
    
    - **Descrição**: Raça ou cor da mãe, autodeclarada. A partir de 2011, esta variável passou a ser coletada diretamente, sendo considerada um marcador socioeconômico crucial para a análise de desigualdades e racismo institucional em saúde, e seu impacto nos desfechos maternos e neonatais.32
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Branca
            
        - `2`: Preta
            
        - `3`: Amarela
            
        - `4`: Parda
            
        - `5`: Indígena
            

#### 1.4.2 Naturalidade

- **NATURALMAE**: Município de Naturalidade da Mãe.
    
    - **Descrição**: Código IBGE do município onde a mãe nasceu.17
        
    - **Valores Possíveis**: Código numérico de 6 dígitos.
        
- **CODMUNNATU**: Código do Município de Naturalidade da Mãe.
    
    - **Descrição**: Campo redundante, geralmente contendo a mesma informação que `NATURALMAE`.
        
    - **Valores Possíveis**: Código numérico de 6 dígitos.
        
- **CODUFNATU**: Código da UF de Naturalidade da Mãe.
    
    - **Descrição**: Código IBGE da Unidade da Federação onde a mãe nasceu.15
        
    - **Valores Possíveis**: Código numérico de 2 dígitos.
        

### 1.5 Variáveis do Histórico Obstétrico e Gestacional

Este grupo de variáveis é fundamental para a avaliação do risco obstétrico, pois descreve a história reprodutiva da mãe e as características da gestação que resultou no nascimento atual.

- **QTDFILVIVO**: Quantidade de Filhos Vivos Anteriores.
    
    - **Descrição**: Número de filhos nascidos vivos que a mãe teve em gestações anteriores.
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **QTDFILMORT**: Quantidade de Filhos Mortos Anteriores.
    
    - **Descrição**: Número de perdas fetais (abortos e natimortos) que a mãe teve em gestações anteriores.
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **QTDGESTANT**: Quantidade de Gestações Anteriores.
    
    - **Descrição**: Número total de gestações prévias, incluindo partos de nascidos vivos, natimortos e abortos.
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **QTDPARTNOR**: Quantidade de Partos Normais Anteriores.
    
    - **Descrição**: Número de partos vaginais que a mãe teve anteriormente.
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **QTDPARTCES**: Quantidade de Partos Cesáreos Anteriores.
    
    - **Descrição**: Número de partos por cesariana que a mãe teve anteriormente. Esta informação é um dos principais determinantes para a Classificação de Robson.
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **PARIDADE**: Paridade da Mãe.
    
    - **Descrição**: Variável derivada que classifica a mãe como primípara (primeira gestação que chega ao parto) ou multípara (já teve partos anteriores). É comumente calculada pela soma de `QTDFILVIVO` e `QTDFILMORT`. Se a soma for igual a 0, a mãe é primípara; se for maior que 0, é multípara. Estudos de avaliação da qualidade do SINASC apontam que as variáveis de base para o cálculo da paridade (`QTDFILVIVO` e `QTDFILMORT`) historicamente apresentam taxas elevadas de incompletude, o que pode comprometer a precisão desta variável derivada.6
        
    - **Valores Possíveis**: `1` (Multípara), `0` (Primípara).
        
- **GESTACAO**: Duração da Gestação (em faixas).
    
    - **Descrição**: Idade gestacional no momento do parto, agrupada em semanas.
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Menos de 22 semanas
            
        - `2`: 22 a 27 semanas
            
        - `3`: 28 a 31 semanas
            
        - `4`: 32 a 36 semanas (prematuro tardio)
            
        - `5`: 37 a 41 semanas (a termo)
            
        - `6`: 42 semanas e mais (pós-termo)
            
        - `9`: Ignorado
            
- **SEMAGESTAC**: Semanas de Gestação (contínua).
    
    - **Descrição**: Idade gestacional em semanas completas. Sendo uma variável contínua, permite análises mais precisas da prematuridade. A qualidade desta variável, no entanto, é um ponto de atenção. Estudos de validação mostram que a idade gestacional é uma das variáveis com menor concordância entre o SINASC e fontes padrão-ouro, com vieses significativos dependendo do método de estimação (DUM vs. ultrassonografia).42
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **DTULTMENST**: Data da Última Menstruação (DUM).
    
    - **Descrição**: Data do primeiro dia da última menstruação da mãe. É o método primário para o cálculo da idade gestacional. A acurácia desta informação depende da memória da mãe e da regularidade de seus ciclos menstruais.8
        
    - **Valores Possíveis**: Data no formato DDMMAAAA.
        
- **TPMETESTIM**: Tipo de Método de Estimação da Idade Gestacional.
    
    - **Descrição**: Indica qual método foi utilizado para estimar a idade gestacional quando a DUM não estava disponível ou não era confiável.
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Exame físico do recém-nascido
            
        - `2`: Outro método (principalmente ultrassonografia)
            
        - `9`: Ignorado.8
            
- **GRAVIDEZ**: Tipo de Gravidez.
    
    - **Descrição**: Classifica a gestação quanto ao número de fetos.
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Única
            
        - `2`: Dupla (gemelar)
            
        - `3`: Tripla ou mais
            
        - `9`: Ignorado.8
            

### 1.6 Variáveis da Assistência Pré-Natal e do Parto

Este conjunto de variáveis permite avaliar a qualidade e o acesso à assistência durante a gestação e o parto, sendo fundamental para monitorar a adequação do pré-natal e as taxas de intervenções obstétricas, como a cesariana.

- **CONSULTAS**: Número de Consultas de Pré-Natal (em faixas).
    
    - **Descrição**: Número de consultas de pré-natal realizadas pela gestante, agrupado em categorias.
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Nenhuma
            
        - `2`: 1 a 3 consultas
            
        - `3`: 4 a 6 consultas
            
        - `4`: 7 e mais consultas
            
        - `9`: Ignorado
            
- **CONSPRENAT**: Número de Consultas de Pré-Natal (contínua).
    
    - **Descrição**: Número exato de consultas de pré-natal. Presente nos modelos mais recentes da DNV, permite uma análise mais detalhada da adequação da assistência.17
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **MESPRENAT**: Mês de Início do Pré-Natal.
    
    - **Descrição**: Mês gestacional em que a primeira consulta de pré-natal foi realizada. É um indicador crucial da captação precoce da gestante pelos serviços de saúde, um dos pilares da qualidade do pré-natal.17
        
    - **Valores Possíveis**: Numérico inteiro (1 a 9).
        
- **PARTO**: Tipo de Parto.
    
    - **Descrição**: Via de parto.
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Vaginal (normal)
            
        - `2`: Cesáreo
            
        - `9`: Ignorado.8
            
- **TPAPRESENT**: Tipo de Apresentação Fetal.
    
    - **Descrição**: Posição do feto no momento do parto.
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Cefálica (de cabeça)
            
        - `2`: Pélvica ou Podálica (sentado ou de pés)
            
        - `3`: Transversa (de lado)
            
        - `9`: Ignorado.8
            
- **STTRABPART**: Trabalho de Parto Induzido.
    
    - **Descrição**: Indica se o trabalho de parto foi iniciado artificialmente por meio de intervenções médicas (e.g., uso de ocitocina ou misoprostol).
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Sim
            
        - `2`: Não
            
        - `9`: Ignorado.8
            
- **STCESPARTO**: Cesárea Antes do Trabalho de Parto.
    
    - **Descrição**: Indica se a cesariana foi realizada antes do início do trabalho de parto, caracterizando uma cesárea eletiva ou agendada. É uma variável crucial para diferenciar os tipos de cesárea e para a Classificação de Robson.8
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Sim
            
        - `2`: Não
            
        - `3`: Não se aplica (se o parto não foi cesáreo)
            
        - `9`: Ignorado
            
- **TPNASCASSI**: Nascimento Assistido Por.
    
    - **Descrição**: Identifica o tipo de profissional de saúde que realizou a assistência ao parto.
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Médico(a)
            
        - `2`: Enfermeiro(a) ou Obstetriz
            
        - `3`: Parteira tradicional
            
        - `4`: Outros
            
        - `9`: Ignorado.8
            

### 1.7 Variáveis do Pai e dos Responsáveis pelo Preenchimento

Este grupo final de variáveis identifica o pai (quando a informação está disponível) e o profissional responsável por preencher a DNV, o que é importante para fins de responsabilidade e auditoria da informação.

- **IDADEPAI**: Idade do Pai.
    
    - **Descrição**: Idade do pai em anos completos. Esta variável é notória por apresentar uma alta taxa de não preenchimento.17
        
    - **Valores Possíveis**: Numérico inteiro.
        
- **TPFUNCRESP**: Função do Responsável pelo Preenchimento.
    
    - **Descrição**: Função ou cargo da pessoa que preencheu a DNV.
        
    - **Valores Possíveis (Codificados)**: `1` (Médico), `2` (Enfermeiro), `3` (Parteira), `4` (Funcionário de cartório), `5` (Outros).17
        
- **TPDOCRESP**: Tipo de Documento do Responsável.
    
    - **Descrição**: Tipo de documento de identificação profissional do responsável pelo preenchimento.
        
    - **Valores Possíveis (Codificados)**: `1` (CNES), `2` (CRM), `3` (COREN), `4` (RG), `5` (CPF).17
        
- **DTDECLARAC**: Data da Declaração.
    
    - **Descrição**: Data em que a DNV foi preenchida.
        
    - **Valores Possíveis**: Data no formato DDMMAAAA.17
        

### 1.8 Variáveis Derivadas e Índices Compostos

A inclusão de índices complexos pré-calculados nos datasets do SINASC representa uma evolução significativa do sistema. Isso democratiza o acesso a análises mais sofisticadas, mas exige que o usuário compreenda profundamente a metodologia por trás de cada índice para garantir sua correta interpretação e uso.

- **TPROBSON**: Classificação de Robson.
    
    - **Descrição**: Classifica todas as parturientes em um dos 10 grupos mutuamente exclusivos e totalmente inclusivos, com base em cinco características obstétricas: paridade, cesárea anterior, idade gestacional, apresentação fetal e início do trabalho de parto.
        
    - **Propósito**: É a ferramenta padrão-ouro recomendada pela Organização Mundial da Saúde (OMS) para monitorar, auditar e comparar as taxas de cesárea. Sua aplicação permite que hospitais e sistemas de saúde identifiquem quais grupos de mulheres estão contribuindo mais para as taxas gerais de cesárea, direcionando estratégias para a redução de procedimentos desnecessários e a promoção do parto vaginal.46 Uma descrição detalhada dos critérios de cada grupo encontra-se no Apêndice C.
        
    - **Valores Possíveis**: Numérico inteiro de 1 a 10.
        
- **KOTELCHUCK**: Índice de Adequação do Pré-Natal de Kotelchuck.
    
    - **Descrição**: Também conhecido como _Adequacy of Prenatal Care Utilization Index_ (APNCU), este é um índice composto que avalia a adequação do uso dos serviços de pré-natal. Ele combina duas dimensões críticas: (1) o **início da assistência** (medido pelo mês gestacional da primeira consulta) e (2) a **adequação dos serviços recebidos** (medida pela razão entre o número de consultas observadas e o número de consultas esperadas para a idade gestacional, ajustada pelo mês de início).
        
    - **Propósito**: Oferece uma medida muito mais refinada e abrangente da qualidade do pré-natal do que a simples contagem de consultas. Permite classificar a assistência pré-natal em categorias que refletem tanto a captação precoce da gestante quanto a continuidade do cuidado, sendo um poderoso indicador para avaliar a efetividade das políticas de atenção à gestante.50 A metodologia de cálculo está detalhada no Apêndice D.
        
    - **Valores Possíveis (Codificados)**:
        
        - `1`: Inadequado
            
        - `2`: Intermediário
            
        - `3`: Adequado
            
        - `4`: Mais que Adequado (ou Intensivo)
            

## Seção 2: Guia Prático para a Análise dos Dados do SINASC

Utilizar os microdados do SINASC requer mais do que apenas conhecer as definições das variáveis. É fundamental ter uma compreensão crítica da qualidade dos dados, dos desafios metodológicos em análises temporais e do potencial analítico que pode ser desbloqueado por meio de técnicas avançadas.

### 2.1 Qualidade dos Dados: Completude, Consistência e Validade

A qualidade dos dados é a base para qualquer análise confiável. No SINASC, embora a cobertura geral seja elevada, a qualidade de variáveis específicas pode variar consideravelmente.

- **Completude**: A cobertura do SINASC, ou seja, sua capacidade de captar a totalidade dos nascimentos, é superior a 90% na maioria dos estados e municípios, sendo considerada de boa a excelente.54 No entanto, a completude, que se refere ao preenchimento de cada campo dentro de um registro, é heterogênea. Variáveis sociodemográficas como
    
    `CODOCUPMAE` (ocupação da mãe) e `IDADEPAI`, e variáveis de histórico obstétrico como `QTDFILVIVO` e `QTDFILMORT`, são historicamente as mais afetadas por altas taxas de dados faltantes ou preenchidos como "ignorado".40 Para avaliar a completude, pesquisadores brasileiros frequentemente utilizam o escore de Romero e Cunha, que classifica a qualidade do preenchimento em categorias como: excelente (<5% de incompletude), bom (5% a <10%), regular (10% a <20%), ruim (20% a <50%) e muito ruim (≥50%).58
    
- **Consistência e Validade**: A validade de uma variável refere-se ao grau em que ela mede o que se propõe a medir. Estudos que comparam os dados do SINASC com fontes padrão-ouro, como prontuários médicos ou pesquisas primárias (a exemplo do inquérito "Nascer no Brasil"), são essenciais para avaliar essa dimensão.59 Tais estudos revelam que, enquanto variáveis como
    
    `PESO` e `SEXO` possuem altíssima concordância, outras são mais problemáticas. A variável `SEMAGESTAC` (idade gestacional) é consistentemente apontada como uma das de menor validade. A concordância é apenas moderada, e há evidências de que a estimativa baseada na DUM tende a superestimar tanto a prematuridade quanto a pós-maturidade em comparação com a ultrassonografia precoce, que é considerada mais acurada.42
    

A heterogeneidade na qualidade dos dados entre as diferentes regiões e municípios do Brasil é uma implicação direta desses achados.61 Análises de abrangência nacional devem, portanto, ser interpretadas com cautela, e os pesquisadores devem sempre considerar a realização de análises de sensibilidade para testar o impacto dos dados faltantes ou inconsistentes em seus resultados. A etapa de limpeza e tratamento de dados, incluindo a verificação de consistência (e.g.,

`IDADEMAE` vs. `DTNASCMAE`) e a decisão sobre como lidar com valores ignorados ou implausíveis, é um passo pré-analítico indispensável e que deve ser detalhadamente descrito na metodologia de qualquer estudo.63

### 2.2 Desafios em Análises Longitudinais: A Harmonização de Variáveis

A análise de tendências temporais com dados do SINASC é uma ferramenta poderosa, mas enfrenta um desafio metodológico significativo: as mudanças no formulário da DNV ao longo do tempo. A revisão de 2011, em particular, alterou a forma de coleta de variáveis-chave, criando quebras estruturais que, se não tratadas, podem levar a conclusões espúrias.18

Um exemplo clássico é a variável de escolaridade materna. Antes de 2011, a variável `ESCMAE` era coletada em faixas de anos de estudo. A partir de 2011, a variável `ESCMAE2010` passou a ser coletada em níveis de ensino. Para conduzir uma análise de série temporal que atravesse esse período, é imprescindível harmonizar as duas variáveis, criando uma terceira, consistente ao longo de todo o período. A tabela abaixo propõe um método para essa harmonização.

**Tabela 1: Proposta de Harmonização para a Variável de Escolaridade Materna**

|`ESCMAE` (Pré-2011)|`ESCMAE2010` (Pós-2011)|Variável Harmonizada (Proposta)|
|---|---|---|
|**Código/Descrição**|**Código/Descrição**|**Código/Descrição**|
|1: Nenhuma|0: Sem escolaridade|1: Sem escolaridade|
|2: 1 a 3 anos|1: Fundamental I (1ª a 4ª)|2: Ensino Fundamental|
|3: 4 a 7 anos|2: Fundamental II (5ª a 8ª)|2: Ensino Fundamental|
|4: 8 a 11 anos|3: Médio|3: Ensino Médio|
|5: 12 anos e mais|4: Superior incompleto|4: Ensino Superior|
|5: 12 anos e mais|5: Superior completo|4: Ensino Superior|
|9: Ignorado|9: Ignorado|9: Ignorado|

A aplicação de um procedimento de harmonização como este é um pré-requisito metodológico para qualquer estudo que busque analisar tendências de longo prazo envolvendo variáveis que sofreram alterações em sua forma de coleta.

### 2.3 Potencializando Análises com Linkage de Dados

O linkage, ou relacionamento de bases de dados, é uma técnica que expande exponencialmente o potencial analítico do SINASC. O processo pode ser determinístico, quando se utiliza um identificador único e comum entre as bases (como o número da DNV), ou probabilístico, que utiliza algoritmos para calcular a probabilidade de dois registros pertencerem ao mesmo indivíduo com base em um conjunto de variáveis (como nome da mãe, data de nascimento e município de residência).65

A aplicação mais poderosa é o linkage do SINASC com o Sistema de Informações sobre Mortalidade (SIM). Este procedimento permite a construção de coortes de nascimentos, possibilitando seguir os recém-nascidos ao longo do tempo para verificar a ocorrência de óbitos.67 Com isso, torna-se possível realizar estudos de sobrevida e analisar os fatores de risco para a mortalidade infantil, associando as características do nascimento (e.g., peso, idade gestacional, Apgar) ao desfecho óbito. Além disso, o linkage é uma ferramenta valiosa para a qualificação de ambos os sistemas, pois permite preencher informações faltantes ou corrigir inconsistências em uma base de dados utilizando as informações da outra. Estudos mostram que mais de 90% dos campos incompletos em variáveis comuns podem ser recuperados através desta técnica.66

Apesar de seu grande potencial, a técnica apresenta desafios. A qualidade dos campos-chave utilizados para o pareamento é fundamental, e erros de digitação ou informações incompletas (especialmente no nome da mãe) podem resultar em falhas de linkage. A incapacidade de parear um subconjunto de registros pode introduzir um viés de seleção, caso os registros não pareados tenham características sistematicamente diferentes dos pareados. Portanto, é crucial que os estudos que utilizam linkage descrevam detalhadamente sua metodologia e analisem as características dos registros perdidos no processo.70

### 2.4 Fronteiras da Análise com Dados do SINASC: Aplicações Avançadas

O SINASC serve de base para uma gama crescente de análises sofisticadas que informam a pesquisa e a política de saúde.

- **Análise Espacial**: As variáveis de geolocalização (`CODMUNRES`, `CODMUNNASC`) são a base para estudos de epidemiologia espacial. Essas análises permitem mapear a distribuição de desfechos perinatais, como baixo peso ao nascer ou prematuridade, identificando clusters (aglomerados) de alto risco e revelando profundas desigualdades geográficas no acesso e na qualidade dos serviços de saúde.72
    
- **Machine Learning e Modelos Preditivos**: Com o avanço da ciência de dados, os microdados do SINASC têm sido cada vez mais utilizados para treinar algoritmos de aprendizado de máquina (_machine learning_). O objetivo é desenvolver modelos capazes de predizer o risco de desfechos adversos (e.g., mortalidade neonatal, baixo peso ao nascer) com base em um conjunto de variáveis preditoras (características da mãe, da gestação e do parto). Esses modelos podem, no futuro, ser integrados a sistemas de apoio à decisão clínica para identificar gestantes e recém-nascidos de alto risco precocemente.75
    
- **Avaliação de Políticas Públicas**: O SINASC é uma ferramenta indispensável para a avaliação do impacto de políticas públicas e programas sociais em larga escala. Estudos recentes, por exemplo, utilizaram o linkage de dados do SINASC com registros do Cadastro Único para Programas Sociais (CadÚnico) para avaliar o impacto do Programa Bolsa Família. Os resultados demonstraram um efeito protetor significativo do programa, com uma redução substancial no risco de mortalidade materna entre as mulheres beneficiárias, especialmente aquelas com maior tempo de exposição ao programa.79 Essas análises fornecem evidências robustas sobre o papel de políticas de transferência de renda na melhoria dos indicadores de saúde.
    

## Conclusão: O SINASC como Ferramenta Dinâmica para a Vigilância e Pesquisa

O Sistema de Informações sobre Nascidos Vivos transcende a função de um mero repositório de dados. Ele se consolida como um sistema de informação dinâmico, essencial para a vigilância epidemiológica e um pilar para a pesquisa em saúde materno-infantil no Brasil. Sua abrangência nacional, a padronização da coleta de dados e a disponibilidade pública de seus microdados o tornam um recurso de valor inestimável. Como demonstrado ao longo deste relatório, o SINASC permite não apenas o monitoramento contínuo de indicadores vitais, mas também a condução de análises complexas sobre determinantes sociais da saúde, desigualdades regionais e o impacto de políticas públicas.

A capacidade do sistema de se adaptar a novas demandas de vigilância, como ficou evidente durante a emergência sanitária do vírus Zika, reforça sua relevância estratégica. No entanto, a utilização eficaz de seus dados exige uma abordagem crítica e metodologicamente rigorosa. Os pesquisadores e analistas devem estar cientes das limitações do sistema, especialmente no que tange à qualidade variável de certos campos e aos desafios impostos por mudanças nos instrumentos de coleta ao longo do tempo. A etapa de pré-processamento dos dados — incluindo limpeza, verificação de consistência e harmonização de variáveis — não é apenas uma boa prática, mas um requisito fundamental para garantir a validade e a confiabilidade dos resultados.82

O futuro do SINASC e dos demais sistemas de informação em saúde no Brasil aponta para uma maior integração e interoperabilidade. A incorporação progressiva à Rede Nacional de Dados em Saúde (RNDS) promete revolucionar a forma como as informações de saúde são compartilhadas, permitindo uma visão mais longitudinal e integrada do cuidado ao paciente.83 Este avanço, contudo, trará consigo novos desafios técnicos, de governança e de privacidade, que exigirão soluções robustas para garantir a segurança e o uso ético dos dados. Em suma, o SINASC continuará a ser uma ferramenta indispensável, evoluindo para fornecer as evidências necessárias para a construção de um sistema de saúde mais equitativo e eficaz para mães e crianças no Brasil.

---

## Apêndices

### Apêndice A: Mapeamento de Variáveis do Dataset para Campos da DNV

A tabela a seguir correlaciona as principais variáveis do dataset do SINASC com seus respectivos campos no formulário da Declaração de Nascido Vivo (modelo 2022), facilitando a compreensão da origem de cada dado.

**Tabela A1: Mapeamento Variáveis SINASC vs. Campos DNV**

|Nome da Variável (Dataset)|Campo na DNV (Número e Descrição)|Bloco da DNV|
|---|---|---|
|`DTNASC`, `HORANASC`|2. Data e Hora do Nascimento|I - Identificação do recém-nascido|
|`SEXO`|3. Sexo|I - Identificação do recém-nascido|
|`RACACOR`|3a. Raça/cor do recém-nascido|I - Identificação do recém-nascido|
|`PESO`|4. Peso ao nascer|I - Identificação do recém-nascido|
|`APGAR1`, `APGAR5`|5. Índice de Apgar (1º e 5º minuto)|I - Identificação do recém-nascido|
|`IDANOMAL`, `CODANOMAL`|6. Detectada alguma anomalia congênita? / 41. Descrever...|I e VI - Anomalia Congênita|
|`LOCNASC`|7. Local da ocorrência|II - Local da ocorrência|
|`CODESTAB`|8. Estabelecimento (Código Cnes)|II - Local da ocorrência|
|`CODMUNNASC`|12. Município de ocorrência|II - Local da ocorrência|
|`IDADEMAE`|19. Idade|III - Parturiente|
|`ESCMAE2010`, `SERIESCMAE`|16. Escolaridade (última série concluída)|III - Parturiente|
|`CODOCUPMAE`|17. Ocupação habitual|III - Parturiente|
|`ESTCIVMAE`|21. Situação conjugal|III - Parturiente|
|`RACACORMAE`|22. Raça/Cor|III - Parturiente|
|`CODMUNRES`|26. Município (Residência)|III - Parturiente|
|`IDADEPAI`|29. Idade (Responsável legal)|IV - Responsável legal|
|`QTDFILVIVO`, `QTDFILMORT`|30. Histórico gestacional|V - Gestação e parto|
|`DTULTMENST`, `SEMAGESTAC`|31/32. Idade Gestacional|V - Gestação e parto|
|`CONSPRENAT`|33. Número de consultas de pré-natal|V - Gestação e parto|
|`MESPRENAT`|34. Mês de gestação em que iniciou o pré-natal|V - Gestação e parto|
|`GRAVIDEZ`|35. Tipo de gravidez|V - Gestação e parto|
|`TPAPRESENT`|36. Apresentação|V - Gestação e parto|
|`STTRABPART`|37. O trabalho de parto foi induzido?|V - Gestação e parto|
|`PARTO`|38. Tipo de parto|V - Gestação e parto|
|`STCESPARTO`|39. Cesárea ocorreu antes do trabalho de parto iniciar?|V - Gestação e parto|
|`TPNASCASSI`|40. Nascimento assistido por|V - Gestação e parto|

### Apêndice B: Tabela de Códigos para Variáveis Categóricas Selecionadas

Este apêndice fornece um guia de referência rápida para os códigos das variáveis categóricas mais utilizadas nas análises do SINASC.8

**Tabela B1: Códigos para `LOCNASC` (Local de Ocorrência)**

|Código|Descrição|
|---|---|
|1|Hospital|
|2|Outro Estabelecimento de Saúde|
|3|Domicílio|
|4|Outros|
|5|Aldeia Indígena|
|9|Ignorado|

**Tabela B2: Códigos para `ESTCIVMAE` (Estado Civil da Mãe)**

|Código|Descrição|
|---|---|
|1|Solteira|
|2|Casada|
|3|Viúva|
|4|Separada/Divorciada|
|5|União Estável|
|9|Ignorado|

**Tabela B3: Códigos para `TPNASCASSI` (Nascimento Assistido Por)**

|Código|Descrição|
|---|---|
|1|Médico(a)|
|2|Enfermagem ou Obstetriz|
|3|Parteira|
|4|Outros|
|9|Ignorado|

### Apêndice C: Critérios Detalhados para a Classificação de Robson (`TPROBSON`)

A Classificação de Robson é uma ferramenta essencial para o monitoramento de taxas de cesárea. A tabela a seguir detalha os critérios para cada um dos 10 grupos, com base nas diretrizes da OMS.48

**Tabela C1: Descrição dos 10 Grupos da Classificação de Robson**

|Grupo|Descrição|Paridade|Cesárea Prévia|Nº de Fetos|Apresentação|Idade Gestacional|Início do T. de Parto|
|---|---|---|---|---|---|---|---|
|1|Nulípara, feto único, cefálico, a termo, em trabalho de parto espontâneo|Nulípara|Não|Único|Cefálica|≥37 semanas|Espontâneo|
|2|Nulípara, feto único, cefálico, a termo, com parto induzido ou cesárea antes do T. de Parto|Nulípara|Não|Único|Cefálica|≥37 semanas|Induzido ou Cesárea Eletiva|
|3|Multípara (sem cesárea prévia), feto único, cefálico, a termo, em T. de Parto espontâneo|Multípara|Não|Único|Cefálica|≥37 semanas|Espontâneo|
|4|Multípara (sem cesárea prévia), feto único, cefálico, a termo, com parto induzido ou cesárea antes do T. de Parto|Multípara|Não|Único|Cefálica|≥37 semanas|Induzido ou Cesárea Eletiva|
|5|Multípara com pelo menos uma cesárea prévia, feto único, cefálico, a termo|Multípara|Sim|Único|Cefálica|≥37 semanas|Qualquer|
|6|Todas as nulíparas com feto único em apresentação pélvica|Nulípara|Não|Único|Pélvica|Qualquer|Qualquer|
|7|Todas as multíparas (incluindo com cesárea prévia) com feto único em apresentação pélvica|Multípara|Qualquer|Único|Pélvica|Qualquer|Qualquer|
|8|Todas as gestações múltiplas (incluindo com cesárea prévia)|Qualquer|Qualquer|Múltiplo|Qualquer|Qualquer|Qualquer|
|9|Todas as gestações com feto único em situação transversa ou oblíqua (incluindo com cesárea prévia)|Qualquer|Qualquer|Único|Transversa/Oblíqua|Qualquer|Qualquer|
|10|Todos os fetos únicos, cefálicos, pré-termo (<37 semanas) (incluindo com cesárea prévia)|Qualquer|Qualquer|Único|Cefálica|<37 semanas|Qualquer|

### Apêndice D: Metodologia de Cálculo do Índice de Kotelchuck (`KOTELCHUCK`)

O Índice de Adequação do Pré-Natal de Kotelchuck (APNCU) é uma medida composta que avalia a utilização dos serviços de pré-natal de forma mais completa do que a simples contagem de consultas. Seu cálculo envolve duas dimensões e quatro etapas, conforme descrito por Kotelchuck.52

Dimensão 1: Adequação do Início do Pré-Natal

Esta dimensão avalia o momento em que a gestante iniciou o acompanhamento pré-natal.

- **Categorias**:
    
    - **Precoce**: Início no 1º ou 2º mês de gestação.
        
    - **Intermediário**: Início no 3º ou 4º mês.
        
    - **Tardio**: Início do 5º ao 9º mês.
        
    - **Sem Pré-Natal**: Nenhuma consulta.
        

Dimensão 2: Adequação dos Serviços Recebidos

Esta dimensão compara o número de consultas realizadas com o número esperado de consultas, com base nas recomendações do American College of Obstetricians and Gynecologists (ACOG), ajustado para a idade gestacional do parto e para o mês de início do pré-natal.

- **Passo 1: Calcular o número esperado de consultas.** O número esperado é baseado na idade gestacional do parto, subtraindo-se as consultas que teriam ocorrido antes do início efetivo do pré-natal. Por exemplo, para um parto de 40 semanas, o esperado pela ACOG são 14 consultas. Se a mãe iniciou o pré-natal no 4º mês, 3 consultas foram "perdidas", então o número esperado ajustado é 14−3=11 consultas.
    
- **Passo 2: Obter o número observado de consultas.** Este valor é a variável `CONSPRENAT` do SINASC.
    
- Passo 3: Calcular a razão de adequação. A razão é calculada como:
    
    $$ 
- \text{Razão} = \frac{\text{Número de Consultas Observadas}}{\text{Número de Consultas Esperadas Ajustado}} \times 100% 
- $$
    
- **Passo 4: Classificar a razão.**
    
    - **Inadequado**: < 50% das consultas esperadas.
        
    - **Intermediário**: 50% a 79% das consultas esperadas.
        
    - **Adequado**: 80% a 109% das consultas esperadas.
        
    - **Mais que Adequado (Intensivo)**: ≥ 110% das consultas esperadas.
        

Índice Final (Combinação das Dimensões)

As duas dimensões são combinadas para gerar a classificação final da variável KOTELCHUCK.

**Tabela D1: Categorização Final do Índice de Kotelchuck**

|Categoria Final|Início do Pré-Natal|Razão de Adequação|
|---|---|---|
|**Inadequado**|Tardio (após o 4º mês)|OU|
|**Intermediário**|Precoce ou Intermediário (até o 4º mês)|E|
|**Adequado**|Precoce ou Intermediário (até o 4º mês)|E|
|**Mais que Adequado**|Precoce ou Intermediário (até o 4º mês)|E|
|**Sem Pré-Natal**|Nenhuma consulta|E|



# Dicionário de Variáveis do Cadastro Nacional de Estabelecimentos de Saúde (CNES) - Tabela de Estabelecimentos

## Introdução: Desvendando a Arquitetura de Dados do Cadastro Nacional de Estabelecimentos de Saúde (CNES)

O Cadastro Nacional de Estabelecimentos de Saúde (CNES) representa um dos pilares fundamentais para a gestão e o planejamento do Sistema Único de Saúde (SUS) no Brasil. Instituído como o sistema de informação oficial para o registro de todos os estabelecimentos de saúde em território nacional, sua abrangência inclui unidades públicas, privadas, filantrópicas, com ou sem vínculo com o SUS.1 A principal finalidade do CNES é servir como base cadastral unificada e confiável para a operacionalização de dezenas de outros sistemas de informação em saúde, como o Sistema de Informação Ambulatorial (SIA) e o Sistema de Informação Hospitalar (SIH), garantindo a interoperabilidade e a consistência dos dados em todo o ecossistema do SUS.1

O conjunto de dados de estabelecimentos, frequentemente disponibilizado em arquivos mensais (`tb_estabelecimento`), funciona como uma "fotografia" da base de dados em um ponto específico no tempo.5 Esta característica temporal, marcada pela variável

`COMPETEN`, é crucial para a correta interpretação e análise dos dados. Cada arquivo mensal reflete o estado cadastral dos estabelecimentos de saúde naquela competência, permitindo a construção de séries históricas detalhadas sobre a evolução da capacidade instalada da rede de saúde brasileira.

A compilação deste relatório baseia-se na síntese e harmonização de uma vasta gama de fontes documentais. Devido à natureza evolutiva do sistema, não existe um único manual canônico que abranja todas as variáveis e suas transformações ao longo do tempo. Portanto, este documento consolida informações de manuais técnicos históricos do Ministério da Saúde 6, da Wiki oficial do CNES mantida pelo DATASUS 7, de dicionários de dados enriquecidos por plataformas de pesquisa como a Plataforma de Ciência de Dados aplicada à Saúde (PCDaS/Fiocruz) 8, e de diversas notas técnicas e portarias.9 A dificuldade em localizar um dicionário de dados único, oficial e atualizado evidencia a necessidade deste guia consolidado para pesquisadores, analistas e gestores.10

A estrutura deste relatório foi organizada em seções temáticas que espelham a lógica das Fichas de Cadastro de Estabelecimentos de Saúde (FCES). Esta abordagem foi escolhida porque a arquitetura da base de dados do CNES deriva diretamente da estrutura dessas fichas, que são os instrumentos de coleta de dados primários.6 Ao seguir esta organização, o relatório não apenas define cada variável, mas também a contextualiza dentro do processo de cadastramento, facilitando uma compreensão mais profunda de seu significado e de suas inter-relações.

## Seção 1: Identificação Fundamental e Metadados do Registro

Esta seção aborda as variáveis que funcionam como chaves de identificação e metadados essenciais. Elas definem unicamente cada estabelecimento, sua natureza jurídica primária e sua localização no tempo, sendo indispensáveis para qualquer tipo de análise de dados.

### CNES

- **Descrição:** Código Nacional do Estabelecimento de Saúde. Este é um identificador numérico único, composto por 7 dígitos, atribuído a cada estabelecimento de saúde no Brasil. Funciona como a chave primária em todo o sistema CNES, garantindo a unicidade de cada registro.14 A obtenção e o gerenciamento deste código são processos formais realizados junto ao gestor de saúde local (Secretaria Municipal ou Estadual de Saúde).15
	 
- **Valores:** Sequência numérica de 7 dígitos. Exemplo: `2337934`.
	 

### CPF_CNPJ

- **Descrição:** Cadastro de Pessoa Física (CPF) ou Cadastro Nacional da Pessoa Jurídica (CNPJ) do estabelecimento. Este campo armazena o número de registro fiscal da entidade responsável pelo estabelecimento junto à Receita Federal do Brasil. A interpretação correta deste campo depende da variável `PF_PJ`.8
	 
- **Valores:** Sequência numérica de 11 dígitos (para CPF) ou 14 dígitos (para CNPJ).
	 

### PF_PJ

- **Descrição:** Indicador de Pessoa Física ou Jurídica. Trata-se de um campo categórico (flag) que especifica a natureza do registro fiscal do estabelecimento. É fundamental para distinguir, por exemplo, um consultório particular de um profissional autônomo (Pessoa Física) de um hospital ou clínica (Pessoa Jurídica).8
	 
- **Valores:**
	 
	 - `1`: Pessoa Física
		  
	 - `3`: Pessoa Jurídica
		  

### NIV_DEP

- **Descrição:** Nível de Dependência. Esta variável indica a relação de autonomia do estabelecimento. Um estabelecimento "Individual" é uma entidade independente, enquanto um "Mantido" é uma filial ou unidade que depende administrativamente de uma entidade mantenedora.6
	 
- **Valores:**
	 
	 - `1`: Individual
		  
	 - `3`: Mantida
		  

### CNPJ_MAN

- **Descrição:** CNPJ da Entidade Mantenedora. Este campo é preenchido apenas quando o `NIV_DEP` é igual a `3` (Mantida). Ele contém o CNPJ da organização principal que mantém financeiramente e administrativamente o estabelecimento. Por exemplo, um posto de saúde municipal (unidade mantida) terá neste campo o CNPJ da Prefeitura Municipal correspondente (entidade mantenedora).6
	 
- **Valores:** Sequência numérica de 14 dígitos. Nulo se `NIV_DEP` for `1`.
	 

### CODUFMUN

- **Descrição:** Código do Município. Identifica o município de localização do estabelecimento, utilizando o padrão de codificação de 6 dígitos do Instituto Brasileiro de Geografia e Estatística (IBGE). O código é formado pela concatenação do código da Unidade da Federação (2 dígitos) com o código do município dentro do estado (4 dígitos, sem o dígito verificador).8
	 
- **Valores:** Código numérico de 6 dígitos. Exemplo: `355030` para São Paulo-SP.
	 

### COD_CEP

- **Descrição:** Código de Endereçamento Postal. Corresponde ao CEP do endereço principal do estabelecimento de saúde.8
	 
- **Valores:** Sequência numérica de 8 dígitos.
	 

### DT_ATUAL

- **Descrição:** Data da Última Atualização. Registra a data em que as informações cadastrais do estabelecimento foram efetivamente alteradas pela última vez na base de dados nacional do CNES.
	 
- **Valores:** Data no formato `AAAAMMDD`.
	 

### COMPETEN

- **Descrição:** Competência do Arquivo. Indica o ano e o mês a que se refere o conjunto de dados, ou seja, a "fotografia" mensal da base. É uma das variáveis mais críticas para a realização de análises temporais e longitudinais.9
	 
- **Valores:** Data no formato `AAAAMM`. Exemplo: `202312` para dezembro de 2023.
	 

A combinação das variáveis `CNES`, `COMPETEN` e `DT_ATUAL` é fundamental para uma análise temporal precisa. O `CNES` identifica o estabelecimento, a `COMPETEN` define o momento da "fotografia" dos dados, e a `DT_ATUAL` indica quando a última mudança real ocorreu. Um estabelecimento pode aparecer com os mesmos dados em várias competências consecutivas se não houver alterações; nesses casos, a `DT_ATUAL` permanecerá constante.

Conforme detalhado na Nota Técnica Nº 07/2023-CGSI/DRAC/SAES/MS, o banco de dados nacional do CNES opera sob um "conceito restrito de competência".18 Os gestores municipais e estaduais enviam atualizações ao longo do mês para uma base de dados dinâmica. Ao final do período (mês), o Ministério da Saúde consolida e "fecha" uma versão estável dos dados para aquela competência. Isso significa que a análise dos dados do CNES não é uma análise em tempo real, mas sim uma análise de uma série de

_snapshots_ mensais. Para um pesquisador, a implicação é direta: ao cruzar dados do CNES com dados de eventos (como internações do SIH ou atendimentos do SIA), é imperativo utilizar a `COMPETEN` do CNES que corresponde ou precede imediatamente a data do evento. Ignorar essa sincronia pode levar a conclusões anacrônicas, como atribuir um procedimento a um serviço que só foi oficialmente cadastrado no mês seguinte, resultando em erros de análise sobre a capacidade e oferta de serviços no momento do atendimento.

## Seção 2: Caracterização Institucional, Natureza e Vínculo com o SUS

Esta seção detalha a "identidade" do estabelecimento, descrevendo sua função na rede de saúde, sua natureza jurídica e administrativa, e sua relação com o Sistema Único de Saúde. Essas variáveis são essenciais para classificar e agrupar os estabelecimentos em análises de políticas públicas.

### TP_UNID

- **Descrição:** Tipo de Unidade. Esta é uma das classificações mais importantes, pois define a finalidade principal do estabelecimento dentro da rede de saúde. A tabela de tipos de unidade é extensa e reflete a diversidade de serviços existentes, desde a atenção primária até a alta complexidade hospitalar.6
	 
- **Valores:** Campo numérico codificado. Uma tabela de domínio é necessária para sua interpretação.
	 

**Tabela 1: Tabela de Domínio para `TP_UNID` (Exemplos)**

|Código|Descrição|Fonte|
|---|---|---|
|01|POSTO DE SAÚDE|16|
|02|CENTRO DE SAÚDE / UNIDADE BÁSICA|16|
|04|POLICLÍNICA|16|
|05|HOSPITAL GERAL|16|
|07|HOSPITAL ESPECIALIZADO|16|
|15|UNIDADE MISTA|16|
|22|CONSULTÓRIO ISOLADO|6|
|36|CLÍNICA/CENTRO DE ESPECIALIDADE|16|
|62|CENTRAL DE REGULAÇÃO DE SERVIÇOS DE SAÚDE|19|
|74|POLO ACADEMIA DA SAÚDE|20|

### ESFERA_A

- **Descrição:** Esfera Administrativa. Indica a esfera de governo (Federal, Estadual, Municipal) à qual o estabelecimento público está subordinado, ou se é uma entidade Privada. **Nota Histórica Importante:** Este campo foi a principal variável para essa classificação até outubro de 2015. A partir de novembro de 2015, a variável `NAT_JUR`, mais granular e confiável, tornou-se a fonte primária para essa informação, sendo alimentada diretamente pela base da Receita Federal.21
	 
- **Valores:**
	 
	 - `01`: FEDERAL
		  
	 - `02`: ESTADUAL
		  
	 - `03`: MUNICIPAL
		  
	 - `04`: PRIVADA
		  
	 - `99`: NÃO INFORMADA
		  

### NATUREZA

- **Descrição:** Natureza da Organização. Campo legado que fornecia detalhes sobre a natureza da organização (ex: Administração Direta, Empresa Pública, Fundação Pública). Assim como `ESFERA_A`, sua utilização foi em grande parte substituída pela maior precisão e padronização da variável `NAT_JUR` a partir de 2015.12
	 
- **Valores:** Campo numérico codificado. Exemplo: `01` para "Administração Direta da Saúde (MS, SES, e SMS)".12
	 

### NAT_JUR

- **Descrição:** Natureza Jurídica. Este é o campo mais preciso e atual para identificar a constituição jurídico-institucional de um estabelecimento. Seus códigos e descrições são baseados na tabela oficial da Comissão Nacional de Classificação (CONCLA) e são atualizados por meio de um serviço de integração com a base de dados de CNPJ da Receita Federal do Brasil.25
	 
- **Valores:** Campo numérico codificado com centenas de valores possíveis, que podem ser agrupados em grandes categorias como Administração Pública, Entidades Empresariais, Entidades sem Fins Lucrativos, Pessoas Físicas e Organizações Internacionais.26
	 

A transição para o uso da `NAT_JUR` como fonte primária em novembro de 2015 representou um marco na qualificação dos dados do SUS. Antes dessa data, campos como `ESFERA_A` e `NATUREZA` eram preenchidos manualmente pelos gestores locais, um processo sujeito a erros e inconsistências.21 A automação via Receita Federal tornou a classificação mais objetiva e padronizada. Para um analista de dados, isso acarreta duas implicações profundas. Primeiro, os dados de

`NAT_JUR` a partir de 11/2015 são significativamente mais confiáveis. Segundo, qualquer análise de série histórica que cruze essa data deve ser feita com extrema cautela. Uma simples contagem de "hospitais filantrópicos" ao longo do tempo pode apresentar um salto ou queda abrupta em 2015, que não reflete uma mudança real na rede, mas sim o efeito da reclassificação sistêmica. Para mitigar esse viés, um pesquisador precisa desenvolver uma tabela de mapeamento ("de-para") para harmonizar os códigos das classificações antigas (`NATUREZA`, `ESFERA_A`) com a nova taxonomia da `NAT_JUR`, uma tarefa complexa que exige profundo conhecimento de ambas as estruturas.

### VINC_SUS

- **Descrição:** Vínculo com o SUS. Indica, por meio de um flag binário, se o estabelecimento possui algum tipo de vínculo formal com o Sistema Único de Saúde. Esse vínculo pode ser por se tratar de uma unidade pública ou por ter um contrato ou convênio para a prestação de serviços.8 É importante notar que a ausência de vínculo (
	 
	 `0`) não impede o cadastramento no CNES, que tem caráter universal.6
	 
- **Valores:**
	 
	 - `1`: Sim
		  
	 - `0`: Não
		  

### TP_PREST

- **Descrição:** Tipo de Prestador. Classifica o estabelecimento com base em sua natureza jurídica e relação com o SUS, sendo uma variável derivada que combina essas informações para facilitar a identificação do perfil do prestador de serviços.6
	 
- **Valores:**
	 
	 - `30`: PÚBLICO FEDERAL
		  
	 - `40`: PÚBLICO ESTADUAL
		  
	 - `50`: PÚBLICO MUNICIPAL
		  
	 - `61`: FILANTRÓPICO COM CNAS VÁLIDO
		  
	 - `20`: PRIVADO COM FINS LUCRATIVOS
		  
	 - `22`: PRIVADO OPTANTE PELO SIMPLES
		  
	 - `60`: PRIVADO SEM FINS LUCRATIVOS
		  
	 - `80`: SINDICATO
		  
	 - `99`: TIPO DE PRESTADOR NÃO INFORMADO
		  

### TPGESTAO

- **Descrição:** Tipo de Gestão. Indica o modelo de gestão do SUS no qual o município ou estado está habilitado, refletindo as responsabilidades pactuadas nas Comissões Intergestores. Essa classificação define quem é o principal responsável pela gestão e financiamento dos serviços de saúde no território.9
	 
- **Valores:**
	 
	 - `M`: MUNICIPAL
		  
	 - `E`: ESTADUAL
		  
	 - `D`: DUPLA
		  
	 - `S`: SEM GESTÃO
		  
	 - `Z`: NÃO INFORMADO
		  

## Seção 3: Organização Territorial e Operacional

Esta seção detalha o posicionamento do estabelecimento dentro da estrutura organizacional e geográfica da rede de saúde, além de descrever seu regime de funcionamento. Essas variáveis são cruciais para análises de planejamento regional e acesso a serviços.

### REGSAUDE

- **Descrição:** Região de Saúde. Código que identifica a Região de Saúde à qual o município do estabelecimento pertence. As Regiões de Saúde são o eixo estruturante do planejamento regional integrado do SUS, definidas para garantir a integralidade da atenção à saúde em um determinado espaço geográfico.8
	 
- **Valores:** Código alfanumérico, definido pelo Plano Diretor de Regionalização de cada estado.
	 

### MICR_REG

- **Descrição:** Microrregião de Saúde. Código que identifica a Microrregião de Saúde, que é uma subdivisão da Região de Saúde, utilizada para um planejamento mais detalhado.8
	 
- **Valores:** Código alfanumérico.
	 

### DISTRSAN

- **Descrição:** Distrito Sanitário. Código do Distrito Sanitário, que representa uma subdivisão territorial para a gestão da saúde dentro de um município. É uma estrutura comum em grandes centros urbanos para aproximar a gestão da realidade local.6
	 
- **Valores:** Código alfanumérico.
	 

### DISTRADM

- **Descrição:** Distrito Administrativo / Módulo Assistencial. Originalmente chamado de Distrito Administrativo, este campo atualmente designa o código do Módulo Assistencial, conforme o plano de regionalização local. É mais um nível de detalhamento da organização territorial da saúde.6
	 
- **Valores:** Código alfanumérico.
	 

### ATIVIDAD

- **Descrição:** Atividade de Ensino e Pesquisa. Indica se o estabelecimento de saúde possui uma política formal e atividades estruturadas de ensino (formação de profissionais de saúde) e/ou pesquisa científica.6
	 
- **Valores:**
	 
	 - `1`: Unidade de Ensino Superior
		  
	 - `2`: Unidade Auxiliar de Ensino
		  
	 - `3`: Unidade sem Atividade de Ensino
		  
	 - Outros códigos podem existir em dados históricos.
		  

### CLIENTEL

- **Descrição:** Fluxo de Clientela. Descreve a forma como os usuários acessam os serviços do estabelecimento, sendo um indicador chave do papel da unidade na rede de atenção.6
	 
- **Valores:**
	 
	 - `01`: Atendimento de demanda espontânea (unidade de "porta aberta")
		  
	 - `02`: Atendimento de demanda referenciada (recebe apenas pacientes encaminhados de outras unidades)
		  
	 - `03`: Atendimento de demanda espontânea e referenciada (modelo misto)
		  
	 - `00`: Fluxo de Clientela não exigido
		  
	 - `99`: Fluxo de Clientela não informado
		  

### TURNO_AT

- **Descrição:** Turno de Atendimento. Indica os períodos de funcionamento do estabelecimento, permitindo aferir a disponibilidade de serviços ao longo do dia.6
	 
- **Valores:**
	 
	 - `01`: ATENDIMENTO SOMENTE PELA MANHÃ
		  
	 - `02`: ATENDIMENTO SOMENTE À TARDE
		  
	 - `03`: ATENDIMENTO NOS TURNOS DA MANHÃ E À TARDE
		  
	 - `04`: ATENDIMENTO NOS TURNOS DA MANHÃ, TARDE E NOITE
		  
	 - `05`: ATENDIMENTO COM TURNOS INTERMITENTES
		  
	 - `06`: ATENDIMENTO CONTÍNUO DE 24 HORAS/DIA (PLANTÃO)
		  
	 - `07`: ATENDIMENTO SOMENTE À NOITE
		  

### NIV_HIER

- **Descrição:** Nível de Hierarquia. Classificação legada que posicionava o estabelecimento dentro de uma pirâmide hierárquica de complexidade do SUS. Embora o conceito de redes de atenção (RAS) seja hoje mais prevalente, esta variável ainda pode ser encontrada nos dados.6
	 
- **Valores:**
	 
	 - `01`: NH 1-PAB-PABA (Nível Hierárquico 1 - Atenção Básica)
		  
	 - `02` a `08`: Códigos para Média e Alta Complexidade Ambulatorial e Hospitalar.
		  

Os campos de organização territorial (`REGSAUDE`, `MICR_REG`, `DISTRSAN`, `DISTRADM`) são mais do que simples rótulos geográficos; eles representam os "nós" e os "elos" que compõem a Rede de Atenção à Saúde (RAS). A análise combinada desses campos com a variável `CLIENTEL` (fluxo de clientela) permite mapear e analisar os fluxos reais de pacientes dentro do sistema. Um analista pode utilizar esses dados para investigar questões complexas sobre a eficiência e a equidade da rede, como, por exemplo, se pacientes de uma microrregião com carência de serviços especializados estão sendo forçados a buscar atendimento em outras regiões de saúde, indicando um "vazio assistencial". Esse tipo de análise é fundamental para o planejamento regional, a alocação de recursos e a avaliação da integralidade do cuidado, superando em muito um simples mapeamento de estabelecimentos.

## Seção 4: Formalização: Contratos, Licenciamento e Finanças

Esta seção abrange os aspectos legais, contratuais e financeiros que formalizam a operação do estabelecimento, sendo particularmente relevante para unidades privadas e filantrópicas que prestam serviços ao SUS e, portanto, necessitam de regularização para faturamento e recebimento de repasses.

### CONTRATM / CONTRATE

- **Descrição:** Número do Contrato com o Gestor Municipal (`CONTRATM`) ou Estadual (`CONTRATE`). Armazena o número de identificação do contrato ou convênio firmado entre o estabelecimento e o gestor de saúde local para a prestação de serviços ao SUS.6
	 
- **Valores:** Campo alfanumérico.
	 

### DT_PUBLM / DT_PUBLE

- **Descrição:** Data de Publicação do Contrato Municipal (`DT_PUBLM`) ou Estadual (`DT_PUBLE`). Registra a data em que o respectivo contrato foi publicado em diário oficial, um requisito legal para sua validade e início de vigência.6
	 
- **Valores:** Data no formato `AAAAMMDD`.
	 

### ALVARA / DT_EXPED / ORGEXPED

- **Descrição:** Dados do Alvará Sanitário. Conjunto de campos que armazena o número do alvará de funcionamento sanitário (`ALVARA`), sua data de expedição (`DT_EXPED`) e o órgão emissor (`ORGEXPED`). A posse de um alvará válido é condição essencial para a operação legal de qualquer estabelecimento de saúde.6
	 
- **Valores:** Alfanuméricos e data.
	 

### RETENCAO

- **Descrição:** Código de Retenção de Tributos. Código que define o regime de retenção de tributos federais aplicável ao estabelecimento. Esta informação é crucial para fins fiscais e para o correto processamento do faturamento de serviços prestados ao SUS.8
	 
- **Valores:**
	 
	 - `10`: ESTABELECIMENTO PÚBLICO
		  
	 - `11`: ESTABELECIMENTO FILANTRÓPICO
		  
	 - `12`: ESTABELECIMENTO SEM FINS LUCRATIVOS
		  
	 - `13`: ESTABELECIMENTO PRIVADO LUCRATIVO SIMPLES
		  
	 - `14`: ESTABELECIMENTO PRIVADO LUCRATIVO
		  
	 - `15`: ESTABELECIMENTO SINDICAL
		  
	 - `16`: ESTABELECIMENTO PESSOA FÍSICA
		  
	 - `00`, `99`: RETENÇÃO NÃO INFORMADA
		  

### COD_IR

- **Descrição:** Código de Retenção de Tributos da Mantenedora. Análogo ao campo `RETENCAO`, mas aplicado à entidade mantenedora, quando o estabelecimento é do tipo "Mantido" (`NIV_DEP=3`).8
	 
- **Valores:** Códigos similares aos do campo `RETENCAO`.
	 

### CO_BANCO / CO_AGENC / C_CORREN

- **Descrição:** Dados Bancários. Conjunto de campos que registra o código do banco, da agência e o número da conta corrente do estabelecimento. Essas informações são utilizadas para o depósito dos repasses financeiros referentes aos serviços prestados ao SUS.6
	 
- **Valores:** Códigos numéricos e alfanuméricos.
	 

A presença de dados nos campos de contrato (`CONTRATM`, `DT_PUBLM`), licenciamento (`ALVARA`) e dados bancários (`CO_BANCO`) está diretamente associada à capacidade de um estabelecimento privado ou filantrópico faturar seus serviços junto ao SUS. Um estabelecimento com `VINC_SUS=1` mas sem um contrato válido (por exemplo, `CONTRATM` nulo ou `DT_PUBLM` com data expirada) representa uma inconsistência cadastral que pode levar à glosa (recusa de pagamento) de sua produção nos sistemas de faturamento (SIA/SIH).4 Para um auditor ou gestor, esses campos formam uma trilha de auditoria essencial, permitindo o cruzamento da base do CNES com os dados de pagamento do Fundo Nacional de Saúde para verificar se os repasses financeiros estão sendo direcionados a estabelecimentos com documentação regularizada.

## Seção 5: Avaliações, Qualificações e Programas de Incentivo

Esta seção contém um conjunto de variáveis que indicam a participação e o status do estabelecimento em diversos programas de qualidade, processos de acreditação e políticas de incentivo financeiro promovidas pelo Ministério da Saúde.

### AV_ACRED / CLASAVAL / DT_ACRED

- **Descrição:** Dados de Acreditação Hospitalar. Este conjunto de campos indica se o hospital participa de um programa de acreditação (`AV_ACRED`), qual a sua classificação ou nível de acreditação obtido (`CLASAVAL`) e a data em que a acreditação foi concedida (`DT_ACRED`).6
	 
- **Valores `CLASAVAL`:**
	 
	 - `1`: ACREDITADO NO NÍVEL 1
		  
	 - `2`: ACREDITADO NO NÍVEL 2
		  
	 - `3`: ACREDITADO NO NÍVEL 3
		  
	 - `0`: NÃO ATENDEU AOS PADRÕES MÍNIMOS
		  

### AV_PNASS / DT_PNASS

- **Descrição:** Avaliação PNASS. Indicam a participação (`AV_PNASS`) e a data (`DT_PNASS`) da avaliação do estabelecimento no âmbito do Programa Nacional de Avaliação dos Serviços de Saúde (PNASS), uma iniciativa para avaliar a qualidade dos serviços de saúde no país.6
	 
- **Valores:** Flags (Sim/Não) e data.
	 

### Bloco `GESPRG*` (Gestão de Programas)

- **Descrição:** Este bloco de campos (`GESPRG1E`, `GESPRG1M`, `GESPRG2E`, `GESPRG2M`, etc.) é destinado a registrar a adesão dos estabelecimentos a programas e políticas de saúde específicas, que são frequentemente transitórias. A letra final 'E' provavelmente se refere a programas de gestão Estadual, enquanto 'M' se refere a programas de gestão Municipal. A documentação detalhada para o significado de cada um desses campos é notavelmente escassa nos manuais gerais 7, pois seu conteúdo é definido por portarias e notas técnicas específicas de cada programa lançado pelo Ministério da Saúde.
	 
- **Valores:** Geralmente são flags (`1` para Sim, `0` para Não) ou códigos específicos definidos na legislação do programa.
	 

### NIVATE_A / NIVATE_H

- **Descrição:** Nível de Atenção Ambulatorial (`NIVATE_A`) e Hospitalar (`NIVATE_H`). Estes campos provavelmente detalham o nível de complexidade (Atenção Básica, Média Complexidade, Alta Complexidade) em que o estabelecimento atua, possivelmente vinculados aos programas registrados no bloco `GESPRG*`. Assim como os campos de programas, sua interpretação pode depender de documentação específica da época.22
	 
- **Valores:** Códigos numéricos ou de texto.
	 

A estrutura de campos genéricos como `GESPRG*` (e, como será visto na Seção 10, os campos `AP*`) reflete uma estratégia de design de banco de dados para acomodar a natureza dinâmica e mutável das políticas públicas de saúde. Em vez de adicionar novas colunas ao schema do banco de dados nacional a cada novo programa lançado — um processo tecnicamente complexo e custoso —, o sistema reutiliza esses campos pré-existentes. O Ministério da Saúde, ao lançar um novo programa, publica uma portaria ou nota técnica que especifica: "A adesão ao Programa X será registrada no campo `GESPRG2M` com o valor '1'". Anos depois, o programa pode ser descontinuado e o campo `GESPRG2M` pode ser "zerado" ou até mesmo reaproveitado para uma nova política. A implicação crítica para o pesquisador é que o significado desses campos **não é fixo no tempo**. Para analisar a adesão a um programa específico, é indispensável localizar a documentação oficial da época que define qual campo foi utilizado e quais eram seus códigos. Analisar a variável `GESPRG2M` ao longo de uma década sem esse contexto levará a conclusões metodologicamente falhas e sem sentido.

## Seção 6: Capacidade Instalada – Leitos (`QTLEIT*`)

Esta seção apresenta um inventário detalhado da quantidade e dos tipos de leitos existentes no estabelecimento. Essas variáveis são vitais para medir a capacidade de internação da rede hospitalar do país, sendo um dos conjuntos de dados mais consultados para o planejamento em saúde. A estrutura dos campos deriva diretamente da Ficha de Cadastro de Leitos (FCES).6

### Campos Agregadores

- **`QTLEITP1`**: Quantidade de Leitos de Internação. Soma dos leitos cirúrgicos, clínicos, obstétricos, pediátricos e de outras especialidades.
	 
- **`QTLEITP2`**: Quantidade de Leitos Complementares. Soma dos leitos de Unidade de Terapia Intensiva (UTI) e Unidade Intermediária (UI).
	 
- **`QTLEITP3`**: Quantidade de Leitos de Hospital Dia.
	 
- **`LEITHOSP`**: Total de Leitos Hospitalares. Soma de `QTLEITP1` e `QTLEITP2`.
	 

### Campos Detalhados (`QTLEIT05` a `QTLEIT40`)

Cada uma dessas variáveis representa a quantidade de leitos de uma especialidade ou tipo específico. Apresentar uma lista exaustiva seria repetitivo; em vez disso, a tabela abaixo decodifica as principais variáveis deste bloco, agrupando-as por tipo de leito para facilitar a compreensão.

**Tabela 2: Decodificação das Variáveis de Quantidade de Leitos (`QTLEIT*`)**

|Variável|Descrição do Leito|Tipo de Leito (Agrupamento)|Fonte|
|---|---|---|---|
|**`QTLEIT05`**|Cirurgia Geral|Cirúrgico|6|
|**`QTLEIT06`**|Ginecologia|Cirúrgico|6|
|**`QTLEIT07`**|Oftalmologia|Cirúrgico|6|
|**`QTLEIT08`**|Ortopedia/Traumatologia|Cirúrgico|6|
|**`QTLEIT09`**|Clínica Geral|Clínico|6|
|**`QTLEIT19`**|Obstetrícia Clínica|Obstétrico|6|
|**`QTLEIT20`**|Obstetrícia Cirúrgica|Obstétrico|6|
|**`QTLEIT21`**|Pediatria Clínica|Pediátrico|6|
|**`QTLEIT22`**|Pediatria Cirúrgica|Pediátrico|6|
|**`QTLEIT23`**|Saúde Mental|Clínico|6|
|**`QTLEIT32`**|UTI Adulto|Complementar|6|
|**`QTLEIT34`**|Unidade Intermediária Adulto|Complementar|6|
|**`QTLEIT38`**|UTI Pediátrica|Complementar|6|
|**`QTLEIT39`**|UTI Neonatal|Complementar|6|
|**`QTLEIT40`**|Unidade Intermediária Neonatal|Complementar|6|

## Seção 7: Capacidade Instalada – Instalações Físicas (`QTINST*`)

Esta seção quantifica a infraestrutura física de assistência do estabelecimento, como consultórios, salas de cirurgia e outros ambientes. Esses dados complementam a informação sobre leitos, oferecendo uma visão mais ampla da capacidade instalada. A estrutura desses campos também deriva da FCES.6

### Campos Detalhados (`QTINST01` a `QTINST37`)

Cada variável `QTINST*` representa a quantidade de um tipo específico de instalação física. A tabela a seguir decodifica as principais variáveis deste bloco, agrupando-as por área de assistência para fornecer um contexto funcional.

**Tabela 3: Decodificação das Variáveis de Quantidade de Instalações (`QTINST*`)**

|Variável|Descrição da Instalação|Agrupamento Funcional|Fonte|
|---|---|---|---|
|**`QTINST01`**|Consultórios - Clínicas Básicas|Ambulatório|6|
|**`QTINST02`**|Consultórios - Clínicas Especializadas|Ambulatório|6|
|**`QTINST03`**|Consultórios - Não Médicos|Ambulatório|6|
|**`QTINST04`**|Consultórios Odontológicos|Ambulatório|6|
|**`QTINST05`**|Sala de Repouso/Observação|Urgência / Ambulatório|6|
|**`QTINST06`**|Sala de Pequena Cirurgia|Urgência / Ambulatório|6|
|**`QTINST07`**|Sala de Curativos|Urgência / Ambulatório|6|
|**`QTINST08`**|Sala de Gesso|Urgência / Ambulatório|6|
|**`QTINST09`**|Sala de Nebulização/Inalação|Ambulatório|6|
|**`QTINST10`**|Sala de Enfermagem (Serviços)|Ambulatório|6|
|**`QTINST11`**|Sala de Cirurgia|Centro Cirúrgico|6|
|**`QTINST12`**|Sala de Recuperação Pós-Anestésica|Centro Cirúrgico|6|
|**`QTINST13`**|Sala de Parto Normal|Centro Obstétrico|6|
|**`QTINST14`**|Sala de Pré-Parto|Centro Obstétrico|6|
|**`QTINST15`**|Unidade Neonatal - Berçário|Unidade Neonatal|6|
|**`QTINST25`**|Sala de Imunização (Vacinação)|Ambulatório|6|
|**`QTINST31`**|Posto de Coleta de Leite Humano|Banco de Leite|6|
|**`QTINST34`**|Farmácia|Serviço de Apoio|6|

## Seção 8: Portfólio de Serviços e Atendimentos

Esta seção descreve os grandes grupos de atendimento que o estabelecimento oferece e detalha os Serviços de Apoio Diagnóstico e Terapêutico (SADT) disponíveis, sejam eles realizados internamente ou por terceiros.

### Indicadores de Modalidade de Atendimento

Estes campos são flags binários (Sim/Não) que indicam a presença de grandes áreas assistenciais no estabelecimento.

- **`URGEMERG`**: Possui Serviço de Urgência e Emergência.
	 
- **`ATENDAMB`**: Realiza Atendimento Ambulatorial.
	 
- **`CENTRCIR`**: Possui Centro Cirúrgico.
	 
- **`CENTROBS`**: Possui Centro Obstétrico.
	 
- **`CENTRNEO`**: Possui Centro Neonatal.
	 
- **`ATENDHOS`**: Realiza Atendimento Hospitalar (Internação).
	 
- **`SERAPOIO`**: Flag geral que indica a existência de algum Serviço de Apoio.
	 

### Bloco `SERAP*` (Serviços de Apoio)

Este bloco de variáveis (`SERAP01P` a `SERAP11T`) indica a oferta de SADT. O design desses campos é particularmente informativo: o sufixo `P` indica que o serviço é **Próprio**, enquanto o sufixo `T` indica que é **Terceirizado**.36

**Tabela 4: Decodificação das Variáveis de Serviços de Apoio (`SERAP*`)**

|Prefixo|Descrição do Serviço de Apoio|Fonte|
|---|---|---|
|**`SERAP01`**|Patologia Clínica / Análises Clínicas|6|
|**`SERAP02`**|Radiodiagnóstico (Ex: Raio-X, Ultrassom)|6|
|**`SERAP03`**|Hemoterapia|6|
|**`SERAP04`**|Medicina Nuclear|6|
|**`SERAP05`**|Anatomia Patológica e Citopatologia|6|
|**`SERAP06`**|Métodos Gráficos (Ex: ECG, EEG)|6|
|**`SERAP07`**|Métodos Ópticos (Ex: Endoscopia)|6|
|**`SERAP08`**|Radioterapia|6|
|**`SERAP09`**|Quimioterapia|6|
|**`SERAP10`**|Litotripsia|6|
|**`SERAP11`**|Fisioterapia / Reabilitação|6|

A distinção entre serviços próprios (`P`) e terceirizados (`T`) permite análises sofisticadas da estrutura do mercado de saúde. Um pesquisador pode identificar "hubs" de serviços (hospitais com muitos serviços `P`) e "spokes" (clínicas menores que dependem da terceirização). Essa análise pode revelar padrões regionais, como a predominância de terceirização em radiologia em certos estados, e pode ser correlacionada com a concentração de clínicas de diagnóstico independentes. Adicionalmente, permite avaliar a complexidade da gestão: um estabelecimento com muitos serviços `T` possui uma carga administrativa maior relacionada à gestão de contratos e fornecedores, o que constitui uma camada de análise de modelo de negócio e de rede que vai muito além de um simples inventário de serviços.

## Seção 9: Estrutura Interna: Comissões e Gestão de Resíduos

Esta seção aborda requisitos organizacionais internos, como a existência de comissões técnicas obrigatórias, e práticas de biossegurança, como a gestão de Resíduos de Serviços de Saúde (RSS).

### Bloco `COMISS*`

Este bloco de variáveis (`COMISS01` a `COMISS12`) utiliza flags para indicar a existência de comissões técnicas que são, em sua maioria, exigidas por legislação ou normas regulatórias para garantir a qualidade e a segurança da assistência.7 O campo

`COMISSAO` é um flag geral que indica se há pelo menos uma comissão ativa.

**Tabela 5: Decodificação das Variáveis de Comissões (`COMISS*`)**

|Variável|Descrição da Comissão|Fonte|
|---|---|---|
|**`COMISS01`**|Comissão de Ética Médica|6|
|**`COMISS02`**|Comissão de Ética de Enfermagem|6|
|**`COMISS03`**|Comissão de Farmácia e Terapêutica|6|
|**`COMISS04`**|Comissão de Controle de Infecção Hospitalar (CCIH)|6|
|**`COMISS05`**|Comissão de Apropriação de Custos|6|
|**`COMISS06`**|Comissão Interna de Prevenção de Acidentes (CIPA)|6|
|**`COMISS07`**|Comissão de Revisão de Prontuários|6|
|**`COMISS08`**|Comissão de Revisão de Documentação Médica e Estatística|6|
|**`COMISS09`**|Comissão de Análise de Óbito e Biópsias|6|
|**`COMISS10`**|Investigação Epidemiológica|6|
|**`COMISS11`**|Notificação de Doenças|6|
|**`COMISS12`**|Controle de Zoonoses e Vetores|6|

### Gestão de Resíduos de Serviços de Saúde (RSS)

- **`RES_BIOL`**: Indica a geração de Resíduo Biológico.
	 
- **`RES_QUIM`**: Indica a geração de Resíduo Químico.
	 
- **`RES_RADI`**: Indica a geração de Resíduo Radioativo.
	 
- **`RES_COMU`**: Indica a geração de Resíduo Comum.
	 
- **`COLETRES`**: Indica se há empresa especializada contratada para a coleta dos RSS.
	 

## Seção 10: Campos Específicos da Atenção Primária à Saúde (APS)

Esta seção contém um grande bloco de variáveis (`AP*CV*`) que, pela sua nomenclatura, parecem destinadas a detalhar aspectos específicos da Atenção Primária à Saúde (APS), também conhecida como Atenção Básica.

- **`ATEND_PR`**: Indica se o estabelecimento realiza Atendimento na Atenção Primária.
	 

### Bloco `AP01CV01` a `AP07CV07`

- **Descrição:** Este é o bloco de variáveis mais opaco da lista fornecida, com documentação pública detalhada sendo extremamente rara nos manuais gerais.7 A nomenclatura sugere uma estrutura matricial de dados.
	 
	 `AP` muito provavelmente significa "Atenção Primária". `CV` poderia ser uma abreviação para "Cobertura e Vínculo", "Característica da Visita" ou outro termo técnico da APS. A primeira série de números (`01` a `07`) pode representar diferentes tipos de equipes (ex: `01` para Equipe de Saúde da Família - eSF, `02` para Equipe de Saúde Bucal - eSB) ou programas específicos da APS. A segunda série de números (`01` a `07`) pode representar indicadores ou características monitoradas para cada tipo de equipe (ex: `01` para População Coberta, `02` para Número de Agentes Comunitários de Saúde, `03` para Carga Horária, etc.).
	 
- **Análise e Interpretação:** A análise precisa desses campos é inviável sem a documentação de referência correta. Para utilizá-los, é mandatório que o pesquisador localize as Notas Técnicas, Portarias ou Manuais específicos da Política Nacional de Atenção Básica (PNAB) que estavam em vigor na competência (`COMPETEN`) dos dados que estão sendo analisados. Esses documentos definirão o layout e o significado de cada campo `AP*CV*` para aquele período específico.
	 

## Seção 11: Campos Finais e Legado

- **`NAT_JUR`**: Este campo aparece novamente no final da lista de colunas fornecida. Trata-se muito provavelmente de uma duplicata ou um artefato da extração da lista de nomes de colunas do banco de dados. Sua definição e valores são idênticos aos do campo `NAT_JUR` descrito na Seção 2. Em qualquer análise, deve-se tratar este campo como redundante e utilizar a primeira ocorrência.
	 

## Anexo: Tabelas de Domínio Consolidadas

Este anexo fornece tabelas de referência rápida para a decodificação de variáveis categóricas chave que são frequentemente utilizadas em análises.

**Tabela A.1: Códigos de Vínculo com o SUS (`VINC_SUS`)**

|Código|Descrição|
|---|---|
|1|Sim, possui vínculo com o SUS|
|0|Não, não possui vínculo com o SUS|

**Tabela A.2: Códigos de Tipo de Gestão (`TPGESTAO`)**

|Código|Descrição|
|---|---|
|M|Gestão Municipal|
|E|Gestão Estadual|
|D|Gestão Dupla|
|S|Sem Gestão|
|Z|Não Informado|

**Tabela A.3: Códigos de Fluxo de Clientela (`CLIENTEL`)**

|Código|Descrição|
|---|---|
|01|Atendimento de demanda espontânea|
|02|Atendimento de demanda referenciada|
|03|Atendimento de demanda espontânea e referenciada|
|00|Fluxo de Clientela não exigido|
|99|Fluxo de Clientela não informado|

**Tabela A.4: Códigos de Turno de Atendimento (`TURNO_AT`)**

|Código|Descrição|
|---|---|
|01|Atendimento somente pela manhã|
|02|Atendimento somente à tarde|
|03|Atendimento nos turnos da manhã e à tarde|
|04|Atendimento nos turnos da manhã, tarde e noite|
|06|Atendimento contínuo de 24 horas/dia (Plantão)|
|07|Atendimento somente à noite|

**Tabela A.5: Códigos de Tipo de Prestador (`TP_PREST`)**

|Código|Descrição|
|---|---|
|30|Público Federal|
|40|Público Estadual|
|50|Público Municipal|
|61|Filantrópico com CNAS Válido|
|20|Privado com Fins Lucrativos|
|22|Privado Optante pelo Simples|
|60|Privado sem Fins Lucrativos|
|80|Sindicato|
|99|Não Informado|

**Tabela A.6: Códigos de Retenção de Tributos (`RETENCAO`)**

|Código|Descrição|
|---|---|
|10|Estabelecimento Público|
|11|Estabelecimento Filantrópico|
|12|Estabelecimento sem Fins Lucrativos|
|14|Estabelecimento Privado Lucrativo|
|00, 99|Retenção não informada|
# Guia de um Especialista para o Arquivo de Produção Ambulatorial (PA) do SIA-SUS: Um Dicionário de Dados Abrangente e Estrutura Analítica

## Seção I: Contexto Fundamental: A Arquitetura do Arquivo `PA` do SIA

Esta seção estabelece o conhecimento de base essencial, explicando que o arquivo `PA` não é uma tabela plana simples, mas uma agregação complexa de múltiplos fluxos de dados. A compreensão desta arquitetura é um pré-requisito para qualquer análise válida.

### 1.1. O Papel do Sistema de Informações Ambulatoriais (SIA) no SUS

O Sistema de Informações Ambulatoriais (SIA) representa uma pedra angular do Sistema Único de Saúde (SUS) do Brasil para a gestão da atenção ambulatorial. Implantado em escala nacional na década de 1990, o sistema foi concebido com o objetivo primordial de registrar, processar e financiar os procedimentos realizados fora do ambiente hospitalar.1 Suas funções transcendem o mero registro financeiro, servindo como uma ferramenta estratégica para o Ministério da Saúde e para os gestores estaduais e municipais. As informações geradas pelo SIA são cruciais para subsidiar o planejamento, a programação, a regulação, o controle, a avaliação e a auditoria dos serviços de saúde ambulatoriais em todo o território nacional.1

O fluxo de dados do sistema opera em um ciclo mensal. Os estabelecimentos de saúde, sejam eles públicos ou privados conveniados ao SUS, registram sua produção ambulatorial. Esses dados são então submetidos aos gestores locais (municipais ou estaduais), que utilizam o software do SIA para processar, validar e consolidar as informações. Após essa etapa de validação, as bases de dados consolidadas são enviadas ao Departamento de Informática do SUS (DATASUS), onde compõem a base de dados nacional, que é então disponibilizada para consulta e análise.4 Este processo garante um repositório centralizado de informações sobre a vasta rede de atendimento ambulatorial do país.

### 1.2. Desconstruindo o Arquivo `PA`: Um Mosaico de Instrumentos

O principal produto do processamento do SIA é o arquivo de Produção Ambulatorial, comumente conhecido como arquivo `PA` (identificado nos sistemas do DATASUS como `PAufaamm.DBC` ou `.DBF`, onde 'uf' é a unidade da federação, 'aa' é o ano e 'mm' é o mês).6 Um erro comum na análise desses dados é presumir que cada linha do arquivo representa o mesmo tipo de evento. Na realidade, o arquivo

`PA` é uma consolidação de registros provenientes de instrumentos de coleta fundamentalmente distintos, cada um com sua própria lógica e nível de agregação.1 Compreender a natureza desses instrumentos de origem é o primeiro passo para uma análise correta.

Os principais instrumentos de registro que alimentam o arquivo `PA` são:

- **Boletim de Produção Ambulatorial (BPA):** É a ferramenta primária para registrar procedimentos que não exigem uma autorização prévia do gestor.3 O BPA se manifesta de duas formas:
    
    - **BPA-C (Consolidado):** Registra os procedimentos de forma agregada. Por exemplo, um único registro em um BPA-C pode representar "50 hemogramas completos" realizados em um determinado mês, sem identificar os pacientes individualmente. Este formato prioriza a simplicidade do registro em detrimento do detalhe clínico-demográfico.3
        
    - **BPA-I (Individualizado):** Registra os procedimentos de forma individualizada, um por paciente. Cada linha corresponde a um atendimento específico, preservando informações demográficas do paciente (como sexo, idade, município de residência) e dados clínicos (como o diagnóstico principal).3
        
- **Autorização de Procedimentos de Alta Complexidade (APAC):** É o instrumento utilizado para procedimentos de alto custo, alta complexidade ou que requerem um controle e monitoramento mais rigorosos, necessitando de autorização prévia do gestor. Exemplos clássicos incluem sessões de quimioterapia, radioterapia e hemodiálise.3 Por sua natureza, os registros de APAC são sempre individualizados.
    
- **Registro das Ações Ambulatoriais de Saúde (RAAS):** Um instrumento mais recente, instituído para monitorar ações e serviços de saúde organizados em Redes de Atenção à Saúde. Possui variações para áreas específicas, como a Atenção Psicossocial (RAAS-PSI) e a Atenção Domiciliar (RAAS-AD).11 Os registros do RAAS também são individualizados.
    

### 1.3. A Pedra de Roseta: O Papel Crítico do Campo `PA_DOCORIG`

Dada a heterogeneidade dos registros no arquivo `PA`, um campo específico funciona como a chave mestra para a correta interpretação dos dados: `PA_DOCORIG` (Documento de Origem). Este campo é, sem dúvida, o mais importante para qualquer analista, pois identifica qual dos instrumentos de registro (BPA-C, BPA-I, APAC ou RAAS) gerou aquela linha específica no banco de dados.7 O valor neste campo determina o nível de observação do registro e, consequentemente, quais outros campos na mesma linha são válidos e interpretáveis.

Ignorar o `PA_DOCORIG` leva a erros analíticos graves. Considere um cenário em que um pesquisador deseja calcular a quantidade total de um determinado procedimento. Se ele simplesmente somar a coluna `PA_QTDAPR` (Quantidade Aprovada) em todo o arquivo, estará somando valores que representam contagens de pacientes únicos (de registros BPA-I, APAC e RAAS, onde a quantidade é geralmente 1) com contagens de lotes de procedimentos (de registros BPA-C, onde a quantidade pode ser de centenas). O resultado seria um número inflado e sem significado estatístico. Da mesma forma, tentar calcular a idade média dos pacientes utilizando todo o arquivo seria inválido, pois os campos demográficos como `PA_IDADE` estão vazios ou não são aplicáveis para os registros originados do BPA-C.

Portanto, a primeira etapa obrigatória de qualquer análise do arquivo `PA` deve ser a segmentação ou filtragem dos dados com base no campo `PA_DOCORIG`. As análises de perfil de paciente só podem ser realizadas em registros individualizados, enquanto as análises de volume total de produção devem tratar os registros consolidados e individualizados de maneira distinta.

**Tabela 1: Definições dos Códigos do Campo `PA_DOCORIG`**

|Código|Descrição|Nível de Observação|
|---|---|---|
|`P`|Procedimento Principal de APAC|Individualizado|
|`S`|Procedimento Secundário de APAC|Individualizado|
|`C`|Procedimento de BPA Consolidado|Agregado|
|`I`|Procedimento de BPA Individualizado|Individualizado|
|`A`|Procedimento de RAAS (Atenção Domiciliar)|Individualizado|
|`R`|Procedimento de RAAS (Atenção Psicossocial)|Individualizado|

Fonte: Derivado do Informe Técnico do SIASUS.7

## Seção II: Dicionário de Dados Granular por Grupo Temático

Esta seção central fornece uma análise exaustiva, campo por campo, das 60 colunas do arquivo `PA`. Cada entrada inclui o nome da coluna, uma descrição detalhada, o tipo e tamanho dos dados (conforme o layout oficial) e uma explicação abrangente de seus valores possíveis, com links para sistemas externos quando necessário.

### Parte A: Identificadores do Estabelecimento, Gestão e Jurídicos

Estes campos identificam o "quem" e o "onde" do prestador de serviços.

- **`PA_CODUNI` (CHAR 7):** _Código da Unidade de Saúde._ Identificador único de 7 dígitos do estabelecimento de saúde onde o procedimento foi realizado. Este código é a chave primária para vincular os dados do SIA ao **Cadastro Nacional de Estabelecimentos de Saúde (CNES)**.7 Através do CNES, é possível obter informações detalhadas sobre o estabelecimento, como nome, endereço, tipo de unidade, infraestrutura, equipamentos e profissionais vinculados.13
    
- **`PA_UFMUN` (CHAR 6):** _UF e Município do Estabelecimento._ Código de 6 dígitos do Instituto Brasileiro de Geografia e Estatística (IBGE) para o município onde o estabelecimento está localizado (2 dígitos para a Unidade da Federação e 4 para o município).7 É essencial para qualquer análise com recorte geográfico.
    
- **`PA_GESTAO` (CHAR 6):** _Código do Gestor._ Código IBGE do município responsável pela gestão financeira e administrativa do estabelecimento. Se o estabelecimento estiver sob gestão estadual, o campo conterá o código da UF seguido de "0000".7 Este campo é crucial para entender a governança do sistema de saúde, os fluxos de financiamento e as responsabilidades de gestão.
    
- **`PA_CONDIC` (CHAR 2):** _Condição de Gestão._ Código que indica a modalidade de habilitação do município ou estado na gestão do SUS (ex: Gestão Plena da Atenção Básica, Gestão Plena do Sistema Municipal). Este campo reflete o nível de descentralização e autonomia do gestor, o que impacta as transferências de recursos e as responsabilidades. Os códigos e suas descrições são encontrados em tabelas auxiliares do SIA.7
    
- **`PA_TPUPS` (CHAR 2):** _Tipo de Estabelecimento._ Código proveniente do CNES que classifica o tipo de unidade de saúde (ex: `01` - Posto de Saúde, `02` - Centro de Saúde/Unidade Básica de Saúde, `05` - Hospital Geral).9 Fornece um contexto vital sobre o cenário do atendimento.
    
- **`PA_TIPPRE` (CHAR 2):** _Tipo de Prestador._ Código que indica a natureza do prestador de serviço (ex: público, privado contratado/conveniado, filantrópico). A informação é originária do CNES e permite análises sobre a participação dos diferentes setores na oferta de serviços do SUS.
    
- **`PA_MN_IND` (CHAR 1):** _Estabelecimento Mantido/Individual._ Indica se o estabelecimento é uma filial ou unidade mantida por uma entidade maior ('M' - Mantido) ou se é uma entidade independente ('I' - Individual).15
    
- **`PA_CNPJCPF` (CHAR 14):** _CNPJ/CPF do Estabelecimento._ Número de inscrição no Cadastro Nacional da Pessoa Jurídica (CNPJ) ou no Cadastro de Pessoas Físicas (CPF) do estabelecimento que realizou o procedimento.7
    
- **`PA_CNPJMNT` (CHAR 14):** _CNPJ da Mantenedora._ CNPJ da entidade mantenedora do estabelecimento, se aplicável (ex: o CNPJ da secretaria municipal de saúde para um posto de saúde, ou de uma universidade para um hospital universitário). Preenchido com zeros se não houver mantenedora.7
    
- **`PA_CNPJ_CC` (CHAR 14):** _CNPJ de Cessão de Crédito._ CNPJ da entidade que recebeu o pagamento pela produção por meio de um contrato de cessão de crédito. Preenchido com zeros se não for o caso.7
    
- **`PA_INE` (CHAR 10):** _Identificador Nacional de Equipe._ Código único que identifica a equipe de saúde responsável pelo atendimento (ex: uma equipe específica da Estratégia Saúde da Família). Este campo é fundamental para a avaliação de modelos de atenção baseados em equipes, especialmente na atenção primária, e estabelece uma ponte com os dados do sistema e-SUS Atenção Primária.7
    
- **`PA_NAT_JUR` (CHAR 4):** _Natureza Jurídica._ Código que define a constituição jurídico-institucional do estabelecimento, conforme a tabela da Comissão Nacional de Classificação (CONCLA) do IBGE e registrada no CNES.17 Este campo permite distinguir com precisão entre órgãos da administração pública, empresas privadas, entidades sem fins lucrativos, etc.
    

### Parte B: Identificadores de Registro, Processamento e Competência

Estes campos definem o "quando" do registro de dados.

- **`PA_MVM` (CHAR 6):** _Data de Movimento._ Ano e mês (formato AAAAMM) em que os dados foram processados pelo gestor local e incluídos no movimento para faturamento e consolidação.7
    
- **`PA_CMP` (CHAR 6):** _Data de Competência._ Ano e mês (formato AAAAMM) em que o serviço de saúde foi efetivamente realizado.7
    

A análise da defasagem entre a competência (`PA_CMP`) e o movimento (`PA_MVM`) é uma ferramenta poderosa. O SUS estabelece prazos para que os prestadores enviem sua produção para processamento.9 Uma diferença significativa e consistente entre essas duas datas para um determinado prestador ou gestor pode indicar ineficiências administrativas, atrasos no envio dos dados ou gargalos no processamento. Ao realizar análises temporais, o pesquisador deve fazer uma escolha consciente: filtrar por

`PA_CMP` para capturar todos os serviços realizados em um determinado mês (mesmo que tenham sido informados tardiamente) ou filtrar por `PA_MVM` para analisar o conjunto de dados exato que foi processado e pago em um ciclo específico. A escolha impacta diretamente os resultados e a interpretação da análise.

### Parte C: Demografia e Localização do Paciente

Estes campos descrevem o "quem" do paciente. Sua presença e validade dependem intrinsecamente do registro ser individualizado (`PA_DOCORIG` com valores 'I', 'P', 'S', 'A' ou 'R').

- **`PA_MUNPCN` (CHAR 6):** _Município de Residência do Paciente._ Código IBGE de 6 dígitos do município de residência do paciente.15 Este é um dos campos mais importantes para estudos de fluxo de pacientes, acesso a serviços, equidade e planejamento da rede de atenção regionalizada.
    
- **`PA_IDADE` (NUMERIC 3):** _Idade do Paciente._ Idade do paciente em anos completos. Para crianças com menos de um ano, este campo geralmente é preenchido com 0, e a idade precisa (em dias ou meses) pode estar em outros campos não presentes nesta lista de 60 colunas, mas disponíveis em layouts mais detalhados de instrumentos como o RAAS.
    
- **`IDADEMIN` & `IDADEMAX` (NUMERIC):** _Idade Mínima e Máxima para o Procedimento._ É crucial notar que estas duas colunas **não são campos nativos** do arquivo `PA` padrão, conforme o layout do Informe Técnico do DATASUS.7 Elas são atributos do
    
    _procedimento_ e não do _paciente_. A sua presença na lista de colunas fornecida indica que os dados foram previamente enriquecidos. O processo para obter esses valores envolve a junção do arquivo `PA` com a tabela do SIGTAP (Tabela de Procedimentos do SUS) usando o campo `PA_PROC_ID` como chave. O SIGTAP define, para cada procedimento, uma faixa etária permitida para sua realização.19 Estes valores são usados pelo sistema SIA para validação, gerando um alerta no campo
    
    `PA_FLIDADE`.
    
- **`PA_SEXO` (CHAR 1):** _Sexo do Paciente._ Campo codificado que informa o sexo do paciente, conforme registrado no atendimento.15
    

**Tabela 2: Definições dos Códigos do Campo `PA_SEXO`**

|Código|Descrição|
|---|---|
|`M`|Masculino|
|`F`|Feminino|
|`I`|Ignorado|

Fonte: Padrão de codificação do SUS.15

- **`PA_RACACOR` (CHAR 2):** _Raça/Cor do Paciente._ Campo para a raça/cor autodeclarada do paciente, seguindo a classificação do IBGE. É um campo vital para análises de equidade em saúde e monitoramento de disparidades raciais no acesso e utilização dos serviços.3
    

**Tabela 3: Definições dos Códigos do Campo `PA_RACACOR`**

|Código|Descrição|
|---|---|
|`01`|Branca|
|`02`|Preta|
|`03`|Parda|
|`04`|Amarela|
|`05`|Indígena|
|`99`|Ignorado|

Fonte: Padrão de codificação do SUS baseado no IBGE.15

- **`PA_ETNIA` (CHAR 4):** _Etnia do Paciente._ Código de 4 dígitos para a etnia indígena do paciente, quando `PA_RACACOR` for `05`. Este campo utiliza uma tabela de referência específica de povos indígenas mantida pela Fundação Nacional do Índio (FUNAI) e pela Secretaria Especial de Saúde Indígena (SESAI), permitindo análises de saúde com um recorte específico para essa população.7
    

### Parte D: Informações sobre Procedimento, Serviço e Clínica

Estes campos descrevem o "o quê" e o "porquê" do atendimento de saúde.

- **`PA_PROC_ID` (CHAR 10):** _Código do Procedimento._ Código de 10 dígitos que identifica univocamente o procedimento realizado, conforme a **Tabela de Procedimentos, Medicamentos, Órteses, Próteses e Materiais Especiais do SUS (SIGTAP)**.7 Este é o campo central para a compreensão do serviço clínico prestado e a principal chave de ligação com a tabela SIGTAP para enriquecimento dos dados.
    
- **`PA_NIVCPL` (CHAR 1):** _Nível de Complexidade._ Classifica a complexidade do procedimento. Este é um atributo do procedimento, importado do SIGTAP. Os valores típicos são: `1` para Atenção Básica, `2` para Média Complexidade e `3` para Alta Complexidade.15
    
- **`PA_CATEND` (CHAR 2):** _Caráter do Atendimento._ Código que descreve a natureza do atendimento, fundamental para análises epidemiológicas e operacionais.3 Distingue, por exemplo, atendimentos eletivos de urgências.
    

**Tabela 4: Definições dos Códigos do Campo `PA_CATEND` (Exemplos para Ambulatorial)**

|Código|Descrição|
|---|---|
|`01`|Eletivo|
|`02`|Urgência|
|`03`|Acidente no local de trabalho ou a serviço da empresa|
|`04`|Acidente de trânsito|
|`05`|Outras lesões e envenenamentos por agentes químicos ou físicos|

Nota: Esta é uma tabela exemplificativa. A tabela oficial completa deve ser consultada na documentação auxiliar do SIA. A referência 20 mostra uma tabela similar para internações, reforçando a necessidade de usar a tabela correta para o contexto ambulatorial.

- **`PA_SRV_C` (CHAR 6):** _Serviço/Classificação._ Código do SIGTAP que agrupa procedimentos em categorias clínicas mais amplas. É composto por um código de "Serviço" (3 dígitos) e um de "Classificação" (3 dígitos). Por exemplo, o Serviço `135` (Serviço de Reabilitação) pode conter a Classificação `005` (Reabilitação Auditiva).21 Permite análises em um nível mais agregado do que o de procedimentos individuais.
    
- **`PA_CIDPRI` (CHAR 4):** _CID Principal._ Código da Classificação Internacional de Doenças, 10ª Revisão (CID-10), que representa o diagnóstico principal ou o motivo que levou à realização do procedimento. O formato é alfanumérico (ex: `J450` para Asma).7
    
- **`PA_CIDSEC` (CHAR 4):** _CID Secundário._ Código de um diagnóstico secundário (CID-10) relevante para o atendimento.7
    
- **`PA_CIDCAS` (CHAR 4):** _CID Causas Associadas._ Código de um diagnóstico (CID-10) de causa associada, frequentemente utilizado para registrar causas externas de lesões e envenenamentos (Capítulo XX da CID-10).7
    

### Parte E: Atendimento, Autorização e Desfecho

Estes campos rastreiam o fluxo administrativo e o resultado da jornada do paciente.

- **`PA_DOCORIG` (CHAR 1):** _Documento de Origem._ Conforme descrito em detalhe na Seção 1.3, este campo identifica o instrumento de registro que deu origem à linha de dados.
    
- **`PA_AUTORIZ` (CHAR 13):** _Número da Autorização._ Para procedimentos originados de uma APAC ou que exigem autorização no BPA-I, este campo contém o número único da autorização emitida pelo gestor.7
    
- **`PA_MOTSAI` (CHAR 2):** _Motivo de Saída/Permanência._ Código que indica o desfecho do tratamento ou do episódio de cuidado, especialmente relevante para tratamentos contínuos registrados via APAC.15
    

**Tabela 5: Definições dos Códigos do Campo `PA_MOTSAI` (Exemplos)**

|Código|Descrição|
|---|---|
|`11`|Alta por cura|
|`14`|Alta a pedido|
|`21`|Permanência por características próprias da doença|
|`31`|Transferência para outro estabelecimento|
|`41`|Óbito com causa diretamente relacionada à doença|
|`42`|Óbito com causa não relacionada à doença|

_Nota: A tabela completa, com dezenas de códigos, deve ser obtida na documentação auxiliar do SIA._

- **`PA_OBITO` (CHAR 1):** _Óbito._ Flag que indica se o paciente veio a óbito durante o tratamento (`1` = Sim, `0` = Não).
    
- **`PA_ENCERR` (CHAR 1):** _Encerramento._ Flag que indica se o episódio de cuidado (ex: uma APAC para um tratamento de 12 meses) foi encerrado.
    
- **`PA_PERMAN` (CHAR 1):** _Permanência._ Flag que indica que o paciente continua em tratamento.
    
- **`PA_ALTA` (CHAR 1):** _Alta._ Flag que indica que o paciente recebeu alta daquele episódio de cuidado.
    
- **`PA_TRANSF` (CHAR 1):** _Transferência._ Flag que indica que o paciente foi transferido para outro serviço ou estabelecimento.
    

### Parte F: Identificação do Profissional de Saúde

Estes campos identificam o profissional que realizou o serviço.

- **`PA_CNSMED` (CHAR 15):** _Cartão Nacional de Saúde do Profissional._ Número do Cartão Nacional de Saúde (CNS) do profissional de saúde que executou o procedimento.15 Permite a identificação única do profissional.
    
- **`PA_CBOCOD` (CHAR 6):** _Código Brasileiro de Ocupação._ Código de 6 dígitos que identifica a ocupação do profissional (ex: `225125` para Médico Clínico), conforme a Classificação Brasileira de Ocupações (CBO) do Ministério do Trabalho e Emprego.9 Este campo é essencial para estudos sobre força de trabalho, distribuição de especialistas e adequação do profissional ao procedimento realizado. A CBO pode ser consultada online nos portais do MTE ou do IBGE.23
    

### Parte G: Dados Financeiros, de Financiamento e Contratuais

Estes campos são centrais para o propósito financeiro e de auditoria do SIA.

- **`PA_QTDPRO` (NUMERIC 10):** _Quantidade Produzida._ A quantidade do procedimento que foi informada pelo prestador de serviço.7
    
- **`PA_QTDAPR` (NUMERIC 10):** _Quantidade Aprovada._ A quantidade do procedimento que foi aprovada para pagamento pelo gestor após as validações do sistema.7
    
- **`PA_VALPRO` (NUMERIC 16,2):** _Valor Produzido._ O valor total submetido pelo prestador, calculado como (preço unitário do procedimento * `PA_QTDPRO`).7
    
- **`PA_VALAPR` (NUMERIC 16,2):** _Valor Aprovado._ O valor total aprovado para pagamento, calculado como (preço unitário * `PA_QTDAPR`).7
    
- **`PA_VL_CF` (NUMERIC 16,2):** _Valor do Complemento Federal._ Valor de incentivos financeiros de nível federal que são somados ao valor base do procedimento. Usado para políticas específicas de saúde.7
    
- **`PA_VL_CL` (NUMERIC 16,2):** _Valor do Complemento Local._ Valor de incentivos financeiros adicionados pelo gestor estadual ou municipal, como parte de políticas locais de saúde.7
    
- **`PA_VL_INC` (NUMERIC 16,2):** _Valor do Incremento._ Valor total de outros tipos de incrementos financeiros, como o de urgência, aplicados ao procedimento.7
    
- **`NU_VPA_TOT` & `NU_PA_TOT` (NUMERIC):** _Valor Total Aprovado & Valor Total._ Semelhante a `IDADEMIN`/`MAX`, estes campos não constam no layout padrão do arquivo `PA`.7 Eles representam campos calculados ou derivados, provavelmente adicionados em uma base de dados pré-processada. A lógica mais provável é que
    
    `NU_VPA_TOT` seja a soma de todos os componentes do valor aprovado: NU_VPA_TOT=PA_VALAPR+PA_VL_CF+PA_VL_CL+PA_VL_INC. O usuário deve verificar esta fórmula ou calculá-la se estiver trabalhando com os dados brutos.
    
- **`PA_DIF_VAL` (NUMERIC 20,2):** _Diferença de Valores._ Registra a diferença entre o valor do procedimento na tabela nacional do SUS e um valor diferenciado negociado localmente pelo gestor, multiplicada pela quantidade aprovada.15
    
- **`PA_TPFIN` (CHAR 2) & `PA_SUBFIN` (CHAR 4):** _Tipo e Subtipo de Financiamento._ Códigos que especificam a fonte de recursos (bloco de financiamento) para o pagamento do procedimento. É um campo crítico para o acompanhamento orçamentário e a análise de políticas de saúde com financiamento específico.7
    

**Tabela 6: Definições dos Códigos do Campo `PA_TPFIN` (Exemplos)**

|Código|Descrição do Bloco de Financiamento|
|---|---|
|`01`|Atenção Básica (PAB)|
|`04`|Média e Alta Complexidade (MAC)|
|`06`|Fundo de Ações Estratégicas e Compensação (FAEC)|
|`07`|Vigilância em Saúde|

_Fonte: Tabela de Financiamento do SIGTAP/SIA._

- **`PA_REGCT` (CHAR 4):** _Regra Contratual._ Código originário do CNES que define regras contratuais específicas entre o prestador e o gestor do SUS, que podem influenciar o pagamento ou as condições de oferta do serviço.7
    
- **`PA_INCOUT` (CHAR 4) & `PA_INCURG` (CHAR 4):** _Incremento Outros & Incremento Urgência._ Códigos que identificam a aplicação de incrementos financeiros específicos ao valor do procedimento, conforme regras definidas na tabela SIGTAP.7
    

### Parte H: Flags do Sistema e Indicadores de Validação

Estes campos são gerados pelo sistema SIA durante o processamento para sinalizar situações específicas ou erros.

- **`PA_INDICA` (CHAR 1):** _Indicativo de Situação da Produção._ Um flag que resume o status de aprovação da produção apresentada.7
    

**Tabela 7: Definições dos Códigos do Campo `PA_INDICA`**

|Código|Descrição|
|---|---|
|`0`|Não aprovado|
|`5`|Aprovado total|
|`6`|Aprovado parcial|

Fonte: Informe Técnico do SIASUS.7

- **`PA_CODOCO` (CHAR 4):** _Código de Ocorrência._ Código que detalha o motivo da rejeição ou alteração da produção informada. Cada código corresponde a uma crítica específica do sistema (ex: "procedimento incompatível com o sexo do paciente", "idade do paciente fora da faixa permitida").
    
- **`PA_UFDIF` (CHAR 1):** _UF Diferente._ Flag que indica se a Unidade da Federação de residência do paciente é diferente da UF de localização do estabelecimento (`S` = Sim, `N` = Não).15
    
- **`PA_MNDIF` (CHAR 1):** _Município Diferente._ Flag que indica se o município de residência do paciente é diferente do município de localização do estabelecimento (`1` = Sim, `0` = Não).7
    
- **`PA_FLIDADE` (CHAR 1):** _Flag de Idade._ Flag gerado pelo sistema que sinaliza uma inconsistência entre a idade do paciente (`PA_IDADE`) e a faixa etária permitida para o procedimento (`IDADEMIN`, `IDADEMAX`) definida no SIGTAP.
    
- **`PA_FLQT` (CHAR 1):** _Flag de Quantidade._ Flag que indica um problema com a quantidade informada (ex: quantidade máxima excedida para o período).
    
- **`PA_FLER` (CHAR 1):** _Flag de Erro._ Um flag de erro genérico, frequentemente associado a inconsistências no preenchimento de uma APAC.7
    

## Seção III: Guia Prático para Navegar nos Sistemas de Saúde Nacionais Vinculados

O arquivo `PA` não deve ser visto como um conjunto de dados isolado, mas como um hub que se conecta a outros sistemas de informação cruciais do SUS. O enriquecimento dos dados do SIA com informações desses sistemas externos é uma etapa fundamental para uma análise aprofundada.

### 3.1. Usando `PA_PROC_ID` para Consultar o SIGTAP

A coluna `PA_PROC_ID` é a chave para desvendar todos os detalhes sobre o serviço clínico prestado.

- **Ação:** Extraia um código do campo `PA_PROC_ID` do seu conjunto de dados.
    
- **Recurso:** Acesse o portal online do SIGTAP ou faça o download da sua base de dados mensal, disponível no site do DATASUS.26
    
- **Resultado:** Ao consultar o código, você obterá o nome oficial e a descrição completa do procedimento, seu nível de complexidade (`PA_NIVCPL`), as regras de financiamento (`PA_TPFIN`), a ocupação do profissional habilitado a realizá-lo (`PA_CBOCOD`), os diagnósticos (CID-10) compatíveis e, de forma crucial, a faixa etária permitida (`IDADEMIN` e `IDADEMAX`).19 Isso explica diretamente a origem das colunas de idade mínima e máxima na sua lista.
    

### 3.2. Usando `PA_CODUNI` para Alavancar o CNES

A coluna `PA_CODUNI` permite traçar o perfil completo do local onde o atendimento ocorreu.

- **Ação:** Utilize um código do campo `PA_CODUNI`.
    
- **Recurso:** Acesse o portal de consulta pública do CNES ou baixe os microdados completos do DATASUS.14
    
- **Resultado:** A consulta retornará o perfil completo do estabelecimento: nome fantasia, endereço, tipo de unidade (`PA_TPUPS`), natureza jurídica (`PA_NAT_JUR`), tipo de gestão, equipamentos disponíveis, serviços habilitados e a lista de profissionais com vínculo ativo.
    

### 3.3. Usando `PA_CBOCOD` para Entender a Força de Trabalho

A coluna `PA_CBOCOD` é a porta de entrada para análises sobre os profissionais de saúde.

- **Ação:** Pegue um código do campo `PA_CBOCOD`.
    
- **Recurso:** Utilize a ferramenta de busca da Classificação Brasileira de Ocupações, disponível no portal do Ministério do Trabalho e Emprego (MTE).23
    
- **Resultado:** Você obterá o título oficial da ocupação e uma descrição detalhada das atividades, competências e responsabilidades associadas àquele código, permitindo uma compreensão clara do papel daquele profissional no sistema.
    

### 3.4. Usando `PA_CID*` para Análise Diagnóstica Precisa

As colunas `PA_CIDPRI`, `PA_CIDSEC` e `PA_CIDCAS` são a base para estudos de morbidade.

- **Ação:** Utilize um código de qualquer um dos campos CID.
    
- **Recurso:** Consulte uma ferramenta online de busca da CID-10 ou as tabelas oficiais disponibilizadas pelo DATASUS ou pela Organização Mundial da Saúde (OMS).31
    
- **Resultado:** A consulta fornecerá a descrição completa do diagnóstico, permitindo a realização de estudos epidemiológicos detalhados, análises de perfil de morbidade e monitoramento de doenças e agravos.
    

## Seção IV: Considerações Analíticas e Recomendações de Especialistas

Esta seção final sintetiza os pontos-chave do relatório em conselhos práticos para o analista de dados, com o objetivo de prevenir erros comuns e promover análises robustas e precisas.

### 4.1. A Armadilha da Agregação: Sempre Comece com `PA_DOCORIG`

A distinção entre registros consolidados (BPA-C) e individualizados (BPA-I, APAC, RAAS) é a consideração mais crítica ao trabalhar com dados do SIA. A recomendação é inequívoca: antes de realizar qualquer cálculo, o conjunto de dados deve ser estratificado por `PA_DOCORIG`. Análises de perfil de paciente (idade, sexo, residência) só podem ser feitas sobre o subconjunto de dados individualizados. Análises de volume ou financeiras devem tratar os dois tipos de registro de forma separada ou utilizar metodologias que ponderem adequadamente cada tipo de registro. Somar ou calcular médias sobre o arquivo completo, sem essa distinção, produzirá resultados estatisticamente inválidos e levará a conclusões equivocadas.

### 4.2. A Trilha de Auditoria Financeira: Analisando `PROD` vs. `APR`

O SIA, em sua essência, é um sistema de pagamento. A existência de campos pareados para "produzido/apresentado" e "aprovado" (`PA_QTDPRO`/`PA_QTDAPR`, `PA_VALPRO`/`PA_VALAPR`) oferece uma oportunidade única de análise. A diferença entre esses pares, quando cruzada com o código de ocorrência (`PA_CODOCO`), transforma o banco de dados em uma poderosa ferramenta de auditoria e análise de desempenho. Essa abordagem pode revelar padrões de erros de faturamento, inconsistências entre as regras do gestor e a prática do prestador, ou identificar áreas que necessitam de capacitação e melhoria nos processos de registro.

### 4.3. Análise de Séries Temporais: Cuidado com as Mudanças Estruturais

O SIA é um sistema dinâmico que passou por evoluções significativas ao longo de sua história. Mudanças importantes, como a implantação da Tabela de Procedimentos Unificada em 2008 15 e a introdução do RAAS em 2012 11, alteraram o layout dos arquivos, a codificação de procedimentos e a forma de registro de certas ações. Ao conduzir estudos longitudinais que abrangem vários anos, é imperativo que o pesquisador esteja ciente dessas mudanças. Recomenda-se sempre verificar a data de competência (

`PA_CMP`) dos dados e consultar as notas técnicas e manuais históricos correspondentes ao período em estudo para garantir a comparabilidade dos dados ao longo do tempo.

### 4.4. Abordando as Colunas "Ausentes"

A lista de colunas fornecida para análise continha quatro campos (`IDADEMIN`, `IDADEMAX`, `NU_VPA_TOT`, `NU_PA_TOT`) que não fazem parte do layout padrão do arquivo `PA` disseminado pelo DATASUS. Conforme detalhado neste relatório, `IDADEMIN` e `IDADEMAX` são atributos do procedimento, provenientes de uma junção com a tabela SIGTAP. Da mesma forma, `NU_VPA_TOT` e `NU_PA_TOT` são, muito provavelmente, campos de conveniência que representam a soma de todos os componentes de valor. É fundamental que o usuário compreenda que está trabalhando com uma versão pré-processada e enriquecida dos dados, e que deve validar a metodologia usada para criar esses campos derivados.

### 4.5. Recomendação Final: O Fluxo de Trabalho "Enriquecimento Primeiro"

O arquivo `PA` bruto é apenas o ponto de partida. Para extrair o máximo valor analítico, um fluxo de trabalho robusto deve ser adotado. A recomendação final é a abordagem de "enriquecimento primeiro": antes de iniciar a análise estatística, o analista deve sistematicamente juntar os microdados do arquivo `PA` com as tabelas mestras do CNES (usando `PA_CODUNI`), SIGTAP (usando `PA_PROC_ID`), CBO (usando `PA_CBOCOD`) e tabelas geográficas do IBGE (usando `PA_UFMUN` e `PA_MUNPCN`). Este processo transforma um arquivo de transações em um conjunto de dados rico e contextualizado, permitindo análises muito mais profundas e precisas sobre o sistema de saúde brasileiro.

# Dicionário de Dados Exaustivo do Sistema de Informações Hospitalares (SIH/SUS): Um Guia de Referência para Análise de Microdados da AIH

## Introdução: Desvendando o Ecossistema do Sistema de Informações Hospitalares (SIH/SUS)

O Sistema de Informações Hospitalares do Sistema Único de Saúde (SIH/SUS) representa uma das mais vastas e detalhadas fontes de dados sobre a saúde da população brasileira. Gerido pelo Ministério da Saúde, por meio da Secretaria de Atenção Especializada à Saúde, e processado pelo DATASUS, este sistema é o repositório central de informações sobre todas as internações hospitalares financiadas com recursos públicos no Brasil.1 Sua alimentação é um processo contínuo e obrigatório para todas as unidades hospitalares, sejam elas públicas ou privadas conveniadas, que integram a rede do SUS.

A compreensão aprofundada do SIH/SUS exige o reconhecimento de sua dupla natureza fundamental. Em sua essência, o sistema foi concebido como uma ferramenta administrativo-financeira. Sua finalidade primária é transcrever e viabilizar o pagamento dos atendimentos que resultam em internação.3 Cada registro no banco de dados corresponde a uma Autorização de Internação Hospitalar (AIH), que funciona, na prática, como uma "conta hospitalar" detalhada, contendo os procedimentos realizados, os diagnósticos, os dias de permanência e os valores a serem ressarcidos pelo gestor público.2

Contudo, o vasto acervo de informações coletadas para fins de faturamento conferiu ao SIH/SUS um valor secundário de magnitude inestimável: ele se tornou um pilar para a saúde pública e a pesquisa no país. Analistas, epidemiologistas e gestores utilizam seus microdados para monitorar a morbidade hospitalar, identificar surtos epidêmicos, planejar a alocação de recursos, avaliar a eficácia de políticas de saúde e conduzir estudos científicos de alto impacto.1

O documento que origina cada registro é a Autorização de Internação Hospitalar (AIH). O fluxo de informação começa com a emissão de um "Laudo para Solicitação de AIH" por um profissional de saúde, que justifica a necessidade da internação.6 Após a aprovação por um médico autorizador ou gestor, a AIH é emitida, recebendo uma numeração única. Ao final da internação, o hospital preenche todos os detalhes do atendimento — incluindo o diagnóstico final, os procedimentos efetivamente realizados e o motivo da alta — para submeter a AIH ao faturamento.8 Este processo, que antes envolvia formulários de papel, hoje é majoritariamente eletrônico, utilizando sistemas como o

`SISAIH01` (no prestador) e o `SIHD2` (no gestor).6

É crucial para qualquer analista entender que o SIH/SUS é um sistema dinâmico, em constante evolução. Ao longo dos anos, seus layouts de arquivo, softwares de processamento e a própria estrutura das variáveis foram atualizados para incorporar novas tecnologias, políticas de saúde e necessidades de informação.6 Mudanças na codificação de variáveis, como a de natureza jurídica, ou a expansão da capacidade de registrar diagnósticos secundários, são exemplos que exigem atenção redobrada em análises de séries históricas para evitar conclusões equivocadas.12

Este guia foi elaborado para servir como um dicionário de dados definitivo para as 113 variáveis presentes nos arquivos de microdados do SIH/SUS. O objetivo é ir além da simples definição de cada campo, oferecendo um contexto clínico, administrativo e financeiro para cada um. O relatório está estruturado em seções temáticas que seguem a lógica de uma internação hospitalar: identificação do registro, caracterização do prestador, perfil do paciente, detalhes clínicos da internação, componentes financeiros e campos de controle. Ao final, são apresentadas as principais tabelas de códigos e uma conclusão sobre as potencialidades e limitações do uso desses dados para pesquisa.

## Parte I: Identificação e Contexto Temporal da AIH

Esta seção detalha as variáveis que são os pilares da organização do banco de dados. Elas situam cada registro de internação no tempo, identificam-no de forma única e o vinculam ao processo de faturamento do DATASUS. A correta compreensão destes campos-chave é o primeiro passo para qualquer análise de dados do SIH.

### Variáveis de Competência e Processamento

Os campos de competência definem o período administrativo em que a AIH foi processada e paga, o que não deve ser confundido com o período em que o evento clínico ocorreu.

- `ANO_CMPT` (Ano de Competência): Representa o ano em que a AIH foi incluída no processamento para faturamento. É um campo numérico de 4 dígitos (ex: 2023).
    
- `MES_CMPT` (Mês de Competência): Representa o mês em que a AIH foi incluída no processamento para faturamento. É um campo numérico de 2 dígitos (1 a 12).
    

A combinação de `ANO_CMPT` e `MES_CMPT` forma a "competência", que é o principal critério de organização dos arquivos disponibilizados pelo DATASUS. No entanto, é fundamental entender a dissociação entre o tempo clínico e o tempo administrativo. Embora a competência frequentemente corresponda ao mês de alta do paciente, existem exceções importantes que podem introduzir um desfasamento temporal nos dados.2 Situações como AIHs que são rejeitadas em um mês e reapresentadas em outro, atrasos no envio do lote de faturamento pelo hospital, ou o faturamento mensal de internações de longa permanência fazem com que a data de competência não reflita a data do evento de saúde. Para análises epidemiológicas que investigam sazonalidade ou a cronologia de surtos, o uso das variáveis

`DT_INTER` (Data de Internação) e `DT_SAIDA` (Data de Saída) é mandatório. As variáveis de competência são mais adequadas para análises de gestão, fluxo de caixa e desempenho administrativo dos hospitais e gestores.

- `REMESSA`: Identifica o lote de dados (remessa) enviado pelo gestor local ao DATASUS. É um campo de controle interno para garantir a rastreabilidade e a integridade do processamento dos arquivos, que historicamente eram agrupados em um Documento para Registro de Internação Hospitalar (DCIH).6
    

### Identificadores Únicos da Internação

Estes campos garantem a unicidade de cada registro de internação e são essenciais para vincular informações relacionadas ao mesmo evento de saúde.

- `N_AIH` (Número da AIH): Este é o identificador único e principal de uma Autorização de Internação Hospitalar. Trata-se de um código numérico de 13 dígitos com uma estrutura específica: os dois primeiros dígitos identificam a Unidade da Federação, os dois seguintes o ano da emissão, o próximo indica o tipo de formulário, os sete seguintes são um número sequencial, e o último é um dígito verificador.6 Qualquer análise que precise rastrear um paciente ou vincular registros (como uma AIH principal e suas continuações) deve usar o
    
    `N_AIH` como chave primária.
    
- `IDENT` (Identificador do Tipo de AIH): Este campo categórico é um dos mais importantes para a correta manipulação dos dados do SIH. Ele especifica a natureza do registro da AIH, e filtrar por este campo é um passo metodológico crucial para evitar, por exemplo, a dupla contagem de pacientes ou a soma incorreta de valores. A estrutura do SIH prevê diferentes tipos de AIH para lidar com a complexidade do faturamento de diferentes situações clínicas e administrativas.6
    

|Código|Descrição|Contexto de Uso|
|---|---|---|
|1|AIH Principal/Normal|Representa o registro principal e, na maioria dos casos, único de uma internação. Contém os dados demográficos, clínicos e financeiros do evento.6|
|3|AIH de Continuação|Utilizada quando a quantidade de serviços profissionais ou procedimentos secundários excede o limite de registros da AIH principal. É uma extensão da AIH de tipo 1, compartilhando o mesmo `N_AIH`.6|
|5|AIH de Longa Permanência|Usada para o faturamento mensal de pacientes em especialidades como Psiquiatria, Cuidados Prolongados e Reabilitação. A mesma internação original gera múltiplos registros (um por mês) com `IDENT=5`, todos vinculados à AIH original.6|

- `SEQ_AIH5` (Sequencial da AIH 5): Quando `IDENT` é igual a 5 (longa permanência), este campo numérico de até 3 dígitos ordena as "parcelas" mensais de faturamento. Ele permite reconstruir a cronologia dos pagamentos de uma mesma internação prolongada.6
    
- `SEQUENCIA`: Esta coluna indica que o conjunto de dados pode ser uma versão "achatada" que combina a tabela principal da AIH (com dados da internação) e a tabela de Serviços Profissionais (SP). Nestes casos, a coluna `SEQUENCIA` funciona como um número de linha para cada serviço profissional registrado dentro de uma mesma AIH. O par `(N_AIH, SEQUENCIA)` identificaria unicamente um serviço específico (ex: um procedimento realizado por um médico específico) dentro de uma internação.1
    

## Parte II: Caracterização do Prestador de Serviço e da Gestão

Esta seção foca nas variáveis que identificam e caracterizam o hospital onde a internação ocorreu. Estes campos são vitais para análises comparativas entre diferentes tipos de prestadores, estudos sobre a rede de atenção à saúde, e para entender o papel das diferentes esferas de governo na gestão do SUS.

### Identificação do Estabelecimento

- `CNES` (Cadastro Nacional de Estabelecimentos de Saúde): É o código único de 7 dígitos que identifica cada hospital, clínica, laboratório ou qualquer outro estabelecimento de saúde no Brasil.15 Este campo é a chave-mestra para o cruzamento de dados do SIH com outras bases de dados do SUS, como o próprio banco de dados do CNES (para obter informações detalhadas sobre infraestrutura, equipamentos, recursos humanos e leitos), o Sistema de Informações Ambulatoriais (SIA) e outros.6
    
- `CGC_HOSP` (CNPJ do Hospital) e `CNPJ_MANT` (CNPJ da Mantenedora): São os identificadores fiscais (Cadastro Nacional da Pessoa Jurídica). Existe uma hierarquia entre eles: o `CNPJ_MANT` refere-se à entidade legal que administra o hospital (ex: uma fundação privada, uma secretaria municipal de saúde), enquanto o `CGC_HOSP` (termo antigo para CNPJ) identifica a unidade hospitalar específica, que pode ser a matriz ou uma filial da mantenedora.6
    

### Localização e Gestão

- `UF_ZI` (Unidade da Federação de Internação): Originalmente um código de 2 dígitos para a UF, este campo foi expandido para um código de 6 dígitos para identificar o município de internação (código IBGE).13 Esta mudança aumentou a granularidade geográfica, permitindo análises espaciais mais precisas sobre a oferta de serviços hospitalares.
    
- `MUNIC_MOV` (Município de Movimento): Código IBGE de 6 dígitos do município onde o estabelecimento de saúde está localizado. Confirma a localização da internação e é fundamental para análises de fluxo de pacientes.
    
- `GESTAO`: Indica o tipo de gestão do SUS sob a qual o hospital opera. Este campo reflete o processo de descentralização do sistema, mostrando se a responsabilidade pela contratação, controle e auditoria do prestador é do estado ou do município (em gestão plena).10
    
- `GESTOR_COD`, `GESTOR_TP`, `GESTOR_CPF`, `GESTOR_DT`: Conjunto de campos que identificam detalhadamente o gestor responsável pela autorização da AIH, incluindo seu código, tipo, CPF e a data da autorização. São campos primariamente utilizados para fins de auditoria e controle.6
    

### Atributos do Estabelecimento

- `NATUREZA` e `NAT_JUR` (Natureza Jurídica): Estes campos classificam o hospital quanto à sua natureza jurídica (público, privado com fins lucrativos, privado sem fins lucrativos, etc.). É fundamental notar a evolução desta variável. Conforme detalhado em notas técnicas do DATASUS, até maio de 2012, a informação estava no campo `NATUREZA`. A partir de junho de 2012, iniciou-se uma transição para o campo `NAT_JUR`, com uma nova codificação, e a partir de novembro de 2015, `NAT_JUR` tornou-se o padrão definitivo.12
    
    Este é um exemplo clássico da evolução dos metadados do SIH e impõe um desafio significativo para análises longitudinais. Um pesquisador que analise o período de 2010 a 2016 sem harmonizar estas variáveis concluiria, erroneamente, que a natureza jurídica de muitos hospitais se tornou "desconhecida" ou mudou drasticamente. A análise correta exige um pré-processamento que crie um campo único e consistente para todo o período, mapeando os códigos antigos de NATUREZA para os novos de NAT_JUR.
    

|Código (Exemplos)|Descrição da Natureza Jurídica (NAT_JUR)|
|---|---|
|1XXX|Administração Pública (Federal, Estadual, Municipal)|
|2XXX|Entidades Empresariais (ex: Sociedade Anônima, Ltda)|
|3XXX|Entidades sem Fins Lucrativos (ex: Fundação, Associação)|
|4XXX|Pessoas Físicas|
|5XXX|Organismos Internacionais e Outras Instituições Extraterritoriais|

- `COMPLEX` (Complexidade): Classifica o procedimento principal da internação como de Média ou Alta Complexidade, um critério central para o planejamento e financiamento da atenção à saúde.
    
- `FINANC` (Financiamento): Distingue a fonte dos recursos financeiros. Os valores podem vir do teto regular de Média e Alta Complexidade (MAC) ou de fontes específicas do Fundo de Ações Estratégicas e Compensação (FAEC).
    
- `FAEC_TP` (Tipo de FAEC): Quando o financiamento é via FAEC, este campo detalha o programa ou política específica que está custeando a internação. Isso permite a avaliação de políticas de saúde direcionadas, como as de transplantes, cardiologia de alta complexidade, oncologia ou cirurgias eletivas.
    

## Parte III: Perfil Demográfico e Socioeconômico do Paciente

Esta seção agrupa as variáveis que descrevem o indivíduo que recebeu o cuidado hospitalar. A análise conjunta destes campos permite traçar o perfil epidemiológico dos pacientes, estudar a distribuição de doenças por diferentes estratos populacionais e investigar possíveis iniquidades no acesso e na utilização dos serviços de saúde.

### Dados Demográficos

- `NASC` (Data de Nascimento): Registrada no formato `AAAAMMDD` (ano, mês, dia).6
    
- `IDADE` e `COD_IDADE` (Idade): `IDADE` representa a idade do paciente em anos completos. No entanto, para análises pediátricas, este campo é insuficiente. A variável `COD_IDADE` é crucial, pois especifica a unidade de tempo da idade registrada: `4` para anos, `3` para meses, `2` para dias e `1` para horas. Isso permite uma análise precisa da idade de recém-nascidos e lactentes, que seriam todos agrupados como "0 anos" se apenas o campo `IDADE` fosse utilizado.
    
- `SEXO`: Sexo biológico do paciente. É codificado numericamente, sendo `1` para Masculino e `3` para Feminino.6
    
- `RACA_COR` (Raça/Cor): Este campo é baseado na autodeclaração do paciente e segue a classificação de cinco categorias do Instituto Brasileiro de Geografia e Estatística (IBGE).17 A qualidade e a obrigatoriedade do preenchimento deste campo têm melhorado ao longo do tempo, impulsionadas por políticas de saúde que visam à equidade racial. É uma variável indispensável para estudos sobre desigualdades em saúde.
    

|Código|Descrição (Raça/Cor - Padrão IBGE)|
|---|---|
|1|Branca|
|2|Preta|
|3|Parda|
|4|Amarela|
|5|Indígena|
|99|Ignorado/Sem informação (pode variar)|

- `ETNIA`: Campo destinado a registrar o código da etnia específica do paciente, quando `RACA_COR` é declarada como indígena. Seu preenchimento é menos consistente e depende da disponibilidade de tabelas auxiliares de povos indígenas no sistema local.
    
- `NACIONAL` (Nacionalidade): Código que indica a nacionalidade do paciente, permitindo diferenciar brasileiros de estrangeiros.6
    

### Localização do Paciente

- `MUNIC_RES` (Município de Residência): Código IBGE de 6 dígitos do município onde o paciente reside.6 Esta é uma das variáveis mais poderosas do SIH. Ao cruzar
    
    `MUNIC_RES` com `MUNIC_MOV` (município do hospital), é possível construir matrizes de fluxo de pacientes, identificando a dependência de um município em relação a outro para cuidados hospitalares, o que é conhecido como "evasão" ou "referência" de pacientes. Essas análises são fundamentais para o planejamento regional da saúde e para identificar "vazios assistenciais". A decodificação deste campo requer a tabela de municípios do IBGE.19
    
- `CEP`: Código de Endereçamento Postal da residência do paciente, permitindo análises geográficas com maior granularidade, embora seu preenchimento possa ser irregular.6
    

### Dados Socioeconômicos e Ocupacionais

- `INSTRU` (Instrução): Grau de instrução do paciente, oferecendo uma medida do nível educacional.6
    
- `VINCPREV` (Vínculo com a Previdência): Este campo funciona como um proxy para o status socioeconômico e a inserção do paciente no mercado de trabalho formal.6
    

|Código|Descrição (Vínculo com a Previdência)|
|---|---|
|1|Autônomo|
|2|Desempregado|
|3|Aposentado|
|4|Não Segurado|
|5|Empregado|
|6|Empregador|

- `CBOR` (Código Brasileiro de Ocupação Reduzido) e `CNAER` (Código Nacional de Atividade Econômica Reduzido): Estes campos são preenchidos especificamente em casos de acidentes de trabalho ou doenças ocupacionais. Eles criam uma ponte vital entre os dados de saúde hospitalar e os sistemas de informação de saúde do trabalhador, permitindo análises sobre os riscos ocupacionais e o perfil dos acidentes.6
    

### Dados Obstétricos e de Planejamento Familiar

- `NUM_FILHOS`, `CONTRACEP1`, `CONTRACEP2`: Conjunto de campos utilizados em AIHs de procedimentos de planejamento familiar, como laqueadura e vasectomia. A legislação brasileira exige a comprovação de histórico reprodutivo e o aconselhamento sobre métodos contraceptivos prévios para autorizar a esterilização cirúrgica. Estes campos registram essa informação: `NUM_FILHOS` indica o número de filhos vivos, e `CONTRACEP1` e `CONTRACEP2` registram os dois principais métodos contraceptivos utilizados anteriormente pela paciente.6
    
- `GESTRISCO` (Gestante de Risco): Indicador binário (`0` para Não, `1` para Sim) que sinaliza se a internação obstétrica é de uma gestante classificada como de alto risco.6
    
- `INSC_PN` (Inscrição no Pré-Natal): Número de inscrição da gestante no programa de pré-natal. Este campo visa rastrear a continuidade do cuidado, vinculando a internação para o parto ao acompanhamento pré-natal recebido na atenção primária.6
    

## Parte IV: Detalhes Clínicos e Assistenciais da Internação

Esta seção aborda o núcleo clínico do conjunto de dados, descrevendo as variáveis que informam o motivo da internação, os diagnósticos estabelecidos, os procedimentos terapêuticos e diagnósticos realizados, o uso de cuidados intensivos e o desfecho final do paciente.

### Admissão, Permanência e Alta

- `DT_INTER` (Data de Internação) e `DT_SAIDA` (Data de Saída): Registram o início e o fim do período de internação no formato `AAAAMMDD`. São as variáveis fundamentais para calcular o tempo de permanência e para análises temporais de eventos de saúde.6
    
- `DIAS_PERM` (Dias de Permanência): Campo calculado que informa o número total de dias que o paciente permaneceu internado.
    
- `CAR_INT` (Caráter da Internação): Classifica a natureza da admissão, sendo crucial para diferenciar atendimentos programados de situações de emergência.
    

|Código|Descrição (Caráter da Internação)|
|---|---|
|01|Eletivo|
|02|Urgência|
|03|Acidente no local de trabalho ou a serviço da empresa|
|04|Acidente de trânsito|
|05|Outros tipos de acidente|
|06|Outros tipos de lesões e envenenamentos por agentes químicos ou físicos|

- `COBRANCA` (Motivo de Saída/Cobrança): Informa o desfecho da internação. Esta variável é essencial para o cálculo de indicadores de resultado, como taxas de mortalidade hospitalar, taxas de transferência e evasão.
    

|Código|Descrição (Motivo de Saída/Cobrança)|
|---|---|
|1X|Alta (ex: 11-Alta curado, 14-Alta melhorado)|
|2X|Permanência (ex: 22-Permanência por mudança de procedimento)|
|3X|Transferência (ex: 31-Transferência para outro estabelecimento)|
|4X|Óbito (ex: 41-Óbito com declaração de óbito fornecida pelo médico assistente)|
|5X|Continuidade do tratamento (ex: 51-Encerramento administrativo)|

- `MORTE`: Campo binário (`0` ou `1`) que simplifica a identificação de óbitos, servindo como uma rápida verificação para o campo `COBRANCA`.
    

### Diagnósticos (Padrão CID-10)

Todos os campos de diagnóstico no SIH/SUS utilizam a Classificação Estatística Internacional de Doenças e Problemas Relacionados com a Saúde, 10ª Revisão (CID-10).21 A versão da CID-10 pode variar com a competência do dado, o que deve ser considerado ao mapear códigos em análises de longo prazo.

- `DIAG_PRINC` (Diagnóstico Principal): É o código da CID-10 que representa a condição que, ao final da investigação, foi identificada como a principal responsável pela necessidade de tratamento hospitalar.
    
- `DIAG_SECUN` (Diagnóstico Secundário): Campo legado, presente em dados mais antigos, que permitia o registro de apenas um diagnóstico secundário.
    
- `DIAGSEC1` a `DIAGSEC9`: Representam uma expansão significativa na capacidade do sistema, permitindo o registro de até nove diagnósticos secundários. Esta mudança aumentou imensamente a riqueza clínica dos dados, possibilitando análises mais sofisticadas de comorbidades e complicações.
    
- `TPDISEC1` a `TPDISEC9`: Campos que tipificam cada diagnóstico secundário, informando se era uma condição pré-existente, uma complicação adquirida durante a internação, etc.
    
- `CID_ASSO` (CID Associada), `CID_MORTE` (CID da Causa Básica do Óbito), `CID_NOTIF` (CID de Notificação Compulsória): Campos específicos para registrar causas associadas, a causa básica do óbito (quando aplicável) e diagnósticos que requerem notificação compulsória às autoridades de vigilância epidemiológica.
    

A transição de um único campo `DIAG_SECUN` para a estrutura de nove diagnósticos secundários (`DIAGSEC1-9`) com tipificação representa um desafio metodológico. Um estudo que compare a prevalência de comorbidades entre períodos antes e depois dessa mudança encontrará um aumento "artificial" nos anos mais recentes, simplesmente porque o sistema passou a ser capaz de registrar mais informações. Este fenômeno, conhecido como "viés de vigilância" ou "efeito de informação", deve ser tratado com rigor. Análises longitudinais de comorbidades devem ou normalizar os dados (ex: usando apenas o primeiro diagnóstico secundário em todos os anos) ou reconhecer explicitamente a quebra na série histórica.

### Procedimentos (Padrão SIGTAP)

Os procedimentos são codificados segundo a Tabela de Procedimentos, Medicamentos, Órteses e Próteses e Materiais Especiais do SUS (SIGTAP), que unificou as tabelas de remuneração a partir de 2008.2

- `PROC_SOLIC` (Procedimento Solicitado): Código do procedimento principal que foi solicitado e autorizado no início da internação.
    
- `PROC_REA` (Procedimento Realizado): Código do procedimento principal que foi efetivamente realizado e está sendo cobrado.
    
- `NUM_PROC`: Campo que também armazena o código do procedimento realizado, provavelmente redundante com `PROC_REA` em muitos casos.
    

A existência de campos distintos para o procedimento solicitado e o realizado não é uma redundância, mas uma poderosa ferramenta de análise. A divergência entre `PROC_SOLIC` e `PROC_REA` pode indicar diversas situações: a evolução do quadro clínico do paciente que exigiu uma mudança de terapia, a ocorrência de complicações, a qualidade do diagnóstico inicial ou, em casos a serem auditados, possíveis tentativas de otimização de faturamento.

### Cuidado em Terapia Intensiva (UTI/UCI)

- `UTI_MES_IN`, `UTI_MES_AN`, `UTI_MES_AL`, `UTI_MES_TO`: Campos que registram o número de diárias de Unidade de Terapia Intensiva (UTI) utilizadas, respectivamente, no mês da internação, no mês anterior à alta, no mês da alta e o total de diárias. Esta estrutura segmentada por mês é um reflexo direto do sistema de faturamento mensal.6
    
- `MARCA_UTI`: Indica o tipo ou nível da UTI utilizada (ex: UTI Adulto Tipo II, UTI Neonatal Tipo III).
    
- `UTI_INT_IN`, `UTI_INT_AN`, `UTI_INT_AL`, `UTI_INT_TO`: Campos análogos aos de UTI, mas para diárias em Unidade de Cuidados Intermediários (UCI).
    
- `MARCA_UCI`: Indica o tipo de UCI utilizada.
    

### Outros Indicadores Assistenciais

- `DIAR_ACOM` e `QT_DIARIAS`: Respectivamente, o número de diárias de acompanhante autorizadas (para crianças, idosos e outros casos previstos em lei) e a quantidade total de diárias da internação.
    
- `IND_VDRL`: Resultado do exame VDRL para detecção de sífilis. Seu preenchimento é obrigatório em AIHs de parto, como parte da política de controle da sífilis congênita.
    
- `INFEHOSP`: Indicador binário (`0` para Não, `1` para Sim) que registra a ocorrência de uma infecção adquirida durante a internação hospitalar.6
    

## Parte V: A Anatomia Financeira da AIH

Esta seção disseca os múltiplos componentes de valor que formam o custo total de uma internação. Compreender estas variáveis é essencial para análises de custo, estudos de eficiência e para entender o SIH em sua função primária como um sistema de faturamento. Os valores são expressos em Reais (R$).

### Componentes de Valor Principais

O valor total de uma AIH é decomposto em diferentes serviços, cada um com seu próprio campo de valor:

- `VAL_SH`: Valor dos Serviços Hospitalares. Engloba os custos de hotelaria, materiais de consumo, medicamentos de uso comum, taxas de sala, etc.
    
- `VAL_SP`: Valor dos Serviços Profissionais. Refere-se aos honorários da equipe de saúde (médicos, enfermeiros, etc.) pelo trabalho realizado.
    
- `VAL_SADT`: Valor dos Serviços de Apoio Diagnóstico e Terapêutico. Cobre os custos de exames laboratoriais, de imagem (raio-x, tomografia), fisioterapia, entre outros.
    
- `VAL_RN`: Valor da assistência ao recém-nascido (em partos).
    
- `VAL_ACOMP`: Valor referente às diárias de acompanhante.
    
- `VAL_ORTP`: Valor de Órteses, Próteses e Materiais Especiais (OPM).
    
- `VAL_SANGUE`: Valor de hemoterapia (bolsas de sangue e hemoderivados).
    
- `VAL_UTI` e `VAL_UCI`: Valor total das diárias em Unidade de Terapia Intensiva e Unidade de Cuidados Intermediários.
    
- `VAL_SADTSR`, `VAL_TRANSP`, `VAL_OBSANG`, `VAL_PED1AC`: Outros componentes de valor para serviços terceirizados, transporte de pacientes, observação em banco de sangue, etc.
    

### Valores Consolidados e Fontes de Repasse

- `VAL_TOT`: Valor Total da AIH. É a soma de todos os componentes de valor aplicáveis para aquela internação.
    
- `US_TOT`: Custo total expresso em "Unidade de Serviço", uma métrica interna do SUS utilizada historicamente para valoração.
    
- `VAL_SH_FED` e `VAL_SP_FED`: Indicam a parcela do `VAL_SH` e `VAL_SP` que é coberta por repasse do governo Federal.
    
- `VAL_SH_GES` e `VAL_SP_GES`: Indicam a parcela do `VAL_SH` e `VAL_SP` que é coberta pelo gestor local (estadual ou municipal).
    

A existência desses campos de valor desagregados por fonte de repasse (`_FED` e `_GES`) é um reflexo direto do pacto federativo e do financiamento tripartite do SUS. O valor de um procedimento é fixado nacionalmente pela tabela SIGTAP, mas a responsabilidade pelo seu pagamento pode ser compartilhada entre a União, os Estados e os Municípios. Um analista interessado no custo total do cuidado deve utilizar os campos de valor consolidados (ex: `VAL_SH`, `VAL_SP`, `VAL_TOT`). Já um analista de políticas de financiamento deve utilizar os campos desagregados para estudar a distribuição do ônus financeiro entre as esferas de governo, a dependência de repasses federais ou o esforço financeiro dos gestores locais.

### Campos de Controle Financeiro

- `RUBRICA`: Código numérico que identifica a dotação orçamentária de onde o recurso financeiro será debitado para pagar a AIH. É um campo de controle contábil.
    
- `TOT_PT_SP`: Total de pontos dos serviços profissionais, uma métrica usada para calcular o `VAL_SP`.
    

## Parte VI: Campos de Controle, Auditoria e Administrativos

Esta seção final descreve as variáveis remanescentes, que desempenham funções de controle interno do sistema, suporte à auditoria e registros administrativos complementares que não se encaixam nas categorias temáticas anteriores.

### Auditoria e Autorização

- `CPF_AUT` (CPF do Autorizador): Número do CPF do profissional que autorizou a internação. É um campo chave para a rastreabilidade e a responsabilização no processo de autorização.6
    
- `HOMONIMO`: Marca utilizada para sinalizar casos de pacientes com nomes idênticos. Este marcador ajuda a evitar erros de identificação e faturamento duplicado, sendo um mecanismo de segurança de dados.
    
- `AUD_JUST` (Justificativa da Auditoria) e `SIS_JUST` (Justificativa do Sistema): Campos de texto livre destinados a registrar observações ou justificativas inseridas por auditores ou geradas automaticamente pelo sistema durante o processamento da AIH.
    

### Campos Administrativos Diversos

Diversas variáveis já detalhadas em outras seções também cumprem funções administrativas e de controle importantes. Por exemplo:

- Os campos relacionados ao planejamento familiar (`NUM_FILHOS`, `CONTRACEP1`, `CONTRACEP2`) e à gestação (`GESTRISCO`, `INSC_PN`) não apenas caracterizam o paciente, mas também servem para verificar a conformidade com as portarias ministeriais.
    
- Os campos de saúde do trabalhador (`CBOR`, `CNAER`) e de vínculo previdenciário (`VINCPREV`) são utilizados para o monitoramento de políticas intersetoriais.
    
- Os campos `ESPEC` (Especialidade do leito), `NATUREZA` (legado) e `REGCT` (Regime de Contratação) também se enquadram nesta categoria de controle administrativo.
    

## Conclusão: Potencialidades e Limitações do SIH/SUS para Pesquisa

O Sistema de Informações Hospitalares do SUS é uma fonte de dados de extraordinária riqueza e complexidade. Sua cobertura quase universal das internações financiadas publicamente no Brasil, o volume massivo de registros e a profundidade dos detalhes demográficos, clínicos e financeiros oferecem um potencial analítico imenso. Com o SIH, é possível realizar estudos de custo-efetividade, mapear o fluxo de pacientes entre regiões, monitorar a epidemiologia de doenças, avaliar o impacto de políticas públicas e investigar iniquidades no acesso e nos resultados em saúde.

No entanto, a utilização robusta e confiável destes dados exige que o pesquisador esteja ciente de suas características e limitações intrínsecas. Este guia buscou não apenas definir as variáveis, mas também destacar os cuidados metodológicos essenciais para uma análise criteriosa:

1. **O Viés de Faturamento:** A finalidade primária do SIH é financeira. Esta característica pode influenciar a forma como diagnósticos e procedimentos são registrados, um fenômeno conhecido como "otimização de faturamento". O analista deve sempre considerar que o dado reflete uma realidade administrativa tanto quanto uma realidade clínica.
    
2. **A Necessidade de Análise Longitudinal Cautelosa:** O SIH é um sistema vivo, que evolui com o tempo. Como demonstrado pela transição de `NATUREZA` para `NAT_JUR` e pela expansão dos campos de diagnóstico, comparações ao longo de grandes períodos históricos exigem um trabalho prévio de harmonização de variáveis para garantir a consistência e evitar conclusões espúrias.
    
3. **O Viés de Seleção:** O banco de dados representa as internações que foram _aprovadas e faturadas com sucesso_.2 Ele não captura, por exemplo, solicitações de AIH que foram negadas ou internações que, por algum motivo, não foram processadas.
    
4. **A Dependência de Tabelas Externas:** A interpretação correta dos dados do SIH é impossível sem o uso das versões corretas das tabelas auxiliares para a competência em análise. Tabelas de CID-10, SIGTAP e códigos de municípios do IBGE são insumos indispensáveis para decodificar e contextualizar as informações.
    
5. **A Riqueza e a Complexidade como Faca de Dois Gumes:** A crescente capacidade do sistema de capturar mais detalhes, como múltiplos diagnósticos secundários, aumenta o poder analítico, mas também introduz desafios metodológicos, como o viés de vigilância, que devem ser explicitamente abordados no desenho do estudo.
    

Em suma, o SIH/SUS é um recurso insubstituível para a compreensão da saúde no Brasil. Quando utilizado com o rigor metodológico e o conhecimento de suas nuances que este guia se propôs a fornecer, ele se revela uma ferramenta poderosa para a geração de conhecimento capaz de subsidiar a tomada de decisão e contribuir para o aprimoramento do Sistema Único de Saúde.

## Anexos: Tabelas de Códigos de Referência Rápida

Esta seção consolida as tabelas de códigos mais utilizadas para facilitar a consulta durante a análise de dados.

### Tabela A: Raça/Cor (RACA_COR - Padrão IBGE)

|Código|Descrição|
|---|---|
|1|Branca|
|2|Preta|
|3|Parda|
|4|Amarela|
|5|Indígena|
|99|Ignorado / Sem Informação|
|Fonte: Padrão IBGE 17|||

### Tabela B: Caráter da Internação (CAR_INT)

|Código|Descrição|
|---|---|
|01|Eletivo|
|02|Urgência|
|03|Acidente no local de trabalho ou a serviço da empresa|
|04|Acidente de trânsito|
|05|Outros tipos de acidente|
|06|Outros tipos de lesões e envenenamentos|
|Fonte: Manuais Técnicos do SIH/SUS 6|||

### Tabela C: Motivo da Saída/Cobrança (COBRANCA)

|Código|Descrição (Exemplos)|
|---|---|
|11|Alta curado|
|14|Alta melhorado|
|31|Transferência para outro estabelecimento|
|41|Óbito com declaração de óbito fornecida pelo médico assistente|
|42|Óbito com declaração de óbito fornecida pelo IML|
|51|Encerramento administrativo|
|_Fonte: Manuais Técnicos do SIH/SUS_||

### Tabela D: Natureza Jurídica (NAT_JUR)

|Código (Grupo)|Descrição|
|---|---|
|1XXX|Administração Pública|
|2XXX|Entidades Empresariais|
|3XXX|Entidades sem Fins Lucrativos|
|4XXX|Pessoas Físicas|
|5XXX|Organismos Internacionais e Outras Instituições Extraterritoriais|
|Fonte: Padrão CONCLA/IBGE, adotado pelo DATASUS 12|||

### Tabela E: Sexo (SEXO)

|Código|Descrição|
|---|---|
|1|Masculino|
|3|Feminino|
|Fonte: Manuais Técnicos do SIH/SUS 6|||

### Tabela F: Unidade de Idade (COD_IDADE)

| Código                               | Descrição |
| ------------------------------------ | --------- |
| 1                                    | Horas     |
| 2                                    | Dias      |
| 3                                    | Meses     |
| 4                                    | Anos      |
| _Fonte: Manuais Técnicos do SIH/SUS_ |           |
# Dicionário Analítico de Variáveis do Sistema de Informação sobre Mortalidade (SIM) - Um Guia Técnico para Pesquisadores e Analistas

## Introdução: A Arquitetura da Informação sobre Mortalidade no Brasil

### O SIM como Pilar da Vigilância em Saúde

O Sistema de Informação sobre Mortalidade (SIM) representa a fundação sobre a qual se assenta a vigilância epidemiológica e a análise da situação de saúde no Brasil. Desenvolvido pelo Ministério da Saúde em 1975, o sistema emergiu da necessidade de unificar e padronizar a coleta de dados sobre mortalidade, que até então era fragmentada em mais de quarenta modelos de instrumentos distintos.1 Sua informatização, iniciada em 1979, e a subsequente descentralização de sua operação para estados e municípios com a implantação do Sistema Único de Saúde (SUS), consolidaram o SIM como a fonte primária e oficial para todas as estatísticas de mortalidade no país.1

Os objetivos do SIM são abrangentes e fundamentais para a gestão da saúde pública. As informações coletadas permitem a construção de indicadores de saúde essenciais, como taxas de mortalidade geral, infantil e materna, e a análise de perfis de mortalidade por causas, estratificados por características demográficas e socioeconômicas.3 Esses dados são indispensáveis para o planejamento de ações, a alocação de recursos, a avaliação de programas e políticas de saúde e a pesquisa acadêmica, fornecendo um panorama detalhado e contínuo da saúde da população brasileira.5 A gestão do sistema em nível federal é de responsabilidade da Secretaria de Vigilância em Saúde e Ambiente (SVSA), por meio do Departamento de Análise Epidemiológica e Vigilância de Doenças Não Transmissíveis (DAENT) e da Coordenação-Geral de Informações e Análises Epidemiológicas (CGIAE).7

### A Declaração de Óbito (DO) como Documento Fonte

A integridade e a utilidade do SIM dependem inteiramente de seu documento-base: a Declaração de Óbito (DO). Este formulário, padronizado em todo o território nacional, é o instrumento legal e epidemiológico que alimenta o sistema.9 A emissão da DO é um ato médico, com responsabilidade ética e jurídica, e possui uma dupla finalidade crítica. Do ponto de vista jurídico, a DO é o documento hábil que permite aos Cartórios de Registro Civil lavrarem a Certidão de Óbito, indispensável para os trâmites legais do sepultamento e para processos sucessórios.10 Do ponto de vista da saúde pública, a DO é a fonte primária de dados para o SIM, contendo as informações que, uma vez processadas, se transformarão nas estatísticas vitais do país.11

A estrutura da DO, organizada em blocos de informação que cobrem desde a identificação do falecido até as causas da morte, é o esqueleto que define a estrutura da base de dados do SIM.13 Portanto, a compreensão aprofundada das variáveis do SIM exige, como pré-requisito, a familiaridade com o formulário da DO e com o manual de instruções para seu preenchimento, que orienta os médicos sobre como registrar as informações de forma precisa e padronizada.12

### O Fluxo da Informação: Da Ocorrência ao Banco de Dados Nacional

O percurso da informação desde o preenchimento da DO até sua consolidação na base de dados nacional é um processo multinível e complexo. As DOs são preenchidas nas unidades notificantes (hospitais, Institutos Médico-Legais, Serviços de Verificação de Óbito, etc.) e recolhidas regularmente pelas Secretarias Municipais de Saúde (SMS).8 Na SMS, os dados da DO são digitados, processados, criticados e consolidados no sistema SIM local. Posteriormente, esses dados municipais são transferidos, geralmente via web, para a base de dados do nível estadual, que os agrega e os envia ao nível federal.6

No nível federal, a CGIAE/DAENT/SVSA é responsável por consolidar os dados de todos os estados, constituindo a base de dados nacional de mortalidade. Essa base é então disponibilizada para acesso público através de plataformas como o TABNET e para download como microdados, permitindo que gestores, pesquisadores e a sociedade civil realizem suas próprias análises.3

### O Dataset como um Registro de um Processo

É fundamental compreender que as 87 colunas do dataset do SIM não representam apenas um retrato estático das características de um óbito. Elas constituem o registro de um complexo processo administrativo, de vigilância e de qualificação da informação. Variáveis como `DTCADASTRO` (data de cadastro), `DTRECEBIM` (data de recebimento), `STCODIFICA` (status da codificação) e todo o bloco de variáveis de investigação são, na verdade, metadados que descrevem a jornada da informação através do sistema de saúde.

A existência de um fluxo de dados em múltiplos níveis, como descrito na documentação oficial 8, implica que há um tempo entre a ocorrência do evento (

`DTOBITO`) e seu registro no sistema (`DTCADASTRO`). A diferença entre essas duas datas, capturada na variável `DIFDATA`, não é apenas um detalhe técnico; é um indicador de desempenho da oportunidade e da eficiência da vigilância epidemiológica local. Atrasos significativos podem comprometer a capacidade do sistema de saúde de detectar e responder a surtos, eventos de saúde pública inusitados ou mudanças abruptas nos padrões de mortalidade. Portanto, o analista de dados deve abordar o dataset do SIM com a percepção de que a "qualidade" do dado não se resume à precisão do preenchimento médico na DO, mas também engloba a eficiência do sistema de informação que coleta, transmite, processa e qualifica essa informação. Essa perspectiva tem implicações diretas na comparabilidade dos dados entre diferentes municípios, estados e períodos de tempo.

## Parte I: Identificação do Evento e Caracterização Sociodemográfica do Falecido

Este primeiro grande bloco de variáveis constitui a identidade fundamental de cada registro de óbito. Ele estabelece o "quem", o "quando" e o "onde" (em termos de origem e residência) do falecido, fornecendo o perfil social e demográfico essencial para qualquer análise estratificada. A correta interpretação destas variáveis é o alicerce para a construção de conhecimento epidemiológico robusto.

### 1.1. Identificação do Registro e do Tipo de Óbito

- **`ORIGEM`**: Esta é uma variável de sistema, não presente na DO física, que descreve a fonte original do registro de dados antes de sua consolidação na base nacional. Ela revela a heterogeneidade dos sistemas estaduais que alimentam o SIM federal.
    
    - **Descrição**: Fonte do sistema de informação.
        
    - **Valores Possíveis**: `1` (Sistema Oracle, padrão do MS), `2` (Banco estadual disponibilizado via FTP), `3` (Banco da Fundação SEADE - Sistema Estadual de Análise de Dados de São Paulo), `9` (Ignorado).15
        
    - **Implicações Analíticas**: A existência desta variável demonstra que o SIM nacional é, na prática, uma federação de sistemas. A Fundação SEADE, por exemplo, é reconhecida por seu rigoroso tratamento e crítica dos dados demográficos e de saúde no estado de São Paulo. Um pesquisador pode utilizar a variável `ORIGEM` para investigar potenciais vieses sistêmicos ou diferenças na qualidade da informação. Por exemplo, pode-se comparar a completude de variáveis como `OCUP` ou `ESC2010` entre registros de `ORIGEM = '3'` e os demais, para avaliar se o processo de qualificação de dados em São Paulo resulta em uma base local mais robusta antes do envio ao nível federal.
        
- **`TIPOBITO`**: Esta é uma variável de distinção crucial, que segmenta a base de dados em dois universos analíticos completamente distintos: os óbitos fetais e os óbitos não-fetais (de nascidos vivos).
    
    - **Descrição**: Tipo do óbito.
        
    - **Valores Possíveis**: `1` (Óbito Fetal), `2` (Óbito Não-Fetal).16
        
    - **Implicações Analíticas**: Esta variável deve ser o primeiro filtro em quase todas as análises. O estudo da mortalidade fetal possui um conjunto de variáveis, indicadores e fatores de risco específicos (relacionados à gestação, ao parto, à saúde materna, etc.), que não se aplicam aos óbitos não-fetais. Misturar os dois tipos de óbito em uma análise geral levaria a conclusões espúrias e epidemiologicamente incorretas.
        

### 1.2. Data e Hora do Óbito

- **`DTOBITO`**: Registra a data em que o óbito ocorreu.
    
    - **Descrição**: Data do óbito.
        
    - **Formato**: Texto no formato `DDMMAAAA` (dia, mês, ano).16
        
    - **Implicações Analíticas**: Variável essencial para análises de tendências temporais (anuais, mensais), estudos de sazonalidade de doenças (e.g., picos de mortalidade por doenças respiratórias no inverno), e para o cálculo de taxas de mortalidade, que requerem a contagem de eventos em um período de tempo definido.
        
- **`HORAOBITO`**: Registra o horário em que o óbito ocorreu.
    
    - **Descrição**: Horário do óbito.
        
    - **Formato**: Texto, geralmente no formato `HHMM` (hora, minuto).16
        
    - **Implicações Analíticas**: Esta variável frequentemente sofre de subnotificação ou preenchimento impreciso. Contudo, quando bem preenchida, é valiosa para estudos específicos, como a análise da mortalidade em serviços de emergência (para identificar horários de pico), a avaliação de desfechos de procedimentos cirúrgicos em relação ao tempo pós-operatório, ou em investigações de mortes por causas externas.
        

### 1.3. Demografia e Origem Geográfica

- **`DTNASC`**: Data de nascimento do falecido.
    
    - **Descrição**: Data de nascimento do falecido.
        
    - **Formato**: Texto no formato `DDMMAAAA`.16
        
    - **Implicações Analíticas**: Utilizada em conjunto com `DTOBITO` para o cálculo preciso da idade, especialmente em crianças menores de um ano. É mais confiável do que a idade declarada, pois permite um cálculo exato em dias, meses e anos.
        
- **`IDADE`**: Idade do falecido, codificada de forma complexa para permitir alta granularidade em idades precoces, o que é vital para a epidemiologia.
    
    - **Descrição**: Idade do falecido, composta por um código de 4 dígitos no formato `TUUA`, onde `T` representa a unidade de tempo e `UUA` a quantidade de unidades.
        
    - **Estrutura e Decodificação**: A lógica desta variável foi projetada especificamente para o cálculo preciso dos componentes da mortalidade infantil (neonatal precoce, neonatal tardia, pós-neonatal), que são indicadores extremamente sensíveis da qualidade da saúde materno-infantil e das condições de vida de uma população. Um erro na sua decodificação pode invalidar completamente uma análise de mortalidade infantil. A tabela abaixo detalha sua estrutura.16
        

|Código (Formato TUUA)|Unidade de Tempo (T)|Valor (UUA)|Descrição Completa|Exemplo de Código|Idade Decodificada|
|---|---|---|---|---|---|
|`1UUA`|1: Horas|`001` a `023`|Idade em horas|`103`|3 horas|
|`2UUA`|2: Dias|`001` a `029`|Idade em dias|`205`|5 dias|
|`3UUA`|3: Meses|`001` a `011`|Idade em meses|`302`|2 meses|
|`4UUA`|4: Anos|`000` a `099`|Idade em anos (até 99)|`425`|25 anos|
|`5UUA`|5: Anos (100+)|`000` a `099`|Idade em anos (100 ou mais)|`501`|101 anos|
|`0000`|0: Ignorada|`000`|Idade completamente ignorada|`0000`|Ignorada|
|`4000`|4: Anos|`000`|Menor de 1 ano (idade exata ignorada)|`4000`|Menor de 1 ano|

- **`SEXO`**: Sexo biológico do falecido.
    
    - **Descrição**: Sexo.
        
    - **Valores Possíveis**: `0` (Ignorado), `1` (Masculino), `2` (Feminino).16
        
    - **Implicações Analíticas**: Variável demográfica fundamental para a estratificação de praticamente todas as análises de mortalidade, permitindo a identificação de perfis de risco e padrões de doença distintos entre homens e mulheres.
        
- **`RACACOR`**: Raça/cor do falecido, conforme declarada por um familiar ou informante.
    
    - **Descrição**: Raça/Cor.
        
    - **Valores Possíveis**: `1` (Branca), `2` (Preta), `3` (Amarela), `4` (Parda), `5` (Indígena). O código `9` (Ignorado) pode ser encontrado em versões mais antigas do sistema.16
        
    - **Implicações Analíticas**: Esta variável é um pilar para estudos sobre iniquidades em saúde. O cruzamento de `RACACOR` com `CAUSABAS` e indicadores socioeconômicos permite analisar as disparidades nos perfis de mortalidade entre diferentes grupos raciais, evidenciando o impacto do racismo estrutural na saúde. A qualidade do preenchimento tem melhorado, mas a proporção de dados ignorados ainda pode ser um desafio analítico em certas regiões ou períodos.
        
- **`NATURAL` e `CODMUNNATU`**: Naturalidade do falecido.
    
    - **Descrição**: `NATURAL` indica a nacionalidade ou, para brasileiros, a Unidade da Federação (UF) de naturalidade. `CODMUNNATU` é o código do município de naturalidade, seguindo o padrão do IBGE.16
        
    - **Implicações Analíticas**: Usadas principalmente em estudos demográficos sobre migração e para analisar perfis de saúde de populações migrantes, comparando-os com os da população nativa de uma determinada região.
        

### 1.4. Perfil Socioeconômico

- **`ESTCIV`**: Estado civil do falecido.
    
    - **Descrição**: Estado civil.
        
    - **Valores Possíveis**: `1` (Solteiro), `2` (Casado), `3` (Viúvo), `4` (Separado judicialmente/Divorciado), `5` (União consensual/estável), `9` (Ignorado).16
        
    - **Implicações Analíticas**: Pode ser usado como um proxy para redes de apoio social. Estudos podem investigar se existem diferenças nos padrões de mortalidade (e.g., por suicídio, doenças crônicas) entre diferentes categorias de estado civil.
        
- **`ESC`, `ESC2010`, `SERIESCFAL`, `ESCFALAGR1`**: Conjunto de variáveis que medem a escolaridade do falecido.
    
    - **Descrição**:
        
        - `ESC`: Padrão antigo de escolaridade, em faixas de anos de estudo concluídos (`1`: Nenhuma, `2`: 1-3 anos, `3`: 4-7 anos, `4`: 8-11 anos, `5`: 12 e mais, `9`: Ignorado).16
            
        - `ESC2010`: Padrão novo, implementado por volta de 2010-2011 para se alinhar às categorias do censo do IBGE, oferecendo maior detalhamento (`0`: Sem escolaridade, `1`: Fundamental I, `2`: Fundamental II, `3`: Médio, `4`: Superior incompleto, `5`: Superior completo, `9`: Ignorado).16
            
        - `SERIESCFAL`: Série escolar, para os níveis fundamental e médio. Valores de `1` a `8`.16
            
        - `ESCFALAGR1`: Variável agregada e padronizada da escolaridade, útil para criar categorias consistentes ao longo do tempo.16
            
    - **Implicações Analíticas**: A escolaridade é um dos determinantes sociais da saúde mais importantes. A existência de múltiplas variáveis para o mesmo conceito é um "fóssil" no dataset que reflete a evolução do sistema de informação. Para análises recentes, `ESC2010` é a variável preferencial por sua maior granularidade e comparabilidade com outras fontes de dados. Para estudos longitudinais que abrangem o período de transição entre os formulários, o pesquisador deve criar uma variável harmonizada, compatibilizando as categorias antigas e novas para garantir a consistência da análise temporal.
        
- **`OCUP`**: Ocupação habitual do falecido.
    
    - **Descrição**: Ocupação, codificada segundo a Classificação Brasileira de Ocupações (CBO), geralmente a versão CBO-2002.16
        
    - **Implicações Analíticas**: Uma variável extremamente poderosa, mas de difícil utilização. A taxa de preenchimento "ignorado" ou com códigos genéricos (e.g., "do lar", "aposentado") é alta. No entanto, quando bem preenchida, permite estudos de mortalidade por categoria profissional, identificando riscos ocupacionais específicos e desigualdades no processo de adoecimento e morte relacionados ao trabalho.
        
- **`CODMUNRES`**: Código do município de residência do falecido.
    
    - **Descrição**: Município de residência, conforme códigos do IBGE.16
        
    - **Implicações Analíticas**: Esta é, para a epidemiologia e o planejamento em saúde, uma das variáveis mais importantes do sistema. As taxas e os indicadores de mortalidade devem ser calculados e analisados com base no local de **residência** do falecido, e não no local de ocorrência do óbito. Isso garante que as estatísticas de saúde de um município reflitam as condições de vida e os riscos aos quais sua população está exposta, e não a capacidade de seu sistema hospitalar de atrair pacientes de outras cidades ou a ocorrência de um grande acidente em seu território envolvendo não-residentes.
        

## Parte II: Onde o Óbito Ocorreu - Localização e Estabelecimento

Este bloco de variáveis situa o evento da morte no espaço geográfico e no contexto institucional do sistema de saúde. A análise desses dados é fundamental para a gestão dos serviços, o planejamento da rede de atenção e a compreensão dos fluxos de pacientes no território.

- **`LOCOCOR`**: Descreve o tipo de local onde o óbito ocorreu.
    
    - **Descrição**: Local de ocorrência do óbito.
        
    - **Valores Possíveis**: `1` (Hospital), `2` (Outro estabelecimento de saúde), `3` (Domicílio), `4` (Via Pública), `5` (Outros), `9` (Ignorado).16
        
    - **Implicações Analíticas**: Esta variável funciona como um indicador indireto do acesso e da trajetória do paciente no sistema de saúde. Uma alta proporção de óbitos ocorridos em domicílio (`LOCOCOR = 3`) ou em via pública (`LOCOCOR = 4`) para doenças que deveriam ser tratadas em ambiente hospitalar pode sinalizar barreiras de acesso aos serviços de saúde, falhas no atendimento pré-hospitalar ou a gravidade de certas condições que levam a uma morte súbita. O cruzamento de `LOCOCOR` com a `CAUSABAS` pode revelar padrões importantes, como uma elevada proporção de mortes por infarto agudo do miocárdio ocorrendo no domicílio, sugerindo a necessidade de campanhas de conscientização sobre os sintomas e a importância da busca rápida por atendimento.
        
- **`CODESTAB` e `ESTABDESCR`**: Identificam o estabelecimento de saúde onde o óbito ocorreu.
    
    - **Descrição**: `CODESTAB` é o código numérico do estabelecimento no Cadastro Nacional de Estabelecimentos de Saúde (CNES). `ESTABDESCR` é um campo de texto com o nome do estabelecimento, que pode não estar presente ou padronizado em todas as versões da base de dados.16
        
    - **Implicações Analíticas**: A vinculação do óbito a um estabelecimento de saúde específico através do `CODESTAB` é extremamente valiosa. Permite análises de mortalidade intra-hospitalar, a avaliação de desempenho de serviços específicos (e.g., UTIs, centros cirúrgicos), a investigação de surtos de infecções hospitalares e a comparação de taxas de letalidade para determinadas condições entre diferentes hospitais. Para utilizar esta variável, é necessário cruzar a base do SIM com a base do CNES para obter mais características do estabelecimento (e.g., tipo de gestão, nível de complexidade).
        
- **`CODMUNOCOR`**: Código do município onde o óbito ocorreu.
    
    - **Descrição**: Município de ocorrência do óbito, conforme códigos do IBGE.16
        
    - **Implicações Analíticas - A Diferença Crucial: Residência vs. Ocorrência**: A análise conjunta e comparativa de `CODMUNRES` (município de residência) e `CODMUNOCOR` (município de ocorrência) é uma das análises espaciais mais fundamentais em saúde pública. Quando o código do município de residência é diferente do código do município de ocorrência, isso indica que o falecido buscou ou foi levado para atendimento em outra cidade. Este fenômeno, conhecido como "evasão" ou "migração pendular por motivos de saúde", é comum em regiões onde há concentração de serviços de média e alta complexidade em poucos municípios. Mapear esses fluxos é vital para o planejamento regional de saúde, pois permite identificar:
        
        1. **Municípios dependentes**: Cidades pequenas que não possuem capacidade instalada para tratar casos mais graves e que sistematicamente "exportam" seus pacientes.
            
        2. **Municípios-polo**: Cidades que funcionam como centros de referência regionais, recebendo um grande volume de pacientes de municípios vizinhos e, consequentemente, registrando um número de óbitos de não-residentes muito superior à sua própria população. Ignorar essa distinção levaria a uma superestimação da mortalidade nos municípios-polo e a uma subestimação nos municípios dependentes.
            

## Parte III: A Saúde Materno-Infantil sob a Lente da Mortalidade

Este conjunto especializado de variáveis é de altíssima relevância para a vigilância epidemiológica, pois permite um mergulho profundo nas circunstâncias que cercam os óbitos fetais, infantis e maternos. O preenchimento destes campos é mandatório para óbitos fetais e para óbitos de mulheres em idade fértil (10 a 49 anos), sendo a base para o funcionamento dos Comitês de Prevenção de Óbitos Maternos, Fetais e Infantis.

### 3.1. Caracterização da Mãe (para óbitos fetais/infantis)

- **`IDADEMAE`**: Idade da mãe em anos completos no momento do parto/óbito fetal.
    
    - **Descrição**: Idade da mãe.16
        
    - **Implicações Analíticas**: Fator de risco clássico em saúde materno-infantil. Idades extremas (adolescência e idade avançada) estão associadas a maiores riscos de desfechos desfavoráveis tanto para a mãe quanto para o concepto.
        
- **`ESCMAE`, `ESCMAE2010`, `SERIESCMAE`, `ESCMAEAGR1`**: Conjunto de variáveis sobre a escolaridade da mãe.
    
    - **Descrição**: Escolaridade da mãe, seguindo os mesmos padrões (antigo, novo, série e agregado) da escolaridade do falecido.16
        
    - **Implicações Analíticas**: A escolaridade materna é um dos determinantes sociais mais fortes da saúde infantil. Níveis mais baixos de escolaridade estão consistentemente associados a maiores taxas de mortalidade infantil, refletindo piores condições de vida, menor acesso à informação e barreiras no acesso a serviços de saúde de qualidade.
        
- **`OCUPMAE`**: Ocupação da mãe.
    
    - **Descrição**: Ocupação da mãe, codificada pela CBO.16
        
    - **Implicações Analíticas**: Permite investigar a relação entre a ocupação materna, a exposição a riscos ambientais ou laborais e desfechos gestacionais adversos, como o óbito fetal.
        

### 3.2. Histórico Reprodutivo e Gestacional

- **`QTDFILVIVO`, `QTDFILMORT`**: Número de filhos tidos pela mãe.
    
    - **Descrição**: `QTDFILVIVO` registra o número de filhos nascidos vivos; `QTDFILMORT` registra o número de filhos que nasceram mortos ou morreram após o nascimento (perdas fetais e infantis anteriores).16
        
    - **Implicações Analíticas**: Fornecem o histórico obstétrico da mãe, permitindo a análise de paridade e de histórico de perdas gestacionais como fatores de risco para o óbito atual.
        
- **`GRAVIDEZ`**: Tipo de gestação.
    
    - **Descrição**: Tipo de gravidez.
        
    - **Valores Possíveis**: `1` (Única), `2` (Dupla), `3` (Tripla e mais), `9` (Ignorado).16
        
    - **Implicações Analíticas**: Gestação múltipla é um fator de risco conhecido para prematuridade, baixo peso ao nascer e, consequentemente, maior risco de óbito fetal e neonatal.
        
- **`SEMAGESTAC`, `GESTACAO`**: Duração da gestação.
    
    - **Descrição**: `SEMAGESTAC` é o número bruto de semanas de gestação. `GESTACAO` é a mesma informação agrupada em faixas categóricas (`1`: Menos de 22 semanas, `2`: 22 a 27 semanas, `3`: 28 a 31 semanas, `4`: 32 a 36 semanas, `5`: 37 a 41 semanas, `6`: 42 semanas e mais, `9`: Ignorado).16
        
    - **Implicações Analíticas**: A idade gestacional é um dos principais preditores do desfecho neonatal. A prematuridade (especialmente a prematuridade extrema, <28 semanas) é a principal causa de mortalidade neonatal no Brasil e no mundo.
        
- **`PARTO`**: Tipo de parto.
    
    - **Descrição**: Tipo de parto.
        
    - **Valores Possíveis**: `1` (Vaginal), `2` (Cesáreo), `9` (Ignorado).16
        
    - **Implicações Analíticas**: Permite analisar a associação entre o tipo de parto e a ocorrência de óbito fetal ou materno.
        
- **`PESO`**: Peso do recém-nascido ou feto em gramas.
    
    - **Descrição**: Peso ao nascer, em gramas.16
        
    - **Implicações Analíticas**: O baixo peso ao nascer (definido como <2500g) é outro indicador crítico de risco para a mortalidade infantil. Está fortemente associado à prematuridade e à restrição de crescimento intrauterino.
        

### 3.3. Relação da Morte com o Ciclo Gravídico-Puerperal

- **`OBITOPARTO`**: Momento do óbito em relação ao trabalho de parto (específico para óbitos fetais).
    
    - **Descrição**: Morte em relação ao parto.
        
    - **Valores Possíveis**: `1` (Antes), `2` (Durante), `3` (Depois), `9` (Ignorado).16
        
    - **Implicações Analíticas**: Ajuda a distinguir entre óbitos fetais anteparto (geralmente relacionados a condições maternas ou fetais crônicas) e intraparto (frequentemente associados à qualidade da assistência ao parto).
        
- **`TPMORTEOCO`, `OBITOGRAV`, `OBITOPUERP`**: Conjunto de variáveis para investigar a mortalidade materna.
    
    - **Descrição**:
        
        - `TPMORTEOCO`: Campo preenchido para óbitos de mulheres em idade fértil (10 a 49 anos), para identificar a relação temporal da morte com a gravidez, parto ou puerpério. Valores: `1` (na gravidez), `2` (no parto), `3` (no aborto), `4` (até 42 dias após o parto), `5` (de 43 dias a 1 ano após o parto), `8` (não ocorreu nestes períodos), `9` (ignorado).16
            
        - `OBITOGRAV`: Morte durante a gravidez? `1` (Sim), `2` (Não), `9` (Ignorado).16
            
        - `OBITOPUERP`: Morte durante o puerpério? `1` (Sim, até 42 dias), `2` (Sim, de 43 dias a 1 ano), `3` (Não), `9` (Ignorado).16
            
    - **Implicações Analíticas - A Vigilância Ativa da Morte Materna**: Este bloco de variáveis é a espinha dorsal da vigilância de óbitos maternos. A ocorrência de um óbito em uma mulher em idade fértil, especialmente se a causa básica registrada na DO for uma condição que _poderia_ estar relacionada à gestação (e.g., hemorragia, hipertensão, infecção), e se um desses campos indicar uma relação temporal com o ciclo gravídico-puerperal, aciona um alerta. Esse alerta dispara um processo de investigação aprofundada pelo comitê de mortalidade materna local ou regional. O objetivo da investigação é analisar prontuários, entrevistar familiares e profissionais de saúde para confirmar ou descartar a morte como sendo de causa materna, identificar a causa correta e, crucialmente, apontar as falhas na assistência que contribuíram para o desfecho fatal, visando prevenir futuras mortes.
        

## Parte IV: O Coração do Atestado - A Cadeia Causal da Morte

Esta seção da Declaração de Óbito (Bloco V) e, consequentemente, do banco de dados do SIM, é a mais complexa e a mais importante do ponto de vista epidemiológico. Ela não registra apenas "a" causa da morte, mas sim a sequência lógica de eventos patológicos, conforme o entendimento do médico atestante, que culminaram no óbito. A correta interpretação desta seção é vital para a geração de estatísticas de mortalidade válidas e comparáveis.

### 4.1. A Cascata de Causas

As linhas do atestado de óbito são projetadas para registrar a cadeia de eventos que levaram à morte, em uma ordem cronológica e etiológica inversa.

- **`LINHAA`, `LINHAB`, `LINHAC`, `LINHAD`**: Estes campos de texto armazenam os códigos da Classificação Internacional de Doenças, 10ª Revisão (CID-10), que descrevem a cadeia causal direta.
    
    - **Lógica de Preenchimento**: A `LINHAA` deve conter a **causa imediata ou terminal** da morte, ou seja, a doença ou condição final que levou diretamente ao óbito (e.g., "Insuficiência Respiratória Aguda"). A `LINHAB` deve conter a condição que levou à causa registrada na Linha A (e.g., "Pneumonia Bacteriana"). A `LINHAC` deve conter a condição que levou à Linha B (e.g., "Broncoaspiração"), e a `LINHAD` a que levou à Linha C. A lógica é que a condição em uma linha inferior deve ser a causa da condição na linha imediatamente superior.16
        
- **`LINHAII`**: Este campo é destinado a registrar **outros estados patológicos significativos** ou comorbidades que contribuíram para a morte, mas que não fizeram parte da cadeia causal direta que levou ao desfecho.
    
    - **Lógica de Preenchimento**: Aqui se registram condições crônicas ou agudas que podem ter debilitado o paciente ou complicado o quadro clínico, mas que não são consideradas a causa inicial da sequência de eventos. Por exemplo, em um paciente que morreu de pneumonia (`LINHAA`), o "Diabetes Mellitus" ou a "Hipertensão Arterial Sistêmica" seriam registrados na `LINHAII`.16
        

A tabela abaixo ilustra a lógica de preenchimento do Bloco V da DO com um exemplo prático.

|Campo na DO|Descrição da Função|Exemplo de Preenchimento (Diagnóstico por extenso)|Código CID-10 Correspondente|
|---|---|---|---|
|**Parte I**||||
|**`LINHAA`**|Causa Imediata/Terminal|Septicemia|A41.9|
|**`LINHAB`**|Devido a (Causa Intermediária)|Infecção do Trato Urinário|N39.0|
|**`LINHAC`**|Devido a (Causa Básica)|Hiperplasia Prostática Benigna|N40|
|**`LINHAD`**|Devido a (Causa Intermediária)|_(não preenchido)_||
|**Parte II**||||
|**`LINHAII`**|Outras Causas Contribuintes|Diabetes Mellitus tipo 2; Hipertensão Arterial Sistêmica|E11; I10|

Neste exemplo, a "Septicemia" foi o que matou o paciente diretamente, mas ela foi causada pela "Infecção do Trato Urinário", que por sua vez foi causada pela dificuldade de esvaziamento da bexiga devido à "Hiperplasia Prostática Benigna". O diabetes e a hipertensão contribuíram para a gravidade geral do quadro, mas não iniciaram a cadeia de eventos.

### 4.2. A Causa Básica - O Padrão-Ouro Epidemiológico

- **`CAUSABAS`**: Esta é a variável mais importante para as estatísticas de saúde. A **Causa Básica do Óbito** é definida pela Organização Mundial da Saúde (OMS) como "(a) a doença ou lesão que iniciou a cadeia de acontecimentos patológicos que conduziram diretamente à morte, ou (b) as circunstâncias do acidente ou violência que produziram a lesão fatal". No exemplo da tabela acima, a Causa Básica é a "Hiperplasia Prostática Benigna" (N40).
    
    - **Processo de Seleção**: É crucial entender que o valor da `CAUSABAS` **não é simplesmente uma cópia da última linha preenchida pelo médico na DO**. Após a digitação das informações das linhas A, B, C, D e II, os dados são processados por codificadores treinados nas secretarias de saúde. Eles utilizam um sistema (software ou processo manual) chamado Seletor de Causa Básica (SCB), que aplica um conjunto complexo de regras e algoritmos definidos pela OMS para selecionar uma única causa como sendo a "básica".16 Este processo padronizado garante que as estatísticas de mortalidade sejam comparáveis entre diferentes locais e ao longo do tempo.
        
- **`CB_PRE`**: Causa selecionada antes da aplicação de certas regras de resseleção do SCB. É uma variável mais técnica, usada no processo de codificação.16
    
- **`CAUSABAS_O`**: A causa básica original, como foi digitada inicialmente no sistema, antes de qualquer processo de correção, qualificação ou investigação epidemiológica.16
    
    - **Implicações Analíticas - A Diferença entre Análise Clínica e Epidemiológica**: A estrutura de múltiplas linhas da DO atende à necessidade clínica de descrever a complexa cascata de eventos fisiopatológicos. No entanto, para fins de saúde pública e epidemiologia, é necessária uma única causa, a Causa Básica, para gerar estatísticas agregadas e comparáveis sobre os principais problemas de saúde que afetam a população. Por isso, 99% das análises estatísticas de mortalidade (e.g., "as principais causas de morte no Brasil") devem utilizar a variável `CAUSABAS`. Analisar a `LINHAA` levaria a conclusões equivocadas, superestimando causas terminais e inespecíficas como "parada cardiorrespiratória" ou "falência de múltiplos órgãos", que são modos de morrer, e não causas básicas. A comparação entre a `CAUSABAS_O` (a informação bruta) e a `CAUSABAS` (a informação qualificada) pode servir como um indicador da extensão da correção e qualificação dos dados realizada pelas secretarias de saúde, refletindo a maturidade do sistema de vigilância local.
        

## Parte V: Circunstâncias Adicionais e Investigação Clínica

Este bloco de variáveis adiciona camadas de contexto sobre a assistência médica recebida pelo falecido e sobre as circunstâncias da morte, sendo particularmente importante para a qualificação da informação causal e para a vigilância de óbitos por causas externas.

### 5.1. Assistência e Procedimentos Médicos

Este conjunto de campos ajuda a entender o contexto do cuidado em saúde que precedeu o óbito e pode ser usado para avaliar a robustez da causa da morte declarada.

- **`ASSISTMED`**: Indica se o falecido recebeu assistência médica durante a doença ou condição que levou à morte.
    
    - **Valores Possíveis**: `1` (Sim, com assistência), `2` (Não, sem assistência), `9` (Ignorado).16
        
- **`EXAME`**: Indica se foi realizado algum exame complementar que auxiliou no diagnóstico da causa da morte.
    
    - **Valores Possíveis**: `1` (Sim), `2` (Não), `9` (Ignorado).16
        
- **`CIRURGIA`**: Indica se foi realizada alguma cirurgia que possa ter relação com a causa da morte.
    
    - **Valores Possíveis**: `1` (Sim), `2` (Não), `9` (Ignorado).16
        
- **`NECROPSIA`**: Indica se foi realizada necrópsia (autópsia clínica ou médico-legal).
    
    - **Valores Possíveis**: `1` (Sim), `2` (Não), `9` (Ignorado).16
        
    - **Implicações Analíticas - Qualificando a Causa da Morte**: Este conjunto de variáveis permite uma análise crítica da qualidade da informação sobre a causa do óbito. A realização de uma necrópsia (`NECROPSIA = 1`) geralmente implica uma causa básica de morte com um grau de certeza diagnóstica muito maior. O cruzamento dessas variáveis com a `CAUSABAS` é uma ferramenta poderosa. Por exemplo, uma alta proporção de mortes classificadas com "causas mal definidas" (Capítulo XVIII da CID-10) associada à falta de assistência médica (`ASSISTMED = 2`) e à ocorrência do óbito em domicílio é um padrão esperado em áreas com barreiras de acesso à saúde. No entanto, uma alta proporção de causas mal definidas em óbitos ocorridos em hospitais (`LOCOCOR = 1`), com assistência médica (`ASSISTMED = 1`) e sem necrópsia (`NECROPSIA = 2`), pode indicar problemas na qualidade do diagnóstico, na capacidade de investigação clínica do serviço ou no preenchimento da DO pelo corpo médico.
        

### 5.2. Óbitos por Causas Externas (Violência e Acidentes)

Estas variáveis são de preenchimento obrigatório quando a causa básica do óbito pertence ao Capítulo XX da CID-10 (Causas Externas de Morbidade e Mortalidade).

- **`CIRCOBITO`**: Descreve a circunstância provável da morte por causa externa.
    
    - **Descrição**: Circunstância do óbito.
        
    - **Valores Possíveis**: `1` (Acidente), `2` (Suicídio), `3` (Homicídio), `4` (Outros, e.g., intervenção legal), `9` (Ignorado/Indeterminado).16
        
    - **Implicações Analíticas**: Essencial para a vigilância de violências e acidentes, permitindo a construção de indicadores específicos sobre a carga de mortalidade por agressões, lesões autoprovocadas, acidentes de transporte, etc.
        
- **`ACIDTRAB`**: Indica se o acidente que levou à morte foi relacionado ao trabalho.
    
    - **Descrição**: Acidente de trabalho.
        
    - **Valores Possíveis**: `1` (Sim), `2` (Não), `9` (Ignorado).16
        
    - **Implicações Analíticas**: Fundamental para a área de Saúde do Trabalhador. Permite o monitoramento da mortalidade por acidentes de trabalho, a identificação de setores produtivos e ocupações de maior risco, e o subsídio a políticas de prevenção e fiscalização. A subnotificação desta variável é historicamente um problema, o que torna as estatísticas oficiais muitas vezes subestimadas.
        

## Parte VI: Os Bastidores do Sistema - Controle, Fluxo e Investigação Epidemiológica

Este bloco final de variáveis é o mais técnico do dataset do SIM. São campos gerados não pelo médico atestante, mas pelo próprio sistema de informação ou pelas equipes de vigilância epidemiológica durante o processamento, a codificação e a investigação dos óbitos. Embora frequentemente ignoradas em análises superficiais, estas variáveis são fundamentais para uma avaliação crítica da qualidade, da oportunidade e da maturidade do sistema de informação, permitindo ao pesquisador compreender como os dados foram produzidos.

### 6.1. O Atestado e o Atestante

- **`ATESTANTE`**: Identifica o tipo de profissional ou serviço que assinou a Declaração de Óbito.
    
    - **Descrição**: Médico ou serviço que atestou o óbito.
        
    - **Valores Possíveis**: `1` (Médico assistente), `2` (Médico substituto), `3` (IML - Instituto Médico Legal), `4` (SVO - Serviço de Verificação de Óbito), `5` (Outros).16
        
    - **Implicações Analíticas**: O valor desta variável oferece pistas importantes sobre a natureza do óbito e a origem da informação causal. Um valor `3` (IML) implica, quase que invariavelmente, uma morte por causa externa (acidente, homicídio, suicídio). Um valor `4` (SVO) indica uma morte por causa natural, mas que ocorreu sem assistência médica, cuja causa foi determinada após uma investigação post-mortem simplificada. Um valor `1` (Médico assistente) geralmente sugere um maior conhecimento prévio sobre o caso e, potencialmente, maior precisão na definição da cadeia causal.
        
- **`DTATESTADO`**: Data em que a DO foi preenchida e assinada pelo médico.16
    
- **`ATESTADO`**: Campo de texto que pode conter um ou mais códigos CID-10 conforme escritos no atestado original.16
    

### 6.2. Processamento e Codificação no Sistema

- **`DTCADASTRO`**: Data em que o registro do óbito foi inserido no sistema informatizado da Secretaria Municipal de Saúde.16
    
- **`DTRECEBIM`**: Data em que a via física da DO foi recebida pela secretaria de saúde.16
    
- **`STCODIFICA` e `CODIFICADO`**: Flags de status (`S` para Sim, `N` para Não) que indicam se o registro já passou pelo processo de codificação da causa básica.16
    
- **`VERSAOSIST` e `VERSAOSCB`**: Campos de texto que registram a versão do software do SIM e do Seletor de Causa Básica (SCB) utilizados.16 São importantes para análises históricas, pois mudanças nas regras de seleção da causa básica podem introduzir artefatos nas séries temporais de mortalidade por certas causas.
    
- **`NUMEROLOTE`**: Número do lote de formulários de DO ao qual o documento físico pertence. Útil para controle administrativo e de distribuição dos formulários.16
    
- **`CONTADOR`**: Campo numérico, geralmente com valor `1`, usado como um contador sequencial para cada registro, garantindo a unicidade em algumas operações de banco de dados.
    

### 6.3. O Processo de Investigação do Óbito

- **`TPPOS`**: Indica se o óbito foi submetido a um processo de investigação epidemiológica.
    
    - **Descrição**: Óbito investigado.
        
    - **Valores Possíveis**: `1` (Sim), `2` (Não).15
        
    - **Contexto**: A investigação de óbitos é uma prática recomendada e rotineira da vigilância epidemiológica para grupos específicos, como óbitos infantis, fetais, maternos, de mulheres em idade fértil, e para óbitos cuja causa básica foi classificada como mal definida ou indeterminada.19
        
- **`DTINVESTIG`, `DTCONINV`, `DTCONCASO`**: Datas que marcam as etapas do processo de investigação: data de início, data de conclusão da investigação e data de conclusão do caso.15
    
- **`FONTE`, `FONTEINV`, `FONTES`, `FONTESINF`**: Conjunto de variáveis que indicam as fontes de informação utilizadas durante a investigação para qualificar a causa da morte (e.g., entrevista com familiares, análise de prontuário hospitalar ou ambulatorial, laudo do SVO ou IML).15
    
- **`ALTCAUSA`**: Indica se o processo de investigação resultou em uma alteração da causa básica do óbito originalmente registrada.
    
    - **Descrição**: Houve alteração da causa após investigação.
        
    - **Valores Possíveis**: `1` (Sim), `2` (Não).15
        
    - **Implicações Analíticas - Medindo a Qualidade e o Esforço do Sistema**: Este conjunto de variáveis de investigação é, talvez, o mais rico para um analista de sistemas de saúde. A proporção de óbitos investigados (`TPPOS = 1`), especialmente para os grupos-alvo, e a proporção de causas alteradas após a investigação (`ALTCAUSA = 1`) não devem ser vistas como um sinal de má qualidade da informação original. Pelo contrário, elas são indicadores diretos da **qualidade e da proatividade da vigilância epidemiológica local**. Um município que investiga ativamente seus óbitos e corrige as causas quando necessário demonstra ter um sistema de vigilância atuante e comprometido com a produção de dados de alta fidedignidade. Analistas devem usar essas variáveis para avaliar a confiabilidade dos dados de uma determinada região antes de fazer comparações. Uma baixa proporção de causas mal definidas em um município pode significar duas coisas opostas: ou a qualidade do preenchimento original é excelente, ou a vigilância local é passiva e não investiga esses óbitos para requalificá-los.
        

### 6.4. Variáveis de Controle e Derivadas

- **`DIFDATA`**: Diferença, em dias, entre a data do óbito (`DTOBITO`) e a data de cadastro no sistema (`DTCADASTRO`). Mede a oportunidade (agilidade) do sistema.16
    
- **`NUDIASOBCO`, `NUDIASOBIN`**: Número de dias decorridos entre a data do óbito e a conclusão da investigação.15
    
- **`STDOEPIDEM`, `STDONOVA`**: Flags de sistema que indicam o status do registro (e.g., se é um registro novo, se foi revisado pela vigilância epidemiológica).
    
- **`CAUSAMAT`**: Campo específico para a causa básica de morte materna, preenchido após o processo de investigação do óbito da mulher em idade fértil.
    
- **`MORTEPARTO`, `TPOBITOCOR`**: Campos que registram o momento do óbito em relação ao parto/gestação, preenchidos ou corrigidos após a investigação.15
    
- **`TPRESGINFO`, `TPNIVELINV`**: Indicam o resultado da investigação (`01` - Não alterou, `02` - Resgatou novas informações, `03` - Corrigiu informações) e o nível de gestão que realizou a investigação (`M` - Municipal, `R` - Regional, `E` - Estadual).15
    

A tabela a seguir resume as variáveis-chave que podem ser transformadas em indicadores para avaliar a qualidade do SIM em uma dada localidade.

|Variável / Indicador|O que Mede|Interpretação Analítica|
|---|---|---|
|**`DIFDATA`**|Oportunidade (agilidade) do sistema|Valores médios ou medianos altos indicam atraso na notificação dos óbitos, o que compromete a capacidade de vigilância e resposta em tempo real.|
|**Proporção de `CAUSABAS` mal definida**|Especificidade da informação médica|Altas proporções, especialmente em óbitos hospitalares com assistência médica, sugerem baixa qualidade do preenchimento da DO ou do processo diagnóstico.|
|**Proporção de `TPPOS` = 1**|Atividade da vigilância epidemiológica|Altas taxas de investigação para óbitos-alvo (infantis, maternos, mal definidos) indicam uma vigilância proativa e comprometida com a qualidade do dado.|
|**Proporção de `ALTCAUSA` = 1**|Efetividade da investigação|Altas taxas de alteração da causa após investigação demonstram que o processo de vigilância é eficaz em corrigir e qualificar a informação de mortalidade.|
|**Completude das variáveis**|Qualidade do preenchimento|O percentual de campos ignorados ou não preenchidos (e.g., para `RACACOR`, `ESC2010`, `OCUP`) é um indicador direto da qualidade geral da coleta de dados.|

## Conclusão: Recomendações para a Análise Crítica e Robusta dos Dados do SIM

O Sistema de Informação sobre Mortalidade é uma das mais poderosas e longevas ferramentas de saúde pública do Brasil. A análise de suas 87 variáveis permite desvendar com profundidade os perfis de saúde e doença da população, sendo um recurso insubstituível para a gestão, o planejamento e a pesquisa. O dataset oferece um potencial imenso para estudos sobre tendências temporais, desigualdades sociais e raciais em saúde (através do cruzamento de `CAUSABAS` com `RACACOR` e `ESC2010`), planejamento da rede regional de saúde (analisando os fluxos entre `CODMUNRES` e `CODMUNOCOR`), e para a vigilância específica de agravos prioritários, como a mortalidade materna, infantil e por causas externas.

Contudo, a utilização robusta e crítica desses dados exige a compreensão de suas nuances e limitações. O analista deve estar ciente de que a qualidade e a completude da informação podem variar consideravelmente no tempo e no espaço geográfico, refletindo as desigualdades do próprio país e de seus sistemas de saúde locais. Algumas recomendações são essenciais:

1. **Analisar pela Residência**: Para fins epidemiológicos e de planejamento, os dados devem ser sempre agregados e analisados pelo município de **residência** (`CODMUNRES`), não pelo de ocorrência, para refletir corretamente o perfil de risco da população de um determinado território.
    
2. **Utilizar a Causa Básica**: A variável `CAUSABAS` é o padrão-ouro para análises estatísticas de mortalidade. O uso das causas terminais ou intermediárias (`LINHAA`, `LINHAB`, etc.) para este fim é um erro metodológico que leva a conclusões inválidas.
    
3. **Decodificar Variáveis Complexas com Cuidado**: Variáveis como `IDADE` possuem uma lógica de codificação específica que deve ser corretamente decodificada para evitar erros graves, especialmente em análises de mortalidade infantil.
    
4. **Harmonizar Variáveis Históricas**: Em estudos longitudinais, é preciso estar atento às mudanças nos formulários e nas variáveis ao longo do tempo (e.g., `ESC` vs. `ESC2010`) e criar categorias harmonizadas para garantir a comparabilidade temporal.
    

Finalmente, a recomendação mais importante é que o pesquisador experiente não deve apenas usar os dados do SIM, mas também entender e avaliar o sistema que os produziu. As variáveis de processo, controle e investigação (detalhadas na Parte VI) não devem ser vistas como um problema ou ruído, mas sim como uma ferramenta poderosa para qualificar as próprias análises. Avaliar a oportunidade do sistema (`DIFDATA`), a proporção de causas mal definidas, e a atividade da vigilância epidemiológica (`TPPOS`, `ALTCAUSA`) permite ao analista ponderar a confiabilidade dos dados de uma determinada região, transformando uma simples descrição estatística em uma avaliação epidemiológica robusta, crítica e verdadeiramente informada.

# Guia de um Especialista para o Arquivo de Produção Ambulatorial (PA) do SIA-SUS: Um Dicionário de Dados Abrangente e Estrutura Analítica

## Seção I: Contexto Fundamental: A Arquitetura do Arquivo `PA` do SIA

Esta seção estabelece o conhecimento de base essencial, explicando que o arquivo `PA` não é uma tabela plana simples, mas uma agregação complexa de múltiplos fluxos de dados. A compreensão desta arquitetura é um pré-requisito para qualquer análise válida.

### 1.1. O Papel do Sistema de Informações Ambulatoriais (SIA) no SUS

O Sistema de Informações Ambulatoriais (SIA) representa uma pedra angular do Sistema Único de Saúde (SUS) do Brasil para a gestão da atenção ambulatorial. Implantado em escala nacional na década de 1990, o sistema foi concebido com o objetivo primordial de registrar, processar e financiar os procedimentos realizados fora do ambiente hospitalar.1 Suas funções transcendem o mero registro financeiro, servindo como uma ferramenta estratégica para o Ministério da Saúde e para os gestores estaduais e municipais. As informações geradas pelo SIA são cruciais para subsidiar o planejamento, a programação, a regulação, o controle, a avaliação e a auditoria dos serviços de saúde ambulatoriais em todo o território nacional.1

O fluxo de dados do sistema opera em um ciclo mensal. Os estabelecimentos de saúde, sejam eles públicos ou privados conveniados ao SUS, registram sua produção ambulatorial. Esses dados são então submetidos aos gestores locais (municipais ou estaduais), que utilizam o software do SIA para processar, validar e consolidar as informações. Após essa etapa de validação, as bases de dados consolidadas são enviadas ao Departamento de Informática do SUS (DATASUS), onde compõem a base de dados nacional, que é então disponibilizada para consulta e análise.4 Este processo garante um repositório centralizado de informações sobre a vasta rede de atendimento ambulatorial do país.

### 1.2. Desconstruindo o Arquivo `PA`: Um Mosaico de Instrumentos

O principal produto do processamento do SIA é o arquivo de Produção Ambulatorial, comumente conhecido como arquivo `PA` (identificado nos sistemas do DATASUS como `PAufaamm.DBC` ou `.DBF`, onde 'uf' é a unidade da federação, 'aa' é o ano e 'mm' é o mês).6 Um erro comum na análise desses dados é presumir que cada linha do arquivo representa o mesmo tipo de evento. Na realidade, o arquivo

`PA` é uma consolidação de registros provenientes de instrumentos de coleta fundamentalmente distintos, cada um com sua própria lógica e nível de agregação.1 Compreender a natureza desses instrumentos de origem é o primeiro passo para uma análise correta.

Os principais instrumentos de registro que alimentam o arquivo `PA` são:

- **Boletim de Produção Ambulatorial (BPA):** É a ferramenta primária para registrar procedimentos que não exigem uma autorização prévia do gestor.3 O BPA se manifesta de duas formas:
    
    - **BPA-C (Consolidado):** Registra os procedimentos de forma agregada. Por exemplo, um único registro em um BPA-C pode representar "50 hemogramas completos" realizados em um determinado mês, sem identificar os pacientes individualmente. Este formato prioriza a simplicidade do registro em detrimento do detalhe clínico-demográfico.3
        
    - **BPA-I (Individualizado):** Registra os procedimentos de forma individualizada, um por paciente. Cada linha corresponde a um atendimento específico, preservando informações demográficas do paciente (como sexo, idade, município de residência) e dados clínicos (como o diagnóstico principal).3
        
- **Autorização de Procedimentos de Alta Complexidade (APAC):** É o instrumento utilizado para procedimentos de alto custo, alta complexidade ou que requerem um controle e monitoramento mais rigorosos, necessitando de autorização prévia do gestor. Exemplos clássicos incluem sessões de quimioterapia, radioterapia e hemodiálise.3 Por sua natureza, os registros de APAC são sempre individualizados.
    
- **Registro das Ações Ambulatoriais de Saúde (RAAS):** Um instrumento mais recente, instituído para monitorar ações e serviços de saúde organizados em Redes de Atenção à Saúde. Possui variações para áreas específicas, como a Atenção Psicossocial (RAAS-PSI) e a Atenção Domiciliar (RAAS-AD).11 Os registros do RAAS também são individualizados.
    

### 1.3. A Pedra de Roseta: O Papel Crítico do Campo `PA_DOCORIG`

Dada a heterogeneidade dos registros no arquivo `PA`, um campo específico funciona como a chave mestra para a correta interpretação dos dados: `PA_DOCORIG` (Documento de Origem). Este campo é, sem dúvida, o mais importante para qualquer analista, pois identifica qual dos instrumentos de registro (BPA-C, BPA-I, APAC ou RAAS) gerou aquela linha específica no banco de dados.7 O valor neste campo determina o nível de observação do registro e, consequentemente, quais outros campos na mesma linha são válidos e interpretáveis.

Ignorar o `PA_DOCORIG` leva a erros analíticos graves. Considere um cenário em que um pesquisador deseja calcular a quantidade total de um determinado procedimento. Se ele simplesmente somar a coluna `PA_QTDAPR` (Quantidade Aprovada) em todo o arquivo, estará somando valores que representam contagens de pacientes únicos (de registros BPA-I, APAC e RAAS, onde a quantidade é geralmente 1) com contagens de lotes de procedimentos (de registros BPA-C, onde a quantidade pode ser de centenas). O resultado seria um número inflado e sem significado estatístico. Da mesma forma, tentar calcular a idade média dos pacientes utilizando todo o arquivo seria inválido, pois os campos demográficos como `PA_IDADE` estão vazios ou não são aplicáveis para os registros originados do BPA-C.

Portanto, a primeira etapa obrigatória de qualquer análise do arquivo `PA` deve ser a segmentação ou filtragem dos dados com base no campo `PA_DOCORIG`. As análises de perfil de paciente só podem ser realizadas em registros individualizados, enquanto as análises de volume total de produção devem tratar os registros consolidados e individualizados de maneira distinta.

**Tabela 1: Definições dos Códigos do Campo `PA_DOCORIG`**

|Código|Descrição|Nível de Observação|
|---|---|---|
|`P`|Procedimento Principal de APAC|Individualizado|
|`S`|Procedimento Secundário de APAC|Individualizado|
|`C`|Procedimento de BPA Consolidado|Agregado|
|`I`|Procedimento de BPA Individualizado|Individualizado|
|`A`|Procedimento de RAAS (Atenção Domiciliar)|Individualizado|
|`R`|Procedimento de RAAS (Atenção Psicossocial)|Individualizado|

Fonte: Derivado do Informe Técnico do SIASUS.7

## Seção II: Dicionário de Dados Granular por Grupo Temático

Esta seção central fornece uma análise exaustiva, campo por campo, das 60 colunas do arquivo `PA`. Cada entrada inclui o nome da coluna, uma descrição detalhada, o tipo e tamanho dos dados (conforme o layout oficial) e uma explicação abrangente de seus valores possíveis, com links para sistemas externos quando necessário.

### Parte A: Identificadores do Estabelecimento, Gestão e Jurídicos

Estes campos identificam o "quem" e o "onde" do prestador de serviços.

- **`PA_CODUNI` (CHAR 7):** _Código da Unidade de Saúde._ Identificador único de 7 dígitos do estabelecimento de saúde onde o procedimento foi realizado. Este código é a chave primária para vincular os dados do SIA ao **Cadastro Nacional de Estabelecimentos de Saúde (CNES)**.7 Através do CNES, é possível obter informações detalhadas sobre o estabelecimento, como nome, endereço, tipo de unidade, infraestrutura, equipamentos e profissionais vinculados.13
    
- **`PA_UFMUN` (CHAR 6):** _UF e Município do Estabelecimento._ Código de 6 dígitos do Instituto Brasileiro de Geografia e Estatística (IBGE) para o município onde o estabelecimento está localizado (2 dígitos para a Unidade da Federação e 4 para o município).7 É essencial para qualquer análise com recorte geográfico.
    
- **`PA_GESTAO` (CHAR 6):** _Código do Gestor._ Código IBGE do município responsável pela gestão financeira e administrativa do estabelecimento. Se o estabelecimento estiver sob gestão estadual, o campo conterá o código da UF seguido de "0000".7 Este campo é crucial para entender a governança do sistema de saúde, os fluxos de financiamento e as responsabilidades de gestão.
    
- **`PA_CONDIC` (CHAR 2):** _Condição de Gestão._ Código que indica a modalidade de habilitação do município ou estado na gestão do SUS (ex: Gestão Plena da Atenção Básica, Gestão Plena do Sistema Municipal). Este campo reflete o nível de descentralização e autonomia do gestor, o que impacta as transferências de recursos e as responsabilidades. Os códigos e suas descrições são encontrados em tabelas auxiliares do SIA.7
    
- **`PA_TPUPS` (CHAR 2):** _Tipo de Estabelecimento._ Código proveniente do CNES que classifica o tipo de unidade de saúde (ex: `01` - Posto de Saúde, `02` - Centro de Saúde/Unidade Básica de Saúde, `05` - Hospital Geral).9 Fornece um contexto vital sobre o cenário do atendimento.
    
- **`PA_TIPPRE` (CHAR 2):** _Tipo de Prestador._ Código que indica a natureza do prestador de serviço (ex: público, privado contratado/conveniado, filantrópico). A informação é originária do CNES e permite análises sobre a participação dos diferentes setores na oferta de serviços do SUS.
    
- **`PA_MN_IND` (CHAR 1):** _Estabelecimento Mantido/Individual._ Indica se o estabelecimento é uma filial ou unidade mantida por uma entidade maior ('M' - Mantido) ou se é uma entidade independente ('I' - Individual).15
    
- **`PA_CNPJCPF` (CHAR 14):** _CNPJ/CPF do Estabelecimento._ Número de inscrição no Cadastro Nacional da Pessoa Jurídica (CNPJ) ou no Cadastro de Pessoas Físicas (CPF) do estabelecimento que realizou o procedimento.7
    
- **`PA_CNPJMNT` (CHAR 14):** _CNPJ da Mantenedora._ CNPJ da entidade mantenedora do estabelecimento, se aplicável (ex: o CNPJ da secretaria municipal de saúde para um posto de saúde, ou de uma universidade para um hospital universitário). Preenchido com zeros se não houver mantenedora.7
    
- **`PA_CNPJ_CC` (CHAR 14):** _CNPJ de Cessão de Crédito._ CNPJ da entidade que recebeu o pagamento pela produção por meio de um contrato de cessão de crédito. Preenchido com zeros se não for o caso.7
    
- **`PA_INE` (CHAR 10):** _Identificador Nacional de Equipe._ Código único que identifica a equipe de saúde responsável pelo atendimento (ex: uma equipe específica da Estratégia Saúde da Família). Este campo é fundamental para a avaliação de modelos de atenção baseados em equipes, especialmente na atenção primária, e estabelece uma ponte com os dados do sistema e-SUS Atenção Primária.7
    
- **`PA_NAT_JUR` (CHAR 4):** _Natureza Jurídica._ Código que define a constituição jurídico-institucional do estabelecimento, conforme a tabela da Comissão Nacional de Classificação (CONCLA) do IBGE e registrada no CNES.17 Este campo permite distinguir com precisão entre órgãos da administração pública, empresas privadas, entidades sem fins lucrativos, etc.
    

### Parte B: Identificadores de Registro, Processamento e Competência

Estes campos definem o "quando" do registro de dados.

- **`PA_MVM` (CHAR 6):** _Data de Movimento._ Ano e mês (formato AAAAMM) em que os dados foram processados pelo gestor local e incluídos no movimento para faturamento e consolidação.7
    
- **`PA_CMP` (CHAR 6):** _Data de Competência._ Ano e mês (formato AAAAMM) em que o serviço de saúde foi efetivamente realizado.7
    

A análise da defasagem entre a competência (`PA_CMP`) e o movimento (`PA_MVM`) é uma ferramenta poderosa. O SUS estabelece prazos para que os prestadores enviem sua produção para processamento.9 Uma diferença significativa e consistente entre essas duas datas para um determinado prestador ou gestor pode indicar ineficiências administrativas, atrasos no envio dos dados ou gargalos no processamento. Ao realizar análises temporais, o pesquisador deve fazer uma escolha consciente: filtrar por

`PA_CMP` para capturar todos os serviços realizados em um determinado mês (mesmo que tenham sido informados tardiamente) ou filtrar por `PA_MVM` para analisar o conjunto de dados exato que foi processado e pago em um ciclo específico. A escolha impacta diretamente os resultados e a interpretação da análise.

### Parte C: Demografia e Localização do Paciente

Estes campos descrevem o "quem" do paciente. Sua presença e validade dependem intrinsecamente do registro ser individualizado (`PA_DOCORIG` com valores 'I', 'P', 'S', 'A' ou 'R').

- **`PA_MUNPCN` (CHAR 6):** _Município de Residência do Paciente._ Código IBGE de 6 dígitos do município de residência do paciente.15 Este é um dos campos mais importantes para estudos de fluxo de pacientes, acesso a serviços, equidade e planejamento da rede de atenção regionalizada.
    
- **`PA_IDADE` (NUMERIC 3):** _Idade do Paciente._ Idade do paciente em anos completos. Para crianças com menos de um ano, este campo geralmente é preenchido com 0, e a idade precisa (em dias ou meses) pode estar em outros campos não presentes nesta lista de 60 colunas, mas disponíveis em layouts mais detalhados de instrumentos como o RAAS.
    
- **`IDADEMIN` & `IDADEMAX` (NUMERIC):** _Idade Mínima e Máxima para o Procedimento._ É crucial notar que estas duas colunas **não são campos nativos** do arquivo `PA` padrão, conforme o layout do Informe Técnico do DATASUS.7 Elas são atributos do
    
    _procedimento_ e não do _paciente_. A sua presença na lista de colunas fornecida indica que os dados foram previamente enriquecidos. O processo para obter esses valores envolve a junção do arquivo `PA` com a tabela do SIGTAP (Tabela de Procedimentos do SUS) usando o campo `PA_PROC_ID` como chave. O SIGTAP define, para cada procedimento, uma faixa etária permitida para sua realização.19 Estes valores são usados pelo sistema SIA para validação, gerando um alerta no campo
    
    `PA_FLIDADE`.
    
- **`PA_SEXO` (CHAR 1):** _Sexo do Paciente._ Campo codificado que informa o sexo do paciente, conforme registrado no atendimento.15
    

**Tabela 2: Definições dos Códigos do Campo `PA_SEXO`**

|Código|Descrição|
|---|---|
|`M`|Masculino|
|`F`|Feminino|
|`I`|Ignorado|

Fonte: Padrão de codificação do SUS.15

- **`PA_RACACOR` (CHAR 2):** _Raça/Cor do Paciente._ Campo para a raça/cor autodeclarada do paciente, seguindo a classificação do IBGE. É um campo vital para análises de equidade em saúde e monitoramento de disparidades raciais no acesso e utilização dos serviços.3
    

**Tabela 3: Definições dos Códigos do Campo `PA_RACACOR`**

|Código|Descrição|
|---|---|
|`01`|Branca|
|`02`|Preta|
|`03`|Parda|
|`04`|Amarela|
|`05`|Indígena|
|`99`|Ignorado|

Fonte: Padrão de codificação do SUS baseado no IBGE.15

- **`PA_ETNIA` (CHAR 4):** _Etnia do Paciente._ Código de 4 dígitos para a etnia indígena do paciente, quando `PA_RACACOR` for `05`. Este campo utiliza uma tabela de referência específica de povos indígenas mantida pela Fundação Nacional do Índio (FUNAI) e pela Secretaria Especial de Saúde Indígena (SESAI), permitindo análises de saúde com um recorte específico para essa população.7
    

### Parte D: Informações sobre Procedimento, Serviço e Clínica

Estes campos descrevem o "o quê" e o "porquê" do atendimento de saúde.

- **`PA_PROC_ID` (CHAR 10):** _Código do Procedimento._ Código de 10 dígitos que identifica univocamente o procedimento realizado, conforme a **Tabela de Procedimentos, Medicamentos, Órteses, Próteses e Materiais Especiais do SUS (SIGTAP)**.7 Este é o campo central para a compreensão do serviço clínico prestado e a principal chave de ligação com a tabela SIGTAP para enriquecimento dos dados.
    
- **`PA_NIVCPL` (CHAR 1):** _Nível de Complexidade._ Classifica a complexidade do procedimento. Este é um atributo do procedimento, importado do SIGTAP. Os valores típicos são: `1` para Atenção Básica, `2` para Média Complexidade e `3` para Alta Complexidade.15
    
- **`PA_CATEND` (CHAR 2):** _Caráter do Atendimento._ Código que descreve a natureza do atendimento, fundamental para análises epidemiológicas e operacionais.3 Distingue, por exemplo, atendimentos eletivos de urgências.
    

**Tabela 4: Definições dos Códigos do Campo `PA_CATEND` (Exemplos para Ambulatorial)**

|Código|Descrição|
|---|---|
|`01`|Eletivo|
|`02`|Urgência|
|`03`|Acidente no local de trabalho ou a serviço da empresa|
|`04`|Acidente de trânsito|
|`05`|Outras lesões e envenenamentos por agentes químicos ou físicos|

Nota: Esta é uma tabela exemplificativa. A tabela oficial completa deve ser consultada na documentação auxiliar do SIA. A referência 20 mostra uma tabela similar para internações, reforçando a necessidade de usar a tabela correta para o contexto ambulatorial.

- **`PA_SRV_C` (CHAR 6):** _Serviço/Classificação._ Código do SIGTAP que agrupa procedimentos em categorias clínicas mais amplas. É composto por um código de "Serviço" (3 dígitos) e um de "Classificação" (3 dígitos). Por exemplo, o Serviço `135` (Serviço de Reabilitação) pode conter a Classificação `005` (Reabilitação Auditiva).21 Permite análises em um nível mais agregado do que o de procedimentos individuais.
    
- **`PA_CIDPRI` (CHAR 4):** _CID Principal._ Código da Classificação Internacional de Doenças, 10ª Revisão (CID-10), que representa o diagnóstico principal ou o motivo que levou à realização do procedimento. O formato é alfanumérico (ex: `J450` para Asma).7
    
- **`PA_CIDSEC` (CHAR 4):** _CID Secundário._ Código de um diagnóstico secundário (CID-10) relevante para o atendimento.7
    
- **`PA_CIDCAS` (CHAR 4):** _CID Causas Associadas._ Código de um diagnóstico (CID-10) de causa associada, frequentemente utilizado para registrar causas externas de lesões e envenenamentos (Capítulo XX da CID-10).7
    

### Parte E: Atendimento, Autorização e Desfecho

Estes campos rastreiam o fluxo administrativo e o resultado da jornada do paciente.

- **`PA_DOCORIG` (CHAR 1):** _Documento de Origem._ Conforme descrito em detalhe na Seção 1.3, este campo identifica o instrumento de registro que deu origem à linha de dados.
    
- **`PA_AUTORIZ` (CHAR 13):** _Número da Autorização._ Para procedimentos originados de uma APAC ou que exigem autorização no BPA-I, este campo contém o número único da autorização emitida pelo gestor.7
    
- **`PA_MOTSAI` (CHAR 2):** _Motivo de Saída/Permanência._ Código que indica o desfecho do tratamento ou do episódio de cuidado, especialmente relevante para tratamentos contínuos registrados via APAC.15
    

**Tabela 5: Definições dos Códigos do Campo `PA_MOTSAI` (Exemplos)**

|Código|Descrição|
|---|---|
|`11`|Alta por cura|
|`14`|Alta a pedido|
|`21`|Permanência por características próprias da doença|
|`31`|Transferência para outro estabelecimento|
|`41`|Óbito com causa diretamente relacionada à doença|
|`42`|Óbito com causa não relacionada à doença|

_Nota: A tabela completa, com dezenas de códigos, deve ser obtida na documentação auxiliar do SIA._

- **`PA_OBITO` (CHAR 1):** _Óbito._ Flag que indica se o paciente veio a óbito durante o tratamento (`1` = Sim, `0` = Não).
    
- **`PA_ENCERR` (CHAR 1):** _Encerramento._ Flag que indica se o episódio de cuidado (ex: uma APAC para um tratamento de 12 meses) foi encerrado.
    
- **`PA_PERMAN` (CHAR 1):** _Permanência._ Flag que indica que o paciente continua em tratamento.
    
- **`PA_ALTA` (CHAR 1):** _Alta._ Flag que indica que o paciente recebeu alta daquele episódio de cuidado.
    
- **`PA_TRANSF` (CHAR 1):** _Transferência._ Flag que indica que o paciente foi transferido para outro serviço ou estabelecimento.
    

### Parte F: Identificação do Profissional de Saúde

Estes campos identificam o profissional que realizou o serviço.

- **`PA_CNSMED` (CHAR 15):** _Cartão Nacional de Saúde do Profissional._ Número do Cartão Nacional de Saúde (CNS) do profissional de saúde que executou o procedimento.15 Permite a identificação única do profissional.
    
- **`PA_CBOCOD` (CHAR 6):** _Código Brasileiro de Ocupação._ Código de 6 dígitos que identifica a ocupação do profissional (ex: `225125` para Médico Clínico), conforme a Classificação Brasileira de Ocupações (CBO) do Ministério do Trabalho e Emprego.9 Este campo é essencial para estudos sobre força de trabalho, distribuição de especialistas e adequação do profissional ao procedimento realizado. A CBO pode ser consultada online nos portais do MTE ou do IBGE.23
    

### Parte G: Dados Financeiros, de Financiamento e Contratuais

Estes campos são centrais para o propósito financeiro e de auditoria do SIA.

- **`PA_QTDPRO` (NUMERIC 10):** _Quantidade Produzida._ A quantidade do procedimento que foi informada pelo prestador de serviço.7
    
- **`PA_QTDAPR` (NUMERIC 10):** _Quantidade Aprovada._ A quantidade do procedimento que foi aprovada para pagamento pelo gestor após as validações do sistema.7
    
- **`PA_VALPRO` (NUMERIC 16,2):** _Valor Produzido._ O valor total submetido pelo prestador, calculado como (preço unitário do procedimento * `PA_QTDPRO`).7
    
- **`PA_VALAPR` (NUMERIC 16,2):** _Valor Aprovado._ O valor total aprovado para pagamento, calculado como (preço unitário * `PA_QTDAPR`).7
    
- **`PA_VL_CF` (NUMERIC 16,2):** _Valor do Complemento Federal._ Valor de incentivos financeiros de nível federal que são somados ao valor base do procedimento. Usado para políticas específicas de saúde.7
    
- **`PA_VL_CL` (NUMERIC 16,2):** _Valor do Complemento Local._ Valor de incentivos financeiros adicionados pelo gestor estadual ou municipal, como parte de políticas locais de saúde.7
    
- **`PA_VL_INC` (NUMERIC 16,2):** _Valor do Incremento._ Valor total de outros tipos de incrementos financeiros, como o de urgência, aplicados ao procedimento.7
    
- **`NU_VPA_TOT` & `NU_PA_TOT` (NUMERIC):** _Valor Total Aprovado & Valor Total._ Semelhante a `IDADEMIN`/`MAX`, estes campos não constam no layout padrão do arquivo `PA`.7 Eles representam campos calculados ou derivados, provavelmente adicionados em uma base de dados pré-processada. A lógica mais provável é que
    
    `NU_VPA_TOT` seja a soma de todos os componentes do valor aprovado: NU_VPA_TOT=PA_VALAPR+PA_VL_CF+PA_VL_CL+PA_VL_INC. O usuário deve verificar esta fórmula ou calculá-la se estiver trabalhando com os dados brutos.
    
- **`PA_DIF_VAL` (NUMERIC 20,2):** _Diferença de Valores._ Registra a diferença entre o valor do procedimento na tabela nacional do SUS e um valor diferenciado negociado localmente pelo gestor, multiplicada pela quantidade aprovada.15
    
- **`PA_TPFIN` (CHAR 2) & `PA_SUBFIN` (CHAR 4):** _Tipo e Subtipo de Financiamento._ Códigos que especificam a fonte de recursos (bloco de financiamento) para o pagamento do procedimento. É um campo crítico para o acompanhamento orçamentário e a análise de políticas de saúde com financiamento específico.7
    

**Tabela 6: Definições dos Códigos do Campo `PA_TPFIN` (Exemplos)**

|Código|Descrição do Bloco de Financiamento|
|---|---|
|`01`|Atenção Básica (PAB)|
|`04`|Média e Alta Complexidade (MAC)|
|`06`|Fundo de Ações Estratégicas e Compensação (FAEC)|
|`07`|Vigilância em Saúde|

_Fonte: Tabela de Financiamento do SIGTAP/SIA._

- **`PA_REGCT` (CHAR 4):** _Regra Contratual._ Código originário do CNES que define regras contratuais específicas entre o prestador e o gestor do SUS, que podem influenciar o pagamento ou as condições de oferta do serviço.7
    
- **`PA_INCOUT` (CHAR 4) & `PA_INCURG` (CHAR 4):** _Incremento Outros & Incremento Urgência._ Códigos que identificam a aplicação de incrementos financeiros específicos ao valor do procedimento, conforme regras definidas na tabela SIGTAP.7
    

### Parte H: Flags do Sistema e Indicadores de Validação

Estes campos são gerados pelo sistema SIA durante o processamento para sinalizar situações específicas ou erros.

- **`PA_INDICA` (CHAR 1):** _Indicativo de Situação da Produção._ Um flag que resume o status de aprovação da produção apresentada.7
    

**Tabela 7: Definições dos Códigos do Campo `PA_INDICA`**

|Código|Descrição|
|---|---|
|`0`|Não aprovado|
|`5`|Aprovado total|
|`6`|Aprovado parcial|

Fonte: Informe Técnico do SIASUS.7

- **`PA_CODOCO` (CHAR 4):** _Código de Ocorrência._ Código que detalha o motivo da rejeição ou alteração da produção informada. Cada código corresponde a uma crítica específica do sistema (ex: "procedimento incompatível com o sexo do paciente", "idade do paciente fora da faixa permitida").
    
- **`PA_UFDIF` (CHAR 1):** _UF Diferente._ Flag que indica se a Unidade da Federação de residência do paciente é diferente da UF de localização do estabelecimento (`S` = Sim, `N` = Não).15
    
- **`PA_MNDIF` (CHAR 1):** _Município Diferente._ Flag que indica se o município de residência do paciente é diferente do município de localização do estabelecimento (`1` = Sim, `0` = Não).7
    
- **`PA_FLIDADE` (CHAR 1):** _Flag de Idade._ Flag gerado pelo sistema que sinaliza uma inconsistência entre a idade do paciente (`PA_IDADE`) e a faixa etária permitida para o procedimento (`IDADEMIN`, `IDADEMAX`) definida no SIGTAP.
    
- **`PA_FLQT` (CHAR 1):** _Flag de Quantidade._ Flag que indica um problema com a quantidade informada (ex: quantidade máxima excedida para o período).
    
- **`PA_FLER` (CHAR 1):** _Flag de Erro._ Um flag de erro genérico, frequentemente associado a inconsistências no preenchimento de uma APAC.7
    

## Seção III: Guia Prático para Navegar nos Sistemas de Saúde Nacionais Vinculados

O arquivo `PA` não deve ser visto como um conjunto de dados isolado, mas como um hub que se conecta a outros sistemas de informação cruciais do SUS. O enriquecimento dos dados do SIA com informações desses sistemas externos é uma etapa fundamental para uma análise aprofundada.

### 3.1. Usando `PA_PROC_ID` para Consultar o SIGTAP

A coluna `PA_PROC_ID` é a chave para desvendar todos os detalhes sobre o serviço clínico prestado.

- **Ação:** Extraia um código do campo `PA_PROC_ID` do seu conjunto de dados.
    
- **Recurso:** Acesse o portal online do SIGTAP ou faça o download da sua base de dados mensal, disponível no site do DATASUS.26
    
- **Resultado:** Ao consultar o código, você obterá o nome oficial e a descrição completa do procedimento, seu nível de complexidade (`PA_NIVCPL`), as regras de financiamento (`PA_TPFIN`), a ocupação do profissional habilitado a realizá-lo (`PA_CBOCOD`), os diagnósticos (CID-10) compatíveis e, de forma crucial, a faixa etária permitida (`IDADEMIN` e `IDADEMAX`).19 Isso explica diretamente a origem das colunas de idade mínima e máxima na sua lista.
    

### 3.2. Usando `PA_CODUNI` para Alavancar o CNES

A coluna `PA_CODUNI` permite traçar o perfil completo do local onde o atendimento ocorreu.

- **Ação:** Utilize um código do campo `PA_CODUNI`.
    
- **Recurso:** Acesse o portal de consulta pública do CNES ou baixe os microdados completos do DATASUS.14
    
- **Resultado:** A consulta retornará o perfil completo do estabelecimento: nome fantasia, endereço, tipo de unidade (`PA_TPUPS`), natureza jurídica (`PA_NAT_JUR`), tipo de gestão, equipamentos disponíveis, serviços habilitados e a lista de profissionais com vínculo ativo.
    

### 3.3. Usando `PA_CBOCOD` para Entender a Força de Trabalho

A coluna `PA_CBOCOD` é a porta de entrada para análises sobre os profissionais de saúde.

- **Ação:** Pegue um código do campo `PA_CBOCOD`.
    
- **Recurso:** Utilize a ferramenta de busca da Classificação Brasileira de Ocupações, disponível no portal do Ministério do Trabalho e Emprego (MTE).23
    
- **Resultado:** Você obterá o título oficial da ocupação e uma descrição detalhada das atividades, competências e responsabilidades associadas àquele código, permitindo uma compreensão clara do papel daquele profissional no sistema.
    

### 3.4. Usando `PA_CID*` para Análise Diagnóstica Precisa

As colunas `PA_CIDPRI`, `PA_CIDSEC` e `PA_CIDCAS` são a base para estudos de morbidade.

- **Ação:** Utilize um código de qualquer um dos campos CID.
    
- **Recurso:** Consulte uma ferramenta online de busca da CID-10 ou as tabelas oficiais disponibilizadas pelo DATASUS ou pela Organização Mundial da Saúde (OMS).31
    
- **Resultado:** A consulta fornecerá a descrição completa do diagnóstico, permitindo a realização de estudos epidemiológicos detalhados, análises de perfil de morbidade e monitoramento de doenças e agravos.
    

## Seção IV: Considerações Analíticas e Recomendações de Especialistas

Esta seção final sintetiza os pontos-chave do relatório em conselhos práticos para o analista de dados, com o objetivo de prevenir erros comuns e promover análises robustas e precisas.

### 4.1. A Armadilha da Agregação: Sempre Comece com `PA_DOCORIG`

A distinção entre registros consolidados (BPA-C) e individualizados (BPA-I, APAC, RAAS) é a consideração mais crítica ao trabalhar com dados do SIA. A recomendação é inequívoca: antes de realizar qualquer cálculo, o conjunto de dados deve ser estratificado por `PA_DOCORIG`. Análises de perfil de paciente (idade, sexo, residência) só podem ser feitas sobre o subconjunto de dados individualizados. Análises de volume ou financeiras devem tratar os dois tipos de registro de forma separada ou utilizar metodologias que ponderem adequadamente cada tipo de registro. Somar ou calcular médias sobre o arquivo completo, sem essa distinção, produzirá resultados estatisticamente inválidos e levará a conclusões equivocadas.

### 4.2. A Trilha de Auditoria Financeira: Analisando `PROD` vs. `APR`

O SIA, em sua essência, é um sistema de pagamento. A existência de campos pareados para "produzido/apresentado" e "aprovado" (`PA_QTDPRO`/`PA_QTDAPR`, `PA_VALPRO`/`PA_VALAPR`) oferece uma oportunidade única de análise. A diferença entre esses pares, quando cruzada com o código de ocorrência (`PA_CODOCO`), transforma o banco de dados em uma poderosa ferramenta de auditoria e análise de desempenho. Essa abordagem pode revelar padrões de erros de faturamento, inconsistências entre as regras do gestor e a prática do prestador, ou identificar áreas que necessitam de capacitação e melhoria nos processos de registro.

### 4.3. Análise de Séries Temporais: Cuidado com as Mudanças Estruturais

O SIA é um sistema dinâmico que passou por evoluções significativas ao longo de sua história. Mudanças importantes, como a implantação da Tabela de Procedimentos Unificada em 2008 15 e a introdução do RAAS em 2012 11, alteraram o layout dos arquivos, a codificação de procedimentos e a forma de registro de certas ações. Ao conduzir estudos longitudinais que abrangem vários anos, é imperativo que o pesquisador esteja ciente dessas mudanças. Recomenda-se sempre verificar a data de competência (

`PA_CMP`) dos dados e consultar as notas técnicas e manuais históricos correspondentes ao período em estudo para garantir a comparabilidade dos dados ao longo do tempo.

### 4.4. Abordando as Colunas "Ausentes"

A lista de colunas fornecida para análise continha quatro campos (`IDADEMIN`, `IDADEMAX`, `NU_VPA_TOT`, `NU_PA_TOT`) que não fazem parte do layout padrão do arquivo `PA` disseminado pelo DATASUS. Conforme detalhado neste relatório, `IDADEMIN` e `IDADEMAX` são atributos do procedimento, provenientes de uma junção com a tabela SIGTAP. Da mesma forma, `NU_VPA_TOT` e `NU_PA_TOT` são, muito provavelmente, campos de conveniência que representam a soma de todos os componentes de valor. É fundamental que o usuário compreenda que está trabalhando com uma versão pré-processada e enriquecida dos dados, e que deve validar a metodologia usada para criar esses campos derivados.

### 4.5. Recomendação Final: O Fluxo de Trabalho "Enriquecimento Primeiro"

O arquivo `PA` bruto é apenas o ponto de partida. Para extrair o máximo valor analítico, um fluxo de trabalho robusto deve ser adotado. A recomendação final é a abordagem de "enriquecimento primeiro": antes de iniciar a análise estatística, o analista deve sistematicamente juntar os microdados do arquivo `PA` com as tabelas mestras do CNES (usando `PA_CODUNI`), SIGTAP (usando `PA_PROC_ID`), CBO (usando `PA_CBOCOD`) e tabelas geográficas do IBGE (usando `PA_UFMUN` e `PA_MUNPCN`). Este processo transforma um arquivo de transações em um conjunto de dados rico e contextualizado, permitindo análises muito mais profundas e precisas sobre o sistema de saúde brasileiro.

# Dicionário de Variáveis do Cadastro Nacional de Estabelecimentos de Saúde (CNES) - Tabela de Estabelecimentos

## Introdução: Desvendando a Arquitetura de Dados do Cadastro Nacional de Estabelecimentos de Saúde (CNES)

O Cadastro Nacional de Estabelecimentos de Saúde (CNES) representa um dos pilares fundamentais para a gestão e o planejamento do Sistema Único de Saúde (SUS) no Brasil. Instituído como o sistema de informação oficial para o registro de todos os estabelecimentos de saúde em território nacional, sua abrangência inclui unidades públicas, privadas, filantrópicas, com ou sem vínculo com o SUS.1 A principal finalidade do CNES é servir como base cadastral unificada e confiável para a operacionalização de dezenas de outros sistemas de informação em saúde, como o Sistema de Informação Ambulatorial (SIA) e o Sistema de Informação Hospitalar (SIH), garantindo a interoperabilidade e a consistência dos dados em todo o ecossistema do SUS.1

O conjunto de dados de estabelecimentos, frequentemente disponibilizado em arquivos mensais (`tb_estabelecimento`), funciona como uma "fotografia" da base de dados em um ponto específico no tempo.5 Esta característica temporal, marcada pela variável

`COMPETEN`, é crucial para a correta interpretação e análise dos dados. Cada arquivo mensal reflete o estado cadastral dos estabelecimentos de saúde naquela competência, permitindo a construção de séries históricas detalhadas sobre a evolução da capacidade instalada da rede de saúde brasileira.

A compilação deste relatório baseia-se na síntese e harmonização de uma vasta gama de fontes documentais. Devido à natureza evolutiva do sistema, não existe um único manual canônico que abranja todas as variáveis e suas transformações ao longo do tempo. Portanto, este documento consolida informações de manuais técnicos históricos do Ministério da Saúde 6, da Wiki oficial do CNES mantida pelo DATASUS 7, de dicionários de dados enriquecidos por plataformas de pesquisa como a Plataforma de Ciência de Dados aplicada à Saúde (PCDaS/Fiocruz) 8, e de diversas notas técnicas e portarias.9 A dificuldade em localizar um dicionário de dados único, oficial e atualizado evidencia a necessidade deste guia consolidado para pesquisadores, analistas e gestores.10

A estrutura deste relatório foi organizada em seções temáticas que espelham a lógica das Fichas de Cadastro de Estabelecimentos de Saúde (FCES). Esta abordagem foi escolhida porque a arquitetura da base de dados do CNES deriva diretamente da estrutura dessas fichas, que são os instrumentos de coleta de dados primários.6 Ao seguir esta organização, o relatório não apenas define cada variável, mas também a contextualiza dentro do processo de cadastramento, facilitando uma compreensão mais profunda de seu significado e de suas inter-relações.

## Seção 1: Identificação Fundamental e Metadados do Registro

Esta seção aborda as variáveis que funcionam como chaves de identificação e metadados essenciais. Elas definem unicamente cada estabelecimento, sua natureza jurídica primária e sua localização no tempo, sendo indispensáveis para qualquer tipo de análise de dados.

### CNES

- **Descrição:** Código Nacional do Estabelecimento de Saúde. Este é um identificador numérico único, composto por 7 dígitos, atribuído a cada estabelecimento de saúde no Brasil. Funciona como a chave primária em todo o sistema CNES, garantindo a unicidade de cada registro.14 A obtenção e o gerenciamento deste código são processos formais realizados junto ao gestor de saúde local (Secretaria Municipal ou Estadual de Saúde).15
	 
- **Valores:** Sequência numérica de 7 dígitos. Exemplo: `2337934`.
	 

### CPF_CNPJ

- **Descrição:** Cadastro de Pessoa Física (CPF) ou Cadastro Nacional da Pessoa Jurídica (CNPJ) do estabelecimento. Este campo armazena o número de registro fiscal da entidade responsável pelo estabelecimento junto à Receita Federal do Brasil. A interpretação correta deste campo depende da variável `PF_PJ`.8
	 
- **Valores:** Sequência numérica de 11 dígitos (para CPF) ou 14 dígitos (para CNPJ).
	 

### PF_PJ

- **Descrição:** Indicador de Pessoa Física ou Jurídica. Trata-se de um campo categórico (flag) que especifica a natureza do registro fiscal do estabelecimento. É fundamental para distinguir, por exemplo, um consultório particular de um profissional autônomo (Pessoa Física) de um hospital ou clínica (Pessoa Jurídica).8
	 
- **Valores:**
	 
	 - `1`: Pessoa Física
		  
	 - `3`: Pessoa Jurídica
		  

### NIV_DEP

- **Descrição:** Nível de Dependência. Esta variável indica a relação de autonomia do estabelecimento. Um estabelecimento "Individual" é uma entidade independente, enquanto um "Mantido" é uma filial ou unidade que depende administrativamente de uma entidade mantenedora.6
	 
- **Valores:**
	 
	 - `1`: Individual
		  
	 - `3`: Mantida
		  

### CNPJ_MAN

- **Descrição:** CNPJ da Entidade Mantenedora. Este campo é preenchido apenas quando o `NIV_DEP` é igual a `3` (Mantida). Ele contém o CNPJ da organização principal que mantém financeiramente e administrativamente o estabelecimento. Por exemplo, um posto de saúde municipal (unidade mantida) terá neste campo o CNPJ da Prefeitura Municipal correspondente (entidade mantenedora).6
	 
- **Valores:** Sequência numérica de 14 dígitos. Nulo se `NIV_DEP` for `1`.
	 

### CODUFMUN

- **Descrição:** Código do Município. Identifica o município de localização do estabelecimento, utilizando o padrão de codificação de 6 dígitos do Instituto Brasileiro de Geografia e Estatística (IBGE). O código é formado pela concatenação do código da Unidade da Federação (2 dígitos) com o código do município dentro do estado (4 dígitos, sem o dígito verificador).8
	 
- **Valores:** Código numérico de 6 dígitos. Exemplo: `355030` para São Paulo-SP.
	 

### COD_CEP

- **Descrição:** Código de Endereçamento Postal. Corresponde ao CEP do endereço principal do estabelecimento de saúde.8
	 
- **Valores:** Sequência numérica de 8 dígitos.
	 

### DT_ATUAL

- **Descrição:** Data da Última Atualização. Registra a data em que as informações cadastrais do estabelecimento foram efetivamente alteradas pela última vez na base de dados nacional do CNES.
	 
- **Valores:** Data no formato `AAAAMMDD`.
	 

### COMPETEN

- **Descrição:** Competência do Arquivo. Indica o ano e o mês a que se refere o conjunto de dados, ou seja, a "fotografia" mensal da base. É uma das variáveis mais críticas para a realização de análises temporais e longitudinais.9
	 
- **Valores:** Data no formato `AAAAMM`. Exemplo: `202312` para dezembro de 2023.
	 

A combinação das variáveis `CNES`, `COMPETEN` e `DT_ATUAL` é fundamental para uma análise temporal precisa. O `CNES` identifica o estabelecimento, a `COMPETEN` define o momento da "fotografia" dos dados, e a `DT_ATUAL` indica quando a última mudança real ocorreu. Um estabelecimento pode aparecer com os mesmos dados em várias competências consecutivas se não houver alterações; nesses casos, a `DT_ATUAL` permanecerá constante.

Conforme detalhado na Nota Técnica Nº 07/2023-CGSI/DRAC/SAES/MS, o banco de dados nacional do CNES opera sob um "conceito restrito de competência".18 Os gestores municipais e estaduais enviam atualizações ao longo do mês para uma base de dados dinâmica. Ao final do período (mês), o Ministério da Saúde consolida e "fecha" uma versão estável dos dados para aquela competência. Isso significa que a análise dos dados do CNES não é uma análise em tempo real, mas sim uma análise de uma série de

_snapshots_ mensais. Para um pesquisador, a implicação é direta: ao cruzar dados do CNES com dados de eventos (como internações do SIH ou atendimentos do SIA), é imperativo utilizar a `COMPETEN` do CNES que corresponde ou precede imediatamente a data do evento. Ignorar essa sincronia pode levar a conclusões anacrônicas, como atribuir um procedimento a um serviço que só foi oficialmente cadastrado no mês seguinte, resultando em erros de análise sobre a capacidade e oferta de serviços no momento do atendimento.

## Seção 2: Caracterização Institucional, Natureza e Vínculo com o SUS

Esta seção detalha a "identidade" do estabelecimento, descrevendo sua função na rede de saúde, sua natureza jurídica e administrativa, e sua relação com o Sistema Único de Saúde. Essas variáveis são essenciais para classificar e agrupar os estabelecimentos em análises de políticas públicas.

### TP_UNID

- **Descrição:** Tipo de Unidade. Esta é uma das classificações mais importantes, pois define a finalidade principal do estabelecimento dentro da rede de saúde. A tabela de tipos de unidade é extensa e reflete a diversidade de serviços existentes, desde a atenção primária até a alta complexidade hospitalar.6
	 
- **Valores:** Campo numérico codificado. Uma tabela de domínio é necessária para sua interpretação.
	 

**Tabela 1: Tabela de Domínio para `TP_UNID` (Exemplos)**

|Código|Descrição|Fonte|
|---|---|---|
|01|POSTO DE SAÚDE|16|
|02|CENTRO DE SAÚDE / UNIDADE BÁSICA|16|
|04|POLICLÍNICA|16|
|05|HOSPITAL GERAL|16|
|07|HOSPITAL ESPECIALIZADO|16|
|15|UNIDADE MISTA|16|
|22|CONSULTÓRIO ISOLADO|6|
|36|CLÍNICA/CENTRO DE ESPECIALIDADE|16|
|62|CENTRAL DE REGULAÇÃO DE SERVIÇOS DE SAÚDE|19|
|74|POLO ACADEMIA DA SAÚDE|20|

### ESFERA_A

- **Descrição:** Esfera Administrativa. Indica a esfera de governo (Federal, Estadual, Municipal) à qual o estabelecimento público está subordinado, ou se é uma entidade Privada. **Nota Histórica Importante:** Este campo foi a principal variável para essa classificação até outubro de 2015. A partir de novembro de 2015, a variável `NAT_JUR`, mais granular e confiável, tornou-se a fonte primária para essa informação, sendo alimentada diretamente pela base da Receita Federal.21
	 
- **Valores:**
	 
	 - `01`: FEDERAL
		  
	 - `02`: ESTADUAL
		  
	 - `03`: MUNICIPAL
		  
	 - `04`: PRIVADA
		  
	 - `99`: NÃO INFORMADA
		  

### NATUREZA

- **Descrição:** Natureza da Organização. Campo legado que fornecia detalhes sobre a natureza da organização (ex: Administração Direta, Empresa Pública, Fundação Pública). Assim como `ESFERA_A`, sua utilização foi em grande parte substituída pela maior precisão e padronização da variável `NAT_JUR` a partir de 2015.12
	 
- **Valores:** Campo numérico codificado. Exemplo: `01` para "Administração Direta da Saúde (MS, SES, e SMS)".12
	 

### NAT_JUR

- **Descrição:** Natureza Jurídica. Este é o campo mais preciso e atual para identificar a constituição jurídico-institucional de um estabelecimento. Seus códigos e descrições são baseados na tabela oficial da Comissão Nacional de Classificação (CONCLA) e são atualizados por meio de um serviço de integração com a base de dados de CNPJ da Receita Federal do Brasil.25
	 
- **Valores:** Campo numérico codificado com centenas de valores possíveis, que podem ser agrupados em grandes categorias como Administração Pública, Entidades Empresariais, Entidades sem Fins Lucrativos, Pessoas Físicas e Organizações Internacionais.26
	 

A transição para o uso da `NAT_JUR` como fonte primária em novembro de 2015 representou um marco na qualificação dos dados do SUS. Antes dessa data, campos como `ESFERA_A` e `NATUREZA` eram preenchidos manualmente pelos gestores locais, um processo sujeito a erros e inconsistências.21 A automação via Receita Federal tornou a classificação mais objetiva e padronizada. Para um analista de dados, isso acarreta duas implicações profundas. Primeiro, os dados de

`NAT_JUR` a partir de 11/2015 são significativamente mais confiáveis. Segundo, qualquer análise de série histórica que cruze essa data deve ser feita com extrema cautela. Uma simples contagem de "hospitais filantrópicos" ao longo do tempo pode apresentar um salto ou queda abrupta em 2015, que não reflete uma mudança real na rede, mas sim o efeito da reclassificação sistêmica. Para mitigar esse viés, um pesquisador precisa desenvolver uma tabela de mapeamento ("de-para") para harmonizar os códigos das classificações antigas (`NATUREZA`, `ESFERA_A`) com a nova taxonomia da `NAT_JUR`, uma tarefa complexa que exige profundo conhecimento de ambas as estruturas.

### VINC_SUS

- **Descrição:** Vínculo com o SUS. Indica, por meio de um flag binário, se o estabelecimento possui algum tipo de vínculo formal com o Sistema Único de Saúde. Esse vínculo pode ser por se tratar de uma unidade pública ou por ter um contrato ou convênio para a prestação de serviços.8 É importante notar que a ausência de vínculo (
	 
	 `0`) não impede o cadastramento no CNES, que tem caráter universal.6
	 
- **Valores:**
	 
	 - `1`: Sim
		  
	 - `0`: Não
		  

### TP_PREST

- **Descrição:** Tipo de Prestador. Classifica o estabelecimento com base em sua natureza jurídica e relação com o SUS, sendo uma variável derivada que combina essas informações para facilitar a identificação do perfil do prestador de serviços.6
	 
- **Valores:**
	 
	 - `30`: PÚBLICO FEDERAL
		  
	 - `40`: PÚBLICO ESTADUAL
		  
	 - `50`: PÚBLICO MUNICIPAL
		  
	 - `61`: FILANTRÓPICO COM CNAS VÁLIDO
		  
	 - `20`: PRIVADO COM FINS LUCRATIVOS
		  
	 - `22`: PRIVADO OPTANTE PELO SIMPLES
		  
	 - `60`: PRIVADO SEM FINS LUCRATIVOS
		  
	 - `80`: SINDICATO
		  
	 - `99`: TIPO DE PRESTADOR NÃO INFORMADO
		  

### TPGESTAO

- **Descrição:** Tipo de Gestão. Indica o modelo de gestão do SUS no qual o município ou estado está habilitado, refletindo as responsabilidades pactuadas nas Comissões Intergestores. Essa classificação define quem é o principal responsável pela gestão e financiamento dos serviços de saúde no território.9
	 
- **Valores:**
	 
	 - `M`: MUNICIPAL
		  
	 - `E`: ESTADUAL
		  
	 - `D`: DUPLA
		  
	 - `S`: SEM GESTÃO
		  
	 - `Z`: NÃO INFORMADO
		  

## Seção 3: Organização Territorial e Operacional

Esta seção detalha o posicionamento do estabelecimento dentro da estrutura organizacional e geográfica da rede de saúde, além de descrever seu regime de funcionamento. Essas variáveis são cruciais para análises de planejamento regional e acesso a serviços.

### REGSAUDE

- **Descrição:** Região de Saúde. Código que identifica a Região de Saúde à qual o município do estabelecimento pertence. As Regiões de Saúde são o eixo estruturante do planejamento regional integrado do SUS, definidas para garantir a integralidade da atenção à saúde em um determinado espaço geográfico.8
	 
- **Valores:** Código alfanumérico, definido pelo Plano Diretor de Regionalização de cada estado.
	 

### MICR_REG

- **Descrição:** Microrregião de Saúde. Código que identifica a Microrregião de Saúde, que é uma subdivisão da Região de Saúde, utilizada para um planejamento mais detalhado.8
	 
- **Valores:** Código alfanumérico.
	 

### DISTRSAN

- **Descrição:** Distrito Sanitário. Código do Distrito Sanitário, que representa uma subdivisão territorial para a gestão da saúde dentro de um município. É uma estrutura comum em grandes centros urbanos para aproximar a gestão da realidade local.6
	 
- **Valores:** Código alfanumérico.
	 

### DISTRADM

- **Descrição:** Distrito Administrativo / Módulo Assistencial. Originalmente chamado de Distrito Administrativo, este campo atualmente designa o código do Módulo Assistencial, conforme o plano de regionalização local. É mais um nível de detalhamento da organização territorial da saúde.6
	 
- **Valores:** Código alfanumérico.
	 

### ATIVIDAD

- **Descrição:** Atividade de Ensino e Pesquisa. Indica se o estabelecimento de saúde possui uma política formal e atividades estruturadas de ensino (formação de profissionais de saúde) e/ou pesquisa científica.6
	 
- **Valores:**
	 
	 - `1`: Unidade de Ensino Superior
		  
	 - `2`: Unidade Auxiliar de Ensino
		  
	 - `3`: Unidade sem Atividade de Ensino
		  
	 - Outros códigos podem existir em dados históricos.
		  

### CLIENTEL

- **Descrição:** Fluxo de Clientela. Descreve a forma como os usuários acessam os serviços do estabelecimento, sendo um indicador chave do papel da unidade na rede de atenção.6
	 
- **Valores:**
	 
	 - `01`: Atendimento de demanda espontânea (unidade de "porta aberta")
		  
	 - `02`: Atendimento de demanda referenciada (recebe apenas pacientes encaminhados de outras unidades)
		  
	 - `03`: Atendimento de demanda espontânea e referenciada (modelo misto)
		  
	 - `00`: Fluxo de Clientela não exigido
		  
	 - `99`: Fluxo de Clientela não informado
		  

### TURNO_AT

- **Descrição:** Turno de Atendimento. Indica os períodos de funcionamento do estabelecimento, permitindo aferir a disponibilidade de serviços ao longo do dia.6
	 
- **Valores:**
	 
	 - `01`: ATENDIMENTO SOMENTE PELA MANHÃ
		  
	 - `02`: ATENDIMENTO SOMENTE À TARDE
		  
	 - `03`: ATENDIMENTO NOS TURNOS DA MANHÃ E À TARDE
		  
	 - `04`: ATENDIMENTO NOS TURNOS DA MANHÃ, TARDE E NOITE
		  
	 - `05`: ATENDIMENTO COM TURNOS INTERMITENTES
		  
	 - `06`: ATENDIMENTO CONTÍNUO DE 24 HORAS/DIA (PLANTÃO)
		  
	 - `07`: ATENDIMENTO SOMENTE À NOITE
		  

### NIV_HIER

- **Descrição:** Nível de Hierarquia. Classificação legada que posicionava o estabelecimento dentro de uma pirâmide hierárquica de complexidade do SUS. Embora o conceito de redes de atenção (RAS) seja hoje mais prevalente, esta variável ainda pode ser encontrada nos dados.6
	 
- **Valores:**
	 
	 - `01`: NH 1-PAB-PABA (Nível Hierárquico 1 - Atenção Básica)
		  
	 - `02` a `08`: Códigos para Média e Alta Complexidade Ambulatorial e Hospitalar.
		  

Os campos de organização territorial (`REGSAUDE`, `MICR_REG`, `DISTRSAN`, `DISTRADM`) são mais do que simples rótulos geográficos; eles representam os "nós" e os "elos" que compõem a Rede de Atenção à Saúde (RAS). A análise combinada desses campos com a variável `CLIENTEL` (fluxo de clientela) permite mapear e analisar os fluxos reais de pacientes dentro do sistema. Um analista pode utilizar esses dados para investigar questões complexas sobre a eficiência e a equidade da rede, como, por exemplo, se pacientes de uma microrregião com carência de serviços especializados estão sendo forçados a buscar atendimento em outras regiões de saúde, indicando um "vazio assistencial". Esse tipo de análise é fundamental para o planejamento regional, a alocação de recursos e a avaliação da integralidade do cuidado, superando em muito um simples mapeamento de estabelecimentos.

## Seção 4: Formalização: Contratos, Licenciamento e Finanças

Esta seção abrange os aspectos legais, contratuais e financeiros que formalizam a operação do estabelecimento, sendo particularmente relevante para unidades privadas e filantrópicas que prestam serviços ao SUS e, portanto, necessitam de regularização para faturamento e recebimento de repasses.

### CONTRATM / CONTRATE

- **Descrição:** Número do Contrato com o Gestor Municipal (`CONTRATM`) ou Estadual (`CONTRATE`). Armazena o número de identificação do contrato ou convênio firmado entre o estabelecimento e o gestor de saúde local para a prestação de serviços ao SUS.6
	 
- **Valores:** Campo alfanumérico.
	 

### DT_PUBLM / DT_PUBLE

- **Descrição:** Data de Publicação do Contrato Municipal (`DT_PUBLM`) ou Estadual (`DT_PUBLE`). Registra a data em que o respectivo contrato foi publicado em diário oficial, um requisito legal para sua validade e início de vigência.6
	 
- **Valores:** Data no formato `AAAAMMDD`.
	 

### ALVARA / DT_EXPED / ORGEXPED

- **Descrição:** Dados do Alvará Sanitário. Conjunto de campos que armazena o número do alvará de funcionamento sanitário (`ALVARA`), sua data de expedição (`DT_EXPED`) e o órgão emissor (`ORGEXPED`). A posse de um alvará válido é condição essencial para a operação legal de qualquer estabelecimento de saúde.6
	 
- **Valores:** Alfanuméricos e data.
	 

### RETENCAO

- **Descrição:** Código de Retenção de Tributos. Código que define o regime de retenção de tributos federais aplicável ao estabelecimento. Esta informação é crucial para fins fiscais e para o correto processamento do faturamento de serviços prestados ao SUS.8
	 
- **Valores:**
	 
	 - `10`: ESTABELECIMENTO PÚBLICO
		  
	 - `11`: ESTABELECIMENTO FILANTRÓPICO
		  
	 - `12`: ESTABELECIMENTO SEM FINS LUCRATIVOS
		  
	 - `13`: ESTABELECIMENTO PRIVADO LUCRATIVO SIMPLES
		  
	 - `14`: ESTABELECIMENTO PRIVADO LUCRATIVO
		  
	 - `15`: ESTABELECIMENTO SINDICAL
		  
	 - `16`: ESTABELECIMENTO PESSOA FÍSICA
		  
	 - `00`, `99`: RETENÇÃO NÃO INFORMADA
		  

### COD_IR

- **Descrição:** Código de Retenção de Tributos da Mantenedora. Análogo ao campo `RETENCAO`, mas aplicado à entidade mantenedora, quando o estabelecimento é do tipo "Mantido" (`NIV_DEP=3`).8
	 
- **Valores:** Códigos similares aos do campo `RETENCAO`.
	 

### CO_BANCO / CO_AGENC / C_CORREN

- **Descrição:** Dados Bancários. Conjunto de campos que registra o código do banco, da agência e o número da conta corrente do estabelecimento. Essas informações são utilizadas para o depósito dos repasses financeiros referentes aos serviços prestados ao SUS.6
	 
- **Valores:** Códigos numéricos e alfanuméricos.
	 

A presença de dados nos campos de contrato (`CONTRATM`, `DT_PUBLM`), licenciamento (`ALVARA`) e dados bancários (`CO_BANCO`) está diretamente associada à capacidade de um estabelecimento privado ou filantrópico faturar seus serviços junto ao SUS. Um estabelecimento com `VINC_SUS=1` mas sem um contrato válido (por exemplo, `CONTRATM` nulo ou `DT_PUBLM` com data expirada) representa uma inconsistência cadastral que pode levar à glosa (recusa de pagamento) de sua produção nos sistemas de faturamento (SIA/SIH).4 Para um auditor ou gestor, esses campos formam uma trilha de auditoria essencial, permitindo o cruzamento da base do CNES com os dados de pagamento do Fundo Nacional de Saúde para verificar se os repasses financeiros estão sendo direcionados a estabelecimentos com documentação regularizada.

## Seção 5: Avaliações, Qualificações e Programas de Incentivo

Esta seção contém um conjunto de variáveis que indicam a participação e o status do estabelecimento em diversos programas de qualidade, processos de acreditação e políticas de incentivo financeiro promovidas pelo Ministério da Saúde.

### AV_ACRED / CLASAVAL / DT_ACRED

- **Descrição:** Dados de Acreditação Hospitalar. Este conjunto de campos indica se o hospital participa de um programa de acreditação (`AV_ACRED`), qual a sua classificação ou nível de acreditação obtido (`CLASAVAL`) e a data em que a acreditação foi concedida (`DT_ACRED`).6
	 
- **Valores `CLASAVAL`:**
	 
	 - `1`: ACREDITADO NO NÍVEL 1
		  
	 - `2`: ACREDITADO NO NÍVEL 2
		  
	 - `3`: ACREDITADO NO NÍVEL 3
		  
	 - `0`: NÃO ATENDEU AOS PADRÕES MÍNIMOS
		  

### AV_PNASS / DT_PNASS

- **Descrição:** Avaliação PNASS. Indicam a participação (`AV_PNASS`) e a data (`DT_PNASS`) da avaliação do estabelecimento no âmbito do Programa Nacional de Avaliação dos Serviços de Saúde (PNASS), uma iniciativa para avaliar a qualidade dos serviços de saúde no país.6
	 
- **Valores:** Flags (Sim/Não) e data.
	 

### Bloco `GESPRG*` (Gestão de Programas)

- **Descrição:** Este bloco de campos (`GESPRG1E`, `GESPRG1M`, `GESPRG2E`, `GESPRG2M`, etc.) é destinado a registrar a adesão dos estabelecimentos a programas e políticas de saúde específicas, que são frequentemente transitórias. A letra final 'E' provavelmente se refere a programas de gestão Estadual, enquanto 'M' se refere a programas de gestão Municipal. A documentação detalhada para o significado de cada um desses campos é notavelmente escassa nos manuais gerais 7, pois seu conteúdo é definido por portarias e notas técnicas específicas de cada programa lançado pelo Ministério da Saúde.
	 
- **Valores:** Geralmente são flags (`1` para Sim, `0` para Não) ou códigos específicos definidos na legislação do programa.
	 

### NIVATE_A / NIVATE_H

- **Descrição:** Nível de Atenção Ambulatorial (`NIVATE_A`) e Hospitalar (`NIVATE_H`). Estes campos provavelmente detalham o nível de complexidade (Atenção Básica, Média Complexidade, Alta Complexidade) em que o estabelecimento atua, possivelmente vinculados aos programas registrados no bloco `GESPRG*`. Assim como os campos de programas, sua interpretação pode depender de documentação específica da época.22
	 
- **Valores:** Códigos numéricos ou de texto.
	 

A estrutura de campos genéricos como `GESPRG*` (e, como será visto na Seção 10, os campos `AP*`) reflete uma estratégia de design de banco de dados para acomodar a natureza dinâmica e mutável das políticas públicas de saúde. Em vez de adicionar novas colunas ao schema do banco de dados nacional a cada novo programa lançado — um processo tecnicamente complexo e custoso —, o sistema reutiliza esses campos pré-existentes. O Ministério da Saúde, ao lançar um novo programa, publica uma portaria ou nota técnica que especifica: "A adesão ao Programa X será registrada no campo `GESPRG2M` com o valor '1'". Anos depois, o programa pode ser descontinuado e o campo `GESPRG2M` pode ser "zerado" ou até mesmo reaproveitado para uma nova política. A implicação crítica para o pesquisador é que o significado desses campos **não é fixo no tempo**. Para analisar a adesão a um programa específico, é indispensável localizar a documentação oficial da época que define qual campo foi utilizado e quais eram seus códigos. Analisar a variável `GESPRG2M` ao longo de uma década sem esse contexto levará a conclusões metodologicamente falhas e sem sentido.

## Seção 6: Capacidade Instalada – Leitos (`QTLEIT*`)

Esta seção apresenta um inventário detalhado da quantidade e dos tipos de leitos existentes no estabelecimento. Essas variáveis são vitais para medir a capacidade de internação da rede hospitalar do país, sendo um dos conjuntos de dados mais consultados para o planejamento em saúde. A estrutura dos campos deriva diretamente da Ficha de Cadastro de Leitos (FCES).6

### Campos Agregadores

- **`QTLEITP1`**: Quantidade de Leitos de Internação. Soma dos leitos cirúrgicos, clínicos, obstétricos, pediátricos e de outras especialidades.
	 
- **`QTLEITP2`**: Quantidade de Leitos Complementares. Soma dos leitos de Unidade de Terapia Intensiva (UTI) e Unidade Intermediária (UI).
	 
- **`QTLEITP3`**: Quantidade de Leitos de Hospital Dia.
	 
- **`LEITHOSP`**: Total de Leitos Hospitalares. Soma de `QTLEITP1` e `QTLEITP2`.
	 

### Campos Detalhados (`QTLEIT05` a `QTLEIT40`)

Cada uma dessas variáveis representa a quantidade de leitos de uma especialidade ou tipo específico. Apresentar uma lista exaustiva seria repetitivo; em vez disso, a tabela abaixo decodifica as principais variáveis deste bloco, agrupando-as por tipo de leito para facilitar a compreensão.

**Tabela 2: Decodificação das Variáveis de Quantidade de Leitos (`QTLEIT*`)**

|Variável|Descrição do Leito|Tipo de Leito (Agrupamento)|Fonte|
|---|---|---|---|
|**`QTLEIT05`**|Cirurgia Geral|Cirúrgico|6|
|**`QTLEIT06`**|Ginecologia|Cirúrgico|6|
|**`QTLEIT07`**|Oftalmologia|Cirúrgico|6|
|**`QTLEIT08`**|Ortopedia/Traumatologia|Cirúrgico|6|
|**`QTLEIT09`**|Clínica Geral|Clínico|6|
|**`QTLEIT19`**|Obstetrícia Clínica|Obstétrico|6|
|**`QTLEIT20`**|Obstetrícia Cirúrgica|Obstétrico|6|
|**`QTLEIT21`**|Pediatria Clínica|Pediátrico|6|
|**`QTLEIT22`**|Pediatria Cirúrgica|Pediátrico|6|
|**`QTLEIT23`**|Saúde Mental|Clínico|6|
|**`QTLEIT32`**|UTI Adulto|Complementar|6|
|**`QTLEIT34`**|Unidade Intermediária Adulto|Complementar|6|
|**`QTLEIT38`**|UTI Pediátrica|Complementar|6|
|**`QTLEIT39`**|UTI Neonatal|Complementar|6|
|**`QTLEIT40`**|Unidade Intermediária Neonatal|Complementar|6|

## Seção 7: Capacidade Instalada – Instalações Físicas (`QTINST*`)

Esta seção quantifica a infraestrutura física de assistência do estabelecimento, como consultórios, salas de cirurgia e outros ambientes. Esses dados complementam a informação sobre leitos, oferecendo uma visão mais ampla da capacidade instalada. A estrutura desses campos também deriva da FCES.6

### Campos Detalhados (`QTINST01` a `QTINST37`)

Cada variável `QTINST*` representa a quantidade de um tipo específico de instalação física. A tabela a seguir decodifica as principais variáveis deste bloco, agrupando-as por área de assistência para fornecer um contexto funcional.

**Tabela 3: Decodificação das Variáveis de Quantidade de Instalações (`QTINST*`)**

|Variável|Descrição da Instalação|Agrupamento Funcional|Fonte|
|---|---|---|---|
|**`QTINST01`**|Consultórios - Clínicas Básicas|Ambulatório|6|
|**`QTINST02`**|Consultórios - Clínicas Especializadas|Ambulatório|6|
|**`QTINST03`**|Consultórios - Não Médicos|Ambulatório|6|
|**`QTINST04`**|Consultórios Odontológicos|Ambulatório|6|
|**`QTINST05`**|Sala de Repouso/Observação|Urgência / Ambulatório|6|
|**`QTINST06`**|Sala de Pequena Cirurgia|Urgência / Ambulatório|6|
|**`QTINST07`**|Sala de Curativos|Urgência / Ambulatório|6|
|**`QTINST08`**|Sala de Gesso|Urgência / Ambulatório|6|
|**`QTINST09`**|Sala de Nebulização/Inalação|Ambulatório|6|
|**`QTINST10`**|Sala de Enfermagem (Serviços)|Ambulatório|6|
|**`QTINST11`**|Sala de Cirurgia|Centro Cirúrgico|6|
|**`QTINST12`**|Sala de Recuperação Pós-Anestésica|Centro Cirúrgico|6|
|**`QTINST13`**|Sala de Parto Normal|Centro Obstétrico|6|
|**`QTINST14`**|Sala de Pré-Parto|Centro Obstétrico|6|
|**`QTINST15`**|Unidade Neonatal - Berçário|Unidade Neonatal|6|
|**`QTINST25`**|Sala de Imunização (Vacinação)|Ambulatório|6|
|**`QTINST31`**|Posto de Coleta de Leite Humano|Banco de Leite|6|
|**`QTINST34`**|Farmácia|Serviço de Apoio|6|

## Seção 8: Portfólio de Serviços e Atendimentos

Esta seção descreve os grandes grupos de atendimento que o estabelecimento oferece e detalha os Serviços de Apoio Diagnóstico e Terapêutico (SADT) disponíveis, sejam eles realizados internamente ou por terceiros.

### Indicadores de Modalidade de Atendimento

Estes campos são flags binários (Sim/Não) que indicam a presença de grandes áreas assistenciais no estabelecimento.

- **`URGEMERG`**: Possui Serviço de Urgência e Emergência.
	 
- **`ATENDAMB`**: Realiza Atendimento Ambulatorial.
	 
- **`CENTRCIR`**: Possui Centro Cirúrgico.
	 
- **`CENTROBS`**: Possui Centro Obstétrico.
	 
- **`CENTRNEO`**: Possui Centro Neonatal.
	 
- **`ATENDHOS`**: Realiza Atendimento Hospitalar (Internação).
	 
- **`SERAPOIO`**: Flag geral que indica a existência de algum Serviço de Apoio.
	 

### Bloco `SERAP*` (Serviços de Apoio)

Este bloco de variáveis (`SERAP01P` a `SERAP11T`) indica a oferta de SADT. O design desses campos é particularmente informativo: o sufixo `P` indica que o serviço é **Próprio**, enquanto o sufixo `T` indica que é **Terceirizado**.36

**Tabela 4: Decodificação das Variáveis de Serviços de Apoio (`SERAP*`)**

|Prefixo|Descrição do Serviço de Apoio|Fonte|
|---|---|---|
|**`SERAP01`**|Patologia Clínica / Análises Clínicas|6|
|**`SERAP02`**|Radiodiagnóstico (Ex: Raio-X, Ultrassom)|6|
|**`SERAP03`**|Hemoterapia|6|
|**`SERAP04`**|Medicina Nuclear|6|
|**`SERAP05`**|Anatomia Patológica e Citopatologia|6|
|**`SERAP06`**|Métodos Gráficos (Ex: ECG, EEG)|6|
|**`SERAP07`**|Métodos Ópticos (Ex: Endoscopia)|6|
|**`SERAP08`**|Radioterapia|6|
|**`SERAP09`**|Quimioterapia|6|
|**`SERAP10`**|Litotripsia|6|
|**`SERAP11`**|Fisioterapia / Reabilitação|6|

A distinção entre serviços próprios (`P`) e terceirizados (`T`) permite análises sofisticadas da estrutura do mercado de saúde. Um pesquisador pode identificar "hubs" de serviços (hospitais com muitos serviços `P`) e "spokes" (clínicas menores que dependem da terceirização). Essa análise pode revelar padrões regionais, como a predominância de terceirização em radiologia em certos estados, e pode ser correlacionada com a concentração de clínicas de diagnóstico independentes. Adicionalmente, permite avaliar a complexidade da gestão: um estabelecimento com muitos serviços `T` possui uma carga administrativa maior relacionada à gestão de contratos e fornecedores, o que constitui uma camada de análise de modelo de negócio e de rede que vai muito além de um simples inventário de serviços.

## Seção 9: Estrutura Interna: Comissões e Gestão de Resíduos

Esta seção aborda requisitos organizacionais internos, como a existência de comissões técnicas obrigatórias, e práticas de biossegurança, como a gestão de Resíduos de Serviços de Saúde (RSS).

### Bloco `COMISS*`

Este bloco de variáveis (`COMISS01` a `COMISS12`) utiliza flags para indicar a existência de comissões técnicas que são, em sua maioria, exigidas por legislação ou normas regulatórias para garantir a qualidade e a segurança da assistência.7 O campo

`COMISSAO` é um flag geral que indica se há pelo menos uma comissão ativa.

**Tabela 5: Decodificação das Variáveis de Comissões (`COMISS*`)**

|Variável|Descrição da Comissão|Fonte|
|---|---|---|
|**`COMISS01`**|Comissão de Ética Médica|6|
|**`COMISS02`**|Comissão de Ética de Enfermagem|6|
|**`COMISS03`**|Comissão de Farmácia e Terapêutica|6|
|**`COMISS04`**|Comissão de Controle de Infecção Hospitalar (CCIH)|6|
|**`COMISS05`**|Comissão de Apropriação de Custos|6|
|**`COMISS06`**|Comissão Interna de Prevenção de Acidentes (CIPA)|6|
|**`COMISS07`**|Comissão de Revisão de Prontuários|6|
|**`COMISS08`**|Comissão de Revisão de Documentação Médica e Estatística|6|
|**`COMISS09`**|Comissão de Análise de Óbito e Biópsias|6|
|**`COMISS10`**|Investigação Epidemiológica|6|
|**`COMISS11`**|Notificação de Doenças|6|
|**`COMISS12`**|Controle de Zoonoses e Vetores|6|

### Gestão de Resíduos de Serviços de Saúde (RSS)

- **`RES_BIOL`**: Indica a geração de Resíduo Biológico.
	 
- **`RES_QUIM`**: Indica a geração de Resíduo Químico.
	 
- **`RES_RADI`**: Indica a geração de Resíduo Radioativo.
	 
- **`RES_COMU`**: Indica a geração de Resíduo Comum.
	 
- **`COLETRES`**: Indica se há empresa especializada contratada para a coleta dos RSS.
	 

## Seção 10: Campos Específicos da Atenção Primária à Saúde (APS)

Esta seção contém um grande bloco de variáveis (`AP*CV*`) que, pela sua nomenclatura, parecem destinadas a detalhar aspectos específicos da Atenção Primária à Saúde (APS), também conhecida como Atenção Básica.

- **`ATEND_PR`**: Indica se o estabelecimento realiza Atendimento na Atenção Primária.
	 

### Bloco `AP01CV01` a `AP07CV07`

- **Descrição:** Este é o bloco de variáveis mais opaco da lista fornecida, com documentação pública detalhada sendo extremamente rara nos manuais gerais.7 A nomenclatura sugere uma estrutura matricial de dados.
	 
	 `AP` muito provavelmente significa "Atenção Primária". `CV` poderia ser uma abreviação para "Cobertura e Vínculo", "Característica da Visita" ou outro termo técnico da APS. A primeira série de números (`01` a `07`) pode representar diferentes tipos de equipes (ex: `01` para Equipe de Saúde da Família - eSF, `02` para Equipe de Saúde Bucal - eSB) ou programas específicos da APS. A segunda série de números (`01` a `07`) pode representar indicadores ou características monitoradas para cada tipo de equipe (ex: `01` para População Coberta, `02` para Número de Agentes Comunitários de Saúde, `03` para Carga Horária, etc.).
	 
- **Análise e Interpretação:** A análise precisa desses campos é inviável sem a documentação de referência correta. Para utilizá-los, é mandatório que o pesquisador localize as Notas Técnicas, Portarias ou Manuais específicos da Política Nacional de Atenção Básica (PNAB) que estavam em vigor na competência (`COMPETEN`) dos dados que estão sendo analisados. Esses documentos definirão o layout e o significado de cada campo `AP*CV*` para aquele período específico.
	 

## Seção 11: Campos Finais e Legado

- **`NAT_JUR`**: Este campo aparece novamente no final da lista de colunas fornecida. Trata-se muito provavelmente de uma duplicata ou um artefato da extração da lista de nomes de colunas do banco de dados. Sua definição e valores são idênticos aos do campo `NAT_JUR` descrito na Seção 2. Em qualquer análise, deve-se tratar este campo como redundante e utilizar a primeira ocorrência.
	 

## Anexo: Tabelas de Domínio Consolidadas

Este anexo fornece tabelas de referência rápida para a decodificação de variáveis categóricas chave que são frequentemente utilizadas em análises.

**Tabela A.1: Códigos de Vínculo com o SUS (`VINC_SUS`)**

|Código|Descrição|
|---|---|
|1|Sim, possui vínculo com o SUS|
|0|Não, não possui vínculo com o SUS|

**Tabela A.2: Códigos de Tipo de Gestão (`TPGESTAO`)**

|Código|Descrição|
|---|---|
|M|Gestão Municipal|
|E|Gestão Estadual|
|D|Gestão Dupla|
|S|Sem Gestão|
|Z|Não Informado|

**Tabela A.3: Códigos de Fluxo de Clientela (`CLIENTEL`)**

|Código|Descrição|
|---|---|
|01|Atendimento de demanda espontânea|
|02|Atendimento de demanda referenciada|
|03|Atendimento de demanda espontânea e referenciada|
|00|Fluxo de Clientela não exigido|
|99|Fluxo de Clientela não informado|

**Tabela A.4: Códigos de Turno de Atendimento (`TURNO_AT`)**

|Código|Descrição|
|---|---|
|01|Atendimento somente pela manhã|
|02|Atendimento somente à tarde|
|03|Atendimento nos turnos da manhã e à tarde|
|04|Atendimento nos turnos da manhã, tarde e noite|
|06|Atendimento contínuo de 24 horas/dia (Plantão)|
|07|Atendimento somente à noite|

**Tabela A.5: Códigos de Tipo de Prestador (`TP_PREST`)**

|Código|Descrição|
|---|---|
|30|Público Federal|
|40|Público Estadual|
|50|Público Municipal|
|61|Filantrópico com CNAS Válido|
|20|Privado com Fins Lucrativos|
|22|Privado Optante pelo Simples|
|60|Privado sem Fins Lucrativos|
|80|Sindicato|
|99|Não Informado|

**Tabela A.6: Códigos de Retenção de Tributos (`RETENCAO`)**

|Código|Descrição|
|---|---|
|10|Estabelecimento Público|
|11|Estabelecimento Filantrópico|
|12|Estabelecimento sem Fins Lucrativos|
|14|Estabelecimento Privado Lucrativo|
|00, 99|Retenção não informada|

# Dicionário de Dados Abrangente para o Módulo 'Acidentes por Animais Peçonhentos' do SINAN: Estrutura, Definições e Perspectivas Analíticas

## Introdução: Compreendendo a Estrutura de Dados do SINAN para a Vigilância Epidemiológica

O Sistema de Informação de Agravos de Notificação (SINAN) representa uma ferramenta central para a vigilância epidemiológica no Brasil. Sua função primordial é coletar, processar e disseminar dados sobre doenças e agravos de notificação compulsória, fornecendo subsídios essenciais para o planejamento, a avaliação e a tomada de decisão em saúde pública.1 Através da análise de seus dados, é possível monitorar a ocorrência de eventos de saúde, identificar populações e áreas de risco, e avaliar o impacto das intervenções.2

Os acidentes por animais peçonhentos constituem um agravo de grande relevância para a saúde pública no Brasil. A Organização Mundial da Saúde (OMS) os incluiu na lista de doenças tropicais negligenciadas, uma vez que acometem, majoritariamente, populações vulneráveis em áreas rurais.4 Em reconhecimento à sua importância epidemiológica, o agravo foi inserido na Lista de Notificação Compulsória (LNC) do Brasil em 2010, tornando seu registro obrigatório em todo o território nacional.4 Esta obrigatoriedade legal é o que fundamenta a existência e a abrangência da base de dados aqui detalhada.

Uma compreensão aprofundada desta base de dados exige o reconhecimento de sua estrutura de componentes duplos. O conjunto de dados final é uma fusão de variáveis provenientes de dois instrumentos distintos: a **Ficha Individual de Notificação (FIN)**, que contém campos padronizados comuns a todos os agravos notificáveis 1, e a

**Ficha de Investigação de Acidente por Animal Peçonhento**, que é específica para este agravo e detalha as circunstâncias do acidente, o quadro clínico e o tratamento.6 Portanto, a interpretação correta dos dados depende do uso combinado dos dicionários de dados correspondentes a cada uma dessas fichas.8

O fluxo de informação se inicia nas unidades de saúde locais, que preenchem as fichas, e segue para as bases de dados municipais, estaduais e, finalmente, a nacional.5 Neste processo, a qualidade dos dados é fundamental. Os dicionários do SINAN distinguem entre "Campo Obrigatório", cuja ausência impede a inserção do registro no sistema, e "Campo Essencial", que, embora não impeditivo, é vital para análises epidemiológicas e operacionais.9 A análise da completude e consistência desses campos é uma etapa crítica para qualquer pesquisador, especialmente considerando que desafios como a subnotificação, particularmente para certos tipos de acidentes, podem limitar a generalização dos achados.3

## Seção 1: Variáveis Centrais de Notificação e Identificação do Paciente (Campos da Ficha Individual de Notificação)

Esta seção detalha as variáveis padronizadas que formam a espinha dorsal de qualquer registro no SINAN, fornecendo o contexto demográfico, geográfico e temporal fundamental do caso. Estes campos são definidos no "Dicionário de Dados - Notificação Individual".8

### Tabela 1.1: Campos de Identificação da Notificação e do Sistema

|Variável|Nome Completo (do Dicionário)|Descrição e Valores Codificados|
|---|---|---|
|`TP_NOT`|Tipo de Notificação|Identifica o tipo de notificação. **Valores:** `1`–Negativa, `2`–Individual, `3`–Surto, `4`–Agregado. Para este conjunto de dados, o valor será quase invariavelmente `2`.8|
|`ID_AGRAVO`|Agravo|Código único para o problema de saúde notificado. Para este conjunto de dados, o código corresponde a "Acidente por Animais Peçonhentos".|
|`DT_NOTIFIC`|Data da Notificação|Data em que o caso foi oficialmente comunicado ao sistema de vigilância. Formato: DD/MM/AAAA.8|
|`SEM_NOT`|Semana Epidemiológica da Notificação|Semana epidemiológica correspondente à data da notificação, utilizada para análise de tendências temporais.|
|`NU_ANO`|Ano da Notificação|Ano da notificação.|
|`SG_UF_NOT`|UF da Notificação|Código da Unidade Federativa (UF) da unidade de saúde notificadora. Utiliza códigos do IBGE.|
|`ID_MUNICIP`|Município da Notificação|Código IBGE para o município da unidade de saúde notificadora.|
|`ID_REGIONA`|Regional de Saúde da Notificação|Código da regional de saúde da unidade notificadora.|
|`DT_SIN_PRI`|Data dos Primeiros Sintomas|Data em que o paciente apresentou os primeiros sintomas. Crucial para calcular o tempo até a busca por atendimento.|
|`SEM_PRI`|Semana Epidemiológica dos Primeiros Sintomas|Semana epidemiológica do início dos sintomas.|
|`DT_DIGITA`|Data de Digitação|Data em que o registro foi inserido pela primeira vez no sistema. É preenchida automaticamente e **não é atualizada** em caso de alterações posteriores no registro.8|

A presença de múltiplas variáveis de data (`DT_SIN_PRI`, `DT_NOTIFIC`, `DT_INVEST`, `DT_ENCERRA`) não é uma redundância, mas sim uma característica estrutural que permite uma avaliação sofisticada da performance do sistema de vigilância. A relação temporal entre esses campos funciona como um conjunto de indicadores de desempenho. Por exemplo, o intervalo entre a data dos primeiros sintomas e a data da notificação (`DT_NOTIFIC` - `DT_SIN_PRI`) mede a oportunidade da notificação, refletindo o tempo que o paciente levou para procurar o serviço de saúde e o tempo que o serviço levou para registrar o caso. Já o intervalo entre a notificação e o início da investigação (`DT_INVEST` - `DT_NOTIFIC`) mede a agilidade da resposta do sistema de saúde pública. A `DT_DIGITA`, por sua vez, é um metadado puramente administrativo, indicando o momento da entrada dos dados, e não deve ser confundida com datas de relevância clínica ou epidemiológica.8

### Tabela 1.2: Características Demográficas e Sociais do Paciente

|Variável|Nome Completo (do Dicionário)|Descrição e Valores Codificados|
|---|---|---|
|`ANO_NASC`|Ano de Nascimento|Ano de nascimento do paciente, frequentemente derivado do campo `dt_nascimento`.8|
|`NU_IDADE_N`|Idade|Idade do paciente. É um campo composto: o primeiro dígito indica a unidade de tempo (`1`: Hora, `2`: Dia, `3`: Mês, `4`: Ano) e os dígitos seguintes representam o valor (ex: `4025` = 25 anos).8|
|`CS_SEXO`|Sexo|Sexo do paciente. **Valores:** `M`–Masculino, `F`–Feminino, `I`–Ignorado.8|
|`CS_GESTANT`|Gestante|Status gestacional. **Valores:** `1`–1º Trimestre, `2`–2º, `3`–3º, `4`–Idade gestacional ignorada, `5`–Não, `6`–Não se aplica, `9`–Ignorado.8|
|`CS_RACA`|Raça/Cor|Raça/cor autodeclarada pelo paciente. **Valores:** `1`–Branca, `2`–Preta, `3`–Amarela, `4`–Parda, `5`–Indígena, `9`–Ignorado.8|
|`CS_ESCOL_N`|Escolaridade|Nível de instrução do paciente. Codificado de `0` (Analfabeto) a `8` (Superior completo), com `9` (Ignorado) e `10` (Não se aplica).8|
|`ID_OCUPA_N`|Ocupação|Ocupação do paciente, utilizando o código de 6 dígitos da Classificação Brasileira de Ocupações (CBO).9|

### Tabela 1.3: Dados de Geolocalização e Residência do Paciente

|Variável|Nome Completo (do Dicionário)|Descrição e Valores Codificados|
|---|---|---|
|`SG_UF`|UF de Residência|Unidade Federativa de residência do paciente. Utiliza códigos do IBGE.8|
|`ID_MN_RESI`|Município de Residência|Código IBGE do município de residência do paciente.8|
|`ID_RG_RESI`|Regional de Saúde de Residência|Código da regional de saúde de residência do paciente.|
|`ID_PAIS`|País de Residência|Código do país de residência do paciente.8|

A análise de variáveis como `ID_MUNICIP`, `ID_MN_RESI` e `ID_OCUPA_N` requer uma etapa de preparação de dados que não é imediatamente óbvia. Esses campos são armazenados como códigos numéricos (padrões IBGE e CBO) e, para se tornarem interpretáveis em uma análise (por exemplo, para mapear a incidência de acidentes ou identificar ocupações de alto risco), é indispensável que o analista vincule a base de dados do SINAN a tabelas de referência externas. A obtenção e fusão com as tabelas oficiais do IBGE (para municípios e UFs) e do Ministério do Trabalho (para a CBO) transforma esses códigos abstratos em variáveis categóricas ricas em significado, como "São Paulo" ou "Trabalhador Agropecuário", viabilizando análises geográficas e de risco ocupacional.8

## Seção 2: Antecedentes do Acidente e Detalhes da Investigação (Campos da Ficha de Investigação)

Esta seção foca nas circunstâncias específicas do acidente, que são cruciais para a identificação de fatores de risco, padrões de ocorrência e para a orientação de medidas de prevenção. Estes campos são definidos no "Dicionário de Dados - Acidente por Animais Peçonhentos".9

### Tabela 2.1: Campos de Cronologia e Localização da Investigação e do Acidente

|Variável|Nome Completo (do Dicionário)|Descrição e Valores Codificados|
|---|---|---|
|`DT_INVEST`|Data da Investigação|Data de início da investigação específica do caso. Deve ser ≥ `DT_NOTIFIC`.9|
|`ANT_DT_ACI`|Data do Acidente|Data em que o acidente ocorreu. Deve ser ≤ `DT_NOTIFIC`.9|
|`ANT_UF`|UF de Ocorrência|Estado onde o acidente ocorreu.9|
|`ANT_MUNIC_`|Município de Ocorrência do Acidente|Município onde o acidente ocorreu.9|
|`ANT_LOCALI`|Zona de Ocorrência|Zona onde o acidente ocorreu. **Valores:** `1`–Urbana, `2`–Rural, `3`–Periurbana, `9`–Ignorado.6|
|`ANT_TEMPO_`|Tempo Decorrido Picada/Atendimento|Intervalo de tempo entre o acidente e o primeiro atendimento médico. **Valores:** `1`–(0-1h), `2`–(1-3h), `3`–(3-6h), `4`–(6-12h), `5`–(12-24h), `6`–(>24h), `9`–Ignorado.9|
|`ANT_LOCA_1`|Local da Picada|Localização anatômica da picada/ferroada. **Valores:** `01`–Cabeça, `02`–Braço, `03`–Ante-Braço, `04`–Mão, `05`–Dedo da Mão, `06`–Tronco, `07`–Coxa, `08`–Perna, `09`–Pé, `10`–Dedo do Pé, `99`–Ignorado.9|

Dentro deste conjunto de variáveis, o campo `ANT_TEMPO_` possui um valor prognóstico excepcional. Ele representa um dos mais fortes preditores do desfecho clínico. A lógica fisiopatológica é direta: o veneno age ao longo do tempo, e a eficácia do soro antiveneno é máxima quando administrado precocemente, antes que danos teciduais e sistêmicos irreversíveis se instalem. Análises de dados de saúde pública confirmam que um maior tempo decorrido entre o acidente e o atendimento está diretamente correlacionado com uma maior gravidade do caso (`TRA_CLASSI`), um risco aumentado de complicações locais e sistêmicas (`COM_LOC`, `COM_SISTEM`), e uma maior letalidade (`EVOLUCAO`).13 Portanto, qualquer análise de desfecho pode ser estratificada por esta variável para quantificar o impacto do acesso rápido ao tratamento, reforçando a mensagem de saúde pública sobre a necessidade de procurar atendimento médico imediato.

## Seção 3: Manifestações Clínicas e Diagnóstico

Esta seção oferece uma análise granular das variáveis clínicas utilizadas para documentar o estado do paciente na sua apresentação ao serviço de saúde. Estes dados são essenciais para classificar a gravidade do envenenamento e para guiar a conduta terapêutica. Os campos são definidos na Ficha de Investigação e no seu respectivo dicionário.6

### Tabela 3.1: Indicadores e Detalhes das Manifestações Clínicas

|Variável|Nome Completo (do Dicionário)|Descrição e Valores Codificados|
|---|---|---|
|`MCLI_LOCAL`|Manifestações Locais|Indicador geral da presença de quaisquer sintomas locais. **Valores:** `1`–Sim, `2`–Não, `9`–Ignorado.6|
|`CLI_DOR`|Dor|Dor no local da picada. (Checkbox sob `MCLI_LOCAL`).|
|`CLI_EDEMA`|Edema|Inchaço no local da picada. (Checkbox sob `MCLI_LOCAL`).|
|`CLI_EQUIMO`|Equimose|Mancha roxa/descoloração no local. (Checkbox sob `MCLI_LOCAL`).|
|`CLI_NECROS`|Necrose|Morte tecidual. **Valores:** `1`–Sim, `2`–Não, `9`–Ignorado.6|
|`CLI_LOCAL_`|Outras Manifestações Locais|Indicador de outros sintomas locais não especificados. **Valores:** `1`–Sim, `2`–Não, `9`–Ignorado.9|
|`CLI_LOCA_1`|Especificar Outras Manifestações Locais|Campo de texto livre para descrever outros sintomas locais.9|
|`MCLI_SIST`|Manifestações Sistêmicas|Indicador geral da presença de quaisquer sintomas sistêmicos. **Valores:** `1`–Sim, `2`–Não, `9`–Ignorado.6|
|`CLI_NEURO`|Manifestações Neuroparalíticas|Ex: ptose palpebral, visão turva. (Checkbox sob `MCLI_SIST`).|
|`CLI_HEMORR`|Manifestações Hemorrágicas|Ex: sangramento gengival. (Checkbox sob `MCLI_SIST`).|
|`CLI_VAGAIS`|Manifestações Vagais|Ex: vômitos, diarreia. (Checkbox sob `MCLI_SIST`).|
|`CLI_MIOLIT`|Manifestações Miolíticas/Hemolíticas|Ex: mialgia, urina escura. (Checkbox sob `MCLI_SIST`).|
|`CLI_RENAL`|Manifestações Renais|Ex: oligúria/anúria. (Checkbox sob `MCLI_SIST`).|
|`CLI_OUTR_2`|Outras Manifestações Sistêmicas|Indicador de outros sintomas sistêmicos não especificados. **Valores:** `1`–Sim, `2`–Não, `9`–Ignorado.9|
|`CLI_OUTR_3`|Especificar Outras Manifestações Sistêmicas|Campo de texto livre para descrever outros sintomas sistêmicos.9|
|`CLI_TEMPO_`|Tempo de Coagulação|Resultado do teste de tempo de coagulação. **Valores:** `1`–Normal, `2`–Alterado, `9`–Não realizado.6|

A combinação das variáveis clínicas permite um poderoso diagnóstico sindrômico. Este é um pilar do manejo clínico, uma vez que exames laboratoriais para confirmação do tipo de veneno frequentemente não estão disponíveis ou não são realizados rotineiramente.13 A Ficha de Investigação é estruturada para capturar os dados que alimentam os algoritmos de decisão clínica. Por exemplo, um quadro com

`MCLI_LOCAL`=Sim, presença de `CLI_DOR`, `CLI_EDEMA` e `CLI_EQUIMO`, associado a `CLI_TEMPO_`=2 (Alterado), sugere fortemente um acidente **Botrópico** (causado por serpentes do gênero _Bothrops_, como a jararaca). Em contraste, um quadro com manifestações locais discretas ou ausentes (`MCLI_LOCAL`=Não/Leve), mas com manifestações sistêmicas proeminentes (`MCLI_SIST`=Sim), especialmente `CLI_NEURO`, aponta para um acidente **Crotálico** (cascavel) ou **Elapídico** (coral-verdadeira). Um analista pode reconstruir essas síndromes criando indicadores baseados em combinações dessas variáveis, permitindo estudos sobre o perfil clínico de diferentes envenenamentos.

Adicionalmente, a presença de campos de texto livre como `CLI_LOCA_1` e `CLI_OUTR_3` oferece flexibilidade para o registro de casos atípicos, mas impõe um desafio analítico significativo. Esses campos contêm informações valiosas que, para serem utilizadas em análises quantitativas, exigem técnicas de Processamento de Linguagem Natural (PLN) ou uma trabalhosa categorização manual, o que muitas vezes leva à sua subutilização.

## Seção 4: Classificação do Acidente, Tratamento e Soroterapia

Esta seção decodifica as variáveis relacionadas ao agente causador e à resposta médica, incluindo a administração crucial do soro antiveneno. Estes campos são definidos na Ficha de Investigação e em seu dicionário correspondente.6

### Tabela 4.1: Animal Causador e Classificação do Acidente

|Variável|Nome Completo (do Dicionário)|Descrição e Valores Codificados|
|---|---|---|
|`TP_ACIDENT`|Tipo de Acidente|Categoria principal do animal peçonhento. **Valores:** `1`–Serpente, `2`–Aranha, `3`–Escorpião, `4`–Lagarta, `5`–Abelha, `6`–Outros, `9`–Ignorado.6|
|`ANI_TIPO_1`|Outro Tipo de Animal|Campo de texto livre para especificar se `TP_ACIDENT` é `6` (Outros).9|
|`ANI_SERPEN`|Serpente - Tipo de Acidente|Especifica a síndrome de envenenamento por serpente. **Valores:** `1`–Botrópico, `2`–Crotálico, `3`–Elapídico, `4`–Laquético, `5`–Serpente Não Peçonhenta, `9`–Ignorado.6|
|`ANI_ARANHA`|Aranha - Tipo de Acidente|Especifica a síndrome de envenenamento por aranha. **Valores:** `1`–Foneutrismo, `2`–Loxoscelismo, `3`–Latrodectismo, `4`–Outra Aranha, `9`–Ignorado.6|
|`ANI_LAGART`|Lagarta - Tipo de Acidente|Especifica a síndrome de envenenamento por lagarta. **Valores:** `1`–Lonomia, `2`–Outra lagarta, `9`–Ignorado.6|
|`TRA_CLASSI`|Classificação do Caso|Gravidade clínica do caso. **Valores:** `1`–Leve, `2`–Moderado, `3`–Grave, `9`–Ignorado.6|

### Tabela 4.2: Administração de Soroterapia (Antiveneno)

A tabela a seguir mapeia as variáveis de contagem de ampolas aos tipos específicos de soro, uma inferência baseada nos nomes dos campos e nos soros listados nos manuais e fichas oficiais.6

|Variável|Tipo de Soro Inferido|Descrição|
|---|---|---|
|`CON_SOROTE`|Soroterapia|Foi administrado soro antiveneno? **Valores:** `1`–Sim, `2`–Não, `9`–Ignorado.6|
|`NU_AMPOLAS`|Soro Antibotrópico (SAB)|Número de ampolas de soro anti-Bothrops.|
|`NU_AMPOL_1`|Soro Antibotrópico-laquético (SABL)|Número de ampolas de soro anti-Bothrops-Lachesis.|
|`NU_AMPOL_8`|Soro Anticrotálico (SAC)|Número de ampolas de soro anti-Crotalus.|
|`NU_AMPOL_6`|Soro Antielapídico (SAE)|Número de ampolas de soro anti-Elapídico.|
|`NU_AMPOL_4`|Soro Antiaracnídico (SAAr)|Número de ampolas de soro anti-Aracnídeo.|
|`NU_AMPO_7`|Soro Antiescorpiônico (SAEsc)|Número de ampolas de soro anti-Escorpiônico.|
|`NU_AMPO_5`|Soro Antilonômico (SALon)|Número de ampolas de soro anti-Lonomia.|
|`NU_AMPOL_9`|Soro Antibotrópico-crotálico (SABC)|Número de ampolas de soro anti-Bothrops-Crotalus.|
|`NU_AMPOL_3`|Outro Soro|Número de ampolas de outro soro/não especificado.|

A combinação das variáveis `TRA_CLASSI` (Gravidade) com os campos `NU_AMPOL_X` (número de ampolas) é extremamente poderosa. Os manuais do Ministério da Saúde prescrevem um número específico de ampolas de soro com base no tipo de acidente e na sua gravidade.14 Um analista pode, portanto, comparar o número de ampolas registradas com o número recomendado para a classificação de cada caso. Este processo cria uma ferramenta de auditoria robusta para medir a adesão aos protocolos clínicos em diferentes regiões ou hospitais, identificando potenciais falhas no treinamento, na disponibilidade de recursos ou no julgamento clínico.

Além disso, esses dados formam a espinha dorsal da logística de saúde pública. A principal finalidade desta coleta detalhada é informar a gestão de estoques.3 Ao agregar o número e o tipo de ampolas de soro utilizadas (

`NU_AMPOL_X`) por município e estado, o Ministério da Saúde pode prever a demanda, gerenciar os estoques nacionais e garantir que os pontos estratégicos de distribuição de soro 16 estejam adequadamente abastecidos. A análise desses dados impacta diretamente a capacidade de salvar vidas, assegurando que o soro certo esteja no lugar certo e na hora certa.

## Seção 5: Evolução do Caso, Complicações e Encerramento

A seção final de dados detalha a trajetória clínica do paciente, incluindo quaisquer desfechos adversos e a conclusão administrativa do caso. Estes campos são definidos no dicionário de dados específico do agravo.9

### Tabela 5.1: Complicações

|Variável|Nome Completo (do Dicionário)|Descrição e Valores Codificados|
|---|---|---|
|`COM_LOC`|Complicações Locais|Indicador geral de complicações locais. **Valores:** `1`–Sim, `2`–Não, `9`–Ignorado.|
|`COM_SECUND`|Infecção Secundária|Infecção secundária no local da picada. (Subitem de `COM_LOC`).|
|`COM_NECROS`|Necrose Extensa|Morte tecidual extensa. (Subitem de `COM_LOC`).|
|`COM_COMPOR`|Síndrome Compartimental|Síndrome compartimental. (Subitem de `COM_LOC`).|
|`COM_DEFICT`|Déficit Funcional|Déficit/comprometimento funcional. (Subitem de `COM_LOC`).|
|`COM_APUTAC`|Amputação|Amputação. (Subitem de `COM_LOC`).|
|`COM_SISTEM`|Complicações Sistêmicas|Indicador geral de complicações sistêmicas. **Valores:** `1`–Sim, `2`–Não, `9`–Ignorado.|
|`COM_RENAL`|Insuficiência Renal|Insuficiência renal. (Subitem de `COM_SISTEM`).|
|`COM_EDEMA`|Insuficiência Respiratória/Edema Pulmonar|Insuficiência respiratória/edema pulmonar agudo. (Subitem de `COM_SISTEM`).|
|`COM_SEPTIC`|Septicemia|Sepse. (Subitem de `COM_SISTEM`).|
|`COM_CHOQUE`|Choque|Choque. (Subitem de `COM_SISTEM`).|
|`DOENCA_TRA`|Acidente Relacionado ao Trabalho|O acidente foi relacionado ao trabalho? **Valores:** `1`–Sim, `2`–Não, `9`–Ignorado.|

### Tabela 5.2: Desfecho Final do Caso e Encerramento

|Variável|Nome Completo (do Dicionário)|Descrição e Valores Codificados|
|---|---|---|
|`EVOLUCAO`|Evolução do Caso|O desfecho final do caso. **Valores:** `1`–Cura, `2`–Óbito por acidente por animais peçonhentos, `3`–Óbito por outras causas, `9`–Ignorado.|
|`DT_OBITO`|Data do Óbito|Data do óbito, se `EVOLUCAO` for 2 ou 3.|
|`DT_ENCERRA`|Data do Encerramento|Data em que o caso foi oficialmente encerrado no sistema. Deve ser ≥ `DT_INVEST`.|

O campo `EVOLUCAO` é mais sutil do que um simples binário de vivo/morto. Ele distingue criticamente entre o óbito devido ao envenenamento (código `2`) e o óbito por outras causas (código `3`). Essa distinção permite o cálculo de uma _taxa de letalidade_ precisa e atribuível ao agravo, que é um indicador epidemiológico muito mais significativo do que uma taxa de mortalidade bruta. Ao excluir do numerador os óbitos por causas não relacionadas, o sistema garante uma avaliação mais acurada da gravidade intrínseca dos envenenamentos.

Este conjunto final de variáveis permite ao analista completar a história epidemiológica. É possível construir modelos para responder a perguntas complexas, como: "Controlando por idade e comorbidades, qual é o impacto do tempo para atendimento (`ANT_TEMPO_`) e da soroterapia insuficiente (doses de `NU_AMPOLAS` abaixo do protocolo) nas chances de desenvolver insuficiência renal (`COM_RENAL`) ou de evoluir para óbito (`EVOLUCAO`=2) em pacientes com envenenamento crotálico (`ANI_SERPEN`=2)?". Isso demonstra o potencial completo do conjunto de dados para análises de fatores de risco multivariadas e sofisticadas.

## Conclusão: Uma Estrutura para a Ação em Saúde Pública Baseada em Dados

A jornada através do dicionário de dados do SINAN para acidentes por animais peçonhentos revela uma estrutura lógica e interconectada, projetada para espelhar o processo clínico e epidemiológico, desde a notificação inicial até o desfecho final do caso. Cada variável, de um simples código geográfico a um indicador clínico complexo, contribui para a construção de um panorama detalhado do agravo no país.

Uma compreensão profunda deste dicionário de dados capacita profissionais de saúde pública e pesquisadores a transcenderem as estatísticas descritivas simples (como o número de casos) e a realizarem estudos analíticos complexos.4 Torna-se possível identificar grupos de alto risco (

`ID_OCUPA_N`, `CS_RACA`), mapear focos geográficos (`ID_MN_RESI`, `ANT_MUNIC_`), avaliar os tempos de resposta do sistema de saúde (`ANT_TEMPO_`), auditar a prática clínica (`TRA_CLASSI` vs. `NU_AMPOLAS`) e, em última instância, formular políticas baseadas em evidências para prevenir acidentes e melhorar os desfechos dos pacientes.

Finalmente, é imperativo reforçar a importância da avaliação da qualidade dos dados. A completude dos "campos essenciais" e a consistência entre as variáveis são pré-requisitos para a geração de conclusões definitivas e confiáveis.10 O SINAN é uma ferramenta poderosa, mas seus resultados são tão confiáveis quanto os dados que o alimentam. O uso criterioso e informado deste rico conjunto de informações é fundamental para fortalecer a vigilância e o controle dos acidentes por animais peçonhentos no Brasil.](<Terminei a pesquisa. Fique à vontade para me fazer perguntas complememtares ou pedir alterações.

http://googleusercontent.com/immersive_entry_chip/0
\%3Cctrl94\%3Ethought
Here's a thinking process that could lead to the detailed explanation of the SINAN data:

1.  **Understand the User's Core Request:** The user has provided a large block of text which is the output of some kind of data processing script. The script is analyzing different datasets (called "agravos") from SINAN (Sistema de Informação de Agravos de Notificação) for the year 2023. For each "agravo," it lists a set of column names (variables). The user wants to know what each column means and what kind of values it can hold.

2.  **Initial Assessment & Strategy:**

      * **Scope:** This is a *massive* request. There are dozens of datasets, each with 50-150 columns. Explaining every single column in detail would result in an impractically long and overwhelming response.
      * **Problem:** The column names are abbreviated and cryptic (e.g., `TP_NOT`, `SG_UF_NOT`, `CS_RACA`). A direct translation isn't enough; context is crucial.
      * **Goal:** Provide a useful, understandable, and well-structured explanation without getting bogged down in every single variable. The best approach is to:
          * First, explain the overall structure and the common, recurring columns. This provides a foundational understanding.
          * Second, explain the *types* of columns and provide illustrative examples. This teaches the user *how to interpret* the column names themselves.
          * Third, offer to do a deep dive on a specific "agravo" if the user needs it. This makes the task manageable and more targeted to the user's actual needs.
          * Finally, provide a general explanation of the possible values (data types and formats).

3.  **Structuring the Response:** I'll break it down into logical sections:

      * **Section 1: Introduction & Overview:**

          * Start by acknowledging what the user provided: output from a script processing SINAN data.
          * Explain what SINAN is: the Brazilian Notifiable Diseases Information System. This is critical context. It's the primary tool for collecting and processing data on diseases and public health events in Brazil.
          * Explain what an "agravo" is in this context: a disease, health condition, or event of public health importance that requires mandatory notification (e.g., Dengue, Tuberculosis, work-related accidents).
          * Explain the output format: for each "agravo," the script lists the column headers (variables) from its specific database file (e.g., `ACBIBR23.dbf` for Acidente com Material Biológico in Brazil for 2023).

      * **Section 2: Decoding the Common Columns (The Foundation):**

          * Identify the columns that appear in almost *every* dataset. These are the boilerplate identification and demographic fields.
          * Go through them one by one, providing a clear explanation.
          * `TP_NOT`: Tipo de Notificação.
          * `ID_AGRAVO`: Identificador do Agravo.
          * `DT_NOTIFIC`: Data da Notificação.
          * `SEM_NOT`: Semana Epidemiológica da Notificação.
          * `NU_ANO`: Ano da Notificação.
          * `SG_UF_NOT`: Sigla da UF de Notificação.
          * `ID_MUNICIP`: Código do Município de Notificação (IBGE code).
          * `ID_UNIDADE`: Código da Unidade de Saúde (CNES code).
          * `ANO_NASC`: Ano de Nascimento do paciente.
          * `NU_IDADE_N`: Idade do paciente.
          * `CS_SEXO`: Sexo.
          * `CS_RACA`: Raça/Cor.
          * `CS_ESCOL_N`: Escolaridade.
          * `SG_UF` / `ID_MN_RESI`: UF e Município de Residência.
          * `ID_OCUPA_N`: Ocupação (using CBO - Classificação Brasileira de Ocupações).
          * `EVOLUCAO`: Evolução do caso (cura, óbito, etc.).
          * `DT_OBITO`: Data do Óbito.
          * `DT_ENCERRA`: Data de Encerramento do caso.
          * This section is crucial because it covers \~20-30% of the columns for many datasets and provides the user with immediate, high-value information.

      * **Section 3: Understanding the Prefixes and Suffixes (The "Secret Decoder Ring"):**

          * This is the most powerful part of the explanation. Instead of listing hundreds of columns, I'll teach the user the *pattern language* of the SINAN database.
          * Create a list of common prefixes and what they generally mean:
              * `DT_`: Data (Date) -\> Example: `DT_SIN_PRI` (Data dos Primeiros Sintomas).
              * `SG_` or `UF_`: Sigla de Unidade Federativa (State) -\> Example: `SG_UF_NOT`.
              * `ID_` or `CO_`: Identificador ou Código -\> Example: `ID_MUNICIP`.
              * `CS_`: Classificação ou Situação (Categorical) -\> Example: `CS_SEXO`.
              * `TP_`: Tipo -\> Example: `TP_NOT`.
              * `NU_`: Número -\> Example: `NU_ANO`.
              * `CLI_`: Clínico (Clinical Symptom) -\> Example: `CLI_FEBRE` (Presença de Febre).
              * `LAB_`: Laboratorial (Lab test/result) -\> Example: `LAB_IGM_R` (Resultado do IGM).
              * `ANT_`: Antecedentes (History) -\> Example: `ANT_TRATAD` (Tratamento Anterior).
              * `TRA_`: Tratamento (Treatment) -\> Example: `TRA_ESQUEM` (Esquema de Tratamento).
              * `OUTR_`: Outro (Other) -\> often paired with a text field for specifics.
              * `_DES` or `_ESP`: Descrição ou Especifique (Description/Specify).

      * **Section 4: Understanding the Possible Values (The Data Types):**

          * Explain the common data formats found in these columns.
          * **Códigos (Codes):** Many fields use numerical codes. Mention that these need to be cross-referenced with the official SINAN dictionary (Dicionário de Dados). Example: `CS_SEXO` might be `1` for Masculino, `2` for Feminino, `9` for Ignorado. `CS_RACA` will have codes for Branca, Preta, Parda, Amarela, Indígena. `EVOLUCAO` will have codes for Cura, Óbito por essa causa, Óbito por outra causa, etc.
          * **Datas (Dates):** Usually in `DD/MM/AAAA` or `YYYY-MM-DD` format.
          * **Sim/Não/Ignorado (Boolean-like):** Many clinical fields (`CLI_FEBRE`) or risk factors (`AGRAVALCOO`) use `1` for Sim, `2` for Não, `9` for Ignorado.
          * **Textos (Strings):** Fields ending in `_DES` or `_ESP` are free-text fields for specifying details.
          * **Números (Integers/Floats):** Like `NU_IDADE_N` (idade em anos/meses/dias) or `NU_AMPOLAS` (número de ampolas de soro).

      * **Section 5: Putting it all together with an Example:**

          * Pick one of the "agravos" from the user's list to demonstrate the decoding process. "SINAN - Acidente de trabalho (ACGR)" is a good choice because it's relatable and has a mix of common and specific columns.
          * Break down a few of its unique columns using the logic from Sections 2, 3, and 4.
              * `LOCAL_ACID`: Local do Acidente (codificado).
              * `CNAE`: Código Nacional de Atividade Econômica (da empresa).
              * `HORA_ACID`: Hora do Acidente.
              * `PART_CORP1`: Parte do Corpo Atingida 1 (codificado).
              * `CID_LESAO`: Código da Lesão pela CID-10.
              * `CAT`: Comunicação de Acidente de Trabalho (Sim/Não).

      * **Section 6: Conclusion and Call to Action:**

          * Summarize the key takeaway: the column names, while cryptic, follow a consistent logic.
          * Reiterate the offer to provide a detailed breakdown of a *specific* "agravo" if the user has a particular one they are interested in. This is a crucial step to manage the scope and provide targeted help.
          * Mention the importance of the official "Dicionário de Dados do SINAN" as the definitive source for codes and definitions. This empowers the user for future work.

4.  **Final Review:** Read through the entire response. Is it clear? Is the structure logical? Does it directly answer the user's question in a comprehensive yet manageable way? Is the tone helpful and expert? The structure looks good: from general to specific, from foundational knowledge to practical application, ending with an offer for more detail. This approach respects the user's time while providing a truly useful and educational answer.\<ctrl95\>Com certeza\! O resultado que você obteve é uma listagem dos "agravos" (doenças e eventos de saúde pública) disponíveis no **SINAN (Sistema de Informação de Agravos de Notificação)** e, para cada um, as colunas (variáveis) de seu respectivo banco de dados.

Compreender essas colunas é a chave para analisar os dados. Vou detalhar a lógica por trás dos nomes das colunas e os tipos de valores que elas podem assumir.

-----

### 1\. O que é o SINAN e um "Agravo"?

  * **SINAN:** É o principal sistema do Ministério da Saúde para coletar e processar dados sobre doenças e eventos de saúde que precisam ser monitorados no Brasil (notificação compulsória).
  * **Agravo:** É qualquer doença, condição ou evento de saúde pública que está na lista de notificação compulsória. Exemplos na sua lista são Tuberculose (`TUBE`), Dengue (`DENG`), Acidentes de Trabalho (`ACGR`), etc. Cada agravo tem uma ficha de notificação específica, que se traduz nessas colunas do banco de dados.

-----

### 2\. Decodificando as Colunas: A Lógica dos Nomes

Os nomes das colunas parecem códigos, mas eles seguem um padrão. Entender esse padrão permite decifrar a maioria deles.

#### **A. Colunas Comuns (Presentes em Quase Todos os Agravos)**

Estas são as colunas de identificação e demográficas básicas do paciente e da notificação.

| Coluna | O que Significa | Valores Possíveis (Exemplos) |
| :--- | :--- | :--- |
| `TP_NOT` | **Tipo de Notificação** | `2` (Individual), `3` (Surto), `4` (Agregado) |
| `ID_AGRAVO` | **Identificador do Agravo** | Um código para a doença. Ex: `A90` (Dengue), `B550` (Leish. Visceral) |
| `DT_NOTIFIC` | **Data da Notificação** | Data no formato `DD/MM/AAAA`. |
| `SEM_NOT` | **Semana Epidemiológica da Notificação** | Número de 1 a 53. Ex: `202330` (30ª semana de 2023). |
| `NU_ANO` | **Ano da Notificação** | `2023` |
| `SG_UF_NOT` | **Sigla da UF de Notificação** | `TO`, `SP`, `RJ`, etc. (Onde a notificação foi feita). |
| `ID_MUNICIP` | **Código do Município de Notificação** | Código IBGE de 7 dígitos. Ex: `1721000` (Palmas - TO). |
| `ID_UNIDADE` | **Código da Unidade de Saúde** | Código CNES da unidade que notificou. Ex: `1234567`. |
| `ANO_NASC` | **Ano de Nascimento** do Paciente | Ex: `1990`. |
| `NU_IDADE_N` | **Idade do Paciente** | Formato `4XXX` onde XXX é a idade em anos, `3XXX` em meses, etc. |
| `CS_SEXO` | **Sexo** | `M` (Masculino), `F` (Feminino), `I` (Ignorado). |
| `CS_RACA` | **Raça / Cor** | `1` (Branca), `2` (Preta), `3` (Amarela), `4` (Parda), `5` (Indígena), `9` (Ignorado). |
| `CS_ESCOL_N` | **Escolaridade** | Códigos de `0` a `10` (Analfabeto, Fundamental, Médio, Superior, etc.), `9` (Ignorado). |
| `SG_UF` | **Sigla da UF de Residência** | `TO`, `SP`, `RJ`, etc. (Onde o paciente mora). |
| `ID_MN_RESI` | **Código do Município de Residência** | Código IBGE de 7 dígitos. |
| `ID_OCUPA_N` | **Ocupação** | Código da CBO (Classificação Brasileira de Ocupações). |
| `EVOLUCAO` | **Evolução do Caso** | `1` (Cura), `2` (Óbito pela doença), `3` (Óbito por outra causa), `4` (Transferência), `9` (Ignorado). |
| `DT_OBITO` | **Data do Óbito** | Data no formato `DD/MM/AAAA`. |
| `DT_ENCERRA` | **Data de Encerramento do Caso** | Data no formato `DD/MM/AAAA`. |

#### **B. A Chave dos Prefixos e Sufixos**

A maioria das outras colunas pode ser entendida pelos seus prefixos:

  * **`DT_`**: Significa **Data**.

      * `DT_SIN_PRI`: Data dos Primeiros Sintomas.
      * `DT_DIAG`: Data do Diagnóstico.
      * `DT_INVEST`: Data da Investigação.

  * **`CLI_`**: Refere-se a um **Sinal Clínico**. Geralmente são perguntas de Sim/Não.

      * `CLI_FEBRE`: Paciente teve febre?
      * `CLI_TOSSE`: Paciente teve tosse?
      * `CLI_VOMITO`: Paciente teve vômito?
      * **Valores:** `1` (Sim), `2` (Não), `9` (Ignorado).

  * **`LAB_`**: Refere-se a um **Exame Laboratorial**.

      * `LAB_HEMA_N`: Realizou Hemograma?
      * `RESUL_PCR_`: Resultado do exame PCR.
      * **Valores:** Podem ser Sim/Não (`1`,`2`,`9`), resultado (`1`=Positivo, `2`=Negativo, `3`=Inconclusivo...), ou um valor numérico.

  * **`ANT_`**: Refere-se a **Antecedentes** (histórico do paciente).

      * `ANT_TRATAD`: Recebeu tratamento anterior?
      * `ANTEC_PRE`: Fez tratamento pré-exposição (ex: Raiva)?
      * **Valores:** Geralmente Sim/Não (`1`,`2`,`9`).

  * **`TRA_`**: Refere-se ao **Tratamento**.

      * `TRA_ESQUEM`: Esquema de tratamento utilizado (codificado).
      * `TRA_HOSP`: Houve hospitalização?
      * **Valores:** Geralmente códigos ou Sim/Não.

  * **`_DES` ou `_ESP`**: Sufixo que indica um campo de **Descrição** ou para **Especificar**.

      * `OUT_EXP_DE`: Descrição de "Outro tipo de exposição".
      * `OUTRO_ESP`: Especifique "Outros" sintomas.
      * **Valores:** Texto livre.

-----

### 3\. Exemplo Prático: Analisando um Agravo

Vamos usar o **`SINAN - Acidente de trabalho (ACGR)`** como exemplo para aplicar a lógica:

  * **`TP_NOT`, `DT_NOTIFIC`, `NU_IDADE_N`, `CS_SEXO`...**: Já sabemos que são colunas de identificação e demográficas.
  * **`DT_ACID`**: **Data do Acidente**.
  * **`LOCAL_ACID`**: **Local do Acidente**. Será um código (ex: `1`=Na própria empresa, `2`=A caminho do trabalho...).
  * **`CNAE`**: **Classificação Nacional de Atividades Econômicas**. É um código que identifica o ramo de atividade da empresa (ex: `8610101` para Atividades de atendimento hospitalar).
  * **`PART_CORP1`, `PART_CORP2`**: **Parte do Corpo Atingida 1, 2**. São campos codificados (ex: `1010`=Cabeça, `1042`=Mão direita...).
  * **`CID_LESAO`**: **Código da Lesão pela CID-10**. Usa a Classificação Internacional de Doenças (ex: `S61` - Ferimento do punho e da mão).
  * **`CAT`**: **Comunicação de Acidente de Trabalho (CAT)**. Pergunta se a CAT foi emitida.
      * **Valores:** `1` (Sim), `2` (Não), `9` (Ignorado).

