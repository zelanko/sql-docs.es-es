---
title: Emulación de las variables del paquete de Oracle
description: Describe cómo SQL Server Migration Assistant (SSMA) para Oracle emula las variables de paquete de Oracle en SQL Server.
authors: nahk-ivanov
ms.service: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 9a8ca5c7dfdda98e1c005c3851d061957cf67449
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "76762829"
---
# <a name="emulating-oracle-package-variables"></a>Emulación de las variables del paquete de Oracle

Oracle admite la encapsulación de variables, tipos, procedimientos almacenados y funciones en un paquete. Al convertir paquetes de Oracle, debe convertir:

* Procedimientos y funciones: tanto públicos como privados
* variables
* Cursores
* Rutinas de inicialización

En este artículo se describe cómo SQL Server Migration Assistant (SSMA) para Oracle convierte las variables de paquete en SQL Server.

## <a name="conversion-basics"></a>Aspectos básicos de la conversión

Para almacenar variables de paquete, SSMA para Oracle utiliza procedimientos almacenados que residen en un `ssma_oracle` esquema especial junto `ssma_oracle.db_storage` con una tabla. Esta tabla se filtra por `SPID` (identificador de sesión) y hora de inicio de sesión. Este filtrado le permite distinguir entre las variables de distintas sesiones.

Al principio de cada procedimiento de paquete convertido, SSMA coloca una llamada al `ssma_oracle.db_check_init_package` procedimiento especial, que comprueba si el paquete se ha inicializado y lo inicializará si es necesario. Cada procedimiento de inicialización limpia la tabla de almacenamiento y establece los valores predeterminados para cada variable de paquete.

## <a name="example"></a>Ejemplo

Considere el ejemplo siguiente para convertir varias variables de paquete:

```sql
CREATE OR REPLACE PACKAGE MY_PACKAGE
IS
    space varchar(1) := ' ';
    unitname varchar(128) := 'My Simple Package';
    ts date := sysdate;
END;
```

SSMA lo convierte en el siguiente código de Transact-SQL:

```sql
CREATE PROCEDURE dbo.MY_PACKAGE$SSMA_Initialize_Package
AS
BEGIN
    EXECUTE ssma_oracle.db_clean_storage

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'SPACE',
        ' '

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'UNITNAME',
        'My Simple Package'

    DECLARE
        @temp datetime2

    SET @temp = sysdatetime()

    EXECUTE sysdb.ssma_oracle.set_pv_datetime2
      DB_NAME(),
      'DBO',
      'MY_PACKAGE',
      'TS',
      @temp
END
```

## <a name="emulating-get-and-set-methods-for-package-variables"></a>Emular métodos GET y set para variables de paquete

Oracle usa `Get` los `Set` métodos y para las variables de paquete, para evitar que otros subprogramas puedan leerlos y escribirlos directamente. Si hay un requisito para mantener algunas variables disponibles entre las llamadas de subprogramas en la misma sesión, estas variables se tratan como variables globales.

Para superar esta regla de ámbito, SSMA para Oracle utiliza procedimientos almacenados `ssma_oracle.set_pv_varchar` como para cada tipo de variable. Para obtener acceso a estas variables, SSMA usa un conjunto de procedimientos y `get_*` funciones `set_*` independientes de las transacciones y.

| Tipo de datos en Oracle | SSMA `Set` (procedimiento)           |
| ------------------- | ------------------------------ |
| VARCHAR             | `ssma_oracle.set_pv_varchar`   |
| DATE                | `ssma_oracle.set_pv_datetime2` |
| CHAR                | `ssma_oracle.set_pv_varchar`   |
| INT                 | `ssma_oracle.set_pv_float`     |
| FLOAT               | `ssma_oracle.set_pv_float`     |

Para distinguir entre las variables de distintas sesiones, SSMA almacena las variables junto con `SPID` su (identificador de sesión) y la hora de inicio de sesión. Por lo `get_*` tanto `set_*` , los procedimientos y mantienen las variables independientes de las sesiones que las ejecutan.
