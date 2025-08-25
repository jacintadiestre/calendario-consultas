# 📧 Configuración de EmailJS para Envío Real de Correos

## 🎯 Resumen
Tu calendario ya está preparado para enviar emails reales. Solo necesitas configurar EmailJS (servicio gratuito) siguiendo estos pasos:

## 📝 Pasos para Configurar EmailJS

### 1. Crear cuenta en EmailJS
1. Ve a [https://www.emailjs.com](https://www.emailjs.com)
2. Haz clic en "Sign Up" y crea tu cuenta gratuita
3. Confirma tu email

### 2. Conectar tu servicio de email
1. En el dashboard, ve a "Email Services"
2. Haz clic en "Add New Service"
3. Selecciona tu proveedor (Gmail, Outlook, etc.)
4. Sigue las instrucciones para conectar tu cuenta
5. **Anota el Service ID** que aparece (ejemplo: `service_0b8dssr`)

### 3. Crear templates de email

#### Template de Confirmación:
1. Ve a "Email Templates" → "Create New Template"
2. **MUY IMPORTANTE:** En la configuración del template:
   - **To email:** Debe usar `{{to_email}}` o `{{email}}` o `{{user_email}}`
   - **To name:** Debe usar `{{to_name}}`
3. Usa estos campos en tu template:

**Subject:** `✅ Consulta confirmada - Prof. {{professor_name}}`

**Content:**
```
Estimado/a {{student_name}},

Su horario de consulta ha sido CONFIRMADO:

📅 Fecha: {{reservation_date}}
⏰ Hora: {{reservation_time}} - {{reservation_end_time}}
📍 Lugar: {{location}}
👥 Acompañante: {{has_companion}} {{#has_companion}}({{companion_name}}){{/has_companion}}

Tema a consultar: {{consultation_topic}}

Saludos,
{{professor_name}}
```

3. Guarda el template y **anota el Template ID** (ejemplo: `template_confirm`)

#### Template de Cancelación:
1. Crear otro template similar para cancelaciones
2. **Anota el Template ID** (ejemplo: `template_cancel`)

### 4. Obtener Public Key
1. Ve a "Account" → "General"
2. Copia tu **Public Key** (ejemplo: `pk_abc123xyz`)

### 5. Configurar el código
En el archivo `calendario-reservas.html`, encuentra las líneas 812-817 y reemplaza:

```javascript
const EMAILJS_CONFIG = {
    publicKey: 'TU_PUBLIC_KEY_AQUI',      // ← Tu Public Key
    serviceID: 'TU_SERVICE_ID_AQUI',      // ← Tu Service ID
    templateConfirm: 'template_confirm',   // ← Template ID de confirmación
    templateCancel: 'template_cancel'      // ← Template ID de cancelación
};
```

### 6. Configurar tu email de respuesta
En la línea 1268, reemplaza:
```javascript
reply_to: 'jacinta.diestre@gmail.com' // ← Tu email real
```

## 🎉 ¡Listo!
Una vez configurado, cuando confirmes reservas desde el panel admin:
1. Se enviará un email real al estudiante
2. Aparecerá "📧 Enviando..." en el botón
3. Recibirás confirmación de envío exitoso

## 🆓 Plan Gratuito
EmailJS incluye **200 emails gratis por mes**, perfecto para consultas académicas.

## 🔧 Solución de Problemas
- Si no funciona, revisa la consola del navegador (F12 → Console)
- Verifica que todos los IDs estén correctos
- Asegúrate de que tu servicio de email esté conectado

## 📞 Alternativa Temporal
Si no quieres configurar EmailJS ahora, el sistema seguirá funcionando en "modo simulación" (los emails aparecen en consola pero no se envían).
