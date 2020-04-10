---
title: Método position (java.lang.String, long) (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 46d4beec-831a-449f-98b6-322a80cc499a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe0bf76df2f2350b76ad6f817b621d01ae2410dc
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80914365"
---
# <a name="position-method-javalangstring-long-sqlservernclob"></a>Método position (java.lang.String, long) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la posición del carácter donde aparece la subcadena *searchstr* especificada en el valor **NCLOB** que este objeto **NClob** representa.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public long position(java.lang.String searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *searchstr*  
  
 La subcadena que se va a buscar.  
  
 *start*  
  
 La posición donde se empieza la búsqueda; la primera posición es 1.  
  
## <a name="return-value"></a>Valor devuelto  
 La posición donde aparece la subcadena o -1 si no está presente. La primera posición es 1.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método position especifica este método position en la interfaz java.sql.NClob.  
  
## <a name="see-also"></a>Consulte también  
 [Método position &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Miembros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
