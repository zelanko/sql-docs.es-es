---
title: 'Tarea 6: Agregar origen de Excel al flujo de datos | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2ce6d1ec5ab2fc9c57bd56e12b56b13231e74606
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280001"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>Tarea 6: agregar el origen de Excel al flujo de datos
  En esta tarea, agregará un origen de Excel al flujo de datos para leer datos de proveedor del archivo de Excel de origen. El origen de Excel extrae datos de hojas de cálculo o de rangos de libros de Microsoft Excel. Vea el tema [Origen de Excel](http://msdn.microsoft.com/library/ms141683.aspx) para obtener más detalles.  
  
1.  Arrastrar y coloque **Origen de Excel** desde **Otros orígenes** en el **Cuadro de herramientas de SSIS** hasta la pestaña **Flujo de datos** .  
  
2.  Haga clic con el botón secundario en **Origen de Excel** en la pestaña **Flujo de datos** y, a continuación, haga clic en **Cambiar nombre**.  
  
3.  Escriba **Leer datos de proveedor de archivo de Excel** y presione **ENTRAR**.  
  
4.  Haga doble clic en **Leer datos de proveedor de archivo de Excel** para abrir el cuadro de diálogo **Editor de origen de Excel** .  
  
5.  En el cuadro de diálogo **Editor de origen de Excel** , haga clic en **Nuevo** para crear una conexión con Excel.  
  
6.  En el cuadro de diálogo **Administrador de conexiones con Excel** , haga clic en **Examinar**y seleccione el archivo **Suppliers.xls** de la carpeta **EIM Tutorial** . Confirme que **Microsoft Excel 97-2003** está seleccionado en el cuadro **Versión de Excel** y haga clic en **Aceptar**.  
  
     ![Cuadro de diálogo Administrador de conexiones de Excel](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "cuadro de diálogo Administrador de conexiones de Excel")  
  
7.  En el cuadro de diálogo **Editor de origen de Excel** , seleccione **IncomingSuppliers$** en el cuadro de lista **Nombre de la hoja de Excel** .  
  
     ![Nombre de hoja de Excel - proveedores entrantes $](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "nombre de hoja de Excel - proveedores entrantes $")  
  
8.  Haga clic en **Vista previa** para obtener una vista previa de los datos del archivo de Excel.  
  
9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
10. Arrastre y coloque la transformación **Limpieza de DQS** de **Otras transformaciones** del **Cuadro de herramientas de SSIS** hasta la pestaña **Flujo de datos** bajo **Leer datos de proveedor de archivo de Excel**. La transformación Limpieza de DQS emplea Data Quality Services (DQS) para corregir datos aplicando reglas aprobadas de la base de conocimiento. Esta transformación, en tiempo de ejecución, crea un proyecto de limpieza de DQS en el servidor de DQS. Vea el tema [Transformación Limpieza de DQS](http://msdn.microsoft.com/library/ee677619.aspx) para obtener más detalles.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 7: Agregar la transformación Limpieza de DQS al flujo de datos](../integration-services/data-flow/data-flow.md)  
  
  
