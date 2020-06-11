---
title: Opciones (resultados de la consulta-SQL Server-resultados a la página de cuadrícula) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToGrid
ms.assetid: f88a0f5c-e800-473b-ae23-c3943de5ed63
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9bde39c64fdf2fbabaec85772d4bfa44d86fd1da
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/26/2020
ms.locfileid: "83856667"
---
# <a name="options-query-results-sql-server-results-to-grid-page"></a>Opciones (resultados de la consulta-SQL Server-resultados a la página de cuadrícula)
  Utilice esta página para especificar las opciones de visualización de un conjunto de resultados de consulta en formato de cuadrícula. Los cambios que se realicen en estas opciones solo se aplicarán a las nuevas consultas de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para cambiar las opciones de las consultas actuales, haga clic en **Opciones de consulta** en el menú **consulta** o haga clic con el botón secundario en la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ventana de consulta y seleccione **Opciones de consulta**. En la página izquierda del cuadro de diálogo **Opciones de consulta** , en **Resultados**, haga clic en **Cuadrícula**.  
  
## <a name="ui-element-list"></a>Lista de elementos de la interfaz de usuario  
 **Incluir la consulta en el conjunto de resultados**  
 Devuelve el texto de la consulta como parte de los resultados de la consulta.  
  
 **Incluir encabezados de columna al copiar o guardar los resultados**  
 Seleccione esta casilla para incluir encabezados de columna cuando los resultados se copian en el Portapapeles o se guardan en un archivo. Si desea que los resultados guardados o copiados incluyan solo los datos y no los encabezados de columna, desactive esta casilla.  
  
 **Descartar resultados tras la ejecución**  
 Evita que los resultados de la consulta se muestren en el panel de revisiones. Dichos resultados se descartan inmediatamente tras la ejecución. Especifique esta opción si desea reducir el uso de memoria.  
  
 **Mostrar resultados en otra pestaña**  
 Seleccione esta casilla para mostrar el conjunto de resultados en una nueva pestaña y no en la parte inferior de la ventana del documento de consulta.  
  
 **Cambiar a la pestaña de resultados tras ejecutar la consulta**  
 Haga clic en esta opción para establecer automáticamente el enfoque de pantalla en el panel de resultados tras ejecutar una consulta.  
  
 **Número máximo de caracteres recuperados**  
 **Datos no XML**:  
  
 Especifique un número entre 1 y 65535 para definir el número máximo de caracteres que aparecerán en cada celda.  
  
> [!NOTE]  
>  La especificación de un número alto puede provocar que los datos del conjunto de resultados aparezcan truncados. El número máximo de caracteres que se muestra en cada celda depende del tamaño de la fuente. Cuando se devuelven conjuntos de resultados grandes, un valor elevado en esta casilla puede provocar que [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] no disponga de suficiente memoria y el rendimiento del sistema se vea afectado.  
  
 **Datos XML**:  
  
 Seleccione **1 MB**, **2 MB**o **5 MB**. Seleccione **Ilimitados** para recuperar todos los caracteres.  
  
 **Valores predeterminados**  
 Restablece todos los valores de esta página a los valores predeterminados originales.  
  
  
