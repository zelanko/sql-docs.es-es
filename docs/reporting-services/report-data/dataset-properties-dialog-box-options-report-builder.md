---
title: "Cuadro de diálogo de propiedades de conjunto de datos, opciones (generador de informes) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- "10020"
- sql13.rtp.rptdesigner.datasetproperties.options.f1
- "10130"
ms.assetid: 43e50133-45ef-47a2-b575-34dfcc28ec98
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8eea917788cfd0811750a1ffb59888fa7e2a156a
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="dataset-properties-dialog-box-options-report-builder"></a>Propiedades del conjunto de datos (cuadro de diálogo), Opciones (Generador de informes)
  Seleccione **Opciones** en el cuadro de diálogo **Propiedades del conjunto de datos** para cambiar opciones de datos, como las opciones de intercalación y el tratamiento de subtotales como datos detallados, para la consulta. Para obtener más información sobre las intercalaciones, vea [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md) en los [Libros en pantalla de SQL Server](http://go.microsoft.com/fwlink/?linkid=98335).  
  
 Las opciones de datos que forman parte de una definición de conjunto de datos compartido en el servidor de informes afectan a todos los informes que usan el conjunto de datos compartido. Puede invalidar las opciones para el conjunto de datos compartido una vez agregado a un informe. Estos cambios solo afectan al informe en el que se definen.  
  
 Las opciones de datos para un conjunto de datos incrustado solo afectan al informe en el que se definen.  
  
 Para obtener más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opciones  
 **Intercalación**  
 Seleccione una configuración regional que determine la secuencia de intercalación que se va a utilizar para ordenar los datos. **Predeterminado** indica que el servidor de informes debería intentar obtener el valor del proveedor de datos al ejecutar el informe. Si no se puede obtener, el valor predeterminado se deriva de la configuración regional del equipo.  
  
 **Distinción de mayúsculas y minúsculas**  
 Seleccione un valor que determine la distinción de mayúsculas y minúsculas. Esta opción indica si en los datos se hace esta distinción. Puede establecer **Distinción de mayúsculas y minúsculas** en **True**, **False**o **Auto**. El valor predeterminado ( **Auto**) indica que el servidor de informes debería intentar obtener el valor del proveedor de datos al ejecutar el informe. Si el proveedor de datos no admite el tipo de distinción de mayúsculas y minúsculas, el informe se ejecuta como si el valor fuera **False**. Si conoce el valor y sabe que el proveedor lo admite, elija **True**.  
  
 **Distinción de acentos**  
 Seleccione un valor que determine la distinción de acentos. **Distinción de acentos** indica si en los datos se hace distinción de acentos; se puede establecer en **True**, **False**o **Auto**. El valor predeterminado ( **Auto**) indica que el servidor de informes debería intentar obtener el valor del proveedor de datos al ejecutar el informe. Si el proveedor de datos no admite el tipo de distinción de acentos, el informe se ejecuta como si el valor fuera **False**. Si conoce el valor y sabe que el proveedor lo admite, elija **True**.  
  
 **Distinción de tipos de kana**  
 Seleccione un valor que determine la distinción de tipos de kana. Esta opción indica si en los datos se hace distinción de tipos de kana; se puede establecer en **True**, **False**o **Auto**. El valor predeterminado ( **Auto**) indica que el servidor de informes debería intentar obtener el valor del proveedor de datos al ejecutar el informe. Si el proveedor de datos no admite el tipo de distinción de tipos de kana, el informe se ejecuta como si el valor fuera **False**. Si conoce el valor y sabe que el proveedor lo admite, elija **True**.  
  
 **Distinción de ancho**  
 Seleccione un valor que determine la distinción de ancho. Esta opción indica si en los datos se hace distinción de ancho y se puede establecer en **True**, **False**o **Auto**. El valor predeterminado ( **Auto**) indica que el servidor de informes debería intentar obtener el valor del proveedor de datos al ejecutar el informe. Si el proveedor de datos no admite el tipo de distinción de ancho, el informe se ejecuta como si el valor fuera **False**. Si conoce el valor y sabe que el proveedor lo admite, elija **True**.  
  
 **Interpretar los subtotales como filas de detalles**  
 Seleccione un valor que indique si desea que las filas de subtotales se interpreten como filas de detalles en lugar de como filas agregadas. El valor predeterminado, **Auto**, indica que las filas de subtotales se deberían tratar como filas de detalles si el informe no usa la función **Aggregate**() para acceder a cualquier campo del conjunto de datos. Si desea que las filas de subtotales se interpreten como filas agregadas, elija **False**. Si quiere que las filas de subtotales se interpreten como filas de detalles y sabe que no usan la función **Aggregate**(), elija **True**.  
  
## <a name="see-also"></a>Vea también  
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [Función de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Propiedades del conjunto de datos (cuadro de diálogo), Consulta &#40;Generador de informes&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md)  
  
  
