# ADR: Remoção de Checkpoint.writes no LangGraph

## Status
Decidido e implementado

## Contexto

O sistema utiliza "checkpoints" para gerenciar o estado dos agentes durante a execução. A propriedade `Checkpoint.writes` existia como parte da estrutura de checkpoint, permitindo o rastreamento de operações de escrita realizadas durante a execução do grafo. No entanto, essa funcionalidade apresentava algumas questões arquiteturais que impactavam a simplicidade e eficiência do sistema.

### Problemas Identificados:
- **Complexidade desnecessária**: A propriedade `writes` adicionava uma camada extra de complexidade ao modelo de checkpoint
- **Overhead de performance**: O rastreamento de todas as operações de escrita criava overhead adicional
- **Modelo de dados redundante**: A informação capturada por `writes` poderia ser derivada de outras partes do estado do checkpoint

## Decisão

Foi decidido remover completamente a propriedade `Checkpoint.writes` da estrutura de checkpoint do LangGraph.

### Mudanças Implementadas:
1. Remoção da propriedade `writes` de `Checkpoint`
2. Simplificação dos métodos de serialização/deserialização
3. Atualização de toda a documentação relacionada
4. Refatoração de testes que dependiam desta funcionalidade

## Consequências

### Positivas:
- **Simplicidade**: O modelo de checkpoint torna-se mais simples e direto
- **Performance**: Redução do overhead de memória e processamento
- **Manutenibilidade**: Código mais limpo e fácil de manter

### Negativas:
- **Quebras devido às mudanças**: Aplicações existentes que dependam de `Checkpoint.writes` precisarão ser atualizadas
- **Migração necessária**: Checkpoints existentes precisarão ser migrados para o novo formato

---

**Data**: Junho de 2025
**PR**: [#4822](https://github.com/langchain-ai/langgraph/pull/4822)
