---
title: 'PDO:: exec | Documentos de Microsoft'
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
ms.assetid: 359a87c6-c13a-4518-8f23-a922e7f3b171
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 48b1d6f918d87d2ad65b4be8b47a5a23975d1811
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="pdoexec"></a>PDO::exec
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Prepara y ejecuta una instrucción SQL en una única llamada a una función, y devuelve el número de filas a las que afecta la instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int PDO::exec ($statement)  
```  
  
#### <a name="parameters"></a>Parámetros  
*$statement*: una cadena que contiene la instrucción SQL que se ejecutará.  
  
## <a name="return-value"></a>Valor devuelto  
Un valor entero que notifica el número de filas afectadas.  
  
## <a name="remarks"></a>Comentarios  
Si *$statement* contiene varias instrucciones SQL, solo se notifica el recuento de filas afectadas de la última instrucción.  
  
PDO::exec no devuelve los resultados de una instrucción SELECT.  
  
Los siguientes atributos afectan al comportamiento de PDO::exec:  
  
-   PDO::ATTR_DEFAULT_FETCH_MODE  
  
-   PDO::SQLSRV_ATTR_ENCODING  
  
-   PDO::SQLSRV_ATTR_QUERY_TIMEOUT  
  
Consulte [PDO::setAttribute](../../connect/php/pdo-setattribute.md) para obtener más información.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo se eliminan las filas de Table1 que incluyen "xxxyy" en col1. En el ejemplo se informa de cuántas filas se han eliminado.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec("use Test");  
   $ret = $c->exec("delete from Table1 where col1 = 'xxxyy'");  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDO](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
