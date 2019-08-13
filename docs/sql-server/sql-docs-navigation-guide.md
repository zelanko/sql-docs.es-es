---
title: Guía de navegación de documentos de SQL Server
description: Una guía para navegar por la documentación técnica de SQL Server, donde se explican aspectos como la página central, la tabla de contenido, el encabezado y cómo usar las rutas de navegación y cómo usar el filtro de versión.
ms.date: 07/11/2019
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: e5a3e33d48b70146b439790e6439ef4f9cac08b5
ms.sourcegitcommit: c2052b2bf7261b3294a3a40e8fed8b9e9c588c37
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/10/2019
ms.locfileid: "68941165"
---
# <a name="sql-server-docs-navigation-guide"></a>Guía de navegación de documentos de SQL Server 

En este tema se proporcionan algunas sugerencias y trucos para navegar por el espacio de documentación técnica de SQL Server.  

## <a name="hub-page"></a>Página central

La página central de SQL Server se puede encontrar en [https://aka.ms/sqldocs](https://aka.ms/sqldocs) y es el punto de entrada para buscar contenido pertinente a SQL Server.

Siempre puede volver a esta página seleccionando **Documentación de SQL** en el encabezado situado en la parte superior de todas las páginas del conjunto de documentación técnica de SQL Server: 

![Documentación de SQL en el encabezado](media/sql-server-docs-navigation-guide/sql-docs-in-header.png)

## <a name="offline-documentation"></a>Documentación sin conexión

Si desea ver la documentación de SQL Server en un sistema sin conexión, tiene dos opciones para hacerlo. Puede crear un archivo PDF cuando se encuentre en la documentación técnica de SQL Server, o bien puede descargar el contenido sin conexión usando [Visor de Ayuda y ayuda sin conexión de SQL Server](sql-server-help-installation.md). 

Si quiere crear un archivo PDF, seleccione el vínculo **Descargar PDF** que se encuentra en la parte inferior de cada tabla de contenido.


![Descargar PDF](media/sql-server-docs-navigation-guide/download-pdf.png)

## <a name="toc-navigation-hints"></a>Sugerencias de navegación por la TDC

Las entradas de la tabla de contenido (TDC) que tienen un `>` al final de la entrada indican que se quitará de docs.microsoft.com. 

![Signos de mayor que sencillos en la TDC](media/sql-server-docs-navigation-guide/single-carrots-in-sql-docs-toc.png)


Las entradas de la TDC que tienen un `>>` indican que se le dirigirá a documentación técnica con una tabla de contenido diferente. 

![Marcadores de navegación de la TDC](media/sql-server-docs-navigation-guide/double-carrots-in-sql-docs-toc.png)

Si navega a una de estas páginas, puede volver a la página técnica principal de SQL Server y a la tabla de contenido seleccionando la entrada "SQL Server >>" que se encuentra en la parte superior de cada una de estas tablas de contenido. 

![Volver a la TDC de SQL](media/sql-server-docs-navigation-guide/navigate-back-to-sql-toc.png)

## <a name="toc-search-tip"></a>Sugerencia de búsqueda de TDC
En docs.microsoft.com, puede buscar en el contenido de la tabla de contenido mediante el cuadro de búsqueda de filtro de la parte superior: 

![Uso del cuadro de filtro](media/sql-server-docs-navigation-guide/sql-docs-toc-filter.gif)

## <a name="version-filter"></a>Filtro de la versión
La documentación técnica de SQL Server proporciona contenido para varias versiones admitidas y tipos de SQL Server. Las características pueden variar entre las versiones y los tipos de SQL Server, y por tanto, a veces el contenido puede variar. 

Puede usar el filtro de versión para asegurarse de estar viendo el contenido de la versión y el tipo adecuados de SQL Server: 

![Filtro de versión de documentación de SQL](media/sql-server-docs-navigation-guide/sql-docs-version-filter.gif)

Al seleccionar **All SQL (Todo SQL)**  > **Hide nothing** (No ocultar nada), se asegura de que todo el contenido esté visible y que no haya nada oculto detrás del filtro de la versión. 

## <a name="breadcrumbs"></a>Rutas de navegación

Las rutas de navegación se pueden encontrar debajo del encabezado y encima de la tabla de contenido, e indican dónde se encuentra el artículo actual en la tabla de contenido.  Esto no solo ayuda a establece el contexto del tipo de contenido que está leyendo, sino que también permite navegar hacia atrás en el árbol de la tabla de contenido:

![Rutas de navegación de documentación de SQL](media/sql-server-docs-navigation-guide/sql-docs-bread-crumbs.gif)


## <a name="article-section-navigation"></a>Navegación por las secciones de un artículo

El panel de navegación de la derecha le permite desplazarse rápidamente a las secciones de un artículo, así como identificar su ubicación en el artículo.  

![Navegación a la derecha](media/sql-server-docs-navigation-guide/sql-docs-right-hand-navigation.gif)


## <a name="submit-docs-feedback"></a>Enviar comentarios de los documentos

Si encuentra algún problema dentro de un artículo, puede enviar comentarios al equipo de contenido de SQL para ese artículo; para ello, desplácese hacia abajo hasta el final de la página y seleccione **Comentarios sobre el contenido**.

![Comentarios del contenido de problemas de GIT](media/sql-server-get-help/git-issues.png)

También puede enviar comentarios y sugerencias generales sobre la documentación en [https://aka.ms/sqldocsfeedback](https://aka.ms/sqldocsfeedback). 

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![Cómo colaborar en la documentación de SQL Server](media/sql-server-docs-navigation-guide/edit-sql-docs.gif)

## <a name="next-steps"></a>Pasos siguientes

- Introducción a la [documentación técnica de SQL Server](sql-server-technical-documentation.md). 
- Para más información sobre el envío de comentarios o la obtención de ayuda con SQL Server, consulte la página [Obtener ayuda](sql-server-get-help.md). 
- Para acceder rápidamente a todas las guías de inicio rápido y tutoriales, vaya al [Centro de aprendizaje de SQL Server](../lp/sql-server/sql-education-center.md).
