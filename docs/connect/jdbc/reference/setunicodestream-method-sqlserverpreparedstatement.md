---
title: Método setUnicodeStream (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a413e83-e0a4-41f8-9fe0-33ce4d368ee4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 450450774bc5e0897150ea049deb5423d2304881
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66783390"
---
# <a name="setunicodestream-method-sqlserverpreparedstatement"></a>Método setUnicodeStream (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el número de parámetro designado en el flujo de entrada determinado, que tendrá el número de bytes indicado.  
  
> [!NOTE]  
>  Este método se ha dejado de incluir en las especificaciones de JDBC y si se llama producirá una excepción de no implementación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setUnicodeStream(int n,  
                                   java.io.InputStream x,  
                                   int length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *n*  
  
 Valor **int** que indica el número de parámetro.  
  
 *x*  
  
 Un objeto InputStream.  
  
 *length*  
  
 El número de bytes.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setUnicodeStream especificado por el método setUnicodeStream en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
