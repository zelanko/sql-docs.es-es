---
title: Códigos de retorno | Microsoft Docs
description: Códigos de retorno
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
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
ms.author: pelopes
ms.openlocfilehash: a1deedd8903f69268ebc5e7f5caafaa79a7f7b18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994927"
---
# <a name="return-codes"></a>Códigos de retorno
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En el nivel más básico, una función miembro se ejecuta correctamente o genera un error. En un nivel algo más preciso, puede que una función se ejecute correctamente pero que el resultado no sea el que esperaba el programador de la aplicación.  
  
 Para obtener más información sobre los códigos de retorno OLE DB, vea [Códigos de retorno (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Cuando un controlador de OLE DB para SQL Server función miembro Devuelve S_OK, la función se realiza correctamente.  
  
 Si una función miembro del controlador OLE DB para SQL Server no devuelve S_OK, las macros que desempaquetan la OLE/COM HRESULT, FAILED e IS_ERROR, pueden determinar si en general una función se ha ejecutado correctamente o no.  
  
 Si FAILED o IS_ERROR devuelven TRUE, el consumidor del controlador OLE DB para SQL Server sabe que se ha producido un error en la ejecución de la función miembro. Cuando FAILed o IS_ERROR devuelven FALSE y HRESULT no es igual a S_OK, el controlador de OLE DB para SQL Server consumidor está seguro de que la función se ha realizado correctamente en algún sentido. El consumidor puede recuperar información detallada sobre este retorno de "ejecución correcta con información" de las interfaces de error del controlador OLE DB para SQL Server. Además, en el caso en el que se produzca claramente un error en una función (la macro FAILED devuelve TRUE), se puede consultar más información sobre el error en las interfaces de error del controlador OLE DB para SQL Server.  
  
 OLE DB controlador para SQL Server los consumidores suelen encontrar el valor devuelto de DB_S_ERRORSOCCURRED "success with Information". Normalmente, las funciones miembro que devuelven DB_S_ERRORSOCCURRED definen uno o más parámetros que proporcionen valores de estado al consumidor. Es posible que no haya más información de error disponible para el consumidor que los parámetros de valor de estado devueltos, de modo que los consumidores deban implementar la lógica de la aplicación para recuperar los valores de estado cuando estén disponibles.  
  
 El controlador de OLE DB para las funciones miembro de SQL Server no devuelve el código de éxito S_FALSE. Todas OLE DB controlador para SQL Server funciones miembro devuelven siempre S_OK para indicar que la operación se ha realizado correctamente.  
  
## <a name="see-also"></a>Consulte también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
