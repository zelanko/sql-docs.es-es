---
title: "Método getSubString (SQLServerClob) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerClob.getSubString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bf915590-a883-4403-befa-5b5bb42f34d8
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0030ce1e83feaa1a619fa9ead2bac3dfec4ccf6d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getsubstring-method-sqlserverclob"></a>Método getSubString (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve una copia de la subcadena especificada en el objeto CLOB según la posición de inicio indicada y el número de caracteres que se van a copiar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getSubString(long pos,  
                                     int length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *punto de venta*  
  
 El primer carácter de la subcadena que se va a extraer. El primer carácter está en la posición 1.  
  
 *length*  
  
 El número de caracteres consecutivos que se van a copiar.  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** que es la subcadena especificada en el objeto CLOB.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getSubString especificado por el método getSubString en la interfaz java.sql.Clob.  
  
 Si se intenta obtener un número de caracteres igual a cero a partir de un CLOB que sea NULL o de longitud cero, se obtiene una cadena vacía. Si se intentar obtener una longitud de caracteres cualquiera en alguna posición que no sea la posición 1 en un CLOB de longitud cero, se producirá una excepción relativa a la posición.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

