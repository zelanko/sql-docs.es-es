---
title: Método getClientInfoProperties (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bf9c0696c2169ee9b0dd1af198fcb50333c5d9ca
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66763767"
---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>Método getClientInfoProperties (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una lista de las propiedades de la información de cliente que admite el controlador.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de conjunto de resultados.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getClientInfoProperties especificado por el método getClientInfoProperties de la interfaz java.sql.DatabaseMetaData.  
  
> [!NOTE]  
>  Este método devuelve un conjunto de resultados vacío. El controlador permite establecer solo la **applicationName** y establece el **applicationName** solo en tiempo de conexión. SQL Server no proporciona soporte técnico para actualizar la información de la aplicación cliente una vez se haya establecido la conexión.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
