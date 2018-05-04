---
title: 'PDO:: BeginTransaction | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d683c702ae731515403de234a2e9628c60da45b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>Comentarios  
Finaliza la transacción iniciada con PDO:: BeginTransaction cuando [PDO:: Commit](../../connect/php/pdo-commit.md) o [PDO:: Rollback](../../connect/php/pdo-rollback.md) se llama.  
  
El valor de PDO::ATTR_AUTOCOMMIT no afecta a PDO::beginTransaction.  
  
No se permiten llamar a PDO::beginTransaction antes de  finalizar la transacción PDO::beginTransaction anterior con PDO::rollback o PDO::commit.  
  
La conexión vuelve al modo de confirmación automática si se produce un error en este método.  
  
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
  
## <a name="see-also"></a>Vea también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
