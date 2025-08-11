# Injeção de SQL (SQLi)

## Descrição  
Injeção de SQL é uma vulnerabilidade que permite a um invasor manipular consultas ao banco de dados, possibilitando acesso não autorizado, modificação ou exclusão de dados sensíveis.

## Exemplo técnico  
Um atacante insere código SQL malicioso em campos de entrada, que é concatenado diretamente na consulta, alterando o comportamento esperado do banco, por exemplo:  

```sql
SELECT * FROM users WHERE username = 'admin' OR '1'='1';

## Impacto

- **Negócio:**  
  Exposição de dados confidenciais (senhas, dados financeiros), perdas financeiras, danos à reputação e multas regulatórias.

- **Técnico:**  
  Comprometimento da integridade e confidencialidade dos dados; possível escalonamento para controle do servidor.

## Prioridade

Alta, pois permite acesso e manipulação de dados críticos. Avaliar com CVSS ou SSVC para definir tratamento imediato.

## Mitigação

- Usar consultas parametrizadas/preparadas que separam dados e código.  
- Evitar concatenação direta de entrada do usuário em queries SQL.  
- Aplicar validação e sanitização rigorosa de entradas.  
- Implementar políticas de privilégio mínimo no banco.

## Plano de acompanhamento

- Revisar código e garantir a adoção de consultas parametrizadas.  
- Executar testes automatizados de injeção após cada release.  
- Monitorar logs para tentativas suspeitas de injeção.  
- Realizar auditorias periódicas no banco e aplicação.
