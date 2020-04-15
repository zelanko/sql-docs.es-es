---
title: Códigos de retorno | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- SQL Server Native Client OLE DB provider, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
ms.assetid: 7f7457e9-fce4-400c-82e5-ee02e9e811c6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09056c9d4964ad10b2b25f63ef5991a1a7742cab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301035"
---
# <a name="return-codes"></a>Códigos de retorno
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  En el nivel más básico, una función miembro se ejecuta correctamente o genera un error. En un nivel algo más preciso, puede que una función se ejecute correctamente pero que el resultado no sea el que esperaba el programador de la aplicación.  
  
 Para obtener más información sobre los códigos de retorno OLE DB, vea [Códigos de retorno (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una función miembro del proveedor OLE DB de Native Client devuelve S_OK, la función se realizó correctamente.  
  
 Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una función miembro del proveedor OLE DB de Native Client no devuelve S_OK, las macros OLE/COM HRESULT-unpacking FAILED y IS_ERROR pueden determinar el éxito general o el error de una función.  
  
 Si FAILED o IS_ERROR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve TRUE, el consumidor del proveedor OLE DB de Native Client está seguro de que se produjo un error en la ejecución de la función miembro. Cuando FAILED o IS_ERROR devuelven FALSE y HRESULT no es igual S_OK, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de cliente nativo está seguro de que la función se realizó correctamente en cierto sentido. El consumidor puede recuperar información detallada sobre este [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorno de "éxito con información" de las interfaces de error del proveedor OLE DB de Native Client. Además, en el caso de que una función falle claramente (la macro FAILED devuelve TRUE), la información de error extendida está disponible en las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de error del proveedor OLE DB de Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Los consumidores de proveedores OLE DB de Native Client suelen encontrar la DB_S_ERRORSOCCURRED retorno HRESULT de "éxito con información". Normalmente, las funciones miembro que devuelven DB_S_ERRORSOCCURRED definen uno o más parámetros que proporcionen valores de estado al consumidor. Es posible que no haya más información de error disponible para el consumidor que los parámetros de valor de estado devueltos, de modo que los consumidores deban implementar la lógica de la aplicación para recuperar los valores de estado cuando estén disponibles.  
  
 Las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciones miembro del proveedor OLE DB de Native Client no devuelven el código de éxito S_FALSE. Todas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las funciones miembro del proveedor OLE DB de Native Client siempre devuelven S_OK para indicar que se ha realizado correctamente.  
  
## <a name="see-also"></a>Consulte también  
 [Errors](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
