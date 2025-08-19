# Funcionalidad de Imágenes de Productos

## 📸 Características

### ✅ Funcionalidades Implementadas

- **Subida de imágenes**: Soporte para formatos JPG, PNG, GIF y WebP
- **Vista previa**: Visualización en tiempo real al seleccionar una imagen
- **Validación**: Límite de 2MB por imagen
- **Almacenamiento**: Imágenes guardadas en `storage/app/public/products/`
- **Eliminación**: Opción para eliminar imágenes existentes
- **Imagen por defecto**: SVG personalizado para productos sin imagen
- **Componente reutilizable**: `<x-product-image>` para mostrar imágenes
- **Filtros**: Búsqueda por productos con/sin imagen
- **Limpieza automática**: Eliminación de imágenes al borrar productos

### 🎨 Componente de Imagen

```blade
<!-- Uso básico -->
<x-product-image :product="$product" />

<!-- Con tamaño específico -->
<x-product-image :product="$product" size="lg" />

<!-- Con badge de imagen -->
<x-product-image :product="$product" size="xl" :showBadge="true" />
```

**Tamaños disponibles:**
- `xs`: 32x32px
- `sm`: 48x48px
- `md`: 80x80px (por defecto)
- `lg`: 128x128px
- `xl`: 256x256px

### 📁 Estructura de Archivos

```
storage/app/public/products/
├── imagen1.jpg
├── imagen2.png
└── ...

public/images/products/
└── default-product.svg  # Imagen por defecto
```

### 🔧 Comandos Artisan

#### Limpiar imágenes huérfanas
```bash
# Ver qué se eliminaría sin hacer cambios
php artisan products:clean-images --dry-run

# Eliminar imágenes huérfanas
php artisan products:clean-images
```

### 🖼️ Formulario de Producto

El formulario incluye:
- **Selector de archivo**: Con estilos personalizados
- **Vista previa**: Muestra la imagen seleccionada
- **Opciones de eliminación**: Checkbox para eliminar imagen actual
- **Validación**: Mensajes de error para archivos inválidos

### 📊 Filtros Disponibles

En la lista de productos:
- **Con imagen**: Muestra solo productos que tienen imagen
- **Sin imagen**: Muestra solo productos sin imagen
- **Todos**: Muestra todos los productos

### 🛡️ Seguridad

- **Validación de tipos**: Solo permite formatos de imagen válidos
- **Límite de tamaño**: Máximo 2MB por imagen
- **Sanitización**: Nombres de archivo seguros
- **Eliminación automática**: Limpia archivos al eliminar productos

### 🎯 Casos de Uso

1. **Crear producto con imagen**:
   - Llenar formulario
   - Seleccionar imagen
   - Ver vista previa
   - Guardar producto

2. **Editar imagen existente**:
   - Subir nueva imagen (reemplaza la anterior)
   - O marcar checkbox para eliminar

3. **Eliminar producto**:
   - La imagen se elimina automáticamente del storage

4. **Mantenimiento**:
   - Ejecutar comando de limpieza periódicamente

### 🔄 Flujo de Trabajo

1. **Subida**: Imagen → Validación → Storage → Base de datos
2. **Visualización**: Base de datos → URL → Componente → Vista
3. **Eliminación**: Checkbox → Controlador → Storage → Base de datos

### 📱 Responsive Design

- **Móvil**: Imágenes se ajustan al tamaño de pantalla
- **Desktop**: Tamaños optimizados para diferentes contextos
- **Tablet**: Adaptación automática según breakpoints

### 🎨 Personalización

Para cambiar la imagen por defecto:
1. Reemplazar `public/images/products/default-product.svg`
2. O modificar el método `getImageUrlAttribute()` en el modelo Product

Para cambiar el directorio de almacenamiento:
1. Modificar la ruta en el controlador: `store('products', 'public')`
2. Actualizar el método `getImageUrlAttribute()`

### 🚀 Optimizaciones Futuras

- **Thumbnails**: Generación automática de miniaturas
- **Compresión**: Optimización de imágenes al subir
- **CDN**: Integración con servicios de CDN
- **Múltiples imágenes**: Soporte para galerías de productos
- **Watermarks**: Marcas de agua automáticas 