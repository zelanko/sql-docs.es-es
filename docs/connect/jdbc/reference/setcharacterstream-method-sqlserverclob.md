---
title: Método setCharacterStream (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c02778f2-6681-4a84-a58b-2bcfac4233e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da842fbc6240b072c7fe907aaa344d8d2ff1c6e7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974653"
---
# <a name="setcharacterstream-method-sqlserverclob"></a>Método setCharacterStream (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un flujo que se va a utilizar para escribir una cadena de caracteres Unicode en el objeto CLOB a partir de la posición especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pos*  
  
 La posición donde se comienza a escribir en el objeto CLOB.  
  
## <a name="return-value"></a>Valor devuelto  
 Un flujo donde se pueden escribir caracteres Unicode codificados.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Observaciones  
 El método setCharacterStream especifica este método setCharacterStream en la interfaz java.sql.Statement.  
  
 El sistema de escritura sobrescribe los datos de carácter del objeto CLOB a partir de la posición especificada y puede exceder la longitud inicial del CLOB. Si se especifica una valor position+1, se anexarán caracteres. Si se especifican valores position+2 o superiores (o cero o menos), se producirá un error de la posición.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
