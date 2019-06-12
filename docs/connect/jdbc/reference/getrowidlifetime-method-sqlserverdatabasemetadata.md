---
title: Método getRowIdLifetime (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 317c0b44-fe3f-4142-9cab-e40e4c4fe070
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7aa2b4f740795169824cb4962f17c2dfecdc7974
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66762527"
---
# <a name="getrowidlifetime-method-sqlserverdatabasemetadata"></a>Método getRowIdLifetime (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un estado que indica si se admite el tipo de datos RowId de SQL. Si así fuera, devuelve la duración de un objeto RowId.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.RowIdLifetime getRowIdLifetime()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto RowIdLifetime.  
  
> [!NOTE]  
>  En la versión de la versión 2.0 del controlador JDBC, este método devuelve el valor de java.sql.RowIdLifetime.ROWID_UNSUPPORTED.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getRowIdLifetime especificado por el método getRowIdLifetime en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
