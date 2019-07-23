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
ms.openlocfilehash: 014f679480caaabd42863d2551cfa4c25bbe94d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992979"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera el valor de un atributo de controlador personalizado o un atributo PDOStatement predefinido.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>Parámetros  
$*attribute*: entero; una de las constantes PDO::ATTR_* o PDO::SQLSRV_ATTR_\*. Los atributos admitidos son los atributos que se pueden establecer con [PDOStatement:: setAttribute](../../connect/php/pdostatement-setattribute.md), PDO:: SQLSRV_ATTR_DIRECT_QUERY (para obtener más información, vea ejecución de la [instrucción directa y ejecución de la instrucción preparada en el controlador PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)), PDO: : ATTR_CURSOR y PDO:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE (para obtener más información, consulte [tipos de cursor (controlador PDO_SQLSRV)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)).  
  
## <a name="return-value"></a>Valor devuelto  
Si se ejecuta correctamente, devuelve un valor (mixto) para un atributo PDO predefinido o el atributo de controlador personalizado. En caso de error, se devuelve Null.  
  
## <a name="remarks"></a>Notas  
Para obtener un ejemplo, consulte [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) .  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="see-also"></a>Consulte también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
