---
title: Opciones (resultados de SQL Server-resultados de la consulta a la página de cuadrícula) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToGrid
ms.assetid: f88a0f5c-e800-473b-ae23-c3943de5ed63
caps.latest.revision: 25
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 23e5634a67ff6daec4f6b0852905d8596b885c60
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37318905"
---
# <a name="options-query-results-sql-server-results-to-grid-page"></a>Opciones (resultados de SQL Server-resultados de la consulta a la página de cuadrícula)
  Utilice esta página para especificar las opciones de visualización de un conjunto de resultados de consulta en formato de cuadrícula. Los cambios que se realicen en estas opciones solo se aplicarán a las nuevas consultas de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para cambiar las opciones de las consultas actuales, haga clic en **Opciones de consulta** en el menú **Consulta** o haga clic con el botón derecho en la ventana Consulta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y seleccione **Opciones de consulta**. En la página izquierda del cuadro de diálogo **Opciones de consulta** , en **Resultados**, haga clic en **Cuadrícula**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Incluir la consulta del conjunto de resultados**  
 Devuelve el texto de la consulta como parte de los resultados de la consulta.  
  
 **Incluir encabezados de columna al copiar o guardar los resultados**  
 Seleccione esta casilla para incluir encabezados de columna cuando los resultados se copian en el Portapapeles o se guardan en un archivo. Si desea que los resultados guardados o copiados incluyan solo los datos y no los encabezados de columna, desactive esta casilla.  
  
 **Descartar resultados tras la ejecución**  
 Evita que los resultados de la consulta se muestren en el panel de revisiones. Dichos resultados se descartan inmediatamente tras la ejecución. Especifique esta opción si desea reducir el uso de memoria.  
  
 **Mostrar resultados en una pestaña independiente**  
 Seleccione esta casilla para mostrar el conjunto de resultados en una nueva pestaña y no en la parte inferior de la ventana del documento de consulta.  
  
 **Cambie a la pestaña de resultados tras ejecutar la consulta**  
 Haga clic en esta opción para establecer automáticamente el enfoque de pantalla en el panel de resultados tras ejecutar una consulta.  
  
 **Número máximo de caracteres recuperado**  
 **Datos no XML**:  
  
 Especifique un número entre 1 y 65535 para definir el número máximo de caracteres que aparecerán en cada celda.  
  
> [!NOTE]  
>  La especificación de un número alto puede provocar que los datos del conjunto de resultados aparezcan truncados. El número máximo de caracteres que se muestra en cada celda depende del tamaño de la fuente. Cuando se devuelven conjuntos de resultados grandes, un valor elevado en esta casilla puede provocar que [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] no disponga de suficiente memoria y el rendimiento del sistema se vea afectado.  
  
 **Datos XML**:  
  
 Seleccione **1 MB**, **2 MB**o **5 MB**. Seleccione **Ilimitados** para recuperar todos los caracteres.  
  
 **Restablecer valores predeterminados**  
 Restablece todos los valores de esta página a los valores predeterminados originales.  
  
  
