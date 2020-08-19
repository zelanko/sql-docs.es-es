---
description: Métodos RDS
title: Métodos de RDS | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- RDS methods [ADO]
- methods [ADO], RDS
ms.assetid: c2c6af1a-3c44-4c9d-ad33-b381552c71af
author: rothja
ms.author: jroth
ms.openlocfilehash: 7f8685ead3b7f62861d6e27792a850af3140ebe3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438797"
---
# <a name="rds-methods"></a>Métodos RDS
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
|Método|Descripción|  
|-|-|  
|[Cancelar (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)|Cancela la ejecución de una llamada de método pendiente y asincrónica.|  
|[CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)|Cancela los cambios realizados en la fila actual o nueva de un objeto de **conjunto de registros** .|  
|[ConvertToString (RDS)](../../../ado/reference/rds-api/converttostring-method-rds.md)|Convierte un **conjunto de registros** en una cadena MIME que representa los datos del conjunto de registros.|  
|[CreateObject (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)|Crea el proxy para el objeto comercial de destino y devuelve un puntero a él.|  
|[CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|Crea un **conjunto de registros**vacío y desconectado.|  
|[Execute (método) (RDS)](../../../ado/reference/rds-api/execute-method-rds.md)|Ejecute la solicitud y cree un conjunto de filas de datos avanzado (para su uso con ADO 2,5 y versiones posteriores).|  
|[Método Execute21 (RDS)](../../../ado/reference/rds-api/execute21-method-rds.md)|Ejecute la solicitud y cree un conjunto de filas de datos avanzado (para su uso con ADO 2,1).|  
|[InvokeService (RDS)](../../../ado/reference/rds-api/invokeservice-rds.md)|Devuelve un puntero a la interfaz solicitada en una versión más capaz del objeto.|  
|[MoveFirst, MoveLast, MoveNext, MovePrevious (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)|Se desplaza al registro primero, último, siguiente o anterior de un objeto de **conjunto de registros** especificado.|  
|[Consulta (RDS)](../../../ado/reference/rds-api/query-method-rds.md)|Utiliza una cadena de consulta SQL válida para devolver un **conjunto de registros**.|  
|[Actualizar (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)|Vuelve a consultar el origen de datos especificado en la propiedad **Connect** y actualiza los resultados de la consulta.|  
|[Restablecer (RDS)](../../../ado/reference/rds-api/reset-method-rds.md)|Ejecuta la ordenación o el filtro en un conjunto de **registros**del lado cliente, en función de las propiedades de ordenación y filtro especificadas.|  
|[SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)|Envía los cambios pendientes del **conjunto de registros** actualizado en caché local al origen de datos especificado en la propiedad **Connect** .|  
|[Synchronize (método) (RDS)](../../../ado/reference/rds-api/synchronize-method-rds.md)|Sincronizar el conjunto de registros dado con la base de datos especificada por la cadena de conexión (para su uso con ADO 2,5 y versiones posteriores).|  
|[Método Synchronize21 (RDS)](../../../ado/reference/rds-api/synchronize21-method-rds.md)|Sincronizar el conjunto de registros dado con la base de datos especificada por la cadena de conexión (para su uso con ADO 2,1).|


