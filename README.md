# Workflow n8n: Gemini DeepResearch → Perplexity → NotebookLM → ChatGPT

## Descripción

Este workflow automatiza un pipeline de investigación y análisis utilizando múltiples servicios de IA. El flujo procesa información desde Gemini DeepResearch, la enriquece con Perplexity, la estructura en NotebookLM y finaliza con un análisis mediante ChatGPT.

## Arquitectura del Workflow

```
Gemini DeepResearch → Perplexity → NotebookLM → ChatGPT
```

### Flujo de datos:
1. **Gemini DeepResearch**: Genera investigación inicial profunda
2. **Perplexity**: Complementa con información actualizada y verificación de datos
3. **NotebookLM**: Estructura y organiza la información en formato notebook
4. **ChatGPT**: Proporciona análisis final y síntesis

## Prerrequisitos

- n8n instalado y configurado
- Credenciales de API para cada servicio
- Node.js 16+ (para n8n)

## Configuración de Credenciales

### 1. Gemini DeepResearch API

**Obtener API Key:**
- Accede a [Google AI Studio](https://aistudio.google.com/)
- Genera una API Key para Gemini

**Configuración en n8n:**
```json
{
  "name": "Gemini DeepResearch",
  "type": "httpHeaderAuth",
  "data": {
    "name": "x-goog-api-key",
    "value": "TU_GEMINI_API_KEY"
  }
}
```

**Documentación API**: [Gemini API Documentation](https://ai.google.dev/docs/gemini_api_overview)

### 2. Perplexity API

**Obtener API Key:**
- Regístrate en [Perplexity API](https://www.perplexity.ai/hub/api)
- Obtén tu API key desde el dashboard

**Configuración en n8n:**
```json
{
  "name": "Perplexity",
  "type": "httpHeaderAuth",
  "data": {
    "name": "Authorization",
    "value": "Bearer TU_PERPLEXITY_API_KEY"
  }
}
```

**Documentación API**: [Perplexity API Documentation](https://docs.perplexity.ai/)

### 3. NotebookLM API

**Obtener API Key:**
- Accede a [Google AI Studio](https://aistudio.google.com/)
- Configura acceso a NotebookLM API

**Configuración en n8n:**
```json
{
  "name": "NotebookLM",
  "type": "httpHeaderAuth",
  "data": {
    "name": "Authorization",
    "value": "Bearer TU_NOTEBOOKLM_API_KEY"
  }
}
```

**Documentación API**: [NotebookLM API Documentation](https://ai.google.dev/docs)

### 4. OpenAI ChatGPT API

**Obtener API Key:**
- Crea cuenta en [OpenAI Platform](https://platform.openai.com/)
- Genera API key en API Keys section

**Configuración en n8n:**
```json
{
  "name": "OpenAI",
  "type": "httpHeaderAuth",
  "data": {
    "name": "Authorization",
    "value": "Bearer TU_OPENAI_API_KEY"
  }
}
```

**Documentación API**: [OpenAI API Documentation](https://platform.openai.com/docs/api-reference)

## Instalación

1. **Importar el workflow JSON**:
   ```bash
   # Descargar el archivo workflow JSON proporcionado
   # En n8n: Settings → Import from file → Seleccionar el archivo JSON
   # O copiar/pegar el contenido JSON directamente en el importador
   ```

2. **Configurar credenciales**:
   - Ve a `Settings → Credentials` en n8n
   - Agrega las credenciales para cada servicio según las configuraciones anteriores

3. **Verificar conexiones**:
   - Ejecuta cada nodo individualmente para verificar conectividad
   - Revisa que las credenciales estén correctamente configuradas

## Estructura del Workflow

### Nodos principales:

1. **Trigger Node**: Inicia el workflow (webhook, schedule, o manual)
2. **Gemini DeepResearch Node**: Investigación inicial
3. **Perplexity Node**: Verificación y enriquecimiento
4. **NotebookLM Node**: Estructuración de información
5. **ChatGPT Node**: Análisis final y síntesis

### Variables de entrada:
- `research_topic`: Tema de investigación
- `depth_level`: Nivel de profundidad (1-5)
- `output_format`: Formato de salida deseado

## Instrucciones de Uso

### Ejecución Manual

1. **Activar el workflow** desde la interfaz de n8n
2. **Proporcionar parámetros de entrada**:
   ```json
   {
     "research_topic": "Inteligencia Artificial en Healthcare",
     "depth_level": 3,
     "output_format": "comprehensive_report"
   }
   ```
3. **Ejecutar** y monitorear progreso en cada nodo

### Ejecución Automática (Webhook)

1. **Configurar webhook URL** en el trigger node
2. **Realizar petición POST**:
   ```bash
   curl -X POST https://tu-n8n-instance.com/webhook/research-workflow \
     -H "Content-Type: application/json" \
     -d '{
       "research_topic": "Blockchain en finanzas",
       "depth_level": 4,
       "output_format": "executive_summary"
     }'
   ```

### Programación automática

1. **Configurar Cron Trigger**:
   ```
   0 9 * * 1  # Todos los lunes a las 9:00 AM
   ```
2. **Definir temas predefinidos** en el nodo de configuración

## Configuración Avanzada

### Manejo de Errores

Cada nodo incluye manejo de errores con:
- Reintentos automáticos (3 intentos)
- Timeouts configurables
- Notificaciones en caso de fallo

### Optimización de Performance

- **Rate Limiting**: Respeta los límites de cada API
- **Caching**: Implementa cache para consultas repetidas
- **Parallel Processing**: Donde sea posible sin violar términos de servicio

### Monitoreo

- Logs detallados en cada paso
- Métricas de tiempo de ejecución
- Alertas por Slack/Email en caso de errores

## Troubleshooting

### Errores Comunes

1. **API Key inválida**:
   ```
   Error: 401 Unauthorized
   Solución: Verificar y regenerar API keys
   ```

2. **Rate Limit excedido**:
   ```
   Error: 429 Too Many Requests
   Solución: Implementar delays entre requests
   ```

3. **Timeout de conexión**:
   ```
   Error: Request timeout
   Solución: Aumentar timeout en configuración del nodo
   ```

## Recursos Adicionales

- [n8n Documentation](https://docs.n8n.io/)
- [Workflow Best Practices](https://docs.n8n.io/workflows/workflows/)
- [API Integration Guide](https://docs.n8n.io/integrations/)

## Soporte

Para reportar issues o solicitar mejoras:
1. Revisa la documentación de cada API
2. Verifica configuración de credenciales
3. Consulta logs de n8n para errores específicos

## Licencia

Este workflow está disponible bajo licencia MIT.

---

**Nota**: Asegúrate de cumplir con los términos de servicio de cada API utilizada y respeta los límites de rate limiting establecidos por cada proveedor.
