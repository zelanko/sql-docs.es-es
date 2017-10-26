---
title: "Método setClientInfo (java.util.Properties) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2a8ec0b-40a2-44d1-90d9-a810d4132e56
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d3484e23a4f7e8997d1bfa21a34a4cdf6f6dee71
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setclientinfo-method-javautilproperties"></a>Método setClientInfo (java.util.Properties)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el valor de las propiedades de información de cliente de la conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setClientInfo (java.util.Properties properties)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *propiedades*  
  
 Un objeto de propiedades que contiene la lista de propiedades de información de cliente para establecer.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setClientInfo especificado por el método setClientInfo en la interfaz java.sql.Connection.  
  
 El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] no admite las propiedades de información de cliente. Este método genera advertencias si el *propiedades* parámetro de entrada no hace referencia a un conjunto de propiedades vacías. Es decir, este método genera advertencias para las propiedades que desea establecer la aplicación. Las aplicaciones deben utilizar [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) método de la [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) clase para recuperar cada advertencia.  
  
## <a name="see-also"></a>Vea también  
 [Método setClientInfo &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

