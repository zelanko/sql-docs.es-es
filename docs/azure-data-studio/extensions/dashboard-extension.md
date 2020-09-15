---
title: Creación de la extensión de panel
description: En este tutorial se muestra cómo crear una extensión de panel para agregar funcionalidad personalizada a Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.reviewer: alayu, maghan
ms.topic: how-to
author: yualan
ms.author: alayu
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: b28b3cd043d6564da7d644bb44469671c9ffa147
ms.sourcegitcommit: c5f0c59150c93575bb2bd6f1715b42716001126b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2020
ms.locfileid: "89392162"
---
# <a name="create-an-azure-data-studio-dashboard-extension"></a>Creación de una extensión de panel de Azure Data Studio

En este tutorial se muestra cómo crear una **extensión de panel de Azure Data Studio**. La extensión contribuye al panel de conexión de Azure Data Studio, para que pueda ampliar la funcionalidad de Azure Data Studio de una manera fácilmente visible para los usuarios.

Durante este tutorial aprenderá a realizar lo siguiente:
> [!div class="checklist"]
> - Instalación del generador de extensiones
> - Creación de la extensión
> - Contribuir al panel en la extensión
> - Prueba de la extensión
> - Empaquetado de la extensión
> - Publicación de la extensión en Marketplace

## <a name="prerequisites"></a>Prerrequisitos

Azure Data Studio se basa en el mismo marco que Visual Studio Code, por lo que las extensiones para Azure Data Studio se crean con Visual Studio Code. Para comenzar, necesitará los siguientes componentes:

- [Node.js](https://nodejs.org) instalado y disponible en su `$PATH`. Node.js incluye [npm](https://www.npmjs.com/), el administrador de paquetes de Node.js, que se usa para instalar el generador de extensiones.
- [Visual Studio Code](https://code.visualstudio.com) para depurar la extensión.
- La [extensión Debug](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) de Azure Data Studio (opcional). Esto permite probar la extensión sin necesidad de empaquetarla e instalarla en Azure Data Studio.
- Asegúrese de que `azuredatastudio` está en su ruta de acceso. En el caso de Windows, asegúrese de elegir la opción `Add to Path` de setup.exe. En Mac o Linux, ejecute la opción de *instalación del comando "azuredatastudio" de PATH*.

## <a name="install-the-extension-generator"></a>Instalación del generador de extensiones

Para simplificar el proceso de creación de extensiones, hemos compilado [un generador de extensiones](https://code.visualstudio.com/docs/extensions/yocode) con Yeoman. Para instalarlo, ejecute lo siguiente desde el símbolo del sistema:

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-dashboard-extension"></a>Creación de la extensión de panel

### <a name="introduction-to-the-dashboard"></a>Introducción al panel

El panel de conexión de Azure Data Studio es una herramienta eficaz que resume y proporciona conclusiones sobre las conexiones de un usuario.

Hay dos variantes del panel: el "panel de servidor" en el que se resume todo el servidor, y el "panel de base de datos", en el que se resume una base de datos individual. Puede acceder a cualquiera de ellos si hace clic con el botón derecho en un servidor o una base de datos en el viewlet Conexiones de Azure Data Studio y hace clic en **Administrar**:

:::image type="content" source="media/dashboard-extension/dashboard-summary.gif" alt-text="Introducción a los paneles":::

Hay tres puntos de contribución clave para que las extensiones agreguen funcionalidad al panel:

1. **Pestaña Panel completo**: una pestaña independiente en el panel de la extensión. Se puede agregar a un panel de servidor o de base de datos. Se puede personalizar con widgets, una barra de herramientas y una sección de navegación.
2. **Acciones de la página principal**: botones de acción en la parte superior de la barra de herramientas de conexión.
3. **Widgets**: grafos que se ejecutan en la instancia de SQL Server.

:::image type="content" source="media/dashboard-extension/dashboard-contrib-points.png" alt-text="Puntos de contribución":::

### <a name="run-the-extension-generator"></a>Ejecución del generador de extensiones

Para crear una extensión:

1. Inicie el generador de extensiones con el siguiente comando:

   `yo azuredatastudio`

2. Elija **Nuevo panel** en la lista de tipos de extensión.

3. Rellene los mensajes como se muestra a continuación. Esto crea una extensión que aporta una pestaña al panel del servidor.

:::image type="content" source="media/dashboard-extension/dashboard-generator.png" alt-text="Generador de extensiones":::

Hay gran cantidad de mensajes, por lo que se muestra más información sobre lo que significa cada pregunta:

:::image type="content" source="media/dashboard-extension/dashboard-flowchart.png" alt-text="Diagrama de flujo de paneles":::

Al completar los pasos anteriores, se crea una carpeta. Abra la carpeta en Visual Studio Code y estará listo para crear una extensión de panel propia.

### <a name="run-the-extension"></a>Ejecución de la extensión

Ahora se ejecutará la extensión para ver qué proporciona la plantilla del panel. Antes de ejecutarla, asegúrese de que la **extensión Debug de Azure Data Studio** está instalada en Visual Studio Code.

Presione **F5** en VS Code para iniciar Azure Data Studio en modo de depuración con la extensión en ejecución. Después, puede ver cómo contribuye esta plantilla predeterminada al panel.

A continuación, se verá cómo modificar este panel predeterminado.

### <a name="develop-the-dashboard"></a>Desarrollo del panel

El archivo más importante para empezar a trabajar con el desarrollo de extensiones es `package.json`. Este es el archivo de manifiesto, donde se registran las contribuciones del panel. Observe las secciones `dashboard.tabs`, `dashboard.insights` y `dashboard.containers`.

Puede probar con estos cambios:

- Experimente con los tipos de información, como "bar", "horizontalBar", "timeSism"
- Escriba consultas propias para ejecutarlas en la conexión de SQL Server
- Consulte este [tutorial de información de ejemplo](../tutorial-qds-sql-server.md) o [este otro](../tutorial-table-space-sql-server.md) para obtener tutoriales sobre información específica.

## <a name="package-your-extension"></a>Empaquetado de la extensión

Para compartirla con otros usuarios, ha de empaquetar la extensión en un solo archivo. Este se puede publicar en el Marketplace de extensiones de Azure Data Studio o compartir entre su equipo o comunidad. Para ello, debe instalar otro paquete npm desde la línea de comandos:

```console
`npm install -g vsce`
```

Edite `README.md` como prefiera, vaya hasta el directorio base de la extensión y ejecute `vsce package`. Opcionalmente, puede vincular un repositorio con la extensión o continuar sin ninguno. Para agregar uno, agregue una línea similar al archivo `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

Después de agregar estas líneas, se crea el archivo my-test-extension-0.0.1.vsix, listo para instalarlo en Azure Data Studio.

:::image type="content" source="media/dashboard-extension/install-vsix.png" alt-text="Instalación de vsix":::

## <a name="publish-your-extension-to-the-marketplace"></a>Publicación de la extensión en Marketplace

El Marketplace de extensiones de Azure Data Studio aún no está totalmente implementado, pero el proceso actual consiste en hospedar la extensión VSIX en algún lugar (por ejemplo, una página de versiones de GitHub) y luego enviar una solicitud de incorporación de cambios [al archivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) con la información de la extensión.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido a:
> [!div class="checklist"]
> - Instalación del generador de extensiones
> - Creación de la extensión
> - Contribuir al panel en la extensión
> - Prueba de la extensión
> - Empaquetado de la extensión
> - Publicación de la extensión en Marketplace

Confiamos en que después de leer esto se sienta inspirado para compilar su propia extensión para Azure Data Studio. Tenemos compatibilidad con información del panel (gráficos atractivos que se ejecutan en la instancia de SQL Server), varias API específicas de SQL y un gran conjunto existente de puntos de extensión heredados de Visual Studio Code.

Si tiene una idea, pero no está seguro de cómo empezar, abra una incidencia o envíe un Tweet al equipo: [azuredatastudio](https://twitter.com/azuredatastudio).

Siempre puede hacer referencia a la [guía de extensiones de Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) porque aborda todas las API y los patrones existentes.

Para obtener información sobre cómo trabajar con T-SQL en Azure Data Studio, siga el tutorial del editor de T-SQL sobre el:

> [!div class="nextstepaction"]
> [uso del editor de Transact-SQL para crear objetos de base de datos](../tutorial-sql-editor.md).
