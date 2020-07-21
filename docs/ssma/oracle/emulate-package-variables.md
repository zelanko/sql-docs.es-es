---
title: Emulación de las variables del paquete de Oracle
description: Describe cómo SQL Server Migration Assistant (SSMA) para Oracle emula las variables de paquete de Oracle en SQL Server.
author: nahk-ivanov
ms.prod: sql
ms.technology: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: ab7de81e16d1324aabd5f07421c1db4c51b3cf7c
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2020
ms.locfileid: "84779467"
---
# <a name="emulating-oracle-package-variables"></a>Emulación de las variables del paquete de Oracle

Oracle admite la encapsulación de variables, tipos, procedimientos almacenados y funciones en un paquete. Al convertir paquetes de Oracle, debe convertir:

* Procedimientos y funciones: tanto públicos como privados
* Variables
* Cursores
* Rutinas de inicialización

En este artículo se describe cómo SQL Server Migration Assistant (SSMA) para Oracle convierte las variables de paquete en SQL Server.

## <a name="conversion-basics"></a>Aspectos básicos de la conversión

Para almacenar variables de paquete, SSMA para Oracle utiliza procedimientos almacenados que residen en un `ssma_oracle` esquema especial junto con una `ssma_oracle.db_storage` tabla. Esta tabla se filtra por `SPID` (identificador de sesión) y hora de inicio de sesión. Este filtrado le permite distinguir entre las variables de distintas sesiones.

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

Oracle usa `Get` `Set` los métodos y para las variables de paquete, para evitar que otros subprogramas puedan leerlos y escribirlos directamente. Si hay un requisito para mantener algunas variables disponibles entre las llamadas de subprogramas en la misma sesión, estas variables se tratan como variables globales.

Para superar esta regla de ámbito, SSMA para Oracle utiliza procedimientos almacenados como `ssma_oracle.set_pv_varchar` para cada tipo de variable. Para obtener acceso a estas variables, SSMA usa un conjunto de procedimientos y `get_*` funciones independientes de las transacciones y `set_*` .

| Tipo de datos en Oracle | SSMA ( `Set` procedimiento)           |
| ------------------- | ------------------------------ |
| VARCHAR             | `ssma_oracle.set_pv_varchar`   |
| DATE                | `ssma_oracle.set_pv_datetime2` |
| CHAR                | `ssma_oracle.set_pv_varchar`   |
| INT                 | `ssma_oracle.set_pv_float`     |
| FLOAT               | `ssma_oracle.set_pv_float`     |

Para distinguir entre las variables de distintas sesiones, SSMA almacena las variables junto con su `SPID` (identificador de sesión) y la hora de inicio de sesión. Por lo tanto, los `get_*` `set_*` procedimientos y mantienen las variables independientes de las sesiones que las ejecutan.
