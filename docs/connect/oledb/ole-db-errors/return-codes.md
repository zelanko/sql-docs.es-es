---
title: Códigos de retorno (controlador OLE DB)
description: Obtenga información sobre los códigos de retorno de las funciones miembro de OLE DB Driver for SQL Server y cómo obtener más información sobre los resultados además de la realización correcta de la operación.
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18d2b3f5029e70379f0692a919aa8fe6cd4ed10b
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862241"
---
# <a name="return-codes"></a>Códigos de retorno
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En el nivel más básico, una función miembro se ejecuta correctamente o genera un error. En un nivel algo más preciso, puede que una función se ejecute correctamente pero que el resultado no sea el que esperaba el programador de la aplicación.  
  
 Para obtener más información sobre los códigos de retorno OLE DB, vea [Códigos de retorno (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Cuando una función miembro de OLE DB Driver for SQL Server devuelve S_OK, la función se ejecuta correctamente.  
  
 Si una función miembro del controlador OLE DB para SQL Server no devuelve S_OK, las macros que desempaquetan la OLE/COM HRESULT, FAILED e IS_ERROR, pueden determinar si en general una función se ha ejecutado correctamente o no.  
  
 Si FAILED o IS_ERROR devuelven TRUE, el consumidor del controlador OLE DB para SQL Server sabe que se ha producido un error en la ejecución de la función miembro. Si FAILED o IS_ERROR devuelven FALSE y HRESULT no es igual a S_OK, el consumidor de OLE DB Driver for SQL Server tiene la seguridad de que la función se ejecutó correctamente en algún sentido. El consumidor puede recuperar información detallada sobre este retorno de "ejecución correcta con información" de las interfaces de error del controlador OLE DB para SQL Server. Además, en el caso en el que se produzca claramente un error en una función (la macro FAILED devuelve TRUE), se puede consultar más información sobre el error en las interfaces de error del controlador OLE DB para SQL Server.  
  
 Los consumidores de OLE DB Driver for SQL Server suelen encontrar el retorno HRESULT de "ejecución correcta con información" DB_S_ERRORSOCCURRED. Normalmente, las funciones miembro que devuelven DB_S_ERRORSOCCURRED definen uno o más parámetros que proporcionen valores de estado al consumidor. Es posible que no haya más información de error disponible para el consumidor que los parámetros de valor de estado devueltos, de modo que los consumidores deban implementar la lógica de la aplicación para recuperar los valores de estado cuando estén disponibles.  
  
 Las funciones miembro de OLE DB Driver for SQL Server no devuelven el elemento S_FALSE de código de acierto. Todas las funciones miembro de OLE DB Driver for SQL Server siempre devuelven S_OK para indicar que la operación se ha realizado correctamente.  
  
## <a name="see-also"></a>Consulte también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
