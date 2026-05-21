# Proxy Anthropic API para Dashboard Xtreme Growth AI

Este proxy permite que el dashboard en GitHub Pages llame al API de Claude sin exponer la API key.

## Deploy en Vercel — 5 minutos

### Paso 1: Sube los archivos a un repo de GitHub

Crea un repo nuevo, por ejemplo `xtreme-growth-claude-proxy`, y sube:
- `api/claude.js`
- `package.json`
- (este `README.md` opcional)

### Paso 2: Conecta el repo a Vercel

1. Ve a https://vercel.com (puedes loguearte con tu cuenta de GitHub — es gratis)
2. Click "Add New..." → "Project"
3. Selecciona el repo `xtreme-growth-claude-proxy`
4. Click "Import"
5. En la pantalla de configuración, **antes de deploy**, expande "Environment Variables" y agrega:
   - Name: `ANTHROPIC_API_KEY`
   - Value: tu API key real de Anthropic (la copias desde https://console.anthropic.com/settings/keys)
6. Click "Deploy"

### Paso 3: Copia la URL del deploy

Cuando termine, Vercel te dará una URL tipo:
```
https://xtreme-growth-claude-proxy.vercel.app
```

Tu endpoint queda en:
```
https://xtreme-growth-claude-proxy.vercel.app/api/claude
```

### Paso 4: Pásale la URL a Tatiana

Tatiana mete esa URL en el dashboard (un campo de configuración que ya quedó listo).

## Cómo obtener la API key de Anthropic

1. Ve a https://console.anthropic.com/
2. Crea cuenta o loguéate
3. Settings → API Keys → "Create Key"
4. Copia la key (empieza con `sk-ant-...`)
5. Pégala en la variable de entorno de Vercel (paso 2.5 arriba)

**Importante:** La API key NUNCA va en el HTML ni en el código del repo. Solo como variable de entorno en Vercel.

## Costo estimado

Cada llamada al botón "Generar Propuesta" usa ~1000 tokens. Con el modelo Claude Sonnet 4.5:
- Input: $3 / 1M tokens
- Output: $15 / 1M tokens
- Costo por llamada: ~$0.01-0.02

Para 100 generaciones en el webinar: ~$1-2 USD total.

Vercel free tier alcanza perfectamente — incluye 100GB de bandwidth/mes y functions ilimitadas.

## Si quieres probar localmente antes de deployar

```bash
npm install -g vercel
vercel dev
```

Y luego el endpoint queda en `http://localhost:3000/api/claude`.
