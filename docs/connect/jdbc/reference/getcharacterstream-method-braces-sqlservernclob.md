---
title: Método getCharacterStream () (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7641698e-b25c-4bb2-bcc7-9273bdd08bf0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 11d0a2c40462784558f4d618c7e3d0a206d6d382
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67953298"
---
# <a name="getcharacterstream-method--sqlservernclob"></a>Método getCharacterStream () (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve los datos de **NCLOB** como un objeto **Reader** o como un flujo de caracteres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.Reader getCharacterStream()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Reader que contiene los datos **NCLOB**.  
  
## <a name="remarks"></a>Observaciones  
 El método getCharacterStream especifica este método getCharacterStream en la interfaz java.sql.NClob.  
  
## <a name="see-also"></a>Consulte también  
 [Método getCharacterStream &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)   
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Miembros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
