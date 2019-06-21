---
title: Método getSubString (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1d91c930-1bac-4da9-b9a5-ac2cfd31541b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6329fbae355b6d6a232aed87c5d786475e08ee19
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66787436"
---
# <a name="getsubstring-method-sqlservernclob"></a>Método getSubString (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una copia de la subcadena especificada en **NCLOB** según la posición de inicio especificada y el número de caracteres a copiar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getSubString(long pos,  
                                  int length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pos*  
  
 El primer carácter de la subcadena que se va a extraer. El primer carácter está en la posición 1.  
  
 *length*  
  
 El número de caracteres consecutivos que se van a copiar.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **String** que es la substring especificada en el objeto **NCLOB**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getSubString especificado por el método getSubString en la interfaz java.sql.NClob.  
  
 Si se intenta obtener un número de caracteres igual a cero a partir de un NCLOB que sea NULL o de longitud cero, se obtiene una cadena vacía. Si se intentar obtener una longitud de caracteres cualquiera en alguna posición que no sea la posición 1 en un NCLOB de longitud cero, se producirá una excepción relativa a la posición.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Miembros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
