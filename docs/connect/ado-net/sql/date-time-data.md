---
title: Datos de fecha y hora
description: Describe cómo usar los nuevos tipos de datos de hora y fecha incorporados en SQL Server 2008.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 75d8b98726a758e0533053dbdf8d2e03b3bfdf0d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896989"
---
# <a name="date-and-time-data"></a>Datos de fecha y hora

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 2008 introduce nuevos tipos de datos para administrar la información de fecha y hora. Los nuevos tipos de datos incluyen tipos independientes para la fecha y la hora y tipos de datos expandidos con mayor control sobre el intervalo, la precisión y la zona horaria. El proveedor de datos SqlClient de Microsoft para SQL Server (<xref:Microsoft.Data.SqlClient>) proporciona compatibilidad total con todas las características nuevas del motor de base de datos de SQL Server 2008. Debe instalar .NET Framework 3.5 SP1 (o posterior) o .NET Core 1.0 (o posterior) para usar estas nuevas características con SqlClient.  
  
Las versiones de SQL Server anteriores a SQL Server 2008 solo tenían dos tipos de datos para trabajar con valores de fecha y hora: `datetime` y `smalldatetime`. Ambos tipos de datos contienen el valor de fecha y el valor de hora, lo que dificulta trabajar solo con valores de fecha o de hora. Además, estos tipos de datos solo admiten las fechas posteriores a la introducción del calendario gregoriano en Inglaterra en 1753. Otra limitación es que estos tipos de datos más antiguos no reconocen la zona horaria, por lo que resulta difícil trabajar con datos que proceden de varias zonas horarias.  
  
La documentación completa de los tipos de datos de SQL Server está disponible en Libros en pantalla de SQL Server. Consulte [Uso de datos de fecha y hora](https://go.microsoft.com/fwlink/?LinkID=98361) para consultar temas de nivel de entrada sobre datos de fecha y hora.
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>Tipos de datos de fecha y hora incorporados en SQL Server 2008  
 En la tabla siguiente se describen los nuevos tipos de datos de fecha y hora.  
  
|Tipos de datos de SQL Server|Descripción|  
|--------------------------|-----------------|  
|`date`|El tipo de datos `date` tiene un intervalo del 1 de enero de 01 al 31 de diciembre de 9999, con una precisión de 1 día. El valor predeterminado es 1 de enero de 1900. El tamaño de almacenamiento es de 3 bytes.|  
|`time`|El tipo de datos `time` solo almacena valores de hora basados en un reloj de 24 horas. El tipo de datos `time` tiene un intervalo de 00:00:00,0000000 a 23:59:59,9999999 con una precisión de 100 nanosegundos. El valor predeterminado es 00:00:00,0000000 (medianoche). El tipo de datos `time` admite la precisión decimal de segundos definida por el usuario y su tamaño de almacenamiento varía entre 3 y 6 bytes en función de la precisión especificada.|  
|`datetime2`|El tipo de datos `datetime2` combina el intervalo y la precisión de los tipos de datos `date` y `time` en un solo tipo de datos.<br /><br /> Los valores predeterminados y los formatos de literales de cadena son los mismos que los definidos en los tipos de datos `date` y `time`.|  
|`datetimeoffset`|El tipo de datos `datetimeoffset` incluye todas las características de `datetime2` con un desfase de zona horaria adicional. El desfase de zona horaria se representa como [+&#124;-] HH:MM. HH es una cifra de dos dígitos que va de 00 a 14 y que representa el número de horas del desfase de zona horaria. MM es una cifra de dos dígitos que va de 00 a 59 y que representa el número minutos adicionales del desfase de zona horaria. Se admiten formatos de hora de hasta 100 nanosegundos. El signo + o- obligatorio indica si el ajuste de zona horaria se suma o se resta de la hora UTC (hora universal coordinada u hora del meridiano de Greenwich) para obtener la hora local.|  
  
> [!NOTE]
>  Para obtener más información sobre el empleo de la palabra clave `Type System Version`, vea <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
## <a name="date-format-and-date-order"></a>Formato de fecha y orden de fecha  
La forma en que SQL Server analiza los valores de fecha y hora no solo depende de la versión del sistema de tipos y de la versión del servidor, sino también de la configuración de formato y idioma predeterminados del servidor. Una cadena de fecha que funcione para los formatos de fecha de un idioma podría ser irreconocible si la consulta se ejecuta por una conexión que utiliza una configuración de formato de fecha y idioma diferente.  
  
La instrucción SET LANGUAGE de Transact-SQL establece implícitamente DATEFORMAT, que determina el orden de las partes de la fecha. Puede usar la instrucción SET DATEFORMAT de Transact-SQL en una conexión para eliminar la ambigüedad de los valores de fecha ordenando las partes de fecha según MDA, DMA, AMD, ADM, MAD o DAM.  
  
Si no especifica ningún valor DATEFORMAT para la conexión, SQL Server utiliza el idioma predeterminado asociado a la conexión. Por ejemplo, una cadena de fecha de "01/02/03" se interpretaría como MDA (2 de enero de 2003) en un servidor con una configuración de idioma de inglés de Estados Unidos y como DMA (1 de febrero de 2003) en un servidor con una configuración de idioma de inglés británico. El año se determina mediante el uso de la regla del año límite de SQL Server, que define la fecha límite para asignar el valor del siglo. Para obtener más información, vea[two digit year cutoff (opción)](https://go.microsoft.com/fwlink/?LinkId=120473) en los Libros en pantalla de SQL Server.  
  
> [!NOTE]
>  No se admite el formato de fecha ADM al convertir de un formato de cadena a `date`, `time`, `datetime2` o `datetimeoffset`.  
  
Para obtener más información sobre cómo SQL Server interpreta los datos de fecha y hora, vea [Usar datos de fecha y hora](https://go.microsoft.com/fwlink/?LinkID=98361) en los Libros en pantalla de SQL Server 2008.  
  
## <a name="datetime-data-types-and-parameters"></a>Tipos de datos y parámetros de fecha y hora  
Se han agregado los siguientes valores de enumeración a <xref:System.Data.SqlDbType> para admitir los nuevos tipos de datos de fecha y hora.  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

Puede especificar el tipo de datos de <xref:Microsoft.Data.SqlClient.SqlParameter> mediante una de las enumeraciones <xref:System.Data.SqlDbType> anteriores. 

> [!NOTE]
> No puede establecer la propiedad `DbType` de un `SqlParameter` en `SqlDbType.Date`.

También puede especificar el tipo de <xref:Microsoft.Data.SqlClient.SqlParameter> de forma genérica si establece la propiedad <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> de un objeto `SqlParameter` en un determinado valor de enumeración <xref:System.Data.DbType>. Se han agregado los siguientes valores de enumeración a <xref:System.Data.DbType> para admitir los tipos de datos `datetime2` y `datetimeoffset`:  
  
- DbType.DateTime2  
  
- DbType.DateTimeOffset  
  
Estas nuevas enumeraciones complementan las enumeraciones `Date`, `Time` y `DateTime`.  
  
El tipo de proveedor de datos SqlClient de Microsoft de un objeto de parámetro se deduce del tipo .NET del valor del objeto de parámetro, o del `DbType` del objeto de parámetro. No se han introducido nuevos tipos de datos de <xref:System.Data.SqlTypes> para admitir los nuevos tipos de datos de fecha y hora. En la tabla siguiente se describen las asignaciones entre los tipos de datos de fecha y hora de SQL Server 2008 y los tipos de datos de CLR.  
  
|Tipos de datos de SQL Server|Tipo de .NET|System.Data.SqlDbType|System.Data.DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|date|System.DateTime|Date|Date|  
|time|System.TimeSpan|Time|Time|  
|datetime2|System.DateTime|DateTime2|DateTime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|datetime|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### <a name="sqlparameter-properties"></a>Propiedades de SqlParameter  
 En la tabla siguiente se describen las propiedades `SqlParameter` que son pertinentes para los tipos de datos de fecha y hora.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.IsNullable%2A>|Obtiene o establece si un valor admite valores NULL. Cuando se envía un valor de parámetro nulo al servidor, se debe especificar <xref:System.DBNull>, en lugar de `null` (`Nothing` en Visual Basic). Para obtener más información sobre valores nulos de base de datos, consulte [Controlar valores NULL](handle-null-values.md).|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Precision%2A>|Obtiene o establece el número máximo de dígitos usado para representar el valor. Este valor se omite para los tipos de datos de fecha y hora.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Scale%2A>|Obtiene o establece el número de posiciones decimales determinado para la parte de hora del valor de `Time`, `DateTime2` y `DateTimeOffset`. El valor predeterminado es 0, lo que significa que la escala real se deduce del valor y se envía al servidor.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|Se ignora para los tipos de datos de fecha y hora.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|Obtiene o establece el valor de parámetro.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|Obtiene o establece el valor de parámetro.|  
  
> [!NOTE]
>  Los valores de hora que son menores que cero o mayores o iguales que 24 horas producirán una excepción <xref:System.ArgumentException>.  
  
### <a name="creating-parameters"></a>Creación de parámetros  
Puede crear un objeto <xref:Microsoft.Data.SqlClient.SqlParameter> mediante su constructor o agregándolo a una colección <xref:Microsoft.Data.SqlClient.SqlCommand>.<xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> llamando al método `Add` del <xref:Microsoft.Data.SqlClient.SqlParameterCollection>. El método `Add` tomará como entrada los argumentos del constructor o un objeto de parámetro existente.  
  
En las secciones siguientes de este tema se proporcionan ejemplos de cómo especificar parámetros de fecha y hora.
  
### <a name="date-example"></a>Ejemplo de fecha  
El fragmento de código siguiente muestra cómo se especifica un parámetro `date`.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
### <a name="time-example"></a>Ejemplo de hora  
El fragmento de código siguiente muestra cómo se especifica un parámetro `time`.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Ejemplo de Datetime2  
En el fragmento de código siguiente se muestra cómo especificar un parámetro `datetime2` con las partes de fecha y hora.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>Ejemplo de DateTimeOffSet  
En el fragmento de código siguiente se muestra cómo especificar un parámetro `DateTimeOffSet` con una fecha, una hora y un ajuste de zona horaria de 0.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>AddWithValue  
También puede proporcionar parámetros mediante el método `AddWithValue` de un <xref:Microsoft.Data.SqlClient.SqlCommand>, como se muestra en el fragmento de código siguiente. Sin embargo, el método `AddWithValue` no permite especificar el valor <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> o <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> para el parámetro.  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
El parámetro `@date` podría asignarse a un tipo de datos `date`, `datetime` o `datetime2` en el servidor. Al trabajar con los nuevos tipos de datos de `datetime`, debe establecer explícitamente la propiedad <xref:System.Data.SqlDbType> del parámetro en el tipo de datos de la instancia. El uso de <xref:System.Data.SqlDbType.Variant> o el suministro implícito de valores de parámetros puede causar problemas de compatibilidad con versiones anteriores de los tipos de datos `datetime` y `smalldatetime`.  
  
En la tabla siguiente se muestra qué valores `SqlDbTypes` se deducen a partir de los tipos de CLR:  
  
|Tipo CLR|SqlDbType deducido|  
|--------------|------------------------|  
|DateTime|SqlDbType.DateTime|  
|TimeSpan|SqlDbType.Time|  
|DateTimeOffset|SqlDbType.DateTimeOffset|  
  
## <a name="retrieving-date-and-time-data"></a>Recuperación de datos de fecha y hora  
En la tabla siguiente se describen los métodos que se usan para recuperar valores de fecha y hora de SQL Server 2008.  
  
|Método SqlClient|Descripción|  
|----------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|Recupera el valor de columna especificado como una estructura <xref:System.DateTime>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|Recupera el valor de columna especificado como una estructura <xref:System.DateTimeOffset>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|Devuelve el tipo específico del proveedor subyacente para el campo. Devuelve los mismos tipos que `GetFieldType` para los nuevos tipos de fecha y hora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|Recupera el valor de la columna especificada. Devuelve los mismos tipos que `GetValue` para los nuevos tipos de fecha y hora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|Recupera los valores de la matriz especificada.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|Recupera el valor de la columna como <xref:System.Data.SqlTypes.SqlString>. Se produce <xref:System.InvalidCastException> si los datos no se pueden expresar como `SqlString`.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|Recupera los datos de la columna como su `SqlDbType` predeterminada. Devuelve los mismos tipos que `GetValue` para los nuevos tipos de fecha y hora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|Recupera los valores de la matriz especificada.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A>|Recupera el valor de columna como una cadena si Type System Version se ha establecido en SQL Server 2005. Se produce <xref:System.InvalidCastException> si los datos no se pueden expresar como una cadena.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|Recupera el valor de columna especificado como una estructura <xref:System.TimeSpan>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>|Recupera el valor de columna especificado como su tipo CLR subyacente.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>|Recupera los valores de columna de una matriz.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|Devuelve un valor <xref:System.Data.DataTable> que describe los metadatos del conjunto de resultados.|  
  
> [!NOTE]
>  Los nuevos `SqlDbTypes` de fecha y hora no se admiten para el código que se ejecuta en proceso en SQL Server. Se producirá una excepción si se pasa uno de estos tipos al servidor.  
  
## <a name="specifying-date-and-time-values-as-literals"></a>Especificación de valores de fecha y hora como literales  
Puede especificar tipos de datos de fecha y hora mediante una variedad de diferentes formatos de cadena literales, que SQL Server evalúa luego en el entorno de ejecución, convirtiéndolos en estructuras de fecha y hora internas. SQL Server reconoce los datos de fecha y hora que se incluyen entre comillas simples ('). Los ejemplos siguientes demuestran algunos formatos:  
  
- Formatos de fecha alfabéticos, como `'October 15, 2006'`.  
  
- Formatos de fecha numéricos, como `'10/15/2006'`.  
  
- Formatos de cadena no separados, como `'20061015'`, que se interpretarán como 15 de octubre de 2006 si usa el formato de fecha estándar ISO.  
  
> [!NOTE]
>  Puede encontrar documentación completa de todos los formatos de cadena literales y otras características de los tipos de datos de fecha y hora en los Libros en pantalla de SQL Server.  
  
Los valores de hora que son menores que cero o mayores o iguales que 24 horas producirán una excepción <xref:System.ArgumentException>.  
  
## <a name="resources-in-sql-server-2008-books-online"></a>Recursos en los Libros en pantalla de SQL Server 2008  
Para obtener más información sobre cómo trabajar con valores de fecha y hora en SQL Server 2008, vea los siguientes recursos en los Libros en pantalla de SQL Server 2008.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Tipos de datos y funciones de fecha y hora (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98360)|Proporciona información general sobre todos los tipos de datos y funciones de fecha y hora de Transact-SQL.|  
|[Uso de datos de fecha y hora](https://go.microsoft.com/fwlink/?LinkId=98361)|Proporciona información sobre las funciones y los tipos de datos de fecha y hora, además de ejemplos de uso.|  
|[Tipos de datos (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98362)|Describe los tipos de datos de sistema que incluye SQL Server 2008.|  
  
## <a name="next-steps"></a>Pasos siguientes
- [Tipos de datos de SQL Server en ADO.NET](sql-server-data-types.md)
