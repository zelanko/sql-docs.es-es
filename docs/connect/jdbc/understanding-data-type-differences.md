---
title: "Diferencias de tipo de datos de descripción | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a0068e98ab284ff3fbe89a7047cf485ecb5ef4b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-data-type-differences"></a>Descripción de las diferencias entre los tipos de datos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Hay varias diferencias entre los tipos de datos de lenguaje de programación Java y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ayuda a facilitar esas diferencias mediante diversos tipos de conversiones.  
  
## <a name="character-types"></a>Tipos de caracteres  
 Los tipos de datos de cadena de caracteres JDBC son **CHAR**, **VARCHAR**, y **LONGVARCHAR**. El controlador JDBC ofrece compatibilidad con la API de JDBC 4.0. En JDBC 4.0, los tipos de datos de cadena de caracteres JDBC también pueden ser **NCHAR**, **NVARCHAR**, y **LONGNVARCHAR**. Estos nuevos tipos de cadena de caracteres mantienen los tipos de caracteres nativos de Java en formato Unicode y quitan la necesidad de realizar cualquier conversión ANSI a Unicode o Unicode a ANSI.  
  
|Tipo|Description|  
|----------|-----------------|  
|Longitud fija|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **char** y **nchar** tipos de datos se asignan directamente a JDBC **CHAR** y **NCHAR** tipos. Estos son tipos de longitud fija con relleno que proporciona el servidor en el caso de que la columna tenga habilitado SET ANSI_PADDING ON. Relleno siempre está activado para **nchar**, pero para **char**, en el caso de que no se rellenan las columnas char del servidor, el controlador JDBC agrega el relleno.|  
|Longitud variable|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **varchar** y **nvarchar** tipos se asignan directamente a JDBC **VARCHAR** y **NVARCHAR** tipos, respectivamente.|  
|Long|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **texto** y **ntext** tipos se asignan a JDBC **LONGVARCHAR** y **LONGNVARCHAR** respectivamente. Estos son los tipos en desuso a partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], por lo que debe usar tipos de valor grande, **varchar (max)** o **nvarchar (max)**, en su lugar.<br /><br /> Con la actualización\<tipo numérico > y [updateObject (int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) métodos se producirá un error en **texto** y **ntext** las columnas de servidor. Sin embargo, utilizando la [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) método con un tipo de conversión de caracteres especificado se admite en **texto** y **ntext** las columnas de servidor.|  
  
## <a name="binary-string-types"></a>Tipos de cadenas binarias  
 Los tipos de datos de cadenas binarias JDBC son **binario**, **VARBINARY**, y **LONGVARBINARY**.  
  
|Tipo|Description|  
|----------|-----------------|  
|Longitud fija|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **binario** tipo se asigna directamente a JDBC **binario** tipo. Es un tipo de longitud fija con relleno que proporciona el servidor en el caso de que la columna tenga habilitado SET ANSI_PADDING. Cuando las columnas char del servidor no tienen relleno, éste lo agrega el controlador JDBC.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **timestamp** tipo es un JDBC **binario** tipo con la longitud fija de 8 bytes.|  
|Longitud variable|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **varbinary** tipo se asigna a JDBC **VARBINARY** tipo.<br /><br /> El **udt** escriba [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se asigna a JDBC como un **VARBINARY** tipo.|  
|Long|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **imagen** tipo se asigna a JDBC **LONGVARBINARY** tipo. Este tipo está en desuso a partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], por lo que debe usar un tipo de valor grande, **varbinary (max)** en su lugar.|  
  
## <a name="exact-numeric-types"></a>Tipos numéricos exactos  
 Los tipos numéricos exactos de JDBC se asignan directamente a los tipos de SQL Server correspondientes.  
  
|Tipo|Description|  
|----------|-----------------|  
|BIT|JDBC **bits** tipo representa un bit único que puede ser 0 ó 1. Se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bits** tipo.|  
|TINYINT|JDBC **TINYINT** tipo representa un solo byte. Se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **tinyint** tipo.|  
|SMALLINT|JDBC **SMALLINT** tipo representa un entero de 16 bits con signo. Se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **smallint** tipo.|  
|INTEGER|JDBC **entero** tipo representa un entero de 32 bits con signo. Se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **int** tipo.|  
|bigint|JDBC **BIGINT** tipo representa un entero de 64 bits con signo. Se asigna a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bigint** tipo.|  
|NUMERIC|JDBC **numérico** tipo representa un valor decimal de precisión fija que contiene los valores de precisión idéntica. El **numérico** tipo se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **numérico** tipo.|  
|DECIMAL|JDBC **DECIMAL** tipo representa un valor decimal de precisión fija que contiene valores de al menos la precisión especifican. El **DECIMAL** tipo se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **decimal** tipo.<br /><br /> JDBC **DECIMAL** tipo también se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **dinero** y **smallmoney** tipos, que son determinados tipos decimales de precisión fija que se almacenan en 8 y 4 bytes, respectivamente.|  
  
## <a name="approximate-numeric-types"></a>Tipos numéricos aproximados  
 Los tipos numéricos aproximados de JDBC son **REAL**, **doble**, y **FLOAT**.  
  
|Tipo|Description|  
|----------|-----------------|  
|REAL|JDBC **REAL** tipo tiene siete dígitos de precisión (precisión simple) y se asigna directamente a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **real** tipo.|  
|DOUBLE|JDBC **doble** tipo tiene 15 dígitos de precisión (precisión doble) y se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **float** tipo. JDBC **FLOAT** tipo es un sinónimo de **doble**. Dado que puede haber confusión entre **FLOAT** y **doble**, **doble** es preferible.|  
  
## <a name="datetime-types"></a>Tipos de fecha y hora  
 JDBC **TIMESTAMP** tipo se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime** y **smalldatetime** tipos. El **datetime** tipo se almacena en dos enteros de 4 bytes. El **smalldatetime** tipo contiene la misma información (fecha y hora), pero con menos precisión, en dos enteros pequeños de 2 bytes.  
  
> [!NOTE]  
>  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **timestamp** tipo es un tipo de cadena binaria de longitud fija. No se asigna a cualquiera de los tipos de tiempo JDBC: **fecha**, **tiempo**, o **marca de tiempo**.  
  
## <a name="custom-type-mapping"></a>Asignación de tipos personalizados  
 La característica de asignación de tipos personalizados de JDBC que emplean las interfaces de datos SQL para JDBC había avanzada tipos (UDT, Struct etc.). no se incluye en el controlador JDBC.  
  
## <a name="see-also"></a>Vea también  
 [Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
