---
title: SQL Server Profiler - cuadro de diálogo Buscar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.pro.find.f1
helpviewer_keywords:
- Find dialog box
ms.assetid: dfaeec04-93d3-4214-9fc1-38b80179b36b
caps.latest.revision: 24
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 311d248acae2b64d106c57f5c7f92024c4174e5c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37199995"
---
# <a name="sql-server-profiler---find-dialog-box"></a>Buscar (cuadro de diálogo de SQL Server Profiler)
  Utilice el cuadro de diálogo **Buscar** para buscar un seguimiento para palabras o caracteres específicos. Para cancelar la búsqueda en curso, presione ESC.  
  
 Para abrir este cuadro de diálogo en el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], en el menú **Editar** , haga clic en **Buscar**.  
  
## <a name="options"></a>Opciones  
 **Buscar**  
 Escriba el texto que desea buscar. La búsqueda mostrará cualquier cadena que contenga la cadena especificada. Por ejemplo, la búsqueda de "Completed" devolverá "SQL:BatchCompleted". No se admiten caracteres comodín (*, ?, etc.).  
  
 **Buscar en columna**  
 Haga clic en la columna de datos en la que quiere realizar la búsqueda o haga clic en **\<Todas las columnas>** para realizar la búsqueda en todas las columnas de datos del seguimiento.  
  
 **Coincidir mayúsculas y minúsculas**  
 Busca texto en el que se usen las mismas mayúsculas y minúsculas que en el cuadro **Buscar** . Desactive esta casilla para buscar ejemplos del seguimiento que tengan caracteres tanto en mayúscula como en minúscula.  
  
 **Solo palabras completas**  
 Limita la búsqueda a palabras completas. Desactive la casilla **Solo palabras completas** si desea realizar la búsqueda de algunos caracteres de una palabra.  
  
 **Buscar siguiente**  
 Busca el ejemplo siguiente de los caracteres del cuadro **Buscar** .  
  
 **Buscar anterior**  
 Realiza una búsqueda hacia atrás en el seguimiento, para buscar el ejemplo anterior de los caracteres del cuadro **Buscar** .  
  
## <a name="see-also"></a>Vea también  
 [Buscar un valor o una columna de datos durante una traza &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)   
 [Crear un seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [Abrir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [Plantillas y permisos de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
