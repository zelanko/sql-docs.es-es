---
title: "Propiedades del conjunto de datos (cuadro de diálogo), Consulta (Generador de informes) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- "10024"
- sql13.rtp.rptdesigner.datasetproperties.query.f1
- "10160"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d803a7ebaa7b33333d3b20b280af354b80d640e7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>Propiedades del conjunto de datos (cuadro de diálogo), Consulta (Generador de informes)
  Seleccione **Consulta** en el cuadro de diálogo **Propiedades del conjunto de datos** para elegir un conjunto de datos compartido de un servidor de informes o para crear un conjunto de datos incrustado. Para un conjunto de datos incrustado, debe elegir un origen de datos y generar una consulta.  
  
 El cuadro de diálogo **Propiedades del conjunto de datos** incluye lo siguiente:  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Parámetros &#40;Generador de informes&#41;](http://msdn.microsoft.com/library/3a0672ad-c969-455b-b952-585164ce1dda)  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Campos &#40;Generador de informes&#41;](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42)  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Opciones &#40;Generador de informes&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-options-report-builder.md)  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Filtros &#40;Generador de informes&#41;](http://msdn.microsoft.com/library/933a6f44-4eb7-4e73-9c40-ac0fd17b23d3)  
  
 Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opciones  
 **Nombre**  
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
 Ejecute el comando de consulta para actualizar la lista de campos de la página [cuadro de diálogo Propiedades del conjunto de datos, Campos](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42) .  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [Diseñadores de consultas &#40;Generador de informes&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)  
  
  
