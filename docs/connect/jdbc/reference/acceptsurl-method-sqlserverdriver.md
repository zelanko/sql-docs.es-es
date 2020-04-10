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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68e12a39cb4a27f170b7f12705f17791bb40b649
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923702"
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
  
  
