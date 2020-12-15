---
title: Códigos de retorno (proveedor de OLE DB de Native Client)
description: Obtenga información sobre los códigos de retorno que se admiten para OLE DB de SQL Server Native Client, incluido el valor de DB_S_ERRORSOCCURRED HRESULT que se encuentra normalmente.
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 64111973f8e1c753a3d342c395d2f457ad1b3401
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97433873"
---
# <a name="return-codes-native-client-ole-db-provider"></a>Códigos de retorno (proveedor de OLE DB de Native Client)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En el nivel más básico, una función miembro se ejecuta correctamente o genera un error. En un nivel algo más preciso, puede que una función se ejecute correctamente pero que el resultado no sea el que esperaba el programador de la aplicación.  
  
 Para obtener más información sobre los códigos de retorno OLE DB, vea [Códigos de retorno (OLE DB)](/previous-versions/windows/desktop/ms725451(v=vs.85)).  
  
 Cuando una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función miembro de proveedor de OLE DB de Native Client devuelve S_OK, la función se realiza correctamente.  
  
 Cuando una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función miembro de proveedor de OLE DB de Native Client no devuelve S_OK, se produce un error en el desempaquetado de HRESULT de OLE/com y IS_ERROR macros pueden determinar el éxito o el error general de una función.  
  
 Si FAILed o IS_ERROR devuelve TRUE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor de OLE DB de Native Client está seguro de que se ha producido un error en la ejecución de la función miembro. Cuando FAILed o IS_ERROR devuelven FALSE y HRESULT no es igual a S_OK, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor de OLE DB de Native Client está seguro de que la función se realizó correctamente en algún sentido. El consumidor puede recuperar información detallada sobre este valor "éxito con información" de las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de error del proveedor de OLE DB de Native Client. Además, en el caso de que se produzca un error claramente en una función (la macro FAILed devuelve TRUE), la información de error ampliada está disponible en las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de error del proveedor de OLE DB de Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Los consumidores de proveedores de OLE DB de Native Client suelen encontrar el valor devuelto por el DB_S_ERRORSOCCURRED "success with Information". Normalmente, las funciones miembro que devuelven DB_S_ERRORSOCCURRED definen uno o más parámetros que proporcionen valores de estado al consumidor. Es posible que no haya más información de error disponible para el consumidor que los parámetros de valor de estado devueltos, de modo que los consumidores deban implementar la lógica de la aplicación para recuperar los valores de estado cuando estén disponibles.  
  
 Las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciones miembro del proveedor de OLE DB de Native Client no devuelven el código de éxito S_FALSE. Todas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las funciones miembro de proveedor de OLE DB de Native Client siempre devuelven S_OK para indicar que se ha realizado correctamente.  
  
## <a name="see-also"></a>Consulte también  
 [Errores](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
