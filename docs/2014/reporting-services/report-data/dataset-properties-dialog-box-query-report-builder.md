---
title: Propiedades del conjunto de datos (cuadro de diálogo), Consulta (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10024"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8a74bac81874eaeeecd9b9abcdcbfee27e07909c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62696573"
---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>Propiedades del conjunto de datos (cuadro de diálogo), Consulta (Generador de informes)
  Seleccione **Consulta** en el cuadro de diálogo **Propiedades del conjunto de datos** para elegir un conjunto de datos compartido de un servidor de informes o para crear un conjunto de datos incrustado. Para un conjunto de datos incrustado, debe elegir un origen de datos y generar una consulta.  
  
 El cuadro de diálogo **Propiedades del conjunto de datos** incluye lo siguiente:  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Parámetros &#40;Generador de informes&#41;](../dataset-properties-dialog-box-parameters-report-builder.md)  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Campos &#40;Generador de informes&#41;](../dataset-properties-dialog-box-fields-report-builder.md)  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Opciones &#40;Generador de informes&#41;](dataset-properties-dialog-box-options-report-builder.md)  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Filtros &#40;Generador de informes&#41;](../dataset-properties-dialog-box-filters-report-builder.md)  
  
 Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opciones  
 **Name**  
 Escriba el nombre del conjunto de datos. Este nombre no puede coincidir con el nombre de cualquier grupo o región de datos del informe.  
  
 **Usar un conjunto de datos compartido**  
 Seleccione esta opción para utilizar un conjunto de datos predefinido del servidor de informes.  
  
 **Examinar**  
 Vaya a una carpeta en un servidor de informes o sitio de SharePoint, y seleccione un conjunto de datos compartido (.rsd).  
  
 **Utilizar un conjunto de datos incrustado en mi informe**  
 Seleccione esta opción para crear un conjunto de datos y usarlo únicamente este informe.  
  
 **Origen de datos**  
 Seleccione el origen de datos en el que se basará el conjunto de datos. Para crear un origen de datos nuevo, haga clic en **Nuevo**.  
  
 **Tipo de consulta**  
 Seleccione el tipo de comando o consulta que se utilizará para el conjunto de datos. Seleccione **Texto** para ejecutar una consulta con el objeto de recuperar datos de la base de datos. Seleccione **Tabla** para usar la característica de **TableDirect** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y seleccionar todos los campos de una tabla. Seleccione **Procedimiento almacenado** para ejecutar un procedimiento almacenado por su nombre. **Text** está seleccionado de manera predeterminada y se utiliza para la mayoría de las consultas. Para editar la consulta de origen de datos seleccionada, haga clic en **Diseñador de consultas**.  
  
> [!NOTE]  
>  Todos los orígenes de datos no admiten todos los tipos de consulta. Por ejemplo, **Tabla** solo la admiten los tipos de orígenes de datos **OLE DB** y **ODBC**.  
  
 **Consulta**  
 Esta opción aparece cuando se elige la opción de tipo de comando **Texto** . Escriba una consulta o importe una consulta existente haciendo clic en **Importar**. Haga clic en el botón **Expresión** (*fx*) para editar la expresión.  
  
> [!NOTE]  
>  Si usó un diseñador de consultas para crear una consulta, el texto de la misma aparece en este cuadro.  
  
 **Nombre de la tabla**  
 Escriba el nombre de la tabla que desea usar como conjunto de datos. Esta opción aparece cuando se selecciona **Tabla**.  
  
 **Seleccione o escriba el nombre del procedimiento almacenado**  
 Escriba o elija el nombre del procedimiento almacenado que desea usar. Haga clic en el botón **Expresión** (*fx*) para editar la expresión. Esta opción aparece cuando se elige la opción de tipo de comando Procedimiento almacenado.  
  
 **Tiempo de espera (en segundos)**  
 Escriba el número de segundos que deben transcurrir para que se supere el tiempo de espera de la consulta. El valor predeterminado es 30 segundos. El valor de **Tiempo de espera** debe permanecer en blanco o ser mayor que cero. Si está en blanco, nunca se supera el tiempo de espera de la consulta.  
  
 **Actualizar los campos**  
 Ejecute el comando de consulta para actualizar la lista de campos de la página [cuadro de diálogo Propiedades del conjunto de datos, Campos](../dataset-properties-dialog-box-fields-report-builder.md) .  
  
## <a name="see-also"></a>Vea también  
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-datasets-ssrs.md)   
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Diseñadores de consultas &#40;Generador de informes&#41;](../query-designers-report-builder.md)  
  
  
