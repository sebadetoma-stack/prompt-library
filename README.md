# 📝 Prompt Library

> Organizá, guardá y sincronizá tus prompts de IA en la nube

[![Live Demo](https://img.shields.io/badge/demo-live-success)](https://sebadetoma-stack.github.io/prompt-library/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

Una aplicación web progresiva (PWA) para gestionar tus prompts de IA con sincronización en tiempo real, variables dinámicas y plantillas predefinidas.

![Prompt Library Screenshot](screenshot.png)

## ✨ Características

### 🔧 Funcionalidades Core
- **Sincronización en la nube** - Firebase Firestore para sync automática entre dispositivos
- **Variables dinámicas** - Usa `{variable}` en tus prompts y completá al copiar
- **Plantillas predefinidas** - Resumir, traducir, analizar, reescribir, SEO, y más
- **Organización inteligente** - Categorías, etiquetas, favoritos, búsqueda avanzada
- **Compartir prompts** - Genera links para compartir prompts específicos
- **Dashboard con estadísticas** - Total de prompts, más usados, recientes, etc.

### 💡 Productividad
- **Atajos de teclado** - `Ctrl+B` nuevo, `Ctrl+P` plantillas, `Ctrl+F` buscar
- **Vista compacta/normal** - Toggle para ver más prompts en pantalla
- **Búsqueda con highlighting** - Resalta palabras buscadas en amarillo
- **Duplicar prompts** - Copia y modifica rápidamente
- **Exportar/Importar** - Backup completo en formato JSON
- **Contador de caracteres** - Control de longitud en tiempo real

### 🎨 UX/UI
- **Modo oscuro** - Toggle automático según preferencia del sistema
- **Diseño responsive** - Optimizado para mobile y desktop
- **PWA** - Instalable como app nativa
- **Offline-first** - Funciona sin conexión

## 🚀 Demo

Probá la app en vivo: [https://sebadetoma-stack.github.io/prompt-library/](https://sebadetoma-stack.github.io/prompt-library/)

## 📦 Instalación

### Como usuario

1. Abrí [https://sebadetoma-stack.github.io/prompt-library/](https://sebadetoma-stack.github.io/prompt-library/)
2. Iniciá sesión con tu cuenta de Google
3. ¡Listo! Empezá a crear prompts

**En mobile:**
- Abrí el menú del navegador → "Agregar a pantalla de inicio"
- La app se instala como PWA

### Como desarrollador

```bash
# Clonar el repositorio
git clone https://github.com/sebadetoma-stack/prompt-library.git

# Abrir el archivo HTML
cd prompt-library
open prompt-library-firebase.html
```

**Nota:** Necesitás configurar tu propio proyecto de Firebase para desarrollo.

## 🔧 Configuración de Firebase

1. Creá un proyecto en [Firebase Console](https://console.firebase.google.com/)
2. Habilitá Authentication (Google)
3. Creá una base de datos Firestore
4. Agregá las credenciales en el archivo HTML:

```javascript
const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "TU_PROJECT.firebaseapp.com",
  projectId: "TU_PROJECT_ID",
  storageBucket: "TU_PROJECT.firebasestorage.app",
  messagingSenderId: "TU_SENDER_ID",
  appId: "TU_APP_ID"
};
```

5. Configurá las reglas de Firestore:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /prompts/{promptId} {
      allow read: if request.auth != null && request.auth.uid == resource.data.userId;
      allow create: if request.auth != null && request.auth.uid == request.resource.data.userId;
      allow update, delete: if request.auth != null && request.auth.uid == resource.data.userId;
    }
  }
}
```

6. Creá el índice compuesto:
   - Collection: `prompts`
   - Campos: `userId` (Ascending), `updatedAt` (Descending)

## 📖 Uso

### Crear un prompt

1. Clic en "+ Nuevo Prompt" (o `Ctrl+B`)
2. Completá título, contenido, categoría y tags
3. Opcionalmente marcá como favorito
4. Guardar

### Usar variables

Creá un prompt con variables entre llaves:

```
Traducí el siguiente texto de {idioma_origen} a {idioma_destino}:

{texto}
```

Al copiar, te pedirá completar los valores.

### Usar plantillas

1. Clic en "📋 Plantillas" (o `Ctrl+P`)
2. Elegí una plantilla
3. Se carga pre-configurada, editá si querés
4. Guardar

### Compartir un prompt

1. Clic en 🔗 en cualquier prompt
2. Copiá el link generado
3. Compartilo - otros pueden verlo y copiarlo a su biblioteca

### Atajos de teclado

- `Ctrl+B` - Nuevo prompt
- `Ctrl+P` - Abrir plantillas
- `Ctrl+F` - Buscar
- `Esc` - Cerrar modal

## 🏗️ Stack Tecnológico

- **Frontend:** HTML5, CSS3, JavaScript (Vanilla)
- **Backend:** Firebase (Authentication + Firestore)
- **Hosting:** GitHub Pages
- **PWA:** Service Workers para funcionalidad offline

## 📊 Estructura de datos

```javascript
{
  id: "auto-generated",
  userId: "firebase-user-id",
  title: "Nombre del prompt",
  content: "Contenido con {variables}",
  category: "Categoría",
  tags: ["tag1", "tag2"],
  favorite: false,
  copyCount: 0,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

## 🤝 Contribuir

Las contribuciones son bienvenidas. Por favor:

1. Fork el proyecto
2. Creá un branch (`git checkout -b feature/NuevaFuncionalidad`)
3. Commit tus cambios (`git commit -m 'Agrega nueva funcionalidad'`)
4. Push al branch (`git push origin feature/NuevaFuncionalidad`)
5. Abrí un Pull Request

## 📝 Roadmap

- [ ] Carpetas anidadas
- [ ] Snippets reutilizables
- [ ] Plantillas personalizadas
- [ ] Colaboración en equipo
- [ ] API REST
- [ ] Extensión de navegador

## 🐛 Reportar bugs

Encontraste un bug? [Abrí un issue](https://github.com/sebadetoma-stack/prompt-library/issues)

## 📄 Licencia

MIT License - ver [LICENSE](LICENSE) para más detalles

## 👨‍💻 Autor

**Sebastián De Toma**
- LinkedIn: [@sebastiandetoma](https://www.linkedin.com/in/sebastiandetoma/)
- GitHub: [@sebadetoma-stack](https://github.com/sebadetoma-stack)
- Web: [El Cronista](https://www.cronista.com)

---

Diseñado por sebadetoma by claude, 2026

## 🙏 Agradecimientos

- Firebase por la infraestructura
- GitHub Pages por el hosting
- Claude (Anthropic) por la asistencia en desarrollo
- La comunidad de usuarios por el feedback

---

⭐ Si te resulta útil, dejá una estrella en GitHub!