---
title: Método setAsciiStream (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setAsciiStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6e1779df-3b2a-41d1-8dca-99692cc9da14
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 665696770d4a683bc67aa469ff0e1b27a8378615
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921955"
---
# <a name="setasciistream-method-sqlserverclob"></a>Método setAsciiStream (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un flujo que se va a utilizar para escribir los caracteres ASCII en el objeto CLOB a partir de la posición especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pos*  
  
 La posición donde se comienza a escribir en el objeto CLOB.  
  
## <a name="return-value"></a>Valor devuelto  
 El flujo en el que se pueden escribir los caracteres codificados ASCII.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Observaciones  
 El método setAsciiStream especifica este método setAsciiStream en la interfaz java.sql.Clob.  
  
 El flujo de salida sobrescribe los datos del carácter en el objeto CLOB a partir de la posición especificada y puede exceder la longitud inicial del CLOB. Si se especifica una valor position+1, se anexarán caracteres ASCII. Si se especifican valores position+2 o superiores (o cero o menos), se producirá un error de la posición.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
