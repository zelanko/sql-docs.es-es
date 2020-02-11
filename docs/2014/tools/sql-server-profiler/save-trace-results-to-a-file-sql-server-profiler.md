---
title: Guardar los resultados de un seguimiento en un archivo (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: ac528747-0c19-4f3d-96f5-44c762a4abed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 206ba778a5c131ac4f9260ed37de63b29de86820
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63025679"
---
# <a name="save-trace-results-to-a-file-sql-server-profiler"></a>Guardar los resultados de un seguimiento en un archivo (SQL Server Profiler)
  En este tema se describe cómo utilizar el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]para guardar los resultados de un seguimiento en un archivo.  
  
### <a name="to-save-trace-results-to-a-file"></a>Para guardar los resultados de un seguimiento en un archivo  
  
1.  En el menú **Archivo** , haga clic en **Nuevo seguimiento**y conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Aparecerá el cuadro de diálogo **Propiedades de seguimiento**.  
  
    > [!NOTE]  
    >  Si se selecciona **Iniciar el seguimiento inmediatamente tras realizar la conexión**, el cuadro de diálogo **Propiedades de seguimiento**no aparecerá y, en su lugar, se iniciará el seguimiento. Para desactivar esta configuración, en el menú **Herramientas**, haga clic en **Opciones**y desactive la casilla **Iniciar el seguimiento inmediatamente tras realizar la conexión** .  
  
2.  En el cuadro **Nombre de seguimiento** , escriba un nombre para el seguimiento.  
  
3.  Active la casilla **Guardar en el archivo** .  
  
     Aparece el cuadro de diálogo **Guardar como**.  
  
4.  En el cuadro de diálogo **Guardar como**, especifique una ruta de acceso y un nombre de archivo. Haga clic en **Guardar**.  
  
    > [!NOTE]  
    >  Asegúrese de que el servicio SQL Server tiene los permisos necesarios para escribir en un archivo en el directorio especificado.  
  
5.  En el cuadro de diálogo **Propiedades de seguimiento** , en el cuadro de texto **Establecer el tamaño máximo de archivo (MB)** , especifique el tamaño máximo del archivo. El valor predeterminado es 5 megabytes (MB).  
  
6.  Opcionalmente, especifique las siguientes opciones:  
  
    -   Active la casilla **Habilitar sustitución incremental de archivos** para que el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] cree archivos para los datos del seguimiento si se alcanza el tamaño máximo del archivo. Esta opción está activada de forma predeterminada.  
  
    -   Active la casilla **El servidor procesa los datos de seguimiento** para asegurarse de que el servidor registra todos los eventos del seguimiento.  
  
        > [!NOTE]  
        >  Cuando la casilla **El servidor procesa los datos de seguimiento**está desactivada, el servidor no registra los eventos si con ello el rendimiento disminuye considerablemente.  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
