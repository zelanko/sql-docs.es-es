---
title: Guardar eventos Showplan XML por separado (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: 33320a7a-36e8-401c-876d-5b82c49abd85
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c92c08349a473aa4a83205cc539eec3577619109
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150429"
---
# <a name="save-showplan-xml-events-separately-sql-server-profiler"></a>Guardar eventos Showplan XML por separado (SQL Server Profiler)
  En este tema se describe cómo guardar eventos **Showplan XML** capturados en seguimientos en archivos .SQLPlan distintos mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Puede abrir los archivos de evento **Showplan XML** en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]para poder ver el plan de ejecución gráfico de cada evento.  
  
### <a name="to-save-showplan-xml-events-separately"></a>Para guardar eventos Showplan XML por separado  
  
1.  En el menú **Archivo** , haga clic en **Nuevo seguimiento**y, a continuación, conéctese a una instancia de SQL Server.  
  
     Aparecerá el cuadro de diálogo **Propiedades de seguimiento**.  
  
    > [!NOTE]  
    >  Si está seleccionada la opción **iniciar el seguimiento inmediatamente después de establecer la conexión**, el cuadro de diálogo Propiedades de **seguimiento**no aparecerá y, en su lugar, se iniciará el seguimiento. Para desactivar esta configuración, en el menú **Herramientas**, haga clic en **Opciones**y desactive la casilla **Iniciar el seguimiento inmediatamente tras realizar la conexión** .  
  
2.  En el cuadro de diálogo **Propiedades de seguimiento** , en el cuadro **Nombre de seguimiento** , escriba un nombre para el seguimiento.  
  
3.  En la lista **Usar la plantilla** , seleccione la plantilla de seguimiento que desea utilizar para el seguimiento o seleccione la opción **En blanco** si no desea utilizar ninguna plantilla.  
  
4.  Realice una de las siguientes acciones:  
  
    -   Active la casilla**Guardar en archivo** para capturar el seguimiento en un archivo. Especifique un valor en **Establecer el tamaño máximo de archivo (MB)** . Opcionalmente, active las casillas **Habilitar sustitución incremental de archivos** y **El servidor procesa los datos de seguimiento** .  
  
    -   Active la casilla**Guardar en tabla** para capturar el seguimiento en una tabla de base de datos. Opcionalmente, haga clic en **establecer número máximo de filas**y especifique un valor.  
  
5.  Opcionalmente, active la casilla **Habilitar hora de detención de seguimiento** para especificar una fecha y hora de detención.  
  
6.  Haga clic en la pestaña **Selección de eventos**.  
  
7.  En el cuadro de diálogo **Eventos**, expanda la categoría de evento **Rendimiento**y luego active la casilla **Showplan XML**. Si la categoría de evento **Rendimiento** no está disponible, active la casilla **Mostrar todos los eventos** para mostrarla.  
  
     Aparecerá el cuadro de diálogo **Configuración de extracción de eventos**se agrega al cuadro de diálogo **Propiedades de seguimiento**.  
  
8.  En el menú **Configuración de extracción de eventos**, haga clic en **Guardar eventos de plan de presentación XML por separado**.  
  
9. En el cuadro de diálogo **Guardar como** , especifique el nombre de archivo para guardar los eventos **Showplan XML** .  
  
10. Haga clic en **Todos los lotes de plan de presentación en un solo archivo** para guardar todos los eventos **Showplan XML** en un solo archivo XML, o haga clic en **Cada lote de plan de presentación en un archivo independiente**para crear un archivo XML nuevo para cada evento **Showplan XML** .  
  
11. Para ver el archivo del evento **Showplan XML** en SQL Server Management Studio, en el menú **Archivo** , seleccione **Abrir**y haga clic en **Archivo**. Navegue al directorio donde ha guardado el archivo o archivos del evento **Showplan XML** para seleccionar uno y abrirlo. Los archivos de evento**Showplan XML** tienen la extensión de archivo .SQLPlan.  
  
## <a name="see-also"></a>Consulte también  
 [Analizar consultas con resultados de SHOWPLAN en SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
