# 💰 Nexmove — Plataforma Financeira Digital

Plataforma de gestão financeira pessoal e empresarial (PF/PJ) em formato single-page app.

## 🚀 Deploy

Publicado via **GitHub Pages** ou **Netlify**.

### Opção 1 — GitHub Pages (grátis, automático)
1. Vá em **Settings → Pages**
2. Em **Source**, selecione `main` branch e pasta `/ (root)`
3. Clique em **Save**
4. Acesse: `https://seu-usuario.github.io/nexmove`

### Opção 2 — Netlify (domínio customizado)
1. Acesse [netlify.com](https://netlify.com)
2. Clique em **Add new site → Import from Git**
3. Conecte seu repositório GitHub
4. Build command: *(vazio)*
5. Publish directory: `.`
6. Deploy!

## ⚙️ Configurar Supabase

Após acessar o app, vá em **Configurações → Supabase** e cole:
- **Project URL**: `https://xxxx.supabase.co`  
- **Anon Key**: `eyJ...`

### SQL para criar a tabela
```sql
CREATE TABLE IF NOT EXISTS lancamentos (
  id         BIGSERIAL PRIMARY KEY,
  user_email TEXT NOT NULL,
  tipo       TEXT NOT NULL,
  categoria  TEXT,
  descricao  TEXT,
  valor      NUMERIC(12,2) DEFAULT 0,
  status     TEXT,
  data_comp  DATE,
  data_pag   DATE,
  obs        TEXT,
  criado_em  TIMESTAMPTZ DEFAULT now()
);
ALTER TABLE lancamentos ENABLE ROW LEVEL SECURITY;
CREATE POLICY "acesso_total" ON lancamentos FOR ALL USING (true) WITH CHECK (true);
GRANT ALL ON lancamentos TO anon;
GRANT USAGE, SELECT ON SEQUENCE lancamentos_id_seq TO anon;
```

## 📱 Mobile
Funciona como PWA — no iPhone: **Compartilhar → Adicionar à Tela de Início**

## 🛡️ Funcionalidades
- Cadastro/login com hash de senha (SHA-256)
- Bloqueio após 5 tentativas erradas
- Dashboard com gráficos (Chart.js)
- Lançamentos com filtros
- Orçamento, DRE, Investimentos
- Consultoria com IA
- Planejamento Tributário (PJ)
- Integração Supabase (persistência em nuvem)
- Exportação Excel (SheetJS)
