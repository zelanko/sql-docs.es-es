---
title: PDO::rollback | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d37145856da6c4b3ff6def1620de443b20faebfb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67936192"
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
  
## <a name="remarks"></a>Observaciones  
El valor de PDO::ATTR_AUTOCOMMIT no afecta a PDO::rollback.  
  
Consulte [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) para ver un ejemplo donde se utiliza PDO::rollback.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="see-also"></a>Consulte también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
