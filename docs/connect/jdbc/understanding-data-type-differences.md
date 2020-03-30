---
title: Descripción de las diferencias entre los tipos de datos | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 906a4abf0768fcad2e5ac31a0ee93345dcc8b30c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027381"
---
# <a name="understanding-data-type-differences"></a>Descripción de las diferencias entre los tipos de datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Hay varias diferencias entre los tipos de datos del lenguaje de programación Java y los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ayuda a facilitar esas diferencias mediante diversos tipos de conversiones.  

## <a name="character-types"></a>Tipos de caracteres

Los tipos de datos de cadena de caracteres de JDBC son **CHAR**, **VARCHAR** y **LONGVARCHAR**. El controlador JDBC ofrece compatibilidad con la API de JDBC 4.0. En JDBC 4.0, los tipos de datos de cadena de caracteres de JDBC también pueden ser **NCHAR**, **NVARCHAR** y **LONGNVARCHAR**. Estos nuevos tipos de cadena de caracteres mantienen los tipos de caracteres nativos de Java en formato Unicode y quitan la necesidad de realizar cualquier conversión ANSI a Unicode o Unicode a ANSI.  
  
| Tipo            | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Longitud fija    | Los tipos de datos **char** y **nchar** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se asignan directamente a los tipos **CHAR** y **NCHAR** de JDBC. Estos son tipos de longitud fija con relleno que proporciona el servidor en caso de que la columna tenga `SET ANSI_PADDING ON`. El relleno siempre está habilitado para **nchar**, pero en el caso de **char**, si las columnas char del servidor no tienen relleno, el servidor lo agrega el controlador JDBC.                                                                                                                                                                                                                                                                                                                                                                                      |
| Longitud variable | Los tipos **varchar** y **nvarchar** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se asignan directamente a los tipos de JDBC **VARCHAR** y **NVARCHAR**, respectivamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| long            | Los tipos **text** y **ntext** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se asignan a los tipos de JDBC **LONGVARCHAR** y **LONGNVARCHAR**, respectivamente. Estos son tipos que ya no se utilizan desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], por lo que en su lugar debería usar tipos de valores mayores, **varchar(max)** o **nvarchar(max)** .<br /><br /> No se pueden usar los métodos update\<Numeric Type> y [updateObject (int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) con las columnas de servidor **text** y **ntext**. Pero se admite el uso del método [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) con un tipo específico de conversión de caracteres en columnas **text** y **ntext** del servidor. |
  
## <a name="binary-string-types"></a>Tipos de cadenas binarias

Los tipos de cadenas binarias de JDBC son **BINARY**, **VARBINARY** y **LONGVARBINARY**.  
  
| Tipo            | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Longitud fija    | El tipo **binary** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se asigna directamente al tipo **BINARY** de JDBC. Es un tipo de longitud fija con relleno que proporciona el servidor en el caso de que la columna tenga habilitado SET ANSI_PADDING. Cuando las columnas char del servidor no tienen relleno, éste lo agrega el controlador JDBC.<br /><br /> El tipo **timestamp** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un tipo **BINARY** de JDBC con la longitud fija de 8 bytes. |
| Longitud variable | El tipo **varbinary** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se asigna al tipo **VARBINARY** de JDBC.<br /><br /> El tipo **udt** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se asigna a JDBC como un tipo **VARBINARY**.                                                                                                                                                                                                                                 |
| long            | El tipo **image** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se asigna al tipo **LONGVARBINARY** de JDBC. Este tipo se ha dejado de utilizar desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], por lo que en su lugar debería usar un tipo de valor grande, **varbinary(max)** .                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>Tipos numéricos exactos

Los tipos numéricos exactos de JDBC se asignan directamente a los tipos de SQL Server correspondientes.  
  
| Tipo     | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | El tipo de JDBC **BIT** representa un bit único que puede ser 0 ó 1. Esto se asigna a un tipo **bit** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | El tipo de JDBC **TINYINT** representa un byte único. Esto se asigna a un tipo **tinyint** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | El tipo de JDBC **SMALLINT** representa un entero con signo de 16 bits. Esto se asigna a un tipo **smallint** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | El tipo de JDBC **INTEGER** representa un entero con signo de 32 bits. Esto se asigna a un tipo **int** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                                                                                                                                                                                                                                                           |
| bigint   | El tipo de JDBC **BIGINT** representa un entero con signo de 64 bits. Esto se asigna a un tipo **bigint** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | El tipo **NUMERIC** de JDBC representa un valor decimal de precisión fija que contiene valores de precisión idéntica. El tipo **NUMERIC** se asigna al tipo **numeric** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                                                                                                                                                                                   |
| DECIMAL  | El tipo **DECIMAL** de JDBC representa un valor decimal de precisión fija que contiene valores de, al menos, la precisión especificada. El tipo **DECIMAL** se asigna al tipo **decimal** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> El tipo **DECIMAL** de JDBC también se asigna a los tipos **money** y **smallmoney** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que son tipos decimales de precisión fija específicos almacenados en 8 y 4 bytes, respectivamente. |
  
## <a name="approximate-numeric-types"></a>Tipos numéricos aproximados

Los tipos numéricos aproximados de JDBC son **REAL**, **DOUBLE** y **FLOAT**.  
  
| Tipo   | Descripción                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | El tipo de JDBC **REAL** tiene siete dígitos de precisión (precisión simple) y se asigna directamente al tipo **real** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                                                     |
| DOUBLE | El tipo **DOUBLE** de JDBC tiene 15 dígitos de precisión (precisión doble) y se asigna al tipo **float** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El tipo**FLOAT** de JDBC es un sinónimo de **DOUBLE**. Dado que puede haber confusión entre **FLOAT** y **DOUBLE**, se prefiere **DOUBLE**. |
  
## <a name="datetime-types"></a>Tipos Datetime

El tipo de JDBC **TIMESTAMP** se asigna a los tipos **datetime** y **smalldatetime** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El tipo **datetime** se almacena en dos enteros de 4 bytes. El tipo **smalldatetime** contiene la misma información (fecha y hora), pero con menos precisión, en dos enteros pequeños de 2 bytes.  
  
> [!NOTE]  
> El tipo **timestamp** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un tipo de cadena binaria de longitud fija. No se asigna a ninguno de los tipos de tiempo de JDBC: **DATE**, **TIME** o **TIMESTAMP**.  
  
## <a name="custom-type-mapping"></a>Asignación de tipos personalizados

La característica de asignación de tipos personalizados de JDBC que emplean las interfaces SQLData para los tipos avanzados de JDBC (UDT, Struct, etc.). no se incluye en el controlador JDBC.  
  
## <a name="see-also"></a>Consulte también

[Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
