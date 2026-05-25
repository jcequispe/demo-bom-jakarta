# demo-bom-jakarta

**Bill of Materials (BOM)** que define las versiones de dependencias para la demostración de vulnerabilidad CVE-2015-6420.

## Descripción

Este es un proyecto Maven que actúa como BOM centralizado. Define todas las versiones de dependencias críticas:
- ✅ **Apache Commons Collections** (versión vulnerable: **3.2.1**)
- ✅ **Jakarta Servlet API**
- ✅ **Spring Boot** (compatible con Jakarta)

## Estructura

```
.
├── pom.xml              ← Define todas las versiones
└── README.md
```

## Propósito

- 🎯 **Centralizar versionado:** Otros proyectos importan este BOM para obtener versiones consistentes
- 🔒 **Mostrar vulnerabilidad:** Usa Commons Collections 3.2.1 que es vulnerable a CVE-2015-6420
- 📈 **Demostrar actualización:** Cambiar la versión aquí propaga la actualización a todos los módulos

## Uso

### Importar en otros proyectos

En el `pom.xml` de otros proyectos:

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.demo</groupId>
            <artifactId>demo-bom-jakarta</artifactId>
            <version>1.0.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Luego usa las dependencias sin especificar versión:

```xml
<dependencies>
    <dependency>
        <groupId>commons-collections</groupId>
        <artifactId>commons-collections</artifactId>
        <!-- Versión viene del BOM: 3.2.1 -->
    </dependency>
</dependencies>
```

## Compilar

```bash
mvn clean install
```

## Versiones Actuales

| Dependencia | Versión | Estado |
|------------|---------|--------|
| commons-collections | **3.2.1** | ⚠️ VULNERABLE a CVE-2015-6420 |
| jakarta.servlet-api | 6.0.0 | ✅ Seguro |
| spring-boot | 3.3.0 | ✅ Seguro |

## ¿Cómo se usa en la demo?

1. Este BOM define `commons-collections:3.2.1` (vulnerable)
2. `demo-utilities-jakarta` importa este BOM
3. `demo-app-vulnerable` importa tanto el BOM como las utilities
4. **Resultado:** La app hereda la dependencia vulnerable de transitividad

## Actualizar a versión segura

Para demostrar el fix, cambiar en `pom.xml`:

```xml
<!-- ANTES (vulnerable) -->
<commons.collections.version>3.2.1</commons.collections.version>

<!-- DESPUÉS (seguro) -->
<commons.collections.version>4.0</commons.collections.version>
```

Luego:

```bash
mvn clean install
```

Esto propagará automáticamente la nueva versión a todos los proyectos que importan este BOM.

## Dependabot

Cuando este repo esté en GitHub con Dependabot habilitado:
- 🔔 Dependabot detectará `commons-collections:3.2.1` como vulnerable
- 📨 Abrirá automáticamente un PR sugiriendo actualizar a una versión segura
- 📊 Mostrará detalles del CVE-2015-6420

## Referencias

- [Bill of Materials (BOM) - Maven Docs](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)
- [CVE-2015-6420 - NVD](https://nvd.nist.gov/vuln/detail/CVE-2015-6420)
- [Apache Commons Collections](https://commons.apache.org/proper/commons-collections/)

---

**Parte de:** Demo educativa de vulnerabilidades CVE-2015-6420
