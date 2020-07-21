---
title: Método supportsSchemasInIndexDefinitions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsSchemasInIndexDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 55ce9e4f-6e3f-482a-93a5-b9ae1b91d7a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e66e619cbae08a8f9f40e182edfac0a62785897
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921727"
---
# <a name="supportsschemasinindexdefinitions-method-sqlserverdatabasemetadata"></a>Método supportsSchemasInIndexDefinitions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si un nombre de esquema se puede utilizar en una instrucción de definición de índice.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsSchemasInIndexDefinitions()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsSchemasInIndexDefinitions especifica este método supportsSchemasInIndexDefinitions en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
