---
title: Método setLoginTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83d6869075e296465ee9c60b0c5032407d4fe2da
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925753"
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>Método setLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el número de segundos que este objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) esperará mientras intenta efectuar una conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *loginTimeout*  
  
 Un valor **int**que representa el número de segundos durante los que se esperará. Un valor cero indica que el tiempo de espera es el predeterminado del sistema, que está especificado inicialmente en 15 segundos.  
  
## <a name="remarks"></a>Observaciones  
 El método setLoginTimeout especifica este método setLoginTimeout en la interfaz javax.sql.DataSource.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
