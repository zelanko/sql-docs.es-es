---
title: 'PDO:: Rollback | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6b0ef351838defa86dee7818727a0d538b3e071a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="pdorollback"></a>PDO::rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Descarta los comandos de base de datos que se ejecutaron después de llamar a [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) y devuelve la conexión al modo de confirmación automática.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
bool PDO::rollBack ();  
```  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve el valor True si la llamada al método se realizó correctamente; en caso contrario, se devuelve False.  
  
## <a name="remarks"></a>Comentarios  
El valor de PDO::ATTR_AUTOCOMMIT no afecta a PDO::rollback.  
  
Consulte [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) para ver un ejemplo donde se utiliza PDO::rollback.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="see-also"></a>Vea también  
[Clase PDO](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

