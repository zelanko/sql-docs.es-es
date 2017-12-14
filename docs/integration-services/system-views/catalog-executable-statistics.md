---
title: catalog.executable_statistics | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 3dda28d6-10d8-4294-9b5e-a6048c07faf9
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efd64e5612f10b3521849ff2da6103d2975f4830
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogexecutablestatistics"></a>catalog.executable_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra una fila para cada aplicación ejecutable que se ejecuta, incluida cada iteración de un ejecutable.  
  
 Un ejecutable es una tarea o un contenedor que se agrega al flujo de control de un paquete.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|Statistics_id|bigint|Identificador único de los datos.|  
|Execution_id|bigint|Identificador único de la instancia de la ejecución.<br /><br /> La vista catalog.executions proporciona información adicional sobre las ejecuciones. Para obtener más información, consulte [catalog.executions &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md).|  
|Executable_id|bigint|Identificador único del componente del paquete.<br /><br /> La vista catalog.executables proporciona información adicional sobre los ejecutables. Para obtener más información, consulte [catalog.executables](../../integration-services/system-views/catalog-executables.md).|  
|Execution_path|nvarchar(max)|La ruta de acceso completa de la ejecución del componente del paquete, incluida cada iteración del componente.|  
|Start_time|datetimeoffset(7)|Hora en que el ejecutable entra en la fase previa a la ejecución.|  
|End_time|datetimeoffset(7)|Hora en que el ejecutable entra en la fase posterior a la ejecución.|  
|Execution_duration|int|Tiempo que el ejecutable empleó en la ejecución. El valor se expresa en milisegundos.|  
|Execution_result|smallint|Los posibles valores son los siguientes:<br /><br /> 0 (Correcto)<br /><br /> 1 (Error)<br /><br /> 2 (Finalización)<br /><br /> 3 (Cancelado)|  
|Execution_value|sql_variant|Valor devuelto por la ejecución. Es un valor definido por el usuario.|  
  
## <a name="permissions"></a>Permissions  
 La vista requiere uno de los siguientes permisos:  
  
-   Permiso READ en la instancia de la ejecución.  
  
-   Pertenencia al rol de base de datos de **ssis_admin**.  
  
-   Pertenencia al rol de servidor de **sysadmin**.  
  
  
