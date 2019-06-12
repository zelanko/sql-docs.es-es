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
manager: jroth
ms.openlocfilehash: 7bb86d9e9c43b6d8c73f8018e80eebd5a0a54f5e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66786058"
---
# <a name="return-codes"></a>Códigos de retorno
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En el nivel más básico, una función miembro se ejecuta correctamente o genera un error. En un nivel algo más preciso, puede que una función se ejecute correctamente pero que el resultado no sea el que esperaba el programador de la aplicación.  
  
 Para obtener más información sobre los códigos de retorno OLE DB, vea [Códigos de retorno (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Cuando un controlador de OLE DB para la función de miembro de SQL Server devuelve S_OK, la función se realizó correctamente.  
  
 Si una función miembro del controlador OLE DB para SQL Server no devuelve S_OK, las macros que desempaquetan la OLE/COM HRESULT, FAILED e IS_ERROR, pueden determinar si en general una función se ha ejecutado correctamente o no.  
  
 Si FAILED o IS_ERROR devuelven TRUE, el consumidor del controlador OLE DB para SQL Server sabe que se ha producido un error en la ejecución de la función miembro. Si FAILED o IS_ERROR devuelven FALSE y HRESULT no igual a S_OK, el controlador OLE DB para SQL Server de consumidor se asegura de la función se realizó correctamente en algún sentido. El consumidor puede recuperar información detallada sobre este retorno de "ejecución correcta con información" de las interfaces de error del controlador OLE DB para SQL Server. Además, en el caso en el que se produzca claramente un error en una función (la macro FAILED devuelve TRUE), se puede consultar más información sobre el error en las interfaces de error del controlador OLE DB para SQL Server.  
  
 Controlador OLE DB para los consumidores de SQL Server suelen encontrar el retorno HRESULT DB_S_ERRORSOCCURRED "ejecución correcta con información". Normalmente, las funciones miembro que devuelven DB_S_ERRORSOCCURRED definen uno o más parámetros que proporcionen valores de estado al consumidor. Es posible que no haya más información de error disponible para el consumidor que los parámetros de valor de estado devueltos, de modo que los consumidores deban implementar la lógica de la aplicación para recuperar los valores de estado cuando estén disponibles.  
  
 El controlador OLE DB para las funciones miembro de SQL Server no devolver el código de operación correcta S_FALSE. Todos los controlador OLE DB para las funciones miembro de SQL Server devuelven siempre S_OK para indicar el éxito.  
  
## <a name="see-also"></a>Consulte también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
