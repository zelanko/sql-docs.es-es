---
title: Cómo colaborar en la documentación de SQL Server | Microsoft Docs
ms.date: 04/12/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 52bc0371c7f60b7b6fcff5c64c5972d7a178b629
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926536"
---
# <a name="how-to-contribute-to-sql-server-documentation"></a>Cómo colaborar en la documentación de SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Cualquier usuario puede colaborar en la documentación de SQL Server. Implica la corrección de errores tipográficos, la sugerencia de explicaciones mejoradas y la mejora de la precisión técnica. En este artículo se explica cómo empezar con las colaboraciones de contenido y cómo funciona el proceso.

Hay dos flujos de trabajo principales que se pueden aplicar para colaborar:

|||
|---|---|
| [Edición en el navegador](#githubui) | Es útil para ediciones rápidas y breves de cualquier artículo. |
| [Edición local con herramientas](#tools) | Es útil para ediciones más complejas, ediciones que afecten a varios artículos y colaboraciones frecuentes en docs.microsoft.com. |

## <a id="githubui"></a> Edición en el navegador

En los siguientes pasos se da una visión general de cómo hacer ediciones sencillas en el contenido de SQL Server con el navegador. El proceso completo está documentado en el artículo [Flujo de trabajo de colaboración de GitHub para cambios menores o poco frecuentes](https://docs.microsoft.com/contribute/light-workflow).

1. En todos los artículos, incluido este, aparece el botón **Editar** situado a la derecha. Busque un artículo que quiera cambiar y haga clic en el botón **Editar** para empezar a trabajar.

   ![Botón Editar para un artículo de SQL](./media/sql-server-docs-contribute/edit-sql-server-docs.png)

   Todo el contenido de docs.microsoft.com se administra en distintos repositorios de GitHub. Al hacer clic en el botón Editar, se le direccionará al artículo del repositorio **sql-docs**. En cambio, si edita un artículo de SQL en la documentación de Azure, se le direccionará al repositorio **azure-docs**. 

1. Después, haga clic en el icono de lápiz situado en la parte superior derecha del artículo de GitHub.

   ![Botón Editar](./media/sql-server-docs-contribute/edit-button.png)

   > [!NOTE]
   > Debe iniciar sesión en GitHub para poder editar un artículo. Si no tiene ninguna cuenta de GitHub, vea [Configuración de la cuenta de GitHub](https://docs.microsoft.com/contribute/get-started-setup-github). Después de crear una cuenta, también deberá comprobar su dirección de correo electrónico con GitHub para poder editar.

1. Edite el artículo en el navegador. Todos los artículos se escriben en Markdown. Si necesita ayuda relacionada con Markdown, puede consultar [Markdown basics](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/) (Conceptos básicos de Markdown). También puede aprender observando cómo representan los artículos publicados el Markdown existente.

1. Desplácese hasta el final de la ventana de edición, escriba un título para el cambio y haga clic en el botón **Propose file change** (Proponer cambio de archivo).

   ![Proponer solicitud de incorporación de cambios](./media/sql-server-docs-contribute/propose-file-change.png)

1. En la siguiente página, haga clic en **Crear solicitud de incorporación de cambios**.

   ![Crear solicitud de incorporación de cambios](./media/sql-server-docs-contribute/create-pull-request.png)

1. Escriba un título y una descripción para la solicitud de incorporación de cambios. Luego, vuelva a hacer clic en **Crear solicitud de incorporación de cambios**.

   ![Crear solicitud de incorporación de cambios](./media/sql-server-docs-contribute/create-pull-request2.png)

En este punto se le debería guiar por el resto del proceso en los comentarios de la solicitud de incorporación de cambios. El proceso completo y los detalles adicionales están en la [guía del colaborador](https://docs.microsoft.com/contribute/light-workflow).

## <a id="tools"></a> Edición local con herramientas

Otra opción de edición consiste en bifurcar el repositorio **sql-docs** o **azure-docs** y clonarlo localmente en el equipo. Después puede usar un editor de Markdown y un cliente de Git para enviar los cambios. Este flujo de trabajo es útil para las ediciones que son más complejas o que afectan a varios archivos. También es práctico para los colaboradores frecuentes de docs.microsoft.com.

Para colaborar con este método, consulte los siguientes artículos:

- [Creación de una cuenta de GitHub](https://docs.microsoft.com/contribute/get-started-setup-github)
- [Instalación de herramientas de creación de contenido](https://docs.microsoft.com/contribute/get-started-setup-tools)
- [Configuración local de un repositorio de Git](https://docs.microsoft.com/contribute/get-started-setup-local)
- [Uso de herramientas para la colaboración](https://docs.microsoft.com/contribute/how-to-write-workflows-majo)

Si envía una solicitud de incorporación de cambios con cambios importantes en la documentación, recibirá un comentario en GitHub en el que se le pedirá que envíe un **contrato de licencia de colaboración (CLA)** en línea. Debe cumplimentar el formulario en línea para que se pueda aceptar la solicitud de incorporación de cambios.

## <a name="recognition"></a>Reconocimiento

Si se aceptan los cambios, será reconocido como colaborador en la parte superior del artículo.

![Reconocimiento de la colaboración en contenido](./media/sql-server-docs-contribute/contribution-recognition.png)

## <a name="sql-docs-overview"></a>información general de sql-docs

En esta sección se muestran instrucciones adicionales sobre cómo trabajar en el repositorio **sql-docs**.

> [!IMPORTANT]
> La información de esta sección es específica de **sql-docs**. Si edita un artículo de SQL en la documentación de Azure, vea [el archivo Léame del repositorio azure-docs en GitHub](https://github.com/MicrosoftDocs/azure-docs/blob/master/README.md).

El repositorio [sql-docs](https://github.com/MicrosoftDocs/sql-docs) usa muchas carpetas estándares para organizar el contenido.

| Carpeta | Descripción |
|---|---|
| [docs](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs) | Contiene todo el contenido publicado de SQL Server. Las subcarpetas organizan de forma lógica distintas áreas del contenido. |
| [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) | Contiene archivos de inclusión. Estos archivos son bloques de contenido que se pueden incluir en uno o más temas. |
| **./media** | Cada carpeta puede tener una subcarpeta **media** para imágenes de artículos. La carpeta **media** tiene a su vez subcarpetas con el mismo nombre que los temas en los que aparece la imagen. Las imágenes deben ser archivos .png con todas las letras en minúsculas y sin espacios en blanco. |
| **TOC.MD** | Archivo de tabla de contenidos. Cada subcarpeta tiene la opción de usar un archivo TOC.MD. |

#### <a name="applies-to-includes"></a>Archivos de inclusión applies-to

Todos los artículos de SQL Server contienen un archivo de inclusión **applies-to** al final del título. Indica las áreas o las versiones de SQL Server a las que se aplica el artículo.

Observe el siguiente ejemplo de Markdown, que incorpora el archivo de inclusión **appliesto-ss-asdb-asdw-pdw-md.md**.

```Markdown
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
```

De esta manera se agrega el siguiente texto en la parte superior del artículo:

![Texto "Se aplica a"](./media/sql-server-docs-contribute/applies-to.png)

Para buscar el archivo de inclusión applies-to correcto para su artículo, aplique las siguientes sugerencias:

- Consulte otros artículos que aborden la misma función o una tarea relacionada. Si edita ese mismo artículo, puede copiar el Markdown del vínculo del archivo de inclusión applies-to (puede cancelar la edición sin enviarla).
- Busque el directorio [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) de los archivos que contienen el texto "applies-to". Puede usar el botón **Find** (Buscar) en GitHub para filtrar rápidamente. Haga clic en el archivo para ver cómo se representa.
- Preste atención a la convención de nomenclatura. Si hay x en el nombre, suelen ser marcadores de posición que indican la falta de compatibilidad de un servicio. Por ejemplo, **appliesto-xx-xxxx-asdw-xxx-md.md** indica compatibilidad con solo Azure SQL Data Warehouse, porque solo se especifica **asdw** y los demás campos contienen x.
- Algunos archivos de inclusión especifican un número de versión, como **tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md**. Use estos archivos de inclusión únicamente si sabe que la característica se ha introducido con una versión específica de SQL Server. 

## <a name="contributor-resources"></a>Recursos para los colaboradores

- [Guía del colaborador de docs.microsoft.com](https://docs.microsoft.com/en-us/contribute/)
- [Guía de estilo de Microsoft](https://docs.microsoft.com/en-us/teamblog/style-guide)
- [Markdown basics](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/) (Conceptos básicos de Markdown)

> [!TIP]
> Si tiene comentarios sobre el producto en vez de comentarios sobre la documentación, [aquí puede enviar comentarios sobre el producto de SQL Server](https://feedback.azure.com/forums/908035-sql-server).

## <a name="next-steps"></a>Pasos siguientes

Explore el [repositorio sql-docs](https://github.com/MicrosoftDocs/sql-docs) en GitHub.

Busque un artículo, envíe un cambio y ayude a la comunidad de SQL Server. 

¡Gracias!