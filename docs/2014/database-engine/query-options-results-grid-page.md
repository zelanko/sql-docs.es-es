---
title: Resultados de opciones de consulta (página cuadrícula) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.grid.f1
ms.assetid: 764bf435-3aab-4c62-b4e0-64fe020a5a95
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7c50957f59ef4e4743ca1667d6eb7a97869bec18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089007"
---
# <a name="query-options-results-grid-page"></a>Resultados de Opciones de consulta (página Cuadrícula)
  Utilice esta página para especificar las opciones de visualización de un conjunto de resultados de consulta en formato de cuadrícula.  
  
## <a name="options"></a>Opciones  
 **Incluir la consulta en el conjunto de resultados**  
 Devuelve el texto de la consulta como parte del conjunto de resultados.  
  
 **Incluir encabezados de columna al copiar o guardar los resultados**  
 Incluye los encabezados de columna (títulos) cuando los resultados se copian en el portapapeles o se guardan en un archivo. Si desea que los resultados guardados o copiados incluyan solo los datos y no los encabezados de columna, desactive esta casilla.  
  
 **Descartar resultados tras la ejecución**  
 Si descarta los resultados de la consulta después de que la pantalla los reciba, liberará memoria.  
  
 **Mostrar los resultados en una pestaña independiente**  
 Muestra el conjunto de resultados en una nueva ventana de documento, en lugar de mostrarlos en la parte inferior de la ventana del documento de consulta.  
  
 **Cambiar a la pestaña de resultados tras ejecutar la consulta**  
 Establece el foco de la pantalla automáticamente en el conjunto de resultados.  
  
 **Número máximo de caracteres recuperados**  
 **Datos no XML**:  
  
 Especifique un número entre 1 y 65535 para definir el número máximo de caracteres que aparecerán en cada celda.  
  
> [!NOTE]  
>  La especificación de un número alto puede provocar que los datos del conjunto de resultados aparezcan truncados. El número máximo de caracteres que se muestra en cada celda depende del tamaño de la fuente. Cuando se devuelven conjuntos de resultados grandes, un valor elevado en esta casilla puede provocar que [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] no disponga de suficiente memoria y el rendimiento del sistema se vea afectado.  
  
 **Datos XML**:  
  
 Seleccione **1 MB**, **2 MB**o **5 MB**. Seleccione **Ilimitados** para recuperar todos los caracteres.  
  
 **Restablecer valores predeterminados**  
 Restablece todos los valores de esta página a los valores predeterminados originales.  
  
  
