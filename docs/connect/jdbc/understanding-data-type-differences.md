---
title: Descripción de las diferencias de tipos de datos | Microsoft Docs
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
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027381"
---
# <a name="understanding-data-type-differences"></a>Descripción de las diferencias entre los tipos de datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Hay varias diferencias entre los tipos de datos del lenguaje de programación Java y los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ayuda a facilitar esas diferencias mediante diversos tipos de conversiones.  

## <a name="character-types"></a>Tipos de caracteres

Los tipos de datos de cadena de caracteres de JDBC son **Char**, **VARCHAR**y **longvarchar**. El controlador JDBC ofrece compatibilidad con la API de JDBC 4.0. En JDBC 4,0, los tipos de datos de cadena de caracteres de JDBC también pueden ser **nchar**, **nvarchar**y **LONGNVARCHAR**. Estos nuevos tipos de cadena de caracteres mantienen los tipos de caracteres nativos de Java en formato Unicode y quitan la necesidad de realizar cualquier conversión ANSI a Unicode o Unicode a ANSI.  
  
| Tipo            | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Longitud fija    | Los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos **Char** y **nchar** se asignan directamente a los tipos **Char** y **nchar** de JDBC. Estos son tipos de longitud fija con relleno que proporciona el servidor en caso de que la columna tenga `SET ANSI_PADDING ON`. El relleno siempre está habilitado para **nchar**, pero en el caso de **char**, si las columnas char del servidor no tienen relleno, el servidor lo agrega el controlador JDBC.                                                                                                                                                                                                                                                                                                                                                                                      |
| Longitud variable | Los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos **VARCHAR** y **nvarchar** se asignan directamente a los tipos de JDBC **VARCHAR** y **nvarchar** , respectivamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Long            | Los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos **Text** y **ntext** se asignan al tipo **longvarchar** y **LONGNVARCHAR** de JDBC, respectivamente. Estos son tipos en desuso a partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]de, por lo que en su lugar debe usar tipos de valor grande, **VARCHAR (Max)** o **nvarchar (Max)** .<br /><br /> El uso de\<los métodos Update Numeric Type > y [updateObject (int, Java. lang. Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) producirá un error en las columnas de servidor **Text** y **ntext** . Pero se admite el uso del método [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) con un tipo específico de conversión de caracteres en columnas **text** y **ntext** del servidor. |
  
## <a name="binary-string-types"></a>Tipos de cadenas binarias

Los tipos de cadenas binarias de JDBC son **Binary**, **varbinary**y **LONGVARBINARY**.  
  
| Tipo            | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Longitud fija    | El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **binario** se asigna directamente al tipo **binario** de JDBC. Es un tipo de longitud fija con relleno que proporciona el servidor en el caso de que la columna tenga habilitado SET ANSI_PADDING. Cuando las columnas char del servidor no tienen relleno, éste lo agrega el controlador JDBC.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de **marca** de tiempo es un tipo **binario** de JDBC con la longitud fija de 8 bytes. |
| Longitud variable | El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **varbinary** se asigna al tipo **varbinary** de JDBC.<br /><br /> El tipo **UDT** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se asigna a JDBC como tipo **varbinary** .                                                                                                                                                                                                                                 |
| Long            | El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de **imagen** se asigna al tipo **LONGVARBINARY** de JDBC. Este tipo se ha dejado de utilizar desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], por lo que en su lugar debería usar un tipo de valor grande, **varbinary(max)** .                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>Tipos numéricos exactos

Los tipos numéricos exactos de JDBC se asignan directamente a los tipos de SQL Server correspondientes.  
  
| Tipo     | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | El tipo de JDBC **BIT** representa un bit único que puede ser 0 ó 1. Esto se asigna a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un tipo de **bit** .                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | El tipo de JDBC **TINYINT** representa un byte único. Se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **tinyint** .                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | El tipo de JDBC **SMALLINT** representa un entero con signo de 16 bits. Esto se asigna a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un tipo **smallint** .                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | El tipo de JDBC **INTEGER** representa un entero con signo de 32 bits. Esto se asigna a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un tipo **int** .                                                                                                                                                                                                                                                                                                                                           |
| bigint   | El tipo de JDBC **BIGINT** representa un entero con signo de 64 bits. Esto se asigna a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un tipo **BIGINT** .                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | El tipo **NUMERIC** de JDBC representa un valor decimal de precisión fija que contiene valores de precisión idéntica. El tipo **numérico** se asigna al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **numérico** .                                                                                                                                                                                                                                                                   |
| DECIMAL  | El tipo **DECIMAL** de JDBC representa un valor decimal de precisión fija que contiene valores de, al menos, la precisión especificada. El tipo **decimal** se asigna al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **decimal** .<br /><br /> El tipo **DECIMAL** de JDBC también se asigna a los tipos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**money** y **smallmoney**, que son tipos decimales de precisión fija almacenados en 8 y 4 bytes, respectivamente. |
  
## <a name="approximate-numeric-types"></a>Tipos numéricos aproximados

Los tipos numéricos aproximados de JDBC son **real**, **Double**y **float**.  
  
| Tipo   | Descripción                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | El tipo de JDBC **REAL** tiene siete dígitos de precisión (precisión simple) y se asigna directamente al tipo **real** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                                                     |
| DOUBLE | El tipo **DOUBLE** de JDBC tiene 15 dígitos de precisión (precisión doble) y se asigna al tipo **float** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El tipo **float** de JDBC es un sinónimo de **Double**. Dado que puede haber confusión entre **float** y **Double**, se prefiere **Double** . |
  
## <a name="datetime-types"></a>Tipos DateTime

El tipo **de marca** de tiempo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC se asigna a los tipos **DateTime** y **smalldatetime** . El tipo **datetime** se almacena en dos enteros de 4 bytes. El tipo **smalldatetime** contiene la misma información (fecha y hora), pero con menos precisión, en dos enteros pequeños de 2 bytes.  
  
> [!NOTE]  
> El tipo **timestamp** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un tipo de cadena binaria de longitud fija. No se asigna a ninguno de los tipos de hora de JDBC: **fecha**, **hora**o **marca**de tiempo.  
  
## <a name="custom-type-mapping"></a>Asignación de tipos personalizados

La característica de asignación de tipos personalizados de JDBC que emplean las interfaces SQLData para los tipos avanzados de JDBC (UDT, Struct, etc.). no se incluye en el controlador JDBC.  
  
## <a name="see-also"></a>Vea también

[Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
