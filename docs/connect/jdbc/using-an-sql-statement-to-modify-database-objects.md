---
title: Usar una instrucción SQL para modificar objetos de base de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 809ad678f6257e7e2cdc4af5915f5d4902a5c144
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>Usar una instrucción SQL para modificar objetos de la base de datos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para modificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos de base de datos mediante una instrucción SQL, puede usar el [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) método de la [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) clase. El método executeUpdate pasará la instrucción SQL para la base de datos para su procesamiento y, a continuación, devuelve un valor de 0 porque no hay filas afectadas.  
  
 Para ello, primero debe crear un objeto SQLServerStatement mediante el uso de la [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase.  
  
> [!NOTE]  
>  Las instrucciones SQL que modifican objetos dentro de una base de datos, se llaman instrucciones de lenguaje de definición de datos (DDL). Estas instrucciones incluyen CREATE TABLE, DROP TABLE, CREATE INDEX y DROP INDEX. Para obtener más información acerca de los tipos de instrucciones de DDL que son compatibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función, se genera una instrucción SQL que creará la TestTable sencilla en la base de datos y, a continuación, se ejecuta la instrucción y se muestra el valor devuelto.  
  
 [!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  
