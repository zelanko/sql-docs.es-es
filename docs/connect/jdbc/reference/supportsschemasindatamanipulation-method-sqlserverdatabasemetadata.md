---
title: Método supportsSchemasInDataManipulation | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsSchemasInDataManipulation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 812dc551-c718-494e-80d9-75732464c8ba
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf72ac197f69ea1f90154bd74a7841466d614ae4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787933"
---
# <a name="supportsschemasindatamanipulation-method-sqlserverdatabasemetadata"></a>Método supportsSchemasInDataManipulation (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si un nombre de esquema se puede utilizar en una instrucción de manipulación de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsSchemasInDataManipulation()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método supportsSchemasInDataManipulation especificado por el método supportsSchemasInDataManipulation en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Ver también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
