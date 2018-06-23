---
title: Códigos de retorno | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 37f3326aacd601dd9b52f0f55e146fa1b17cdcc7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103077"
---
# <a name="return-codes"></a>Códigos de retorno
  En el nivel más básico, una función miembro se ejecuta correctamente o genera un error. En un nivel algo más preciso, puede que una función se ejecute correctamente pero que el resultado no sea el que esperaba el programador de la aplicación.  
  
 Para obtener más información sobre los códigos de retorno de OLE DB, vea [códigos de retorno (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Cuando un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función de miembro de proveedor OLE DB de Native Client devuelve S_OK, la función se realizó correctamente.  
  
 Cuando un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función de miembro de proveedor OLE DB de Native Client no devuelve S_OK, las macros OLE/COM HRESULT-FAILED e is_error, pueden determinar el éxito o fracaso de una función global.  
  
 Si FAILED o IS_ERROR devuelven TRUE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client se asegura de que la ejecución de una función miembro no se pudo. Si FAILED o IS_ERROR devuelven FALSE y HRESULT no es igual a S_OK, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client se asegura de que la función se realizó correctamente en algún sentido. El consumidor puede recuperar información detallada en este "ejecución correcta con información" devolver desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de error de proveedor OLE DB de Native Client. Además, en el caso de que una función no claramente (la macro FAILED devuelve TRUE), información de error extendida está disponible en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de error de proveedor OLE DB de Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Consumidores del proveedor OLE DB de cliente nativo suelen encuentran el retorno HRESULT DB_S_ERRORSOCCURRED "ejecución correcta con información". Normalmente, las funciones miembro que devuelven DB_S_ERRORSOCCURRED definen uno o más parámetros que proporcionen valores de estado al consumidor. Es posible que no haya más información de error disponible para el consumidor que los parámetros de valor de estado devueltos, de modo que los consumidores deban implementar la lógica de la aplicación para recuperar los valores de estado cuando estén disponibles.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciones de miembro del proveedor OLE DB de Native Client no devuelven el código de correcto S_FALSE. Todos los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciones de miembro del proveedor OLE DB de Native Client devuelven siempre S_OK para indicar una operación correcta.  
  
## <a name="see-also"></a>Vea también  
 [Errores](errors.md)  
  
  