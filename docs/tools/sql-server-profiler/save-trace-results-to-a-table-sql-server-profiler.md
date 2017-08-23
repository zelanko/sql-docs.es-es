---
title: Guardar los resultados de seguimiento en una tabla (SQL Server Profiler) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 41505214d2ae9e53cc9cd45433183d3250650313
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>Guardar los resultados de un seguimiento en una tabla (SQL Server Profiler)
  En este tema se describe cómo utilizar el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]para guardar los resultados de un seguimiento en una tabla de base de datos.  
  
### <a name="to-save-trace-results-to-a-table"></a>Para guardar los resultados de un seguimiento en una tabla  
  
1.  En el menú **Archivo** , haga clic en **Nuevo seguimiento**y conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Aparecerá el cuadro de diálogo **Propiedades de seguimiento**.  
  
    > [!NOTE]  
    >  Si se selecciona **Iniciar el seguimiento inmediatamente tras realizar la conexión**, el cuadro de diálogo **Propiedades de seguimiento**no aparecerá y, en su lugar, se iniciará el seguimiento. Para desactivar esta configuración, en el menú **Herramientas**, haga clic en **Opciones**y desactive la casilla **Iniciar el seguimiento inmediatamente tras realizar la conexión** .  
  
2.  En el cuadro **Nombre de seguimiento** , escriba un nombre para el seguimiento y haga clic en **Guardar en la tabla**.  
  
3.  En el cuadro de diálogo **Conectar al servidor** , conéctese a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contendrá la tabla de seguimiento.  
  
4.  En el cuadro **Tabla de destino** , seleccione una base de datos de la lista **Base de datos**.  
  
5.  En la lista **Propietario** , seleccione el propietario del seguimiento.  
  
6.  En la lista **Tabla** , escriba o seleccione el nombre de tabla para los resultados de seguimiento. Haga clic en **Aceptar.**  
  
7.  En el cuadro de diálogo **Propiedades de seguimiento** , active la casilla **Establecer número máximo de filas (en miles)**para especificar el número máximo de filas que se guardarán.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
