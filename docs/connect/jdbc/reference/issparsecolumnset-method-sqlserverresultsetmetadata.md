---
title: Método isSparseColumnSet (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ac363670-78ae-49f1-aeda-4fba3329a258
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b902ddf8e9e05900e55492116ee9e22a3dbbccc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67977222"
---
# <a name="issparsecolumnset-method-sqlserverresultsetmetadata"></a>Método isSparseColumnSet (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si una columna de un conjunto de resultados es un conjunto de columnas dispersas.  
  
## <a name="syntax"></a>Sintaxis  
  
```scr  
public boolean isSparseColumnSet(int column)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *column*  
  
 Índice (basado en uno) de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si una columna de un conjunto de resultados es un conjunto de columnas dispersas, de lo contrario **false**.  
  
## <a name="remarks"></a>Observaciones  
 Este método no recupera información de la base de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Miembros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
