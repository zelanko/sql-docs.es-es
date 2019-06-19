---
title: Restricciones de características | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 99a0a768334ab5335591fae69e4f18060fba9866
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506923"
---
# <a name="feature-restrictions"></a>Restricciones de características

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Un origen común de ataques de SQL Server es a través de aplicaciones web que acceden a la base de datos, donde diversas formas de ataques por inyección de código SQL suelen hacerse con información sobre la base de datos.  Lo ideal es desarrollar código de la aplicación que impida la inyección de código SQL.  Sin embargo, cuando las bases de código son grandes e incluyen código heredado y externo, nunca se puede estar seguro de si se ha hecho frente a todos los casos, de modo que las inyecciones de código SQL son un hecho del que tenemos que protegernos.  El objetivo de las restricciones de características es impedir que algunas formas de inyección de código SQL filtren información sobre la base de datos, incluso cuando la inyección de código SQL se realice correctamente.

## <a name="enabling-feature-restrictions"></a>Habilitación de restricciones de características

Para habilitar las restricciones de características hay que usar el procedimiento almacenado `sp_add_feature_restriction` del siguiente modo:

```sql
EXEC sp_add_feature_restriction <feature>, <object_class>, <object_name>
```

Se pueden restringir las siguientes características:

| Característica          | Descripción |
|------------------|-------------|
| N'ErrorMessages' | Cuando se restringe, se enmascaran los datos de usuario que haya en el mensaje de error. Vea [Restricción de la característica de mensajes de error](#error-messages-feature-restriction). |
| N'Waitfor'       | Cuando se restringe, el comando regresará inmediatamente sin ningún retraso. Vea [Restricción de la característica WAITFOR](#waitfor-feature-restriction). |

El valor de `object_class` puede ser `N'User'` o `N'Role'` para indicar si `object_name` es un nombre de usuario o un nombre de rol en la base de datos.

En el siguiente ejemplo, todos los mensajes de error del usuario `MyUser` se enmascararán:

```sql
EXEC sp_add_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="disabling-feature-restrictions"></a>Deshabilitación de las restricciones de características

Para deshabilitar las restricciones de características hay que usar el procedimiento almacenado `sp_drop_feature_restriction` del siguiente modo:

```sql
EXEC sp_drop_feature_restriction <feature>, <object_class>, <object_name>
```

En el siguiente ejemplo, se deshabilita el enmascaramiento de mensajes de error del usuario `MyUser`:

```sql
EXEC sp_drop_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="viewing-feature-restrictions"></a>Visualización de restricciones de características

La vista `sys.sql_feature_restrictions` presenta todas las restricciones de características definidas actualmente en la base de datos. Vea [sys.sql_feature_restrictions](../system-catalog-views/sys-sql-feature-restrictions.md) para obtener más información.

## <a name="feature-restrictions"></a>Restricciones de características

### <a name="error-messages-feature-restriction"></a>Restricción de la característica de mensajes de error

Un método común de ataque de inyección de código SQL consiste en insertar código que hace que se produzca un error.  Si un atacante examina el mensaje de error, podrá obtener información sobre el sistema, lo que dará pie a ataques más específicos.  Este ataque puede ser especialmente útil cuando la aplicación no muestra los resultados de una consulta, pero sí mensajes de error.

Imagine una aplicación web que tiene una solicitud con el siguiente formato:

```html
http://www.contoso.com/employee.php?id=1
```

Esta solicitud ejecuta la siguiente consulta de base de datos:

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

Si el valor pasado como parámetro `Id` a la solicitud de aplicación web se copia para reemplazar $EmpId en la consulta de base de datos, un atacante podría realizar la siguiente solicitud:

```html
http://www.contoso.com/employee.php?id=1 AND CAST(DB_NAME() AS INT)=0
```

Y se devolvería el siguiente error, lo que permitiría al atacante conocer el nombre de la base de datos:

```sql
Conversion failed when converting the nvarchar value 'HR_Data' to data type int.
```

Después de habilitar la restricción de la característica de mensajes de error para el usuario de la aplicación en la base de datos, el mensaje de error devuelto estará enmascarado, de modo que no se filtrará ninguna información interna de la base de datos:

```sql
Conversion failed when converting the ****** value '******' to data type ******.
```

De forma similar, el atacante podría realizar la siguiente solicitud:

```html
http://www.contoso.com/employee.php?id=1 AND CAST(Salary AS TINYINT)=0
```

Y se devolvería el siguiente error, lo que permitiría al atacante conocer el sueldo del empleado:

```sql
Arithmetic overflow error for data type tinyint, value = 140000.
```

Si se usa la restricción de la característica de mensajes de error, la base de datos devolvería lo siguiente:

```sql
Arithmetic overflow error for data type ******, value = ******.
```

### <a name="waitfor-feature-restriction"></a>Restricción de la característica WAITFOR

Una inyección de código SQL oculta se produce cuando una aplicación no proporciona a un atacante los resultados del código SQL insertado ni ningún mensaje de error, pero el atacante sí puede deducir la información de la base de datos creando una consulta condicional en la que las dos ramas condicionales tardan un tiempo distinto en ejecutarse. Al comparar el tiempo de respuesta, el atacante puede saber qué rama se ha ejecutado y, por tanto, obtener información sobre el sistema. La variante de este ataque más sencilla es usar la instrucción `WAITFOR` para incluir el retraso correspondiente.

Imagine una aplicación web que tiene una solicitud con el siguiente formato:

```html
http://www.contoso.com/employee.php?id=1
```

Esta solicitud ejecuta la siguiente consulta de base de datos:

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

Si el valor pasado como parámetro `Id` a las solicitudes de aplicación web se copia para reemplazar $EmpId en la consulta de base de datos, un atacante podría realizar la siguiente solicitud:

```html
http://www.contoso.com/employee.php?id=1; IF SYSTEM_USER='sa' WAITFOR DELAY '00:00:05'
```

Con lo cual la consulta tardaría 5 segundos más si se usara la cuenta `sa`. Si la restricción de la característica `WAITFOR` está deshabilitada en la base de datos, la instrucción `WAITFOR` se omitirá y no se filtrará ninguna información con este ataque.
