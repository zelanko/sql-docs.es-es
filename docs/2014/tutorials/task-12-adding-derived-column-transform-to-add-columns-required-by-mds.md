---
title: 'Tarea 12: agregar la transformación columna derivada para agregar las columnas requeridas por MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 18789f5bc1d97e1531588d50e2430829f95912b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65485238"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>Tarea 12: agregar la transformación Columna derivada para agregar las columnas necesarias en MDS
  En esta tarea, agregará la transformación Columna derivada al flujo de datos. Agrega dos columnas derivadas, **ImportType** y **BatchTag**, a los registros que se pasan a esta transformación. Debe agregar estas columnas antes de cargar los datos en las tablas de ensayo en MDS. Son dos columnas necesarias para las tablas de ensayo en MDS. Consulte [tablas de almacenamiento provisional de miembros hoja](../master-data-services/leaf-member-staging-table-master-data-services.md) para obtener más detalles.  
  
1.  Arrastre y coloque la **transformación columna derivada** desde la sección **común** del **cuadro de herramientas de SSIS** hasta la pestaña flujo de **datos** .  
  
2.  Haga clic con el botón secundario en transformación de **columna derivada** en la pestaña **flujo de datos** y haga clic en **cambiar nombre**. Escriba **Add Columns required by MDS** y presione **entrar**.  
  
3.  Conecte **filtros duplicados** para **Agregar las columnas requeridas por MDS** mediante el conector azul. Debería ver el cuadro de diálogo **selección de entrada y salida** .  
  
4.  En el cuadro de diálogo **selección de salida de entrada** , seleccione **Registros únicos**y haga clic en **Aceptar**.  
  
     ![Cuadro de diálogo Selección de entrada y salida](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "Cuadro de diálogo Selección de entrada y salida")  
  
5.  Haga clic en **SSIS** en la barra de menús y haga clic en **variables**.  
  
6.  En la ventana **variables** , haga clic en el botón **Agregar variable** de la barra de herramientas.  
  
     ![Ventana Variables de SSIS](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "Ventana Variables de SSIS")  
  
7.  Escriba **ImportType** para el **nombre** y **2** para el **valor**. Debe especificar el valor 2 porque desea agregar dos miembros nuevos a una entidad en MDS. Para obtener más información sobre este parámetro, consulte [tabla de almacenamiento provisional de miembros hoja](../master-data-services/leaf-member-staging-table-master-data-services.md).  
  
8.  Haga clic de nuevo en el botón **Agregar variable** de la barra de herramientas.  
  
9. Escriba **BatchTag** para el **nombre**, seleccione **cadena** para el **tipo de datos**y **EIMBatch** para el **valor**. **BatchTag** es simplemente un nombre único para el lote que se va a enviar a MDS.  
  
10. En la pestaña **flujo de datos** , haga doble clic en **Agregar columnas requeridas por MDS**.  
  
11. En el cuadro de diálogo **Editor de transformación columna derivada** , en el **cuadro de lista del panel inferior**, escriba **ImportType** para el nombre de la **columna derivada**.  
  
12. Expanda **variables y parámetros** en el panel superior izquierdo, arrastre y coloque **User:: ImportType** a la columna **Expression** .  
  
     ![Columna derivada, editor de transformación](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "Columna derivada, editor de transformación")  
  
13. Escriba **BatchTag** en la siguiente fila del nombre de la **columna derivada**.  
  
14. Arrastre y coloque **User:: BatchTag** desde **variables y parámetros** a la columna **Expression** .  
  
15. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **transformación columna derivada** .  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 13: agregar el destino de OLE DB para escribir datos en la tabla de ensayo de MDS](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
