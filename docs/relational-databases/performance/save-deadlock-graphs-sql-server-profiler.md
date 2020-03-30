---
title: Guardar grafos de interbloqueo (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], saving deadlock graphs
- graphs [SQL Server]
- saving deadlock graphs
ms.assetid: bf1fc906-abd6-4a89-842e-da0d66b2defe
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: c27ed8ea6fbd2e4b89d27cb7772f533150cf0e5c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68099372"
---
# <a name="save-deadlock-graphs-sql-server-profiler"></a>Guardar grafos de interbloqueo (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se explica cómo guardar un gráfico de interbloqueo mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Los gráficos de interbloqueo se guardan como archivos XML.  
  
## <a name="save-deadlock-graph-events-separately"></a>Guardar eventos de grafo de interbloqueo por separado  
  
1. En el menú **Archivo**, seleccione **Nuevo seguimiento** y, a continuación, conéctese a una instancia de SQL Server.  
  
     Aparecerá el cuadro de diálogo **Propiedades de seguimiento** .  
  
    > [!NOTE]  
    >  Si selecciona **Iniciar el seguimiento inmediatamente tras realizar la conexión**, el cuadro de diálogo **Propiedades de seguimiento** no aparecerá y, en su lugar, se iniciará el seguimiento. Para desactivar esta configuración, en el menú **Herramientas**, seleccione **Opciones** y desmarque la casilla **Iniciar el seguimiento inmediatamente tras realizar la conexión**.  
  
2. En el cuadro de diálogo **Propiedades de seguimiento** , en el cuadro **Nombre de seguimiento** , escriba un nombre para el seguimiento.  
  
3. En la lista **Usar la plantilla**, seleccione una plantilla de seguimiento en la que se basará el seguimiento. Si no quiere usar una plantilla, seleccione **En blanco**.  
  
4. Realice una de las siguientes acciones:  
  
    -   Active la casilla **Guardar en archivo** para capturar el seguimiento en un archivo. Especifique un valor en **Establecer el tamaño máximo de archivo (MB)** .  
  
         Opcionalmente, active las casillas **Habilitar sustitución incremental de archivos** y **El servidor procesa los datos de seguimiento** . 
  
    -   Active la casilla **Guardar en tabla** para capturar el seguimiento en una tabla de base de datos.  
  
         Si quiere, seleccione **Establecer número máximo de filas** y especifique un valor.  
  
5. Opcionalmente, active la casilla **Habilitar hora de detención de seguimiento** para especificar una fecha y hora de detención. 
  
6. Seleccione la pestaña **Selección de eventos**.  
  
7. En la columna de datos **Eventos**, expanda la categoría de eventos **Locks** y active la casilla **Deadlock graph**. Si la categoría de eventos **Locks** no está disponible, active la casilla **Mostrar todos los eventos** para mostrarla.  
  
     La pestaña **Configuración de extracción de eventos** se agrega al cuadro de diálogo **Propiedades de seguimiento**.  
  
8. En la pestaña **Configuración de extracción de eventos**, seleccione **Guardar eventos XML de interbloqueo por separado**.  
  
9. En el cuadro de diálogo **Guardar como**, escriba el nombre del archivo en que quiera almacenar los eventos de grafo de interbloqueo.  
  
10. Seleccione **Todos los lotes XML de interbloqueo en un solo archivo** para guardar todos los eventos de grafo de interbloqueo en un solo archivo XML. O bien seleccione **Cada lote XML de interbloqueo en un archivo independiente** para crear un nuevo archivo XML para cada grafo de interbloqueo.  
  
 Una vez guardado el archivo de interbloqueo, puede abrir el archivo en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, vea [Abrir, ver e imprimir un archivo de interbloqueo &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/open-view-and-print-a-deadlock-file-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Consulte también  
 [Analizar interbloqueos con SQL Server Profiler](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)  
  
  
