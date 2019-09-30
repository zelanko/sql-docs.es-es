---
title: Revisar asignación de tipos de datos (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.reviewissues.f1
ms.assetid: 0625c4f9-b8ff-4593-b884-39398b9d43af
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f0bd7fe34b1945c3f0f2255e256ead38a6d15e3a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296268"
---
# <a name="review-data-type-mapping-sql-server-import-and-export-wizard"></a>Revisar asignación de tipos de datos (Asistente para importación y exportación de SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Si ha especificado una asignación de tipo de datos que puede que no se complete correctamente en la lista **Asignaciones** del cuadro de diálogo **Asignaciones de columnas** , en el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se mostrará la página **Revisar asignación de tipos de datos** . En esta página, revise información detallada sobre las conversiones de tipos de datos que el asistente necesita realizar para que los datos de origen sean compatibles con el destino. En esta información se incluyen indicaciones visuales para distinguir las conversiones de tipos de datos que se espera que sean correctas de las que podrían producir errores o truncamientos. En cada conversión puede decidir si quiere aceptar la conversión que sugiere el asistente, así como especificar cómo administrar los errores que se produzcan.   
  
> [!TIP]
> No se pueden cambiar las asignaciones de tipos de datos en la página **Revisar asignación de tipos de datos** . Pero puede hacer clic en **Volver** para volver a la página **Seleccionar tablas y vistas de origen** y, después, hacer clic en **Editar asignaciones** para volver a abrir el cuadro de diálogo **Asignaciones de columnas** . En el cuadro de diálogo **Asignaciones de columnas** puede especificar asignaciones de tipos de datos que es más probable que se completen correctamente. Para volver a ver el cuadro de diálogo **Asignaciones de columnas** , vea [Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  
  
## <a name="screen-shot-of-the-review-data-type-mapping-page"></a>Captura de pantalla de la página Revisar asignación de tipo de datos
 La siguiente captura de pantalla muestra un ejemplo de la página del asistente **Revisar asignación de tipos de datos**.
 
 En este ejemplo:
 -   El usuario ha especificado una asignación en el cuadro de diálogo **Asignaciones de columnas** que podría no realizarse correctamente.
 -   El icono de advertencia en la fila de la lista **Tabla** indica que hay un problema al convertir, como mínimo, una columna de datos de los resultados de la consulta a un tipo de datos compatible en la tabla de destino.
 -   El icono de advertencia de la primera fila de la lista **Asignación de tipo de datos** indica que la asignación del tipo de datos **int** de la columna de origen al tipo de datos **smalldatetime** de la columna de destino podría provocar una pérdida de datos.
 
 ![Página Revisar asignación de tipos de datos del Asistente para importación y exportación](../../integration-services/import-export-data/media/review-mapping.png "Página Revisar asignación de tipos de datos del Asistente para importación y exportación") 
 
## <a name="review-the-source-and-destination-tables"></a>Revisar las tablas de origen y destino  
 En la sección superior de la página **Revisar asignación de tipos de datos** se muestra la lista **Tabla** , que contiene una lista de las tablas que se van a copiar del origen al destino. Para ver información de conversión sobre una tabla individual, seleccione una tabla en la lista **Tabla** . La información de conversión de las columnas individuales de la tabla seleccionada aparece en la cuadrícula **Asignación de tipo de datos** de la parte inferior de la página.

En este ejemplo, los resultados de la consulta que el usuario proporcionó se copiarán en la tabla Sales.CustomerNew2 en el destino. El icono de advertencia indica que hay un problema al convertir, como mínimo, una columna de datos de los resultados de la consulta a un tipo de datos compatible en la tabla de destino.

![Revisar asignación: Tablas](../../integration-services/import-export-data/media/review-mapping-tables.png)
  
 En la tabla siguiente se describen las columnas de la lista **Tabla** .  
  
|columna|Descripción|  
|------------|-----------------|  
|(Icono de origen)|Indica la probabilidad de que las conversiones de tipos de datos sean correctas:<br /> - Un icono de marca de verificación **verde** indica que el asistente espera que todas las conversiones de tipos de datos para esta tabla sean correctas.<br />- Un icono de advertencia **amarillo** indica que necesita revisar las conversiones individuales que realizará el asistente. Para revisar estas conversiones, seleccione la tabla y, a continuación, revise las conversiones para las columnas individuales en la lista **Asignación de tipo de datos** .<br />- Un icono de error **rojo** indica que el asistente no puede realizar algunas de las conversiones para esta tabla de forma confiable.|  
|**Origen**|El nombre de la tabla de origen.|  
|(Icono de destino)|Indica si el destino ya existe o lo crea el asistente:<br /> - Un icono de tabla indica que el destino es una tabla existente.<br />- Un icono de tabla con un rayo de sol indica que el destino es una tabla nueva que va a crear el asistente.|  
|**Destino**|Nombre de la tabla de destino.|  
  
## <a name="review-the-data-type-mappings"></a>Revisar las asignaciones de tipos de datos  
 La sección central de la página **Revisar asignación de tipos de datos** es la lista **Asignación de tipo de datos** . En esta cuadrícula se proporciona información de conversión detallada sobre las columnas de la tabla de origen que está seleccionada en la lista **Tabla** de la parte superior de la página.

En este ejemplo, cada una de las columnas del origen se copiará en una columna con el mismo nombre y el mismo tipo de datos en el destino. El icono de advertencia de la primera fila de la lista **Asignación de tipo de datos** indica que la asignación del tipo de datos **int** de la columna de origen al tipo de datos **smalldatetime** de la columna de destino podría provocar una pérdida de datos.
 
![Revisar asignación: Asignaciones](../../integration-services/import-export-data/media/review-mapping-mappings.png)  

En la tabla siguiente se describen las columnas de la lista **Asignación de tipo de datos** . 

|columna|Descripción|  
|------------|-----------------|  
|(Icono de conversión)|Indica la probabilidad de que las conversiones de tipos de datos sean correctas:<br /> - Un icono de marca de verificación **verde** indica que el asistente espera que la conversión de tipos de datos de esta columna sea correcta.<br />- Un icono de advertencia **amarillo** indica que necesita revisar la conversión que va a realizar el asistente. Para revisar la conversión, haga doble clic en la columna para ver el cuadro de diálogo **Detalles de conversión de columna** . Para más información, vea [Cuadro de diálogo Detalles de conversión de columna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md).<br />- Un icono de error **rojo** indica que el asistente no puede realizar la conversión de forma confiable.|  
|**Columna de origen**|El nombre de la columna de origen.|  
|**Tipo de origen**|El tipo de datos de la columna de origen.|  
|**Columna de destino**|El nombre de la columna de destino.|  
|**Tipo de destino**|El tipo de datos de la columna de destino.|  
|**Convertir**|Especifique si quiere continuar con la conversión planeada:<br /> - Seleccione la casilla para que el asistente continúe con la conversión planeada.<br />- Desactive la casilla para cancelar la conversión de tipos de datos.|  
|**Al producirse un error**|Especifique cómo controla el asistente los errores:<br /> - Use la configuración **Al producirse un error (global)** , que puede especificar en la parte inferior de esta página.<br />- Se produce un error y se detiene el proceso de importación o exportación.<br />- Se omite el error.|  
|**Al producirse truncamiento**|Especifique cómo controla el asistente el truncamiento:<br /> - Use la configuración **Al producirse truncamiento (global)** , que puede especificar en la parte inferior de esta página.<br />- Se produce un error y se detiene el proceso de importación o exportación.<br />- Se omite el truncamiento.|  

> [!TIP]
> Para ver información detallada sobre la conversión de una columna de datos específica, haga doble clic en cualquier fila de la lista. El cuadro de diálogo **Detalles de conversión de columna** se abre y muestra información de conversión más detallada para la columna. Para más información, vea [Cuadro de diálogo Detalles de conversión de columna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md).
 
## <a name="specify-global-error-handling-options"></a>Especificar opciones globales de control de errores  
 En la sección inferior de la página **Revisar asignación de tipos de datos** puede especificar las opciones de control de errores que se aplican de forma predeterminada a todas las columnas. Esta configuración se aplica a todas las conversiones que tienen seleccionada la opción **Usar global** en las columnas **Al producirse un error** o **Al producirse truncamiento** de la lista **Asignación de tipo de datos** .   

En este ejemplo se muestran los valores predeterminados para las dos opciones de control de errores globales.

![Revisar asignación: Errores](../../integration-services/import-export-data/media/review-mapping-errors.png)

 **Al producirse un error (global)**  
 Especifique cómo controla el asistente los errores:  
 -   Termine con un error y detenga el proceso de importación o exportación. Este es el valor predeterminado.
 -   Omita el error y continúe el proceso de importación o exportación.  
  
 **Al producirse truncamiento (global)**  
 Especifique cómo controla el asistente el truncamiento de datos:  
 -   Termine con un error y detenga el proceso de importación o exportación. Este es el valor predeterminado.
 -   Omita el trocamiento y continúe el proceso de importación o exportación.  
   
## <a name="whats-next"></a>¿Qué sigue?  
 Después de revisar las advertencias, de especificar las opciones de conversión y de especificar cómo prefiere administrar los errores, en la página **Revisar asignación de tipos de datos** se volverá a mostrar el cuadro de diálogo **Asignaciones de columnas** . Para más información, vea [Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Vea también
[Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

