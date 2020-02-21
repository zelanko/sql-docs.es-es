---
title: Método acceptsURL (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.acceptsURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fc744566-7191-4b15-9f76-b4b8087fb14a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7c51da69e7218f91630543fe7bee5ec0d7fd6b0e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67956027"
---
# <a name="acceptsurl-method-sqlserverdriver"></a>Método acceptsURL (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Comprueba si la dirección URL especificada es válida.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean acceptsURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *url*  
  
 Un valor **String** que contiene la dirección URL que se utiliza para conectar a la base de datos.  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si la dirección URL especificada es válida. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método acceptsURL especifica este método acceptsURL en la interfaz java.sql.Driver.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Miembros de SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Clase SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
