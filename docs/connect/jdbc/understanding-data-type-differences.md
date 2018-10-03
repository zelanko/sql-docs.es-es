---
title: Diferencias de tipo de datos de descripción | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 546dc71fad06fc69d816d16c1d6c2d67f59f968b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773213"
---
# <a name="understanding-data-type-differences"></a>Descripción de las diferencias entre los tipos de datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Hay varias diferencias entre los tipos de datos del lenguaje de programación Java y los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ayuda a facilitar esas diferencias mediante diversos tipos de conversiones.  

## <a name="character-types"></a>Tipos de caracteres

Los tipos de datos de cadena de caracteres JDBC son **CHAR**, **VARCHAR**, y **LONGVARCHAR**. El controlador JDBC ofrece compatibilidad con la API de JDBC 4.0. En JDBC 4.0, los tipos de datos de cadena de caracteres JDBC también pueden ser **NCHAR**, **NVARCHAR**, y **LONGNVARCHAR**. Estos nuevos tipos de cadena de caracteres mantienen los tipos de caracteres nativos de Java en formato Unicode y quitan la necesidad de realizar cualquier conversión ANSI a Unicode o Unicode a ANSI.  
  
| Tipo            | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Longitud fija    | El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char** y **nchar** tipos de datos se asignan directamente a JDBC **CHAR** y **NCHAR** tipos. Estos son tipos de longitud fija con relleno que proporciona el servidor en caso de que la columna tenga `SET ANSI_PADDING ON`. El relleno siempre está habilitado para **nchar**, pero en el caso de **char**, si las columnas char del servidor no tienen relleno, el servidor lo agrega el controlador JDBC.                                                                                                                                                                                                                                                                                                                                                                                      |
| Longitud variable | El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varchar** y **nvarchar** tipos se asignan directamente a JDBC **VARCHAR** y **NVARCHAR** tipos, respectivamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Long            | El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **texto** y **ntext** tipos se asignan a JDBC **LONGVARCHAR** y **LONGNVARCHAR** escriba, respectivamente. Estos son los tipos en desuso a partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], por lo que debe usar tipos de valor grande, **varchar (max)** o **nvarchar (max)** en su lugar.<br /><br /> Con la actualización de\<tipo numérico > y [updateObject (int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) métodos se producirá un error en **texto** y **ntext** las columnas de servidor. Pero se admite el uso del método [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) con un tipo específico de conversión de caracteres en columnas **text** y **ntext** del servidor. |
  
## <a name="binary-string-types"></a>Tipos de cadenas binarias

Los tipos de datos de cadenas binarias JDBC son **binario**, **VARBINARY**, y **LONGVARBINARY**.  
  
| Tipo            | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Longitud fija    | El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binario** tipo se asigna directamente a JDBC **binario** tipo. Es un tipo de longitud fija con relleno que proporciona el servidor en el caso de que la columna tenga habilitado SET ANSI_PADDING. Cuando las columnas char del servidor no tienen relleno, éste lo agrega el controlador JDBC.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** tipo es un JDBC **binario** tipo con la longitud fija de 8 bytes. |
| Longitud variable | El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varbinary** tipo se asigna a JDBC **VARBINARY** tipo.<br /><br /> El **udt** escriba [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se asigna a JDBC como un **VARBINARY** tipo.                                                                                                                                                                                                                                 |
| Long            | El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **imagen** tipo se asigna a JDBC **LONGVARBINARY** tipo. Este tipo se ha dejado de utilizar desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], por lo que en su lugar debería usar un tipo de valor grande, **varbinary(max)**.                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>Tipos numéricos exactos

Los tipos numéricos exactos de JDBC se asignan directamente a los tipos de SQL Server correspondientes.  
  
| Tipo     | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | El tipo de JDBC **BIT** representa un bit único que puede ser 0 ó 1. Esto se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit** tipo.                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | El tipo de JDBC **TINYINT** representa un byte único. Esto se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint** tipo.                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | El tipo de JDBC **SMALLINT** representa un entero con signo de 16 bits. Esto se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **smallint** tipo.                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | El tipo de JDBC **INTEGER** representa un entero con signo de 32 bits. Esto se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int** tipo.                                                                                                                                                                                                                                                                                                                                           |
| bigint   | El tipo de JDBC **BIGINT** representa un entero con signo de 64 bits. Esto se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bigint** tipo.                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | El tipo **NUMERIC** de JDBC representa un valor decimal de precisión fija que contiene valores de precisión idéntica. El **numérico** tipo se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **numérico** tipo.                                                                                                                                                                                                                                                                   |
| DECIMAL  | El tipo **DECIMAL** de JDBC representa un valor decimal de precisión fija que contiene valores de, al menos, la precisión especificada. El **DECIMAL** tipo se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **decimal** tipo.<br /><br /> El tipo **DECIMAL** de JDBC también se asigna a los tipos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**money** y **smallmoney**, que son tipos decimales de precisión fija almacenados en 8 y 4 bytes, respectivamente. |
  
## <a name="approximate-numeric-types"></a>Tipos numéricos aproximados

Los tipos numéricos aproximados de JDBC son **REAL**, **doble**, y **FLOAT**.  
  
| Tipo   | Descripción                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | El tipo de JDBC **REAL** tiene siete dígitos de precisión (precisión simple) y se asigna directamente al tipo **real** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                                                     |
| DOUBLE | El tipo **DOUBLE** de JDBC tiene 15 dígitos de precisión (precisión doble) y se asigna al tipo **float** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. JDBC **FLOAT** tipo es un sinónimo de **doble**. Dado que puede haber confusión entre **FLOAT** y **doble**, **doble** es preferible. |
  
## <a name="datetime-types"></a>Tipos de fecha y hora

JDBC **TIMESTAMP** tipo se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** y **smalldatetime** tipos. El tipo **datetime** se almacena en dos enteros de 4 bytes. El tipo **smalldatetime** contiene la misma información (fecha y hora), pero con menos precisión, en dos enteros pequeños de 2 bytes.  
  
> [!NOTE]  
> El tipo **timestamp** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un tipo de cadena binaria de longitud fija. No se asigna a cualquiera de los tipos de tiempo JDBC: **fecha**, **tiempo**, o **TIMESTAMP**.  
  
## <a name="custom-type-mapping"></a>Asignación de tipos personalizados

La característica de asignación de tipos personalizados de JDBC que emplean las interfaces SQLData para los tipos avanzados de JDBC (UDT, Struct, etc.). no se incluye en el controlador JDBC.  
  
## <a name="see-also"></a>Ver también

[Describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
