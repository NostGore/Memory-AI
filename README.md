# AI Chat Interface

Interfaz de chat AI universal y personalizable. Compatible con múltiples proveedores de inteligencia artificial.

## Características

- Diseño moderno con tema oscuro
- Compatible con múltiples proveedores de AI (11+ proveedores)
- Sistema de memoria para recordar conversaciones
- Animación de escritura con opción de skip
- Soporte para imágenes y documentos
- Renderizado de Markdown con bloques de código
- Responsive para móviles
- Menú hamburguesa en móvil con sidebar deslizante
- Selector de modelos con auto-selección
- Edición y regeneración de mensajes
- Copiar mensajes al portapapeles (sin formato markdown)
- Título animado con efecto typewriter
- Modal de preferencias con toggle de animación
- Persistencia de sesión al recargar la página
- Historial de conversaciones con auto-títulos

## Instalación

1. Clona el repositorio
2. Abre `index.html` en tu navegador
3. Configura tu API key en `env.json`

## Estructura del Proyecto

```
Memory-AI/
├── index.html      # Interfaz principal (HTML)
├── style.css       # Estilos CSS
├── script.js       # Lógica JavaScript
├── indicator.js    # System prompt y configuración de la IA
├── env.json        # Configuración de modelos y API keys
└── README.md       # Documentación
```

## Funcionalidades de la Interfaz

### Sidebar
- **Nuevo** - Inicia una nueva conversación
- **Preferencias** - Abre el modal de configuración (toggle de animación)
- **Documentación** - Enlace a documentación externa
- **Historial** - Lista de conversaciones anteriores con auto-títulos
- **Eliminar conversaciones** - Botón de eliminar por cada conversación
- **Iniciar sesión** - Botón en el footer

### Chat
- **Enviar mensajes** - Botón o tecla Enter
- **Editar mensajes** - Botón de lápiz que rellena el input para reenviar
- **Copiar mensajes** - Copia sin formato markdown con feedback visual
- **Regenerar** - Genera una nueva respuesta para el último mensaje
- **Skip** - Botón para saltar la animación de escritura
- **Me gusta / No me gusta** - Botones de feedback (UI)

### Animaciones
- **Typewriter** - Efecto de escritura variable (lento en puntos, rápido en espacios)
- **Título rotativo** - Cicla entre 4 frases con cursor parpadeante
- **Loading dots** - Puntos rebotantes mientras espera respuesta

### Archivos
- **Imágenes** - Vista previa de 60x60px con botón de eliminar
- **Documentos** - Icono azul con nombre del archivo (PDF, DOC, TXT)
- **Formatos aceptados**: `image/*`, `.pdf`, `.doc`, `.docx`, `.txt`

### Persistencia (localStorage)
- Conversaciones guardadas automáticamente
- Sesión restaurada al recargar la página
- Preferencia de animación persistida
- Vista actual (home/chat) restaurada

### Móvil (≤768px)
- Sidebar se convierte en panel deslizante
- Botón hamburguesa para abrir/cerrar
- Overlay oscuro al abrir sidebar
- Sidebar se cierra automáticamente al seleccionar opciones
- Input y mensajes adaptados al ancho del dispositivo

## Configuración

Edita el archivo `env.json` para agregar tus modelos:

```json
{
  "APIS-AI": {
    "nombre-del-modelo": {
      "name": "Nombre para mostrar",
      "host": "URL del endpoint",
      "key": "tu_api_key",
      "model": "model-id"
    }
  }
}
```

## Guía de Proveedores y Modelos

### Google Gemini

Gemini utiliza un endpoint específico por modelo. Cada modelo tiene su propia URL.

**Autenticación:** Header `X-goog-api-key`

| Modelo | Host | Model ID |
|--------|------|----------|
| Gemini Pro | `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent` | `gemini-pro` |
| Gemini Flash | `https://generativelanguage.googleapis.com/v1beta/models/gemini-flash-latest:generateContent` | `gemini-flash-latest` |
| Gemini 2.0 Flash | `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent` | `gemini-2.0-flash` |
| Gemini 1.5 Pro | `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-pro:generateContent` | `gemini-1.5-pro` |

**Ejemplo en env.json:**
```json
{
  "gemini-pro": {
    "name": "Gemini Pro",
    "host": "https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent",
    "key": "AIzaSyXXXXXXXXXXXXXXXXXXXXXX",
    "model": "gemini-pro"
  }
}
```

---

### Groq

Groq utiliza un endpoint universal. Cambias el model-id para usar diferentes modelos.

**Autenticación:** Bearer Token

**Host universal:** `https://api.groq.com/openai/v1/chat/completions`

| Modelo | Model ID |
|--------|----------|
| Llama 3.3 70B Versatile | `llama-3.3-70b-versatile` |
| Llama 3.1 8B Instant | `llama-3.1-8b-instant` |
| Mixtral 8x7B | `mixtral-8x7b-32768` |
| Gemma 2 9B | `gemma2-9b-it` |

**Ejemplo en env.json:**
```json
{
  "groq-llama": {
    "name": "Groq - Llama 3.3",
    "host": "https://api.groq.com/openai/v1/chat/completions",
    "key": "gsk_XXXXXXXXXXXXXXXXXXXXXX",
    "model": "llama-3.3-70b-versatile"
  }
}
```

---

### OpenAI

OpenAI utiliza un endpoint universal. Cambias el model-id para usar diferentes modelos.

**Autenticación:** Bearer Token

**Host universal:** `https://api.openai.com/v1/chat/completions`

| Modelo | Model ID |
|--------|----------|
| GPT-4o | `gpt-4o` |
| GPT-4o Mini | `gpt-4o-mini` |
| GPT-4 Turbo | `gpt-4-turbo` |
| GPT-3.5 Turbo | `gpt-3.5-turbo` |
| o1-preview | `o1-preview` |
| o1-mini | `o1-mini` |

**Ejemplo en env.json:**
```json
{
  "openai-gpt4o": {
    "name": "OpenAI - GPT-4o",
    "host": "https://api.openai.com/v1/chat/completions",
    "key": "sk-XXXXXXXXXXXXXXXXXXXXXX",
    "model": "gpt-4o"
  }
}
```

---

### Anthropic (Claude)

Anthropic utiliza un endpoint universal con headers especiales.

**Autenticación:** Header `x-api-key`

**Host universal:** `https://api.anthropic.com/v1/messages`

| Modelo | Model ID |
|--------|----------|
| Claude 3.5 Sonnet | `claude-3-5-sonnet-20241022` |
| Claude 3.5 Haiku | `claude-3-5-haiku-20241022` |
| Claude 3 Opus | `claude-3-opus-20240229` |
| Claude 3 Sonnet | `claude-3-sonnet-20240229` |
| Claude 3 Haiku | `claude-3-haiku-20240307` |

**Ejemplo en env.json:**
```json
{
  "anthropic-claude": {
    "name": "Claude 3.5 Sonnet",
    "host": "https://api.anthropic.com/v1/messages",
    "key": "sk-ant-XXXXXXXXXXXXXXXXXXXXXX",
    "model": "claude-3-5-sonnet-20241022"
  }
}
```

---

### Mistral AI

Mistral utiliza un endpoint universal.

**Autenticación:** Bearer Token

**Host universal:** `https://api.mistral.ai/v1/chat/completions`

| Modelo | Model ID |
|--------|----------|
| Mistral Large | `mistral-large-latest` |
| Mistral Medium | `mistral-medium-latest` |
| Mistral Small | `mistral-small-latest` |
| Mixtral 8x22B | `open-mixtral-8x22b` |
| Mixtral 8x7B | `open-mixtral-8x7b` |

**Ejemplo en env.json:**
```json
{
  "mistral-large": {
    "name": "Mistral Large",
    "host": "https://api.mistral.ai/v1/chat/completions",
    "key": "XXXXXXXXXXXXXXXXXXXXXX",
    "model": "mistral-large-latest"
  }
}
```

---

### DeepSeek

DeepSeek utiliza un endpoint universal.

**Autenticación:** Bearer Token

**Host universal:** `https://api.deepseek.com/chat/completions`

| Modelo | Model ID |
|--------|----------|
| DeepSeek Chat | `deepseek-chat` |
| DeepSeek Coder | `deepseek-coder` |

**Ejemplo en env.json:**
```json
{
  "deepseek-chat": {
    "name": "DeepSeek Chat",
    "host": "https://api.deepseek.com/chat/completions",
    "key": "XXXXXXXXXXXXXXXXXXXXXX",
    "model": "deepseek-chat"
  }
}
```

---

### OpenRouter

OpenRouter聚合多家 proveedor. Utiliza un endpoint universal.

**Autenticación:** Bearer Token

**Host universal:** `https://openrouter.ai/api/v1/chat/completions`

| Modelo | Model ID |
|--------|----------|
| Llama 3.3 70B | `meta-llama/llama-3.3-70b-instruct` |
| GPT-4o | `openai/gpt-4o` |
| Claude 3.5 Sonnet | `anthropic/claude-3.5-sonnet` |
| Gemini Pro | `google/gemini-pro-1.5` |

**Ejemplo en env.json:**
```json
{
  "openrouter-llama": {
    "name": "OpenRouter - Llama 3.3",
    "host": "https://openrouter.ai/api/v1/chat/completions",
    "key": "sk-or-XXXXXXXXXXXXXXXXXXXXXX",
    "model": "meta-llama/llama-3.3-70b-instruct"
  }
}
```

---

### Cohere

Cohere utiliza un endpoint universal.

**Autenticación:** Bearer Token

**Host universal:** `https://api.cohere.com/v2/chat`

| Modelo | Model ID |
|--------|----------|
| Command R+ | `command-r-plus` |
| Command R | `command-r` |
| Command | `command` |

**Ejemplo en env.json:**
```json
{
  "cohere-command": {
    "name": "Cohere - Command R+",
    "host": "https://api.cohere.com/v2/chat",
    "key": "XXXXXXXXXXXXXXXXXXXXXX",
    "model": "command-r-plus"
  }
}
```

---

### HuggingFace

HuggingFace utiliza un endpoint por modelo.

**Autenticación:** Bearer Token

**Host:** `https://api-inference.huggingface.co/models/{model-id}/v1/chat/completions`

| Modelo | Model ID |
|--------|----------|
| Llama 3.1 8B | `meta-llama/Meta-Llama-3.1-8B-Instruct` |
| Llama 3.1 70B | `meta-llama/Meta-Llama-3.1-70B-Instruct` |
| Mistral 7B | `mistralai/Mistral-7B-Instruct-v0.3` |
| Phi-3 | `microsoft/Phi-3-medium-4k-instruct` |

**Ejemplo en env.json:**
```json
{
  "huggingface-llama": {
    "name": "HuggingFace - Llama 3.1",
    "host": "https://api-inference.huggingface.co/models/meta-llama/Meta-Llama-3.1-8B-Instruct/v1/chat/completions",
    "key": "hf_XXXXXXXXXXXXXXXXXXXXXX",
    "model": "meta-llama/Meta-Llama-3.1-8B-Instruct"
  }
}
```

---

### Fireworks AI

Fireworks utiliza un endpoint universal con namespaces.

**Autenticación:** Bearer Token

**Host universal:** `https://api.fireworks.ai/inference/v1/chat/completions`

| Modelo | Model ID |
|--------|----------|
| Llama 3.3 70B | `accounts/fireworks/models/llama-v3p3-70b-instruct` |
| Llama 3.1 8B | `accounts/fireworks/models/llama-v3p1-8b-instruct` |
| Mixtral 8x22B | `accounts/fireworks/models/mixtral-8x22b-instruct` |
| Qwen 2.5 72B | `accounts/fireworks/models/qwen-v2p5-72b-instruct` |

**Ejemplo en env.json:**
```json
{
  "fireworks-llama": {
    "name": "Fireworks - Llama 3.3",
    "host": "https://api.fireworks.ai/inference/v1/chat/completions",
    "key": "fw_XXXXXXXXXXXXXXXXXXXXXX",
    "model": "accounts/fireworks/models/llama-v3p3-70b-instruct"
  }
}
```

---

### Perplexity

Perplexity utiliza un endpoint universal con modelos que incluyen búsqueda web.

**Autenticación:** Bearer Token

**Host universal:** `https://api.perplexity.ai/chat/completions`

| Modelo | Model ID | Descripción |
|--------|----------|-------------|
| Sonar Large Online | `sonar-large-online` | Con acceso a internet |
| Sonar Small Online | `sonar-small-online` | Rápido con internet |
| Sonar Large | `sonar-large` | Sin internet |
| Sonar Small | `sonar-small` | Rápido sin internet |

**Ejemplo en env.json:**
```json
{
  "perplexity-sonar": {
    "name": "Perplexity - Sonar",
    "host": "https://api.perplexity.ai/chat/completions",
    "key": "pplx_XXXXXXXXXXXXXXXXXXXXXX",
    "model": "sonar-large-online"
  }
}
```

---

### Together AI

Together AI utiliza un endpoint universal.

**Autenticación:** Bearer Token

**Host universal:** `https://api.together.xyz/v1/chat/completions`

| Modelo | Model ID |
|--------|----------|
| Llama 3.3 70B | `meta-llama/Llama-3.3-70B-Instruct-Turbo` |
| Llama 3.1 8B | `meta-llama/Meta-Llama-3.1-8B-Instruct-Turbo` |
| Mixtral 8x22B | `mistralai/Mixtral-8x22B-Instruct-v0.1` |

**Ejemplo en env.json:**
```json
{
  "together-llama": {
    "name": "Together - Llama 3.3",
    "host": "https://api.together.xyz/v1/chat/completions",
    "key": "XXXXXXXXXXXXXXXXXXXXXX",
    "model": "meta-llama/Llama-3.3-70B-Instruct-Turbo"
  }
}
```

---

### Replicate

Replicate utiliza un endpoint universal.

**Autenticación:** Bearer Token

**Host universal:** `https://api.replicate.com/v1/chat/completions`

**Ejemplo en env.json:**
```json
{
  "replicate-llama": {
    "name": "Replicate - Llama",
    "host": "https://api.replicate.com/v1/chat/completions",
    "key": "r8_XXXXXXXXXXXXXXXXXXXXXX",
    "model": "meta/meta-llama-3.1-8b-instruct"
  }
}
```

---

### Vertex AI (Google Cloud)

Vertex AI utiliza autenticación con API key de Google.

**Autenticación:** Header `X-goog-api-key`

**Ejemplo en env.json:**
```json
{
  "vertex-gemini": {
    "name": "Vertex AI - Gemini",
    "host": "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/gemini-2.0-flash:generateContent",
    "key": "AIzaSyXXXXXXXXXXXXXXXXXXXXXX",
    "model": "gemini-2.0-flash"
  }
}
```

---

### AWS Bedrock

Bedrock utiliza un endpoint universal.

**Autenticación:** Bearer Token

**Ejemplo en env.json:**
```json
{
  "bedrock-claude": {
    "name": "Bedrock - Claude",
    "host": "https://bedrock-runtime.us-east-1.amazonaws.com/model/anthropic.claude-3-5-sonnet-20241022-v2:0/invoke",
    "key": "XXXXXXXXXXXXXXXXXXXXXX",
    "model": "anthropic.claude-3-5-sonnet-20241022-v2:0"
  }
}
```

---

### Proveedor Compatible con OpenAI

Cualquier proveedor no listado se trata como compatible con OpenAI. Solo necesitas proporcionar la URL del endpoint y tu API key.

**Ejemplo en env.json:**
```json
{
  "custom-provider": {
    "name": "Mi Proveedor Custom",
    "host": "https://mi-proveedor.com/v1/chat/completions",
    "key": "tu_api_key",
    "model": "model-id"
  }
}
```

---

## Tipos de Autenticación

El sistema auto-detecta el tipo de autenticación según el host:

| Tipo | Proveedores | Header |
|------|-------------|--------|
| **Bearer Token** | OpenAI, Groq, Mistral, DeepSeek, OpenRouter, Cohere, HuggingFace, Fireworks, Perplexity, Together, Replicate, Bedrock | `Authorization: Bearer {key}` |
| **API Key Header** | Gemini, Vertex AI | `X-goog-api-key: {key}` |
| **Custom Header** | Anthropic | `x-api-key: {key}` |

## System Prompt

El system prompt está configurado en `indicator.js` con las siguientes reglas:

- Responder solo en español
- No mostrar proceso de pensamiento
- Usar markdown para formateo
- Memoria contextual (primeros 5 + últimos 45 mensajes)
- Limpiar respuestas en inglés automático

## Navegador

Funciona en todos los navegadores modernos:
- Chrome
- Firefox
- Safari
- Edge

## Licencia

Proyecto abierto para uso libre. Adapta como necesites.

## Créditos

- **zDxniel** - Desarrollador principal

Desarrollado como herramienta libre para la comunidad.

---

# English

## AI Chat Interface

Universal and customizable AI chat interface. Compatible with multiple artificial intelligence providers.

## Features

- Modern dark theme design
- Compatible with 11+ AI providers
- Memory system to remember conversations
- Typing animation with skip option
- Image and document upload support
- Markdown rendering with code blocks
- Fully responsive for mobile devices
- Hamburger menu with sliding sidebar on mobile
- Model selector with auto-selection
- Edit and regenerate messages
- Copy messages to clipboard (plain text, no markdown)
- Animated title with typewriter effect
- Preferences modal with animation toggle
- Session persistence on page reload
- Conversation history with auto-generated titles

## Installation

1. Clone the repository
2. Open `index.html` in your browser
3. Configure your API key in `env.json`

## Project Structure

```
Memory-AI/
├── index.html      # Main interface (HTML)
├── style.css       # CSS styles
├── script.js       # JavaScript logic
├── indicator.js    # System prompt and AI configuration
├── env.json        # Model and API key configuration
└── README.md       # Documentation
```

## Interface Features

### Sidebar
- **New** - Start a new conversation
- **Preferences** - Opens settings modal (animation toggle)
- **Documentation** - Link to external docs
- **History** - List of previous conversations with auto-titles
- **Delete conversations** - Delete button for each conversation
- **Login** - Button in footer

### Chat
- **Send messages** - Button or Enter key
- **Edit messages** - Pen icon fills input to resend
- **Copy messages** - Copies without markdown formatting with visual feedback
- **Regenerate** - Generates a new response for the last message
- **Skip** - Button to skip the typing animation
- **Like / Dislike** - Feedback buttons (UI)

### Animations
- **Typewriter** - Variable writing effect (slow on periods, fast on spaces)
- **Rotating title** - Cycles through 4 phrases with blinking cursor
- **Loading dots** - Bouncing dots while waiting for response

### Files
- **Images** - 60x60px preview thumbnail with remove button
- **Documents** - Blue icon with file name (PDF, DOC, TXT)
- **Accepted formats**: `image/*`, `.pdf`, `.doc`, `.docx`, `.txt`

### Persistence (localStorage)
- Conversations saved automatically
- Session restored on page reload
- Animation preference persisted
- Current view (home/chat) restored

### Mobile (≤768px)
- Sidebar becomes a sliding panel
- Hamburger button to open/close
- Dark overlay when sidebar is open
- Sidebar auto-closes when selecting options
- Input and messages adapted to screen width

## Configuration

Edit `env.json` to add your models:

```json
{
  "APIS-AI": {
    "model-name": {
      "name": "Display name",
      "host": "Endpoint URL",
      "key": "your_api_key",
      "model": "model-id"
    }
  }
}
```

## Provider Guide

### Google Gemini

Gemini uses a model-specific endpoint. Each model has its own URL.

**Authentication:** Header `X-goog-api-key`

| Model | Host | Model ID |
|--------|------|----------|
| Gemini Pro | `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent` | `gemini-pro` |
| Gemini Flash | `https://generativelanguage.googleapis.com/v1beta/models/gemini-flash-latest:generateContent` | `gemini-flash-latest` |
| Gemini 2.0 Flash | `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent` | `gemini-2.0-flash` |
| Gemini 1.5 Pro | `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-pro:generateContent` | `gemini-1.5-pro` |

---

### Groq

Groq uses a universal endpoint. Change the model-id to use different models.

**Authentication:** Bearer Token

**Universal Host:** `https://api.groq.com/openai/v1/chat/completions`

| Model | Model ID |
|--------|----------|
| Llama 3.3 70B Versatile | `llama-3.3-70b-versatile` |
| Llama 3.1 8B Instant | `llama-3.1-8b-instant` |
| Mixtral 8x7B | `mixtral-8x7b-32768` |
| Gemma 2 9B | `gemma2-9b-it` |

---

### OpenAI

OpenAI uses a universal endpoint. Change the model-id to use different models.

**Authentication:** Bearer Token

**Universal Host:** `https://api.openai.com/v1/chat/completions`

| Model | Model ID |
|--------|----------|
| GPT-4o | `gpt-4o` |
| GPT-4o Mini | `gpt-4o-mini` |
| GPT-4 Turbo | `gpt-4-turbo` |
| GPT-3.5 Turbo | `gpt-3.5-turbo` |
| o1-preview | `o1-preview` |
| o1-mini | `o1-mini` |

---

### Anthropic (Claude)

Anthropic uses a universal endpoint with special headers.

**Authentication:** Header `x-api-key`

**Universal Host:** `https://api.anthropic.com/v1/messages`

| Model | Model ID |
|--------|----------|
| Claude 3.5 Sonnet | `claude-3-5-sonnet-20241022` |
| Claude 3.5 Haiku | `claude-3-5-haiku-20241022` |
| Claude 3 Opus | `claude-3-opus-20240229` |
| Claude 3 Sonnet | `claude-3-sonnet-20240229` |
| Claude 3 Haiku | `claude-3-haiku-20240307` |

---

### Mistral AI

Mistral uses a universal endpoint.

**Authentication:** Bearer Token

**Universal Host:** `https://api.mistral.ai/v1/chat/completions`

| Model | Model ID |
|--------|----------|
| Mistral Large | `mistral-large-latest` |
| Mistral Medium | `mistral-medium-latest` |
| Mistral Small | `mistral-small-latest` |
| Mixtral 8x22B | `open-mixtral-8x22b` |
| Mixtral 8x7B | `open-mixtral-8x7b` |

---

### DeepSeek

DeepSeek uses a universal endpoint.

**Authentication:** Bearer Token

**Universal Host:** `https://api.deepseek.com/chat/completions`

| Model | Model ID |
|--------|----------|
| DeepSeek Chat | `deepseek-chat` |
| DeepSeek Coder | `deepseek-coder` |

---

### OpenRouter

OpenRouter aggregates multiple providers. Uses a universal endpoint.

**Authentication:** Bearer Token

**Universal Host:** `https://openrouter.ai/api/v1/chat/completions`

| Model | Model ID |
|--------|----------|
| Llama 3.3 70B | `meta-llama/llama-3.3-70b-instruct` |
| GPT-4o | `openai/gpt-4o` |
| Claude 3.5 Sonnet | `anthropic/claude-3.5-sonnet` |
| Gemini Pro | `google/gemini-pro-1.5` |

---

### Cohere

Cohere uses a universal endpoint.

**Authentication:** Bearer Token

**Universal Host:** `https://api.cohere.com/v2/chat`

| Model | Model ID |
|--------|----------|
| Command R+ | `command-r-plus` |
| Command R | `command-r` |
| Command | `command` |

---

### HuggingFace

HuggingFace uses a model-specific endpoint.

**Authentication:** Bearer Token

**Host:** `https://api-inference.huggingface.co/models/{model-id}/v1/chat/completions`

| Model | Model ID |
|--------|----------|
| Llama 3.1 8B | `meta-llama/Meta-Llama-3.1-8B-Instruct` |
| Llama 3.1 70B | `meta-llama/Meta-Llama-3.1-70B-Instruct` |
| Mistral 7B | `mistralai/Mistral-7B-Instruct-v0.3` |
| Phi-3 | `microsoft/Phi-3-medium-4k-instruct` |

---

### Fireworks AI

Fireworks uses a universal endpoint with namespaces.

**Authentication:** Bearer Token

**Universal Host:** `https://api.fireworks.ai/inference/v1/chat/completions`

| Model | Model ID |
|--------|----------|
| Llama 3.3 70B | `accounts/fireworks/models/llama-v3p3-70b-instruct` |
| Llama 3.1 8B | `accounts/fireworks/models/llama-v3p1-8b-instruct` |
| Mixtral 8x22B | `accounts/fireworks/models/mixtral-8x22b-instruct` |
| Qwen 2.5 72B | `accounts/fireworks/models/qwen-v2p5-72b-instruct` |

---

### Perplexity

Perplexity uses a universal endpoint with models that include web search.

**Authentication:** Bearer Token

**Universal Host:** `https://api.perplexity.ai/chat/completions`

| Model | Model ID | Description |
|--------|----------|-------------|
| Sonar Large Online | `sonar-large-online` | With internet access |
| Sonar Small Online | `sonar-small-online` | Fast with internet |
| Sonar Large | `sonar-large` | Without internet |
| Sonar Small | `sonar-small` | Fast without internet |

---

### Together AI

Together AI uses a universal endpoint.

**Authentication:** Bearer Token

**Universal Host:** `https://api.together.xyz/v1/chat/completions`

| Model | Model ID |
|--------|----------|
| Llama 3.3 70B | `meta-llama/Llama-3.3-70B-Instruct-Turbo` |
| Llama 3.1 8B | `meta-llama/Meta-Llama-3.1-8B-Instruct-Turbo` |
| Mixtral 8x22B | `mistralai/Mixtral-8x22B-Instruct-v0.1` |

---

### Replicate

Replicate uses a universal endpoint.

**Authentication:** Bearer Token

**Universal Host:** `https://api.replicate.com/v1/chat/completions`

---

### Vertex AI (Google Cloud)

Vertex AI uses Google API key authentication.

**Authentication:** Header `X-goog-api-key`

---

### AWS Bedrock

Bedrock uses a universal endpoint.

**Authentication:** Bearer Token

---

### OpenAI-Compatible Provider

Any unlisted provider is treated as OpenAI-compatible. Just provide the endpoint URL and your API key.

## Authentication Types

The system auto-detects the authentication type based on the host:

| Type | Providers | Header |
|------|-----------|--------|
| **Bearer Token** | OpenAI, Groq, Mistral, DeepSeek, OpenRouter, Cohere, HuggingFace, Fireworks, Perplexity, Together, Replicate, Bedrock | `Authorization: Bearer {key}` |
| **API Key Header** | Gemini, Vertex AI | `X-goog-api-key: {key}` |
| **Custom Header** | Anthropic | `x-api-key: {key}` |

## System Prompt

The system prompt is configured in `indicator.js` with the following rules:

- Respond only in Spanish
- Do not show thinking process
- Use markdown for formatting
- Contextual memory (first 5 + last 45 messages)
- Auto-clean English responses

## Browser Support

Works in all modern browsers:
- Chrome
- Firefox
- Safari
- Edge

## License

Open source for free use. Adapt as needed.

## Credits

- **zDxniel** - Lead developer

Built as a free tool for the community.
