---
title: Método setBytes (long, byte, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee4ab641ede4d4ec614a306f9c0e08c9f16aa5ee
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974947"
---
# <a name="setbytes-method-long-byte-int-int"></a>Método setBytes (long, byte, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Escribe todo o parte de la matriz de bytes determinada en el BLOB comenzando en la posición, desplazamiento y longitud determinados; posteriormente devuelve el número de bytes escritos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes,  
                    int offset,  
                    int len)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pos*  
  
 La posición (de base 1) en el objeto BLOB en la que se comienzan a escribir los datos.  
  
 *bytes*  
  
 La matriz de bytes que se va a escribir en el BLOB.  
  
 *offset*  
  
 El desplazamiento en la matriz de bytes donde se comenzarán a leer los datos desde la matriz **byte**.  
  
 *len*  
  
 El número de bytes que se intentarán leer desde la matriz de bytes en el objeto BLOB.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que contiene el número de bytes escritos.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Observaciones  
 El método setBytes especifica este método setBytes en la interfaz java.sql.Blob.  
  
 Los datos se sobrescriben tomando como punto de inicio la posición especificada y pueden saturar la longitud inicial del BLOB. Si se especifican valores position+1, se anexarán bytes. Si se pasan valores position+2 o superiores (o cero o menos), se producirá un error de la posición. Si se pasa una matriz **byte** de longitud cero, se devolverá cero porque no se escribieron bytes.  
  
## <a name="see-also"></a>Consulte también  
 [Método setBytes &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Miembros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
