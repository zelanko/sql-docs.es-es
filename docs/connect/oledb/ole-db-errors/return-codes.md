---
title: Códigos de retorno | Documentos de Microsoft
description: Códigos de retorno
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- OLE DB Driver for SQL Server, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 37efa9ce4a80cb9d90b3cddccefab243ef3a90ea
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="return-codes"></a>Códigos de retorno
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  En el nivel más básico, una función miembro se ejecuta correctamente o genera un error. En un nivel algo más preciso, puede que una función se ejecute correctamente pero que el resultado no sea el que esperaba el programador de la aplicación.  
  
 Para obtener más información sobre los códigos de retorno de OLE DB, vea [códigos de retorno (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Cuando un controlador de OLE DB para la función de miembro de SQL Server devuelve S_OK, la función se realizó correctamente.  
  
 Cuando un controlador de OLE DB para la función de miembro de SQL Server no devuelve S_OK, las macros OLE/COM HRESULT-FAILED e is_error, pueden determinar el éxito o fracaso de una función global.  
  
 Si FAILED o IS_ERROR devuelven TRUE, el controlador OLE DB para el consumidor de SQL Server se asegura de que la ejecución de una función miembro no se pudo. Si FAILED o IS_ERROR devuelven FALSE y HRESULT no es igual a S_OK, el controlador OLE DB para SQL Server al consumidor es la seguridad de la función se realizó correctamente en algún sentido. El consumidor puede recuperar información detallada sobre esta devolución de "ejecución correcta con información" desde el controlador OLE DB para las interfaces de error de SQL Server. Además, en el caso de que una función no claramente (la macro FAILED devuelve TRUE), información de error extendida está disponible desde el controlador OLE DB para las interfaces de error de SQL Server.  
  
 Controlador de OLE DB para los consumidores de SQL Server suelen encontrar el retorno HRESULT DB_S_ERRORSOCCURRED "ejecución correcta con información". Normalmente, las funciones miembro que devuelven DB_S_ERRORSOCCURRED definen uno o más parámetros que proporcionen valores de estado al consumidor. No hay información de error puede estar disponible para el consumidor que se devuelven en parámetros con valores de estado, por lo que los consumidores deban implementar la lógica de la aplicación para recuperar valores de estado cuando estén disponibles.  
  
 El controlador OLE DB para las funciones miembro de SQL Server no devuelve el código de correcto S_FALSE. Todos los controlador OLE DB para las funciones miembro de SQL Server devuelven siempre S_OK para indicar una operación correcta.  
  
## <a name="see-also"></a>Vea también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
