---
title: Método getClientInfo (java.lang.String) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e8e632c4-d6cc-4c5e-b6ad-873579343b19
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d221477af9d39b65c359712682132e15a54fce25
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getclientinfo-method-javalangstring"></a>Método getClientInfo (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de una propiedad de información del cliente especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getClientInfo (java.lang.String name)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
  
 Una cadena que contiene el nombre de la propiedad de información de cliente para recuperar.  
  
## <a name="return-value"></a>Valor devuelto  
 Una cadena que contiene el valor de la propiedad de información de cliente.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getClientInfo especificado por el método getClientInfo en la interfaz java.sql.Connection.  
  
 El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] no admite propiedades de información de cliente. Como resultado, este método devuelve **null**.  
  
 De forma similar, las aplicaciones pueden utilizar el [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) método de la [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) clase para recuperar una lista de las propiedades de información de cliente que admite el controlador. El [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) método devuelve un conjunto de resultados vacío.  
  
## <a name="see-also"></a>Vea también  
 [Método getClientInfo &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
