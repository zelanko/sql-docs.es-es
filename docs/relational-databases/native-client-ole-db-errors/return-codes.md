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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73790236"
---
# <a name="return-codes"></a>Códigos de retorno
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  En el nivel más básico, una función miembro se ejecuta correctamente o genera un error. En un nivel algo más preciso, puede que una función se ejecute correctamente pero que el resultado no sea el que esperaba el programador de la aplicación.  
  
 Para obtener más información sobre los códigos de retorno OLE DB, vea [Códigos de retorno (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Cuando una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función miembro de proveedor de OLE DB de Native Client Devuelve S_OK, la función se realiza correctamente.  
  
 Cuando una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función miembro de proveedor de OLE DB de Native Client no Devuelve S_OK, se produce un error en el desempaquetado de HRESULT de OLE/COM y IS_ERROR macros pueden determinar el éxito o el error general de una función.  
  
 Si FAILed o IS_ERROR devuelve TRUE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el consumidor del proveedor de OLE DB de Native Client está seguro de que se ha producido un error en la ejecución de la función miembro. Cuando FAILed o IS_ERROR devuelven FALSE y HRESULT no es igual a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] S_OK, el consumidor del proveedor de OLE DB de Native Client está seguro de que la función se realizó correctamente en algún sentido. El consumidor puede recuperar información detallada sobre este valor "éxito con información" de las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de error del proveedor de OLE DB de Native Client. Además, en el caso de que se produzca un error claramente en una función (la macro FAILed devuelve TRUE), la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información de error ampliada está disponible en las interfaces de error del proveedor de OLE DB de Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Los consumidores de proveedores de OLE DB de Native Client suelen encontrar el valor devuelto por el DB_S_ERRORSOCCURRED "success with Information". Normalmente, las funciones miembro que devuelven DB_S_ERRORSOCCURRED definen uno o más parámetros que proporcionen valores de estado al consumidor. Es posible que no haya más información de error disponible para el consumidor que los parámetros de valor de estado devueltos, de modo que los consumidores deban implementar la lógica de la aplicación para recuperar los valores de estado cuando estén disponibles.  
  
 Las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciones miembro del proveedor de OLE DB de Native Client no devuelven el código de éxito S_FALSE. Todas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las funciones miembro de proveedor de OLE DB de Native Client siempre devuelven S_OK para indicar que se ha realizado correctamente.  
  
## <a name="see-also"></a>Consulte también  
 [Errors](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
