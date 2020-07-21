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
ms.openlocfilehash: 141cfe63151f65e171550beda1c20e232a6205e0
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928686"
---
# <a name="sql-server-profiler---find-dialog-box"></a>Buscar (cuadro de diálogo de SQL Server Profiler)
  Utilice el cuadro de diálogo **Buscar** para buscar un seguimiento para palabras o caracteres específicos. Para cancelar la búsqueda en curso, presione ESC.  
  
 Para abrir este cuadro de diálogo en el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], en el menú **Editar** , haga clic en **Buscar**.  
  
## <a name="options"></a>Opciones  
 **Buscar**  
 Escriba el texto que desea buscar. La búsqueda mostrará cualquier cadena que contenga la cadena especificada. Por ejemplo, la búsqueda de "Completed" devolverá "SQL:BatchCompleted". No se admiten caracteres comodín (*, ?, etc.).  
  
 **Buscar en columna**  
 Haga clic en una columna de datos para realizar la búsqueda o haga clic en **\<All columns>** para buscar en todas las columnas de datos del seguimiento.  
  
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
 [Plantillas y permisos de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
