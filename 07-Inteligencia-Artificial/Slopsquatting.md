# Slopsquatting

**Publicado em: 30 de julho de 2025**

**Público-alvo:** Profissionais de TI, de estudantes a administradores de sistemas.
**Objetivo:** Fornecer uma referência prática e didática sobre essa amaeaça emergente.

## Introdução

Com a presença emergente da IA, no auxílio e produção de códigos, para aumento de produtividade e redução de tempo de execução de projetos, as ameaças produzidas pela IA, começams vir a tona e tornar o ambiente de produção potencialmente inseguro sem o devido conhecimento das ameaças trazidas pela IA. 
---

## Seção 1: O que É Slopsquatting?

É um vulnerabilidade criada pela IA, de mesmo estilo do typosquatting - técnica em que cibercriminosos registram pacotes ou bibliotecas com nomes parecidos com os originais (ex: expres ao invés de express), esperando que o progrmador cometa o erro de digitação.
O Slopquatting, é uma evolução dessa vulnerabilidade, tendo como origem a IA, explorando as "alucinações" delas.

### 1.1 Exploração da Alucinação

Modelos de linguagens generativas, por muitas vezes, inventam dados com total convicção de que são reais. Na alucinação, uma IA pode gerar um bloco de código perfeitamente lógico e coerente, porém, que dependa de um pacote ou biblioteca que simplesmente não exista, "alucinando" um nome fictício de pacote, que pareça ser coerente na resolução do problema na programação.

### 1.2 Fluxo de Ataque

1. **A IA Sugere:** O desenvolvedor pede a IA, para gerar o código. A IA, porsua vez, retorna o código com alguma dependência de biblioteca pacote, incluindo no código a instalação, como ``npm install pacote-fantasma-necessario``.
2.  **O Criminoso Estuda e Age:** Os criminosos estudam o comprtamente de alucinação de IAs populares, que são utilizadas no auxílio de desenvolvimento de códigos, identificando "pacotes fantasmas" mais comumente geradas por elas. Com o reconhecimento desse padrão, os criminosos, criam repositório públicos em distribuidores de pacotes ou bibliotecas oficiais como PyPI(Python) ou npm(JavaScript), tendo nesses repositório, o código malicioso. 
3.  **O Desenvolvedor Instala:** O desenvolvedor, seja por confiança no código gerado pela IA, ou pela falta de verificação do conteúdo, utiliza o comando no terminal da máquina. Ao fazer isso, ele instala o malware diretamente no equipamento utilizado para o desenvolvimento.

### 1.3 Como Realizar a Mitigação
- **Revisão de Código:** Revisão do código, um ato simples, que nunca pode ser deixado de lado. A verificação de bibliotecas ou pacotes no código gerado pela IA é essencial: O pacote existe? É popular? É conhecido? Foi criado recentemente? Possui manutenção ativa? Consulte nos repositórios oficiais sempre essas informações. 
- **Execução em Ambientes Isolados:** Uma prática de segurança fundamental. Teste comandos e códigos gerados por IA em ambientes contidos, como um contêiner Docker ou uma VM efêmera. Se o pacote for malicioso, o dano fica restrito a esse ambiente, sem comprometer sua máquina ou a rede da empresa.
- **Adoção de Scanners de Vulnerabilidade SBOM:** Integre ferramentas que escaneiam suas dependências em busca de vulnerabilidades conhecidas. O uso de um SBOM (Software Bill of Materials) também é crucial, pois cria um inventário de todos os componentes do seu software, facilitando a auditoria e o rastreamento da origem de cada pacote.
- **Nunca confie cegamente em uma IA:** Premissa básica para essa e todas futuras vulnerabilidades geradas por IA.

## Conclusão
O Slopsquatting é um lembrete claro de que, à medida que integramos a IA em nossos processos, nossas estratégias de segurança precisam evoluir junto. A resolução de dependências não pode ser vista apenas como uma conveniência; ela é um ponto crítico de segurança que exige um fluxo auditável e consciente.