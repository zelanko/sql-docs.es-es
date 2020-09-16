---
description: Método getXAConnection (java.lang.String, java.lang.String)
title: Método getXAConnection (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXADataSource.getXAConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276e0093-3d42-4f73-acc4-2b5b98245b40
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 988c8c3d7c1ba3cc09d20ae35f066d260cf543fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433757"
---
# <a name="getxaconnection-method-javalangstring-javalangstring"></a>Método getXAConnection (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Intenta establecer una conexión a bases de datos física mediante el nombre de usuario y contraseña especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public javax.sql.XAConnection getXAConnection(java.lang.String user,  
                                              java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *user*  
  
 Objeto **String** que contiene el nombre del usuario.  
  
 *password*  
  
 Objeto **String** que contiene la contraseña.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto XAConnection.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Observaciones  
 El método getXAConnection especifica este método getXAConnection en la interfaz javax.sql.XADataSource.  
  
> [!NOTE]  
>  Las implementaciones del grupo de conexiones XA, y no los códigos de aplicación JDBC, llaman normalmente a este método.  
  
## <a name="see-also"></a>Consulte también  
 [Método getXAConnection &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [Métodos SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Miembros de clase SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Clase SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
