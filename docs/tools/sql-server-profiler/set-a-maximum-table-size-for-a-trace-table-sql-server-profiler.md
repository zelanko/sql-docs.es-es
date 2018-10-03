---
title: Establecer un tamaño máximo de tabla para una tabla de seguimiento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
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
ms.openlocfilehash: a9237726570f35d913f27b24c69eebb1e58f8e39
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47737213"
---
# <a name="set-a-maximum-table-size-for-a-trace-table-sql-server-profiler"></a>Establecer un tamaño máximo de tabla para una tabla de seguimiento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo establecer un tamaño máximo de tabla para tablas de seguimiento mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-set-a-maximum-table-size-for-a-trace-table"></a>Para establecer un tamaño máximo de tabla para una tabla de seguimiento  
  
1.  En el menú **Archivo** , haga clic en **Nuevo seguimiento**y, a continuación, conéctese a una instancia de SQL Server.  
  
     Aparece el cuadro de diálogo **Propiedades de seguimiento**.  
  
    > [!NOTE]  
    >  Si se selecciona **Iniciar el seguimiento inmediatamente tras realizar la conexión**, el cuadro de diálogo **Propiedades de seguimiento**no aparecerá y, en su lugar, se iniciará el seguimiento. Para desactivar esta configuración, en el menú **Herramientas**, haga clic en **Opciones**y desactive la casilla **Iniciar el seguimiento inmediatamente tras realizar la conexión** .  
  
2.  En el cuadro **Nombre de seguimiento** , escriba un nombre para el seguimiento.  
  
3.  En el cuadro **Nombre de plantilla**.  
  
4.  Active la casilla **Guardar en la tabla**.  
  
5.  Conéctese al servidor en el que desee que se almacene el seguimiento.  
  
     Aparecerá el cuadro de diálogo **Tabla de destino** .  
  
6.  En la lista **Base de datos** , seleccione una base de datos para el seguimiento.  
  
7.  En el cuadro **Tabla** , escriba o seleccione un nombre de tabla.  
  
8.  Active la casilla **Establecer número máximo de filas (en miles)** y especifique un número máximo de filas para la tabla de seguimiento.  
  
    > [!NOTE]  
    >  Cuando el número de filas de la tabla supere el máximo especificado, dejarán de registrarse los eventos de seguimiento. No obstante, la traza continuará.  
  
## <a name="see-also"></a>Ver también  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
