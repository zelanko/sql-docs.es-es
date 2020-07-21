---
title: 'Tarea 13: agregar OLE DB destino para escribir datos en la tabla de ensayo de MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bb39e9d50d135adfedcf307cda2ad703e302eda5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061143"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>Tarea 13: Adición del destino de OLE DB para escribir datos en la tabla de ensayo de MDS
  Ahora que ha agregado los valores de **ImportType** y **BatchTag** a todos los registros, está listo para enviarlos a MDS para el almacenamiento provisional. En esta tarea, usará el destino OLE DB para escribir los datos en **STG. supplier_Leaf** tabla de ensayo.  
  
1.  Arrastre **OLE DB destino** desde la sección **otros destinos** del **cuadro de herramientas de SSIS** hasta la pestaña **flujo de datos** y colóquelo en **Agregar columnas requeridas por MDS**.  
  
2.  Haga clic con el botón secundario en **OLE DB destino** en la pestaña **flujo de datos** y haga clic en **cambiar nombre**. Escriba **escribir datos de proveedor en la tabla de ensayo de MDS** y presione **entrar**.  
  
3.  Conecte las **columnas Add required by MDS** para **escribir datos de proveedor en la tabla de ensayo de MDS** mediante el conector azul.  
  
4.  Haga doble clic en **escribir datos de proveedor en la tabla de ensayo de MDS** en la pestaña flujo de **datos** .  
  
5.  En el cuadro de diálogo **Editor de destino de OLE DB** , asegúrese de que **(local). MDS** (o **localhost). MDS**) se selecciona para el campo **Administrador de conexiones de OLE DB** .  
  
6.  Seleccione **STG. Supplier_Leaf** tabla de la lista de **nombres de la tabla o la vista**.  
  
     ![Editor de destino OLEDB](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "Editor de destino OLEDB")  
  
7.  Cambie a la página **asignaciones** ; para ello, haga clic en **asignación** en el menú de la izquierda.  
  
8.  Asigne las columnas de **entrada** y de **destino** como se muestra en la tabla siguiente.  
  
     ![Editor de destino de OLEDB - Asignaciones](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "Editor de destino de OLEDB - Asignaciones")  
  
9. Confirme que está usando **_Output** columnas para las columnas de entrada, no para las columnas de **_Status** o **_Source** . **_Output** columnas contienen los valores de salida de limpieza de DQS.  
  
10. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editor de destino de OLE DB** .  
  
11. El flujo de datos debe ser similar al de la ilustración siguiente.  
  
     ![Flujo de datos completado](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "Flujo de datos completado")  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 14: Adición de la tarea Ejecutar SQL al flujo de control para ejecutar el procedimiento almacenado de MDS](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
