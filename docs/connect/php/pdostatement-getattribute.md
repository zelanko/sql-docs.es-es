---
title: PDOStatement::getAttribute | Microsoft Docs
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b3c1c79da6d1efc51778cb09eb6bd2fed460576a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799151"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera el valor de un atributo de controlador personalizado o un atributo PDOStatement predefinido.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>Parámetros  
$*attribute*: entero; una de las constantes PDO::ATTR_* o PDO::SQLSRV_ATTR_\*. Los atributos compatibles son los atributos que se pueden establecer con [pdostatement:: setAttribute](../../connect/php/pdostatement-setattribute.md), PDO:: sqlsrv_attr_direct_query (para obtener más información, consulte [Direct Statement Execution and Prepared Statement Execution en el controlador PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)), PDO:: attr_cursor y PDO:: sqlsrv_attr_cursor_scroll_type (para obtener más información, consulte [tipos de Cursor (controlador PDO_SQLSRV)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)).  
  
## <a name="return-value"></a>Valor devuelto  
Si se ejecuta correctamente, devuelve un valor (mixto) para un atributo PDO predefinido o el atributo de controlador personalizado. En caso de error, se devuelve Null.  
  
## <a name="remarks"></a>Notas  
Para obtener un ejemplo, consulte [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) .  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="see-also"></a>Consulte también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
