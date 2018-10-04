---
title: Códigos de retorno | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 7a84ad46068260524a2e6232ca668da445447529
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207425"
---
# <a name="return-codes"></a>Códigos de retorno
  En el nivel más básico, una función miembro se ejecuta correctamente o genera un error. En un nivel algo más preciso, puede que una función se ejecute correctamente pero que el resultado no sea el que esperaba el programador de la aplicación.  
  
 Para obtener más información sobre los códigos de retorno OLE DB, vea [Códigos de retorno (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Cuando un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función miembro de proveedor OLE DB de Native Client devuelve S_OK, la función se realizó correctamente.  
  
 Cuando un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función miembro de proveedor OLE DB de Native Client no devuelve S_OK, las macros se ha OLE/COM HRESULT y IS_ERROR pueden determinar el éxito o fracaso de una función global.  
  
 Si FAILED o IS_ERROR devuelve TRUE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client se asegura de que la ejecución de la función miembro no se pudo. Si FAILED o IS_ERROR devuelven FALSE y HRESULT no es igual a S_OK, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client se asegura de que la función se realizó correctamente en algún sentido. El consumidor puede recuperar información detallada sobre esta "ejecución correcta con información" devolver desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de error de proveedor OLE DB de Native Client. Además, en el caso donde funkci claramente se produce un error (la macro FAILED devuelve TRUE), información de error extendida está disponible desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de error de proveedor OLE DB de Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Consumidores del proveedor OLE DB de cliente nativos suelen encuentran el retorno HRESULT DB_S_ERRORSOCCURRED "ejecución correcta con información". Normalmente, las funciones miembro que devuelven DB_S_ERRORSOCCURRED definen uno o más parámetros que proporcionen valores de estado al consumidor. Es posible que no haya más información de error disponible para el consumidor que los parámetros de valor de estado devueltos, de modo que los consumidores deban implementar la lógica de la aplicación para recuperar los valores de estado cuando estén disponibles.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciones miembro del proveedor OLE DB de Native Client no devuelven el código de operación correcta S_FALSE. Todos los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciones miembro del proveedor OLE DB de Native Client devuelven siempre S_OK para indicar el éxito.  
  
## <a name="see-also"></a>Vea también  
 [Errores](errors.md)  
  
  
