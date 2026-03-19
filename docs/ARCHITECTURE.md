# FertilityHub — Arquitetura Técnica

## 🏗️ Padrões de Engenharia

### Factory Pattern
```python
def create_app(env='development'):
    app = Flask(__name__)
    app.config.from_object(config_by_name[env])
    db.init_app(app)
    return app
blueprints/
├── auth/          # Autenticação + JWT
├── dashboard/     # Cockpit clínico
├── api/           # REST endpoints
└── pep/           # Prontuário eletrônico
RBAC (Role-Based Access Control)4 perfis com permissões específicas:
admin — Gestão completa
medica — Dashboard + PEP
secretaria — Agendamentos + cadastros
paciente — Consultas + histórico
📊 Modelos de DadosPaciente
  ├─ ciclos_reprodutivos: List[Ciclo]
  └─ agendamentos: List[Agendamento]

Ciclo (tipo: 'fiv' | 'iiu' | 'natural')
  ├─ status: 'ativo' | 'concluido' | 'cancelado'
  └─ data_inicio, data_fim

Agendamento
  ├─ data_hora
  └─ status: 'agendado' | 'realizado' | 'cancelado'🔌 API RESTPOST   /auth/login          # Login
GET    /api/pacientes       # Listar
POST   /api/pacientes       # Criar
GET    /pep/{id}            # Prontuário
POST   /pep/{id}/evolucao   # Evolução clínica🔐 Segurança
JWT tokens (expiry: 1 hora)
CSRF protection
Password hashing (werkzeug.security)
.env variables (nunca em código)
