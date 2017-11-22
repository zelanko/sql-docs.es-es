---
title: 'PDO:: BeginTransaction | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 131edab231009e63c32a3c5b7a4d6ffccfc7d407
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
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
Cuando finalice la transacción iniciada con PDO::beginTransaction, se llamará a [PDO::commit](../../connect/php/pdo-commit.md) o [PDO::rollback](../../connect/php/pdo-rollback.md) .  
  
El valor de PDO::ATTR_AUTOCOMMIT no afecta a PDO::beginTransaction.  
  
No se permiten llamar a PDO::beginTransaction antes de  finalizar la transacción PDO::beginTransaction anterior con PDO::rollback o PDO::commit.  
  
Si se produce un error en este método, la conexión volverá al modo de confirmación automática.  
  
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
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
