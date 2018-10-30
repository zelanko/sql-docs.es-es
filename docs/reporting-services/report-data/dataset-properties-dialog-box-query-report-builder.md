---
title: Propiedades del conjunto de datos (cuadro de diálogo), Consulta (Generador de informes) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: reference
f1_keywords:
- "10024"
- sql13.rtp.rptdesigner.datasetproperties.query.f1
- "10160"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d6e0d987c9976759a870bb58578c9f39593bfb87
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50021769"
---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>Propiedades del conjunto de datos (cuadro de diálogo), Consulta (Generador de informes)
 
Seleccione **Consulta** en el cuadro de diálogo **Propiedades del conjunto de datos** para elegir un conjunto de datos compartido de un servidor de informes o para crear un conjunto de datos incrustado. Para un conjunto de datos incrustado, debe elegir un origen de datos y generar una consulta.  
  
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
>  Si usa un diseñador de consultas para crear una consulta, el texto de la misma aparece en este cuadro.  
  
**Nombre de la tabla**  
Esta opción aparece cuando se selecciona **Tabla**. Escriba el nombre de la tabla que desea usar como conjunto de datos.   
  
**Seleccione o escriba el nombre del procedimiento almacenado**  
Esta opción aparece cuando se elige la opción de tipo de comando Procedimiento almacenado. Escriba o elija el nombre del procedimiento almacenado que desea usar. Haga clic en el botón **Expresión** (*fx*) para editar la expresión.   
  
 **Tiempo de espera (en segundos)**  
 Escriba el número de segundos que deben transcurrir para que se supere el tiempo de espera de la consulta. El valor predeterminado es 30 segundos. El valor de **Tiempo de espera** debe permanecer en blanco o ser mayor que cero. Si está en blanco, nunca se supera el tiempo de espera de la consulta.  
  
 **Actualizar los campos**  
 Ejecute el comando de consulta para actualizar la lista de campos en la página **Campos del cuadro de diálogo Propiedades del conjunto de datos**.  
  
## <a name="see-also"></a>Ver también  
[Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
[Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
[Diseñadores de consultas &#40;Generador de informes&#41;](https://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)  
  
  
