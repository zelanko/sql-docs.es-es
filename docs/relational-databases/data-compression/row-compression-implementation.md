---
title: "Implementaci&#243;n de la compresi&#243;n de fila | Microsoft Docs"
ms.custom: ""
ms.date: "06/30/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-data-compression"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "compresión [SQL Server], fila"
  - "compresión de fila [motor de base de datos]"
ms.assetid: dcd97ac1-1c85-4142-9594-9182e62f6832
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Implementaci&#243;n de la compresi&#243;n de fila
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En este tema se resume cómo el [!INCLUDE[ssDE](../../includes/ssde-md.md)] implementa la compresión de fila. Este resumen proporciona la información básica para ayudarle a planear el espacio de almacenamiento que necesita para sus datos.  
  
 La habilitación de la compresión solo cambia el formato de almacenamiento físico de los datos asociados a un tipo de datos, pero no cambia la sintaxis ni la semántica. No es necesario realizar cambios en la aplicación cuando una o varias tablas están habilitadas para la compresión. El nuevo formato de almacenamiento de registros tiene los siguientes cambios principales:  
  
-   Reduce la sobrecarga de metadatos asociada al registro. Estos metadatos son información sobre las columnas, sus longitudes y desplazamientos. En algunos casos, la sobrecarga de los metadatos podría ser mayor que en el formato de almacenamiento anterior.  
  
-   Emplea el formato de almacenamiento de longitud variable para los tipos numéricos (por ejemplo, **integer**, **decimal** y **float**) y para los tipos que están basados en tipos numéricos (por ejemplo, **datetime** y **money**).  
  
-   Almacena las cadenas de caracteres fijas utilizando el formato de longitud variable sin almacenar los caracteres en blanco.  
  
> [!NOTE]  
>  Los valores NULL y 0 se optimizan para todos los tipos de datos y no utilizan ningún byte.  
  
## Cómo afecta la compresión de fila al almacenamiento  
 En la tabla siguiente se describe cómo afecta la compresión de fila a los tipos existentes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]. La tabla no incluye el ahorro que se puede obtener utilizando la compresión de página.  
  
|Tipo de datos|Afecta al almacenamiento|Descripción|  
|---------------|--------------------------|-----------------|  
|**tinyint**|No|1 byte es el almacenamiento mínimo necesario.|  
|**smallint**|Sí|Si el valor se ajusta a 1 byte, solo se usará 1 byte.|  
|**int**|Sí|Usa solo los bytes necesarios. Por ejemplo, si un valor se puede almacenar en 1 byte, el almacenamiento tomará solo 1 byte.|  
|**bigint**|Sí|Usa solo los bytes necesarios. Por ejemplo, si un valor se puede almacenar en 1 byte, el almacenamiento tomará solo 1 byte.|  
|**decimal**|Sí|Este almacenamiento es exactamente el mismo que el formato de almacenamiento vardecimal.|  
|**numeric**|Sí|Este almacenamiento es exactamente el mismo que el formato de almacenamiento vardecimal.|  
|**bit**|Sí|La sobrecarga de metadatos hace que ocupe 4 bits.|  
|**smallmoney**|Sí|Usa la representación de datos enteros utilizando un entero de 4 bytes. El valor de moneda se multiplica por 10.000 y el valor entero resultante se almacena quitando los dígitos situados después del separador decimal. Este tipo tiene una optimización de almacenamiento similar a la de los tipos enteros.|  
|**money**|Sí|Usa la representación de datos enteros utilizando un entero de 8 bytes. El valor de moneda se multiplica por 10.000 y el valor entero resultante se almacena quitando los dígitos situados después del separador decimal. Este tipo tiene un intervalo mayor que **smallmoney**. Este tipo tiene una optimización de almacenamiento similar a la de los tipos enteros.|  
|**float**|Sí|Los bytes menos significativos con ceros no se almacenan. La compresión**float** se aplica principalmente a valores no decimales de mantisa.|  
|**real**|Sí|Los bytes menos significativos con ceros no se almacenan. La compresión**real** se aplica principalmente a valores no decimales de mantisa.|  
|**smalldatetime**|No|Usa la representación de datos enteros con dos enteros de 2 bytes. La fecha toma 2 bytes. Es el número de días desde el 1/1/1901. Necesita 2 bytes que se inician en 1902. Por lo tanto, no se produce ningún ahorro después de ese punto.<br /><br /> El tiempo es el número de minutos desde medianoche. Los valores de tiempo situados ligeramente después de 4 a.m. empiezan a utilizar el segundo byte.<br /><br /> Si se usa solo **smalldatetime** para representar una fecha (un caso común), el tiempo será 0.0. La compresión ahorra 2 bytes almacenando el tiempo en el formato de byte más significativo para la compresión de fila.|  
|**datetime**|Sí|Usa la representación de datos enteros utilizando dos enteros de 4 bytes. El valor entero representa el número de días con la fecha base 1/1/1900. Los 2 primeros bytes pueden representar hasta el año 2079. La compresión siempre puede guardar aquí 2 bytes hasta ese punto. Cada valor entero representa 3,33 milisegundos. La compresión agota los primeros 2 bytes en los primeros cinco minutos y necesita el cuarto byte después de las 4 p.m. Por consiguiente, la compresión puede guardar solo 1 byte después de las 4 p.m. Cuando **datetime** se comprime como cualquier otro entero, la compresión ahorra 2 bytes en la fecha.|  
|**date**|No|Usa la representación de datos enteros con 3 bytes. Representa la fecha desde 1/1/0001. Para las fechas contemporáneas, la compresión de fila utiliza los 3 bytes. No se obtiene ningún tipo de ahorro.|  
|**time**|No|Usa la representación de datos enteros utilizando de 3 a 6 bytes. Existen varias precisiones que se inician con 0 a 9 y que pueden tomar de 3 a 6 bytes. El espacio comprimido se utiliza como sigue:<br /><br /> **Precisión = 0. Bytes = 3**. Cada valor entero representa un segundo. La compresión puede representar el tiempo hasta las 6 p.m. utilizando 2 bytes, obteniendo un ahorro potencial de 1 byte.<br /><br /> **Precisión = 1. Bytes = 3**. Cada valor entero representa 1/10 segundos. La compresión utiliza el tercer byte antes de las 2 a.m. Se obtiene un pequeño ahorro.<br /><br /> **Precisión = 2. Bytes = 3**. Similar al caso anterior, es improbable que se obtenga algún tipo de ahorro.<br /><br /> **Precisión = 3. Bytes = 4**. Dado que los 3 primeros bytes se usan antes de las 5 a.m., obtiene pequeños ahorros.<br /><br /> **Precisión = 4. Bytes = 4**. Los primeros 3 bytes se toman en los primeros 27 segundos. No se obtiene ningún tipo de ahorro.<br /><br /> **Precisión = 5, Bytes = 5**. El quinto byte se utilizará después de las 12 del mediodía.<br /><br /> **Precisión = 6 y 7, Bytes = 5**. No logra ningún ahorro.<br /><br /> **Precisión = 8, Bytes = 6**. El sexto byte se utilizará después de las 3 a.m.<br /><br /> <br /><br /> Tenga en cuenta que no hay ningún cambio en el almacenamiento para la compresión de fila. En conjunto, no se puede esperar obtener muchos ahorros de la compresión del tipo de datos **time** .|  
|**datetime2**|Sí|Usa la representación de datos enteros utilizando de 6 a 9 bytes. Los primeros 4 bytes representan la fecha. Los bytes tomados por la fecha dependerán de la precisión del tiempo que se especifique.<br /><br /> El valor entero representa el número de días desde el 1/1/0001, con un límite superior del 12/31/9999. Para representar una fecha del año 2005, la compresión toma 3 bytes.<br /><br /> No hay ningún ahorro en el tiempo porque permite usar de 2 a 4 bytes para varias precisiones de tiempo. Por consiguiente, para una precisión de tiempo de un segundo, la compresión utiliza 2 bytes para el tiempo, usando el segundo byte cuando han transcurrido 255 segundos.|  
|**datetimeoffset**|Sí|Se parece a **datetime2**, salvo que hay 2 bytes de zona horaria del formato (HH:MM).<br /><br /> Al igual que **datetime2**, la compresión puede ahorrar 2 bytes.<br /><br /> Para valores de zona horaria, el valor MM podría ser 0 en la mayoría de los casos. Por consiguiente, la compresión solo podrá ahorrar 1 byte.<br /><br /> No hay ningún cambio en el almacenamiento para la compresión de fila.|  
|**char**|Sí|Se quitan los caracteres de relleno final. Observe que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] inserta el mismo carácter de relleno, independientemente de la intercalación que se utilice.|  
|**varchar**|No|Ningún efecto.|  
|**texto**|No|Ningún efecto.|  
|**nchar**|Sí|Se quitan los caracteres de relleno final. Observe que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] inserta el mismo carácter de relleno, independientemente de la intercalación que se utilice.|  
|**nvarchar**|No|Ningún efecto.|  
|**ntext**|No|Ningún efecto.|  
|**binario**|Sí|Se quitan los ceros finales.|  
|**varbinary**|No|Ningún efecto.|  
|**imagen**|No|Ningún efecto.|  
|**cursor**|No|Ningún efecto.|  
|**timestamp** / **rowversion**|Sí|Usa la representación de datos enteros con 8 bytes. Hay un contador de marca de tiempo que se mantiene para cada base de datos y su valor se inicia en 0. Se puede comprimir como cualquier otro valor entero.|  
|**sql_variant**|No|Ningún efecto.|  
|**uniqueidentifier**|No|Ningún efecto.|  
|**table**|No|Ningún efecto.|  
|**xml**|No|Ningún efecto.|  
|Tipos definidos por el usuario|No|Se representa internamente como **varbinary**.|  
|FILESTREAM|No|Se representa internamente como **varbinary**.|  
  
## Vea también  
 [Comprimir datos](../../relational-databases/data-compression/data-compression.md)   
 [Implementación de la compresión de página](../../relational-databases/data-compression/page-compression-implementation.md)  
  
  