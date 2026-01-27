# Instruções para Agentes de IA - tech-python-auth2

## Visão Geral do Projeto

Este é um projeto de implementação de autenticação OAuth2 em Python desenvolvido para fins educacionais na Alura.

## Arquitetura Principal

### Estrutura Esperada (quando implementada)
- **app/**: Aplicação principal Flask/FastAPI
  - `auth/`: Lógica de autenticação OAuth2
  - `routes/`: Endpoints da API
  - `models/`: Modelos de dados
  - `config.py`: Configurações de ambiente
- **tests/**: Testes unitários e de integração
- **requirements.txt**: Dependências Python

### Fluxo de Autenticação OAuth2
1. Redirecionamento para provedor (Google, GitHub, etc.)
2. Callback com authorization code
3. Troca de code por token de acesso
4. Validação e armazenamento de sessão
5. Acesso a recursos protegidos

## Padrões e Convenções do Projeto

### Python
- Python 3.10+
- Usar `venv` para ambiente virtual (localizado em `./venv`)
- Dependências listadas em `requirements.txt`

### Estrutura de Código
- Separar lógica de autenticação em módulos específicos (`auth/`)
- Usar variáveis de ambiente para dados sensíveis (client_id, client_secret, etc.)
- Implementar tratamento de erros específico para fluxos OAuth2

### Padrões de Segurança
- **State Parameter**: Sempre incluir parâmetro `state` para prevenir CSRF
- **HTTPS**: Código deve suportar HTTPS em produção
- **Token Validation**: Validar tokens antes de conceder acesso
- **Scope Limiting**: Solicitar apenas escopos necessários do provedor

## Fluxo de Desenvolvimento

### Ambiente de Desenvolvimento
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# ou venv\Scripts\activate para Windows
pip install -r requirements.txt
```

### Execução
- Rodar servidor local: `flask run` ou `uvicorn main:app --reload`
- Usar variáveis de ambiente via `.env` (use `.env.example` como referência)

### Testes
- Framework: `pytest`
- Localização: `tests/` directory
- Executar: `pytest` ou `pytest tests/`
- Cobertura: Verificar com `pytest --cov=app tests/`

## Integração com Provedores OAuth2

### Configuração Típica
- Cada provedor requer: `client_id`, `client_secret`, `redirect_uri`
- Usar variáveis de ambiente (não hard-code em código)
- Implementar tratamento específico por provedor conforme necessário

### Exemplos de Provedores
- Google: OpenID Connect
- GitHub: OAuth2 padrão
- Microsoft: Azure AD
- Custom: Qualquer servidor OAuth2 compatível

## Pontos-Chave para IA

1. **Variáveis Sensíveis**: Sempre usar `os.environ` ou bibliotecas como `python-dotenv`
2. **Validação de State**: Verificar correspondência entre state enviado e recebido
3. **Erros de Rede**: Implementar retry logic para chamadas HTTP para provedores
4. **Token Refresh**: Lidar com expiração de tokens e refresh
5. **Logout**: Implementar revogação de tokens quando suportado

## Recursos Relacionados

- [RFC 6749 - OAuth 2.0 Authorization Framework](https://tools.ietf.org/html/rfc6749)
- [OpenID Connect Core](https://openid.net/specs/openid-connect-core-1_0.html)
- Documentação específica de cada provedor OAuth2 sendo integrado
