---
title: 'SQL Server Profiler: cuadro de diálogo Buscar | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.find.f1
helpviewer_keywords:
- Find dialog box
ms.assetid: dfaeec04-93d3-4214-9fc1-38b80179b36b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 81ed454290a5ca62093fe9bdb619179106ca9985
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088855"
---
# <a name="sql-server-profiler---find-dialog-box"></a>Buscar (cuadro de diálogo de SQL Server Profiler)
  Utilice el cuadro de diálogo **Buscar** para buscar un seguimiento para palabras o caracteres específicos. Para cancelar la búsqueda en curso, presione ESC.  
  
 Para abrir este cuadro de diálogo en el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], en el menú **Editar** , haga clic en **Buscar**.  
  
## <a name="options"></a>Opciones  
 **Buscar**  
 Escriba el texto que desea buscar. La búsqueda mostrará cualquier cadena que contenga la cadena especificada. Por ejemplo, la búsqueda de "Completed" devolverá "SQL:BatchCompleted". No se admiten caracteres comodín (*, ?, etc.).  
  
 **Buscar en columna**  
 Haga clic en una columna de datos para realizar la búsqueda o haga clic en ** \<todas las columnas>** para buscar en todas las columnas de datos del seguimiento.  
  
 **Coincidir mayúsculas y minúsculas**  
 Busca texto en el que se usen las mismas mayúsculas y minúsculas que en el cuadro **Buscar** . Desactive esta casilla para buscar ejemplos del seguimiento que tengan caracteres tanto en mayúscula como en minúscula.  
  
 **Solo palabras completas**  
 Limita la búsqueda a palabras completas. Desactive la casilla **Solo palabras completas** si desea realizar la búsqueda de algunos caracteres de una palabra.  
  
 **Buscar siguiente**  
 Busca el ejemplo siguiente de los caracteres del cuadro **Buscar** .  
  
 **Buscar anterior**  
 Realiza una búsqueda hacia atrás en el seguimiento, para buscar el ejemplo anterior de los caracteres del cuadro **Buscar**.  
  
## <a name="see-also"></a>Consulte también  
 [Buscar un valor o una columna de datos durante el seguimiento de &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)   
 [Cree un SQL Server Profiler de &#40;de seguimiento&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [Abra una tabla de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [Abra un archivo de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [SQL Server Profiler plantillas y permisos](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
