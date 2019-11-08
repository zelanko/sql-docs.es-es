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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 36f376710dbcdd09daf664e9eee20533c5372641
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790236"
---
# <a name="return-codes"></a>Códigos de retorno
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  En el nivel más básico, una función miembro se ejecuta correctamente o genera un error. En un nivel algo más preciso, puede que una función se ejecute correctamente pero que el resultado no sea el que esperaba el programador de la aplicación.  
  
 Para obtener más información sobre los códigos de retorno OLE DB, vea [Códigos de retorno (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Cuando una función miembro del proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Devuelve S_OK, la función se realiza correctamente.  
  
 Cuando una función miembro de proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB no Devuelve S_OK, se produce un error en el desempaquetado de HRESULT de OLE/COM y las macros de IS_ERROR pueden determinar el éxito o el error general de una función.  
  
 Si FAILed o IS_ERROR devuelve TRUE, el consumidor del proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client está seguro de que se ha producido un error en la ejecución de la función miembro. Cuando FAILed o IS_ERROR devuelven FALSE y HRESULT no es igual a S_OK, el consumidor del proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB está seguro de que la función se realizó correctamente en algún sentido. El consumidor puede recuperar información detallada sobre este valor "éxito con información" de las interfaces de error del proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Además, en el caso de que se produzca un error claramente en una función (la macro FAILed devuelve TRUE), la información de error ampliada está disponible en las interfaces de error del proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los consumidores de proveedores de OLE DB de Native Client suelen encontrar el valor devuelto DB_S_ERRORSOCCURRED "success with Information". Normalmente, las funciones miembro que devuelven DB_S_ERRORSOCCURRED definen uno o más parámetros que proporcionen valores de estado al consumidor. Es posible que no haya más información de error disponible para el consumidor que los parámetros de valor de estado devueltos, de modo que los consumidores deban implementar la lógica de la aplicación para recuperar los valores de estado cuando estén disponibles.  
  
 Las funciones miembro del proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no devuelven el S_FALSE de código correcto. Todas las funciones miembro del proveedor de OLE DB Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre devuelven S_OK para indicar que la operación se ha realizado correctamente.  
  
## <a name="see-also"></a>Vea también  
 [Errores](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
