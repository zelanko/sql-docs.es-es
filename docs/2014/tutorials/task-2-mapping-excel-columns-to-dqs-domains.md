---
title: 'Tarea 2: asignar columnas de Excel a dominios de DQS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f347cc92-950f-4021-b7af-393640dfe821
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 646204e2c40c09ac0fac9259f5acc43c7f422894
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006650"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>Tarea 2: Asignación de columnas de Excel a dominios de DQS
    
1.  En la página **Asignación** , seleccione **Archivo de Excel** en **Origen de datos**.  
  
2.  Haga clic en **examinar**, seleccione **Suppliers.xlsx**y haga clic en **abrir**.  
  
3.  Seleccione **IncomingSuppliers $** en la **hoja de cálculo**.  
  
4.  Asigne las columnas como se muestra en la tabla y en la captura de pantalla siguientes. Al crear asignaciones para el dominio de **Estado** , haga clic en el botón **Agregar una asignación de columna** en la barra de herramientas situada justo encima de la lista.  
  
    > [!TIP]  
    >  No se usa la columna o el dominio de ID. de **proveedor** para la limpieza. Usará el dominio ID. de **proveedor** más adelante en la actividad de búsqueda de coincidencias.  
  
    |Columna de Excel|Dominio de DQS|  
    |------------------|----------------|  
    |Nombre del proveedor|Nombre del proveedor|  
    |ContactEmailAddress|Dirección de correo electrónico de contacto|  
    |Address Line|Address Line|  
    |City|City|  
    |State|State|  
    |País (haga clic en **+ (agregar una asignación de columnas)** barra de herramientas para agregar una fila|País|  
    |Zip Code|Zip|  
  
     ![Asignaciones de columnas de Excel a dominios](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "Asignaciones de columnas de Excel a dominios")  
  
5.  Como ha asignado todos los dominios individuales dentro del dominio compuesto **validación de direcciones** , el dominio compuesto participa automáticamente en el proceso de limpieza. Haga clic en el botón **Ver/seleccionar dominios compuestos** para ver que el dominio compuesto **validación de direcciones** se selecciona automáticamente y, a continuación, haga clic en **Aceptar**.  
  
     ![Cuadro de diálogo Ver o seleccionar dominios compuestos](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "Cuadro de diálogo Ver o seleccionar dominios compuestos")  
  
6.  Haga clic en **siguiente** para cambiar a la página **limpieza** .  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 3: Limpieza de datos en la base de conocimiento Proveedores](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  
