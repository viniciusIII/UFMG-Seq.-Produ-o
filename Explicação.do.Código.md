# UFMG-Seq.Produção

Problema de sequenciamento em máquina única para minimizar a soma dos atrasos ponderados (1||∑w_jT_j)

Objetivo do código: implementar Branch and Bound eficiente, com relaxação do problema de transporte e visualização da árvore

## Estruturas básicas

- Classe Job: modela tarefa com id, tempo, prazo, peso
- Classe Node: representa nó na árvore, sequência construída de trás para frente, controla jobs fixados, restantes, lower bound, poda, etc

## Lógica do Branch and Bound

- Cálculo do custo real de uma sequência completa (calculate_weighted_tardiness)
- Relaxação do problema de transporte para jobs restantes (solve_transportation_relaxation): encaixe otimista, gera lower bound eficiente
- Cálculo do lower bound de cada nó (calculate_lower_bound): soma custo real dos jobs fixados e custo relaxado dos restantes
- Expansão dos nós (expand_node): para cada job restante, cria filho, calcula lower bound, verifica se é solução completa e se é a melhor até agora
- Poda: se lower bound não é melhor que o melhor valor já encontrado, nó é podado e não expandido
  Possibilidade de usar o lema 3.6.1 para evitar gerar nós dominados

## Execução do algoritmo (solve)

- Inicializa com nó raiz
- Expande sempre o nó com menor lower bound (best-first search)
- Imprime progresso: nós explorados, podados, filhos gerados
- Retorna melhor sequência e valor ótimo ao final

## Exemplo de execução

- Instância exemplo com 6 jobs
- Mostra sequência ótima, valor ótimo, detalhes dos jobs (tempo, atraso, custo), estatísticas (nós criados, podados, soluções completas)

## Validação por força bruta

- Gera todas as permutações possíveis
- Compara resultado com Branch and Bound para garantir correção
