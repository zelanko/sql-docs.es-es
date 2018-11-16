---
title: 'PDO:: Commit | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a0db4a00-9700-4f49-ab16-6522dd1101d3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f30119d7fb8d2e1f23b719273738cc52cf3b7d00
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606335"
---
# <a name="pdocommit"></a>PDO::commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Envía a la base de datos comandos que se emitieron después de llamar a [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) y devuelve la conexión al modo de confirmación automática.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
bool PDO::commit();  
```  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve el valor True si la llamada al método se realizó correctamente; en caso contrario, se devuelve False.  
  
## <a name="remarks"></a>Notas  
PDO::commit no afecta al valor de PDO::ATTR_AUTOCOMMIT y no se ve afectado por este último.  
  
Consulte [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) para ver un ejemplo donde se utiliza PDO::commit.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="see-also"></a>Ver también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
