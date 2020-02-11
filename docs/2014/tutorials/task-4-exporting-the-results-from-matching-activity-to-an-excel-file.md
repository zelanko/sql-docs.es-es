---
title: 'Tarea 4: exportar los resultados de la actividad de coincidencia a un archivo de Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 74164c6f6178acbcfe4784dac855c7c0485fc3b0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489443"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>Tarea 4: exportar los resultados de la actividad de coincidencia a un archivo de Excel
  En esta tarea, exportará los resultados de la actividad de coincidencia a un archivo de Excel.  
  
1.  En la página **exportar** , seleccione **archivo de Excel** para el **tipo de destino**.  
  
2.  Seleccione la opción **resultados de permanencia** . En el proceso de permanencia, DQS determina un registro de permanencia para cada clúster en función de la **regla de permanencia** seleccionada.  
  
3.  Haga clic en **examinar** y navegue hasta la carpeta en la que desea almacenar el archivo de salida.  
  
4.  Escriba **cleaned and matched Suppliers. xls** como nombre y haga clic en **abrir**.  
  
5.  Confirme que se ha seleccionado **registro dinámico** para la **regla de permanencia**. Al seleccionar esta opción, se elige el registro dinámico de cada clúster para la salida de un clúster. Las demás opciones de la regla de supervivencia son las siguientes:  
  
    1.  **Registro más completo:** El registro de permanencia es el que tiene el mayor número de campos rellenos.  
  
    2.  **Registro más largo:** El registro de permanencia es el que tiene el mayor número de términos en los campos de origen.  
  
    3.  **Registro más completo y más largo:** El registro de permanencia es el que tiene el mayor número de campos rellenos y tiene el mayor número de términos en cada campo.  
  
     ![Exportar resultados de la página de coincidencias](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "Exportar resultados de la página de coincidencias")  
  
6.  Haga clic en **exportar** para exportar los resultados a un archivo de Excel.  
  
7.  Haga clic en **cerrar** para cerrar el cuadro de diálogo **exportar correspondiente** .  
  
8.  Haga clic en **Finalizar** para finalizar la actividad de búsqueda de coincidencias.  
  
9. Abra el archivo **cleaned and matched Suppliers. xlsx** y confirme que no ve ningún duplicado (SupplierID).  
  
 Ahora, tiene datos de proveedor que se han limpiado y en el que se han buscado coincidencias para quitar valores duplicados.  
  
## <a name="next-step"></a>siguiente paso  
 [Lección 4: almacenar datos de proveedor en MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)  
  
  
