---
title: Interfaz ISQLServerStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f83b514-6e76-4f37-baf3-a10db2010e7c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b736ed84e0fed6794b036d22af84912f240539fb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67977340"
---
# <a name="isqlserverstatement-interface"></a>Interfaz ISQLServerStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa la implementación básica de la funcionalidad de la instrucción de JDBC. Esta interfaz se agregó en el controlador JDBC 3.0 de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** java.sql.Statement  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public interface ISQLServerStatement  
```  
  
## <a name="remarks"></a>Observaciones  
 Esta interfaz se implementa mediante la [clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
 Esta interfaz expone los siguientes métodos específicos del [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]:  
  
|Método|Para obtener más información, vea|  
|------------|-------------------------------|  
|public String getResponseBuffering|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|  
|public void setResponseBuffering|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
