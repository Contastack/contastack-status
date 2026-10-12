# 📊 ContaStack Status Page

Página pública de estado y monitoreo en tiempo real para **ContaStack** alojada 100% en **GitHub Actions** y **GitHub Pages** mediante [Upptime](https://upptime.js.org).

- **URL de la página de estado:** [https://status.contastack.app](https://status.contastack.app)
- **Frecuencia de monitoreo:** Cada 5 minutos
- **Generación de gráficas:** Diaria

---

## 🚀 Despliegue en 3 Pasos

### 1. Crear el repositorio en GitHub
1. Crea un nuevo repositorio en tu cuenta u organización de GitHub (por ejemplo, `contastack-status`).
2. Sube los archivos de este directorio:
   ```bash
   cd contastack-status
   git init
   git add .
   git commit -m "feat: inicializar status page con Upptime"
   git branch -M main
   git remote add origin https://github.com/<tu-usuario>/contastack-status.git
   git push -u origin main
   ```

### 2. Configurar el Secreto `GH_PAT` (Personal Access Token)
Upptime necesita permisos para hacer commits automáticos en el historial de uptime y crear issues:
1. Ve a **GitHub** > **Settings** > **Developer settings** > **Personal access tokens** > **Tokens (classic)**.
2. Crea un nuevo token con alcances:
   - `repo` (Acceso completo a repositorios)
   - `workflow` (Actualizar flujos de trabajo de GitHub Actions)
3. Copia el token generado.
4. En tu repositorio `contastack-status`, ve a **Settings** > **Secrets and variables** > **Actions** > **New repository secret**.
5. Nombre: `GH_PAT`
6. Valor: *(Pega el token generado)*

### 3. Configurar el Dominio en DNS (`status.contastack.app`)
En tu proveedor de DNS (Cloudflare, Namecheap, etc.):
- **Tipo de registro:** `CNAME`
- **Nombre / Host:** `status`
- **Destino / Valor:** `<tu-usuario>.github.io`
- *(Si usas Cloudflare, activa inicialmente el modo "Solo DNS / Nube gris" para permitir que GitHub genere el certificado SSL gratis).*

### 4. Activar GitHub Pages
1. Ve a tu repositorio en GitHub > **Settings** > **Pages**.
2. En **Build and deployment** > **Source**, selecciona `Deploy from a branch`.
3. Rama: `gh-pages` / Directorio: `/ (root)`.
4. Una vez propagado el DNS, marca la casilla **Enforce HTTPS**.

---

## 🛠️ Servicios Monitoreados

| Servicio | Endpoint | Tipo |
| :--- | :--- | :--- |
| **🌐 Web Landing** | `https://contastack.app/` | HTTP 200 |
| **💻 Panel SaaS** | `https://app.contastack.app/` | HTTP 200 |
| **⚡ Core API & Base de Datos** | `https://contastack.app/api/health` | HTTP 200 (`operational`) |
| **🔐 Autenticación (Clerk)** | `https://contastack.app/sign-in` | HTTP 200 |
| **📊 Estado Global Clerk** | `https://status.clerk.com/` | HTTP 200 |
| **💳 Pasarela de Pagos (Polar.sh)**| `https://status.polar.sh/` | HTTP 200 |
| **🎫 Soporte y Chat en Vivo** | `https://contastack.app/api/tickets?ping=true` | HTTP 200 / 401 |
| **🖼️ Almacenamiento de Multimedia**| `https://contastack.app/api/media` | HTTP 200 |
| **🔒 Expiración de Certificados SSL**| `contastack.app` & `app.contastack.app` | Alerta programada a 14 días |
