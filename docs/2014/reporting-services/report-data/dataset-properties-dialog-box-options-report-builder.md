---
title: Propiedades del conjunto de datos (cuadro de diálogo), Opciones (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10020"
ms.assetid: 43e50133-45ef-47a2-b575-34dfcc28ec98
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b174f9ad33ee38c2f47ffc8a684cddd7ea4376bf
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107359"
---
# <a name="dataset-properties-dialog-box-options-report-builder"></a>Propiedades del conjunto de datos (cuadro de diálogo), Opciones (Generador de informes)
  Seleccione **Opciones** en el cuadro de diálogo **Propiedades del conjunto de datos** para cambiar opciones de datos, como las opciones de intercalación y el tratamiento de subtotales como datos detallados, para la consulta. Para obtener más información sobre las intercalaciones, vea [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md) en los [Libros en pantalla de SQL Server](https://go.microsoft.com/fwlink/?linkid=98335).  
  
 Las opciones de datos que forman parte de una definición de conjunto de datos compartido en el servidor de informes afectan a todos los informes que usan el conjunto de datos compartido. Puede invalidar las opciones para el conjunto de datos compartido una vez agregado a un informe. Estos cambios solo afectan al informe en el que se definen.  
  
 Las opciones de datos para un conjunto de datos incrustado solo afectan al informe en el que se definen.  
  
 Para obtener más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opciones  
 **Intercalación**  
 Seleccione una configuración regional que determine la secuencia de intercalación que se va a utilizar para ordenar los datos. **Predeterminado** indica que el servidor de informes debería intentar obtener el valor del proveedor de datos al ejecutar el informe. Si no se puede obtener, el valor predeterminado se deriva de la configuración regional del equipo.  
  
 **Distinción de mayúsculas y minúsculas**  
 Seleccione un valor que determine la distinción de mayúsculas y minúsculas. Esta opción indica si en los datos se hace esta distinción. Puede establecer **Distinción de mayúsculas y minúsculas** en **True**, **False**o **Auto**. El valor predeterminado (**Auto**) indica que el servidor de informes debería intentar obtener el valor del proveedor de datos al ejecutar el informe. Si el proveedor de datos no admite el tipo de distinción de mayúsculas y minúsculas, el informe se ejecuta como si el valor fuera **False**. Si conoce el valor y sabe que el proveedor lo admite, elija **True**.  
  
 **Distinción de acentos**  
 Seleccione un valor que determine la distinción de acentos. **Distinción de acentos** indica si en los datos se hace distinción de acentos; se puede establecer en **True**, **False**o **Auto**. El valor predeterminado (**Auto**) indica que el servidor de informes debería intentar obtener el valor del proveedor de datos al ejecutar el informe. Si el proveedor de datos no admite el tipo de distinción de acentos, el informe se ejecuta como si el valor fuera **False**. Si conoce el valor y sabe que el proveedor lo admite, elija **True**.  
  
 **Distinción de tipos de kana**  
 Seleccione un valor que determine la distinción de tipos de kana. Esta opción indica si en los datos se hace distinción de tipos de kana; se puede establecer en **True**, **False**o **Auto**. El valor predeterminado (**Auto**) indica que el servidor de informes debería intentar obtener el valor del proveedor de datos al ejecutar el informe. Si el proveedor de datos no admite el tipo de distinción de tipos de kana, el informe se ejecuta como si el valor fuera **False**. Si conoce el valor y sabe que el proveedor lo admite, elija **True**.  
  
 **Distinción de ancho**  
 Seleccione un valor que determine la distinción de ancho. Esta opción indica si en los datos se hace distinción de ancho y se puede establecer en **True**, **False**o **Auto**. El valor predeterminado (**Auto**) indica que el servidor de informes debería intentar obtener el valor del proveedor de datos al ejecutar el informe. Si el proveedor de datos no admite el tipo de distinción de ancho, el informe se ejecuta como si el valor fuera **False**. Si conoce el valor y sabe que el proveedor lo admite, elija **True**.  
  
 **Interpretar los subtotales como filas de detalles**  
 Seleccione un valor que indique si desea que las filas de subtotales se interpreten como filas de detalles en lugar de como filas agregadas. El valor predeterminado, **automática**, indica que se deben tratar las filas de subtotales como filas de detalles si el informe no usa el `Aggregate`función () para tener acceso a los campos del conjunto de datos. Si desea que las filas de subtotales se interpreten como filas agregadas, elija **False**. Si desea que las filas de subtotales se interpreten como filas de detalles y sabe que no usan el `Aggregate`() de función, elija **True**.  
  
## <a name="see-also"></a>Vea también  
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Función de agregado &#40;Generador de informes y SSRS&#41;](../report-design/report-builder-functions-aggregate-function.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Propiedades del conjunto de datos (cuadro de diálogo), Consulta &#40;Generador de informes&#41;](dataset-properties-dialog-box-query-report-builder.md)  
  
  
