---
title: 'PDO:: __construct | Documentos de Microsoft'
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
ms.topic: article
ms.assetid: 3ee53aff-6fe4-44cd-a15b-51770c98c712
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9cf4a81701d1ad4ddaa1491ea877331f933a9e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="pdoconstruct"></a>PDO::__construct
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Crear una conexión a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PDO::__construct($dsn [,$username [,$password [,$driver_options ]]] )  
```  
  
#### <a name="parameters"></a>Parámetros  
*$dsn*: una cadena que contiene el nombre del prefijo (siempre `sqlsrv`), dos puntos y la palabra clave Server. Por ejemplo, `"sqlsrv:server=(local)"`. También puede especificar otras palabras clave de conexión. Consulte [Connection Options](../../connect/php/connection-options.md) para obtener una descripción de la palabra clave Server y del resto de las palabras clave de conexión. *$dsn* está entre comillas, por lo que no se debe entrecomillar cada palabra clave de conexión.  
  
*$username*: opcional. Una cadena que contiene el nombre del usuario. Para establecer la conexión utilizando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , especifique el id. de inicio de sesión. Para establecer la conexión utilizando la autenticación de Windows, especifique `""`.  
  
*$password*: opcional. Una cadena que contiene la contraseña del usuario. Para establecer la conexión utilizando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , especifique la contraseña. Para establecer la conexión utilizando la autenticación de Windows, especifique `""`.  
  
*$driver_options*: opcional. Puede especificar los atributos del Administrador de controladores de PDO y [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] atributos de controladores específicos--PDO:: sqlsrv_attr_encoding y PDO:: sqlsrv_attr_direct_query. Un atributo no válido no genera una excepción. solo lo harán cuando se especifican con [PDO::setAttribute](../../connect/php/pdo-setattribute.md).  
  
## <a name="return-value"></a>Valor devuelto  
Devuelve un objeto de PDO. Si se produce un error, devuelve un objeto PDOException.  
  
## <a name="exceptions"></a>Excepciones  
PDOException  
  
## <a name="remarks"></a>Comentarios  
Puede cerrar un objeto de conexión estableciendo el valor de la instancia en Null.  
  
Después de una conexión, PDO:: ErrorCode muestra 01000 en lugar de 00000.  
  
Si se produce un error en PDO:: __construct por cualquier motivo, se produce una excepción, aunque se establezca PDO:: attr_errmode en PDO:: errmode_silent.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo se muestra cómo conectarse a un servidor mediante la autenticación de Windows y especificar una base de datos.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:Server=(local) ; Database = AdventureWorks ", "", "", array(PDO::SQLSRV_ATTR_DIRECT_QUERY => true));   
  
   $query = 'SELECT * FROM Person.ContactType';   
   $stmt = $c->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ) {   
      print_r( $row );   
   }  
   $c = null;   
?>  
```  
  
## <a name="example"></a>Ejemplo  
En este ejemplo se muestra cómo conectarse a un servidor especificando la base de datos más adelante.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec( "USE AdventureWorks");  
   $query = 'SELECT * FROM Person.ContactType';  
   $stmt = $c->query( $query );  
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
      print_r( $row );  
   }  
   $c = null;  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
