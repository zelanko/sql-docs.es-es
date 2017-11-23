---
title: 'Pdostatement:: Execute | Documentos de Microsoft'
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
ms.assetid: c2e80566-fa41-4918-8521-cf2e05374cbd
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f07ac6e21c465ca04c071e70624de138e918e23
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="pdostatementexecute"></a>PDOStatement::execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ejecuta una instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
bool PDOStatement::execute ([ $input ] );  
```  
  
#### <a name="parameters"></a>Parámetros  
*$input*: (opcional) una matriz asociativa que contiene los valores para los marcadores de parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve True si se ejecuta correctamente; de lo contrario, se devuelve False.  
  
## <a name="remarks"></a>Comentarios  
Las instrucciones ejecutadas con PDOStatement::execute deben prepararse primero con [PDO::prepare](../../connect/php/pdo-prepare.md). Vea [Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver (Ejecución de la instrucción preparada o directa en el controlador PDO_SQLSRV)](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md) para obtener información sobre cómo especificar la ejecución de la instrucción preparada o directa.  
  
Todos los valores de la matriz de parámetros de entrada se tratan como valores de PDO::PARAM_STR.  
  
Si la instrucción preparada incluye marcadores de parámetros, debe llamar a PDOStatement::bindParam para enlazar las variables PHP a tales marcadores, o bien transmitir una matriz de valores de parámetro de solo entrada.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query );  
$stmt->execute();  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
  
echo "\n";  
$param = "Owner";  
$query = "select * from Person.ContactType where name = ?";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
