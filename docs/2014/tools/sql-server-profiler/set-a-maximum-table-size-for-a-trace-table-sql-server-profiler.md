---
title: Establecer un tamaño máximo de tabla para una tabla de seguimiento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- size [SQL Server], trace tables
- maximum table size for traces
ms.assetid: d0ae83e5-1c88-4a2e-be05-2c341280b978
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 15ef5e8621a5edd216b300a8a96f3a9656b55b12
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63267152"
---
# <a name="set-a-maximum-table-size-for-a-trace-table-sql-server-profiler"></a>Establecer un tamaño máximo de tabla para una tabla de seguimiento (SQL Server Profiler)
  En este tema se describe cómo establecer un tamaño máximo de tabla para tablas de seguimiento mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-set-a-maximum-table-size-for-a-trace-table"></a>Para establecer un tamaño máximo de tabla para una tabla de seguimiento  
  
1.  En el menú **Archivo** , haga clic en **Nuevo seguimiento**y, a continuación, conéctese a una instancia de SQL Server.  
  
     Aparecerá el cuadro de diálogo **Propiedades de seguimiento**.  
  
    > [!NOTE]  
    >  Si se selecciona **Iniciar el seguimiento inmediatamente tras realizar la conexión**, el cuadro de diálogo **Propiedades de seguimiento**no aparecerá y, en su lugar, se iniciará el seguimiento. Para desactivar esta configuración, en el menú **Herramientas**, haga clic en **Opciones**y desactive la casilla **Iniciar el seguimiento inmediatamente tras realizar la conexión** .  
  
2.  En el cuadro **Nombre de seguimiento** , escriba un nombre para el seguimiento.  
  
3.  En el cuadro **Nombre de plantilla**, seleccione una plantilla de seguimiento.  
  
4.  Active la casilla **Guardar en la tabla**.  
  
5.  Conéctese al servidor en el que desee que se almacene el seguimiento.  
  
     Aparecerá el cuadro de diálogo **Tabla de destino** .  
  
6.  En la lista **Base de datos** , seleccione una base de datos para el seguimiento.  
  
7.  En el cuadro **Tabla** , escriba o seleccione un nombre de tabla.  
  
8.  Active la casilla **Establecer número máximo de filas (en miles)** y especifique un número máximo de filas para la tabla de seguimiento.  
  
    > [!NOTE]  
    >  Cuando el número de filas de la tabla supere el máximo especificado, dejarán de registrarse los eventos de seguimiento. No obstante, la traza continuará.  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Profiler](sql-server-profiler.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
