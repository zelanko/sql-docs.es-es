---
title: Cuadro de diálogo de propiedades de conjunto de datos, la consulta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10160"
- sql12.rtp.rptdesigner.datasetproperties.query.f1
ms.assetid: 1fa34a4b-7de0-4e92-99fa-bc28a206773f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 588927f94d2c50d5d34485cae030e9cea6a6b5ec
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292398"
---
# <a name="dataset-properties-dialog-box-query"></a>Propiedades del conjunto de datos (cuadro de diálogo), Consulta
  Seleccione **Consulta** en el cuadro de diálogo **Propiedades del conjunto de datos** para elegir un origen de datos y crear una consulta.  
  
 El cuadro de diálogo **Propiedades del conjunto de datos** incluye lo siguiente:  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Parámetros](report-data/dataset-properties-dialog-box-parameters.md)  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Campos](../../2014/reporting-services/dataset-properties-dialog-box-fields.md)  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Opciones](../../2014/reporting-services/dataset-properties-dialog-box-options.md)  
  
-   [Propiedades del conjunto de datos (cuadro de diálogo), Filtros](report-data/dataset-properties-dialog-box-filters.md)  
  
## <a name="options"></a>Opciones  
 **Name**  
 Escriba el nombre del conjunto de datos. Este nombre no puede coincidir con el nombre de cualquier grupo o región de datos del informe.  
  
 **Origen de datos**  
 Seleccione el origen de datos en el que se basará el conjunto de datos. Para crear un origen de datos nuevo, haga clic en **Nuevo**.  
  
 **Tipo de consulta**  
 Seleccione el tipo de comando o consulta que se utilizará para el conjunto de datos. Seleccione **Texto** para ejecutar una consulta con el objeto de recuperar datos de la base de datos. Seleccione **Tabla** para usar la característica de **TableDirect** de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y seleccionar todos los campos de una tabla. Seleccione **Procedimiento almacenado** para ejecutar un procedimiento almacenado por su nombre. **Text** está seleccionado de manera predeterminada y se utiliza para la mayoría de las consultas. Para editar la consulta de origen de datos seleccionada, haga clic en **Diseñador de consultas**.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Diseñadores de consultas &#40;Generador de informes&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [Diseñadores de consultas de Reporting Services](../../2014/reporting-services/reporting-services-query-designers.md)  
  
  
