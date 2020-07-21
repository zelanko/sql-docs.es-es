---
title: Método setLockTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10dca5aa-1851-4326-9ae9-7a8430d12d11
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8143233de52f1272cf63a31f79ed280cf5124a9a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925766"
---
# <a name="setlocktimeout-method-sqlserverdatasource"></a>Método setLockTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor de tipo **int** que indica el número de milisegundos que transcurrirán antes de que la base de datos notifique un tiempo de espera de bloqueo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setLockTimeout(int lockTimeout)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *lockTimeout*  
  
 Un valor **int** que contiene el número de milisegundos que transcurrirán.  
  
## <a name="remarks"></a>Observaciones  
 El tiempo de espera de bloqueo es el número de milisegundos que hay que esperar antes de que la base de datos informe del tiempo de espera para la exclusión. El valor predeterminado de -1 indica que la espera será indefinida. Si se especifica, este valor será el predeterminado para todas las instrucciones de la conexión.  
  
> [!NOTE]  
>  Un valor de 0 indica que el tiempo de espera será nulo. Si no se establece la propiedad lockTimeout, el método [getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md) devuelve el valor predeterminado de -1.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
