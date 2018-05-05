---
title: setBytes (método) (long, byte, int, int) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b18005c16cd62358eb5f269504fc9d80eadb6de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setbytes-method-long-byte-int-int"></a>setBytes (long, byte, int, int) (método)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Escribe todo o parte de la matriz de bytes en el BLOB comenzando en la posición especificada, el desplazamiento y la longitud; y, a continuación, devuelve el número de bytes escritos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes,  
                    int offset,  
                    int len)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *punto de venta*  
  
 La posición (de base 1) en el objeto BLOB en la que se comienzan a escribir los datos.  
  
 *bytes*  
  
 La matriz de bytes que se va a escribir en el BLOB.  
  
 *offset*  
  
 El desplazamiento de los bytes de matriz que desea iniciar la lectura de datos de la **bytes** matriz.  
  
 *len*  
  
 El número de bytes que se intentarán leer desde la matriz de bytes en el objeto BLOB.  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que contiene el número de bytes escritos.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentarios  
 Este método setBytes es especificado por el método setBytes en la interfaz java.sql.Blob.  
  
 Sobrescribe a partir de la posición especificada de datos y pueden exceder la longitud inicial del BLOB. Si se especifican valores position+1, se anexarán bytes. Si se pasan valores position+2 o superiores (o cero o menos), se producirá un error de la posición. Pasar una longitud de cero **bytes** matriz devolverá cero porque no se escribieron bytes.  
  
## <a name="see-also"></a>Vea también  
 [Método setBytes &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Miembros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
