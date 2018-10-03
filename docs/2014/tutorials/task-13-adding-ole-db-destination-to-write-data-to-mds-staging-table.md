---
title: 'Tarea 13: Agregar destino de OLE DB para escribir datos en la tabla de ensayo de MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bf8a96891040a6a751e0a6e34c902d77cec9dd35
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48223105"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>Tarea 13: agregar el destino de OLE DB para escribir datos en la tabla de ensayo de MDS
  Ahora que ha agregado **ImportType** y **BatchTag** valores de todos los registros, está listo para enviarlos a MDS para el almacenamiento provisional. En esta tarea, utilice el destino de OLE DB para escribir los datos en **stg.supplier_Leaf** tabla de ensayo.  
  
1.  Arrastre **destino de OLE DB** desde **otros destinos** sección la **cuadro de herramientas de SSIS** a la **de flujo de datos** pestaña y colóquelo en  **Agregar columnas necesarias en MDS**.  
  
2.  Haga clic en **destino de OLE DB** en el **de flujo de datos** ficha y haga clic en **cambiar el nombre**. Tipo **escribir datos de proveedor en la tabla de ensayo de MDS** y presione **ENTRAR**.  
  
3.  Conectar el **agregar columnas necesarias en MDS** a **escribir datos de proveedor en la tabla de ensayo de MDS** mediante el conector azul.  
  
4.  Haga doble clic en **escribir datos de proveedor en la tabla de ensayo de MDS** en el **de flujo de datos** ficha.  
  
5.  En el **Editor de destino de OLE DB** diálogo cuadro, asegúrese de que **(local). MDS** (o **localhost. MDS**) está seleccionada para la **OLE DB Connection Manager** campo.  
  
6.  Seleccione **stg. Supplier_Leaf** tabla en la lista de **nombre de la tabla o la vista**.  
  
     ![Editor de destino de OLE DB](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "Editor de destino de OLE DB")  
  
7.  Cambie a la **asignaciones** página haciendo clic en **asignación** en el menú izquierdo.  
  
8.  Mapa **entrada** y **destino** columnas tal como se muestra en la tabla siguiente.  
  
     ![Editor de destino de OLEDB - asignaciones](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "Editor de destino de OLEDB - asignaciones")  
  
9. Confirme que está usando **_Output** columnas para las columnas de entrada, no el **_Status** o **_Source** columnas. **_Salida** columnas contienen los valores de salida de limpieza de DQS.  
  
10. Haga clic en **Aceptar** para cerrar el **Editor de destino de OLE DB** cuadro de diálogo.  
  
11. El flujo de datos debe ser similar al de la ilustración siguiente.  
  
     ![Completar el flujo de datos](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "completado el flujo de datos")  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 14: Agregar la tarea Ejecutar SQL al flujo de control para ejecutar el procedimiento almacenado de MDS](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
