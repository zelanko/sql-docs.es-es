---
title: 'PDO:: BeginTransaction | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c3e4fc0dce4b712d1a7bea39f0b69f605d68fcb9
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606625"
---
# <a name="pdobegintransaction"></a>PDO::beginTransaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Desactiva el modo de confirmación automática e inicia una transacción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
bool PDO::beginTransaction();  
```  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve el valor True si la llamada al método se realizó correctamente; en caso contrario, se devuelve False.  
  
## <a name="remarks"></a>Notas  
Cuando finalice la transacción iniciada con PDO::beginTransaction, se llamará a [PDO::commit](../../connect/php/pdo-commit.md) o [PDO::rollback](../../connect/php/pdo-rollback.md).  
  
El valor de PDO::ATTR_AUTOCOMMIT no afecta a PDO::beginTransaction.  
  
No se permiten llamar a PDO::beginTransaction antes de  finalizar la transacción PDO::beginTransaction anterior con PDO::rollback o PDO::commit.  
  
Si se produce un error en este método, la conexión vuelve al modo de confirmación automática.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se utiliza una base de datos denominada "Test" y una tabla llamada "Table1". Inicia una transacción y, luego, ejecuta comandos para agregar dos filas y eliminar una. Los comandos se envían a la base de datos y la transacción se finaliza explícitamente con `PDO::commit`.  
  
```  
<?php  
   $conn = new PDO( "sqlsrv:server=(local); Database = Test", "", "");  
   $conn->beginTransaction();  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'b') ");  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'c') ");  
   $ret = $conn->exec("delete from Table1 where col1 = 'a' and col2 = 'b'");  
   $conn->commit();  
   // $conn->rollback();  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>Ver también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
