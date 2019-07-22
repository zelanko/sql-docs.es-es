---
title: Tipos de datos de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- data types [Integration Services], listed
- data types [Integration Services]
- column data types [Integration Services]
- SSIS, data types
- Integration Services, data types
- SQL Server Integration Services, data types
ms.assetid: 896fc3e8-3aa6-4396-ba82-5d7741cffa56
author: janinezhang
ms.author: janinez
ms.openlocfilehash: eab2401dc3cb85dfeaedc22b406f1da73c112127
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941469"
---
# <a name="integration-services-data-types"></a>Tipos de datos de Integration Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Cuando los datos entran en un flujo de datos en un paquete, el origen que extrae los datos convierte los datos en un tipo de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . A los datos numéricos se les asigna un tipo de dato numérico, a los datos de cadena se les asigna un tipo de datos de caracteres y se asignan fechas a un tipo de datos de fecha. A otros datos, tales como GUID y bloques de objetos binarios grandes (BLOB), también se les asignan los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] correspondientes. Si los datos son de un tipo que no se puede convertir en un tipo de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se produce un error.  
  
 Algunos componentes de flujo de datos convierten tipos de datos entre los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los tipos de datos administrados de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para obtener más información sobre las asignaciones entre los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los tipos de datos administrados, vea [Trabajar con tipos de datos del flujo de datos](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
 La siguiente tabla enumera los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Algunos de los tipos de datos de la tabla tienen la información de precisión y escala que les corresponde. Para obtener más información sobre la precisión y la escala, consulte [Precisión, escala y longitud &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|DT_BOOL|Valor booleano.|  
|DT_BYTES|Valor de datos binarios. La longitud es variable y la longitud máxima es de 8000 bytes.|  
|DT_CY|Un valor de moneda. Este tipo de datos es un entero con signo de 8 bytes con una escala de 4 y una precisión máxima de 19 dígitos.|  
|DT_DATE|Una estructura de fecha formada por año, mes, día, hora, minuto, segundo y fracciones de segundo.  Las fracciones de segundo tienen una escala fija de 7 dígitos.<br /><br /> El tipo de datos DT_DATE se implementa utilizando un número de punto flotante de 8 bytes. Los días se representan mediante incrementos de números enteros, comenzando por el 30 de diciembre de 1899 y la medianoche como hora cero. Los valores de hora se expresan como el valor absoluto de la parte fraccionaria del número. Sin embargo, un valor de punto flotante no puede representar todos los valores reales; por lo tanto, existen límites en el intervalo de fechas que se puede presentar en DT_DATE.<br /><br /> Por otra parte, DT_DBTIMESTAMP se representa mediante una estructura que posee internamente campos individuales para año, mes, día, horas, minutos, segundos y milisegundos. Este tipo de datos tiene límites más amplios que los intervalos de fechas que puede presentar.|  
|DT_DBDATE|Una estructura de fecha compuesta por año, mes y día.|  
|DT_DBTIME|Una estructura de hora compuesta por horas, minutos y segundos.|  
|DT_DBTIME2|Una estructura de hora formada por hora, minuto, segundo y fracciones de segundo. Las fracciones de segundo tienen una escala máxima de 7 dígitos.|  
|DT_DBTIMESTAMP|Una estructura de marca de tiempo formada por año, mes, día, hora, minuto, segundo y fracciones de segundo. Las fracciones de segundo tienen una escala máxima de 3 dígitos.|  
|DT_DBTIMESTAMP2|Una estructura de marca de tiempo formada por año, mes, día, hora, minuto, segundo y fracciones de segundo. Las fracciones de segundo tienen una escala máxima de 7 dígitos.|  
|DT_DBTIMESTAMPOFFSET|Una estructura de marca de tiempo formada por año, mes, día, hora, minuto, segundo y fracciones de segundo. Las fracciones de segundo tienen una escala máxima de 7 dígitos.<br /><br /> A diferencia de los tipos de datos DT_DBTIMESTAMP y DT_DBTIMESTAMP2, el tipo de datos DT_DBTIMESTAMPOFFSET tiene un ajuste de zona horaria. Este ajuste especifica el desplazamiento de la hora en número de horas y minutos respecto a la hora universal coordinada (UTC). El sistema utiliza el ajuste de zona horaria para obtener la hora local.<br /><br /> El ajuste de zona horaria debe incluir un signo, más o menos, para indicar si el ajuste se agrega o se resta de la UTC. El número válido de ajuste de horas está entre -14 y +14. El signo para el ajuste de minutos depende del signo del ajuste de horas:<br /><br /> Si el signo del ajuste de horas es negativo, el ajuste de minutos debe ser negativo o cero.<br /><br /> Si el signo para el ajuste de horas es positivo, el ajuste de minutos debe ser positivo o cero.<br /><br /> Si el signo del ajuste de horas es cero, el ajuste de minutos puede ser cualquier valor desde 0,59 negativo a 0,59 positivo.|  
|DT_DECIMAL|Un valor numérico exacto con una precisión fija y una escala fija. Este tipo de dato es un entero sin signo de 12 bytes con un signo aparte, una escala de 0 a 28 y una precisión máxima de 29.|  
|DT_FILETIME|Un valor de 64 bits que representa la cantidad de intervalos de 100 nanosegundos desde el 1 de enero de 1601. Las fracciones de segundo tienen una escala máxima de 3 dígitos.|  
|DT_GUID|Identificador único global (GUID).|  
|DT_I1|Un entero con signo de un byte.|  
|DT_I2|Un entero con signo de dos bytes.|  
|DT_I4|Un entero con signo de cuatro bytes.|  
|DT_I8|Un entero con signo de ocho bytes.|  
|DT_NUMERIC|Un valor numérico exacto con una precisión y escala fijas. Este tipo de dato es un entero sin signo de 16 bytes con un signo aparte, una escala de 0 a 38 y una precisión máxima de 38.|  
|DT_R4|Un valor de punto flotante y precisión simple.|  
|DT_R8|Un valor de punto flotante y precisión doble.|  
|DT_STR|Una cadena de caracteres [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS terminada en NULL, con una longitud máxima de 8000 caracteres. (Si un valor de columna contiene otros terminadores NULL, la cadena se truncará cuando se encuentre el primer NULL.)|  
|DT_UI1|Un entero sin signo de un byte.|  
|DT_UI2|Un entero sin signo de dos bytes.|  
|DT_UI4|Un entero sin signo de cuatro bytes.|  
|DT_UI8|Un entero sin signo de ocho bytes.|  
|DT_WSTR|Una cadena de caracteres Unicode terminada en NULL, con una longitud máxima de 4000 caracteres. (Si un valor de columna contiene otros terminadores NULL, la cadena se truncará cuando se encuentre el primer NULL.)|  
|DT_IMAGE|Valor binario con un tamaño máximo de 2^31-1 (2 147 483 647) bytes. .|  
|DT_NTEXT|Cadena de caracteres Unicode con una longitud máxima de 2^30–1 (1 073 741 823) caracteres.|  
|DT_TEXT|Una cadena de caracteres [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS con una longitud máxima de 2^31-1 (2 147 483 647) caracteres.|  
  
## <a name="conversion-of-data-types"></a>Conversión de tipos de datos  
 Si los datos en una columna no requieren el ancho total asignado por el tipo de datos de origen, puede ser recomendable cambiar el tipo de datos de la columna. Si se hace que cada fila de datos sea lo más estrecha posible, esto ayuda a optimizar el rendimiento cuando se transfieren datos porque, cuanto más estrecha sea una fila, más rápido los datos se desplazarán del origen al destino.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye un conjunto completo de tipos de datos numéricos, de manera que puede hacer coincidir estrechamente el tipo de datos con el tamaño de los datos. Por ejemplo, si los valores en una columna con un tipo de datos DT_UI8 siembre son enteros entre 0 y 3000, puede cambiar el tipo de datos a DT_UI2. De forma similar, si una columna con el tipo de datos DT_CY puede reunir los requisitos de datos de paquete utilizando un tipo de datos enteros, puede cambiar el tipo de datos a DT_I4.  
  
 Puede cambiar el tipo de datos de una columna de las siguientes maneras:  
  
-   Utilice una expresión para convertir los tipos de datos implícitamente. Para obtener más información, vea [Tipos de datos de Integration Services en las expresiones](../../integration-services/expressions/integration-services-data-types-in-expressions.md), [Tipos de datos de Integration Services en las expresiones](../../integration-services/expressions/integration-services-data-types-in-expressions.md) y [Expresiones de Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
-   Utilice el operador de conversión para convertir los tipos de datos. Para más información, vea [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
-   Utilice la transformación de conversión de datos para convertir el tipo de datos de una columna de un tipo de datos en un tipo de datos diferente. Para más información, consulte [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
-   Utilice la transformación Columna derivada para crear una copia de una columna que tiene un tipo de datos distinto al de la columna original. Para más información, consulte [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
### <a name="converting-between-strings-and-datetime-data-types"></a>Conversión entre los tipos de datos de cadena y de fecha u hora  
 En la tabla siguiente se enumeran los resultados de la conversión entre los tipos de datos de fecha u hora, y las cadenas:  
  
-   Al utilizar el operador de conversión o la transformación Conversión de datos, el tipo de datos de fecha u hora se convertirá al formato de cadena correspondiente. Por ejemplo, el tipo de datos DT_DBTIME se convertirá en una cadena que tiene el formato "hh:mm:ss".  
  
-   Si desea convertir una cadena en un tipo de datos de fecha u hora, la cadena debe utilizar el formato de cadena que se corresponda con el tipo de datos de fecha u hora apropiados. Por ejemplo, para convertir correctamente algunas cadenas de fecha en el tipo de datos DT_DBDATE, deben estar en el formato "aaaa-mm-dd".  
  
    |Tipo de datos|Formato de cadena|  
    |---------------|-------------------|  
    |DT_DBDATE|aaaa-mm-dd|  
    |DT_FILETIME|yyyy-mm-dd hh:mm:ss:fff|  
    |DT_DBTIME|hh:mm:ss|  
    |DT_DBTIME2|hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMP|yyyy-mm-dd hh:mm:ss[.fff]|  
    |DT_DBTIMESTAMP2|yyyy-mm-dd hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMPOFFSET|yyyy-mm-dd hh:mm:ss[.fffffff] [{+&#124;-} hh:mm]|  
  
 En el formato para DT_FILETIME y DT_DBTIMESTAMP fff es un valor entre 0 y 999 que representa las fracciones de segundo.  
  
 En el formato de fecha para DT_DBTIMESTAMP2, DT_DBTIME2 y DT_DBTIMESTAMPOFFSET, fffffff es un valor entre 0 y 9999999 que representa fracciones de segundo.  
  
 El formato de fecha para DT_DBTIMESTAMPOFFSET también incluye un elemento de zona horaria. Hay un espacio entre el elemento de tiempo y el elemento de zona horaria.  
  
### <a name="converting-datetime-data-types"></a>Convertir tipos de datos de fecha y hora  
 Puede cambiar el tipo de datos en una columna con los datos de fecha/hora para extraer la parte de la fecha o la hora de los datos. En las tablas siguientes se muestran listas de los resultados de cambiar de un tipo de datos de fecha y hora a otro.  
  
#### <a name="converting-from-dtfiletime"></a>Convertir a partir de DT_FILETIME  
  
|Convertir DT_FILETIME a|Resultado|  
|-----------------------------|------------|  
|DT_FILETIME|Sin cambios.|  
|DT_DATE|Convierte el tipo de datos.|  
|DT_DBDATE|Quita el valor de hora.|  
|DT_DBTIME|Quita el valor de fecha.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos fraccionarios que el tipo de datos DT_DBTIME puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Quita el valor de fecha representado por el tipo de datos DT_FILETIME.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos de DT_DBTIME2 puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Convierte el tipo de datos.|  
|DT_DBTIMESTAMP2|Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMP2 puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Establece en cero el campo de zona horaria del tipo de datos DT_DBTIMESTAMPOFFSET.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMPOFFSET puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdate"></a>Convertir a partir de DT_DATE  
  
|Convertir DT_DATE a|Resultado|  
|-------------------------|------------|  
|DT_FILETIME|Convierte el tipo de datos.|  
|DT_DATE|Sin cambios.|  
|DT_DBDATE|Quita el valor de hora representado por el tipo de datos DT_DATA.|  
|DT_DBTIME|Quita el valor de fecha representado por el tipo de datos DT_DATA.|  
|DT_DBTIME2|Quita el valor de fecha representado por el tipo de datos DT_DATA.|  
|DT_DBTIMESTAMP|Convierte el tipo de datos.|  
|DT_DBTIMESTAMP2|Convierte el tipo de datos.|  
|DT_DBTIMESTAMPOFFSET|Establece en cero el campo de zona horaria del tipo de datos DT_DBTIMESTAMPOFFSET.|  
  
#### <a name="converting-from-dtdbdate"></a>Convertir a partir de DT_DBDATE  
  
|Convertir DT_DBDATE a|Resultado|  
|---------------------------|------------|  
|DT_FILETIME|Establece en cero los campos de hora del tipo de datos DT_FILETIME.|  
|DT_DATE|Establece en cero los campos de hora del tipo de datos DT_DATE.|  
|DT_DBDATE|Sin cambios.|  
|DT_DBTIME|Establece en cero los campos de hora del tipo de datos DT_DBTIME.|  
|DT_DBTIME2|Establece en cero los campos de hora del tipo de datos DT_DBTIME2.|  
|DT_DBTIMESTAMP|Establece en cero los campos de hora del tipo de datos DT_DBTIMESTAMP.|  
|DT_DBTIMESTAMP2|Establece en cero los campos de hora del tipo de datos DT_DBTIMESTAMP.|  
|DT_DBTIMESTAMPOFFSET|Establece en cero los campos de hora y el campo de zona horaria del tipo de datos DT_DBTIMESTAMPOFFSET.|  
  
#### <a name="converting-from-dtdbtime"></a>Convertir a partir de DT_DBTIME  
  
|Convertir DT_DBTIME a|Resultado|  
|---------------------------|------------|  
|DT_FILETIME|Establece el campo de fecha del tipo de datos DT_FILETIME en la fecha actual.|  
|DT_DATE|Establece el campo de fecha del tipo de datos DT_DATE en la fecha actual.|  
|DT_DBDATE|Establece el campo de fecha del tipo de datos DT_DBDATE en la fecha actual.|  
|DT_DBTIME|Sin cambios.|  
|DT_DBTIME2|Convierte el tipo de datos.|  
|DT_DBTIMESTAMP|Establece el campo de fecha del tipo de datos DT_DBTIMESTAMP en la fecha actual.|  
|DT_DBTIMESTAMP2|Establece el campo de fecha del tipo de datos DT_DBTIMESTAMP2 en la fecha actual.|  
|DT_DBTIMESTAMPOFFSET|Establece el campo de fecha y el campo de zona horaria del tipo de datos DT_DBTIMESTAMPOFFSET en la fecha actual y en cero respectivamente.|  
  
#### <a name="converting-from-dtdbtime2"></a>Convertir a partir de DT_DBTIME2  
  
|Convertir DT_DBTIME2 a|Resultado|  
|----------------------------|------------|  
|DT_FILETIME|Establece el campo de fecha del tipo de datos DT_FILETIME en la fecha actual.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_FILETIME puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DATE|Establece el campo de fecha del tipo de datos DT_DATE en la fecha actual.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DATE puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Establece el campo de fecha del tipo de datos DT_DBDATE en la fecha actual.|  
|DT_DBTIME|Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIME puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos de destino DT_DBTIME2 puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Establece el campo de fecha del tipo de datos DT_DBTIMESTAMP en la fecha actual.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMP puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Establece el campo de fecha del tipo de datos DT_DBTIMESTAMP2 en la fecha actual.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMP2 puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Establece el campo de fecha y el campo de zona horaria del tipo de datos DT_DBTIMESTAMPOFFSET en la fecha actual y en cero respectivamente.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMPOFFSET puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para obtener más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdbtimestamp"></a>Convertir a partir de DT_DBTIMESTAMP  
  
|Convertir DT_DBTIMESTAMP a|Resultado|  
|--------------------------------|------------|  
|DT_FILETIME|Convierte el tipo de datos.|  
|DT_DATE|Si un valor representado por el tipo de datos DT_DBTIMESTAMP desborda el rango del tipo de datos DT_DATE, se devuelve el error DB_E_DATAOVERFLOW. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Quita el valor de hora representado por el tipo de datos DT_DBTIMESTAMP.|  
|DT_DBTIME|Quita el valor de fecha representado por el tipo de datos DT_DBTIMESTAMP.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIME puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Quita el valor de fecha representado por el tipo de datos DT_DBTIMESTAMP.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos de DT_DBTIME2 puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Sin cambios.|  
|DT_DBTIMESTAMP2|Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMP2 puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Establece en cero el campo de zona horaria del tipo de datos DT_DBTIMESTAMPOFFSET.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMPOFFSET puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para obtener más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdbtimestamp2"></a>Convertir a partir de DT_DBTIMESTAMP2  
  
|Convertir DT_DBTIMESTAMP2 a|Resultado|  
|---------------------------------|------------|  
|DT_FILETIME|Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_FILETIME puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DATE|Si un valor representado por el tipo de datos DT_DBTIMESTAMP2 desborda el intervalo del tipo de datos DT_DATE, se devuelve el error DB_E_DATAOVERFLOW. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DATE puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Quita el valor de hora representado por el tipo de datos DT_DBTIMESTAMP2.|  
|DT_DBTIME|Quita el valor de fecha representado por el tipo de datos DT_DBTIMESTAMP2.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIME puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Quita el valor de fecha representado por el tipo de datos DT_DBTIMESTAMP2.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos de DT_DBTIME2 puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Si un valor representado por el tipo de datos DT_DBTIMESTAMP2 desborda el intervalo del tipo de datos DT_DBTIMESTAMP, se devuelve el error DB_E_DATAOVERFLOW.<br /><br /> DT_DBTIMESTAMP2 asigna a un tipo de datos de SQL Server, datetime2, con un intervalo desde el 1 de enero del año 1 hasta el 31 de diciembre del año 9999. DT_DBTIMESTAMP se asigna a un tipo de datos de SQL Server, datetime, con un intervalo menor, del 1 de enero de 1.753 hasta el 31 de diciembre de 9.999.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMP puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos.<br /><br /> Para obtener más información sobre los errores, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos de destino DT_DBTIMESTAMP2 puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Establece en cero el campo de zona horaria del tipo de datos DT_DBTIMESTAMPOFFSET.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMPOFFSET puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para obtener más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdbtimestampoffset"></a>Convertir a partir de DT_DBTIMESTAMPOFFSET  
  
|Convertir DT_DBTIMESTAMPOFFSET a|Resultado|  
|--------------------------------------|------------|  
|DT_FILETIME|Cambia el valor de hora representado por el tipo de datos DT_DBTIMESTAMPOFFSET a la hora universal coordinada (UTC).<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_FILETIME puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DATE|Cambia el valor de hora representado por el tipo de datos DT_DBTIMESTAMPOFFSET a UTC.<br /><br /> Si un valor representado por el tipo de datos DT_DBTIMESTAMPOFFSET desborda el intervalo del tipo de datos DT_DATE, se devuelve el error DB_E_DATAOVERFLOW.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DATE puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos.<br /><br /> Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Cambia el valor de hora representado por el tipo de datos DT_DBTIMESTAMPOFFSET a UTC, lo que puede afectar al valor de fecha. A continuación se quita el valor de hora.|  
|DT_DBTIME|Cambia el valor de hora representado por el tipo de datos DT_DBTIMESTAMPOFFSET a UTC.<br /><br /> Quita el valor de fecha representado por el tipo de datos DT_DBTIMESTAMPEOFFSET.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIME puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Cambia el valor de hora representado por el tipo de datos DT_DBTIMESTAMPOFFSET a UTC.<br /><br /> Quita el valor de fecha representado por el tipo de datos DT_DBTIMESTAMPOFFSET.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos de DT_DBTIME2 puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Cambia el valor de hora representado por el tipo de datos DT_DBTIMESTAMPOFFSET a UTC.<br /><br /> Si un valor representado por el tipo de datos DT_DBTIMESTAMPOFFSET desborda el intervalo del tipo de datos DT_DBTIMESTAMP, se devuelve el error DB_E_DATAOVERFLOW.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMP puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos.<br /><br /> Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Cambia el valor de hora representado por el tipo de datos DT_DBTIMESTAMPOFFSET a UTC.<br /><br /> Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos DT_DBTIMESTAMP2 puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Quita el valor de fracciones de segundo cuando su escala es mayor que el número de dígitos de fracciones de segundo que el tipo de datos de destino DT_DBTIMESTAMPOFFSET puede contener. Después de quitar el valor de fracciones de segundo, genera un informe sobre este truncamiento de datos. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).|  
  
## <a name="mapping-of-integration-services-data-types-to-database-data-types"></a>Asignación de tipos de datos de Integration Services a tipos de datos de bases de datos  
 En la siguiente tabla se proporciona orientación sobre cómo asignar los tipos de datos que usan ciertas bases de datos a los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Estas asignaciones se resumen a partir de los archivos de asignación que utiliza el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando importa datos de los orígenes mencionados. Para obtener más información sobre estos archivos de asignación, vea [Asistente para importación y exportación de SQL Server](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
> [!IMPORTANT]  
>  Estas asignaciones no están diseñadas para representar equivalencias estrictas, sino solo para ofrecer orientación. En ciertas situaciones, puede ser necesario utilizar un tipo de datos diferente del incluido en esta tabla.  
  
> [!NOTE]  
>  Puede usar los tipos de datos de SQL Server para calcular el tamaño de los tipos de datos de fecha y hora de Integration Services correspondientes.  
  
|Tipo de datos|SQL Server<br /><br /> (SQLOLEDB; SQLNCLI10)|SQL Server (SqlClient)|Jet|Oracle<br /><br /> (OracleClient)|DB2<br /><br /> (DB2OLEDB)|DB2<br /><br /> (IBMDADB2)|  
|---------------|--------------------------------------------|------------------------------|---------|---------------------------------|--------------------------|--------------------------|  
|DT_BOOL|bit|bit|bit||||  
|DT_BYTES|binary, varbinary, timestamp|binary, varbinary, timestamp|BigBinary, VarBinary|RAW|||  
|DT_CY|smallmoney, money|smallmoney, money|Moneda||||  
|DT_DATE|||||||  
|DT_DBDATE|[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)|[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)||Date|Date|Date|  
|DT_DBTIME||||TIMESTAMP|time|time|  
|DT_DBTIME2|[hora &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)(p)|[hora &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)(p)|||||  
|DT_DBTIMESTAMP|[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md), [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md), [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|DateTime|TIMESTAMP, DATE, INTERVAL|TIME, TIMESTAMP, DATE|TIME, TIMESTAMP, DATE|  
|DT_DBTIMESTAMP2|[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)|[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)||TIMESTAMP|TIMESTAMP|TIMESTAMP|  
|DT_DBTIMESTAMPOFFSET|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)(p)|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md) (p)||timestampoffset|timestamp,<br /><br /> varchar|timestamp,<br /><br /> varchar|  
|DT_DECIMAL|||||||  
|DT_FILETIME|||||||  
|DT_GUID|UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|GUID||||  
|DT_I1|||||||  
|DT_I2|SMALLINT|SMALLINT|Short||smallint|SMALLINT|  
|DT_I4|INT|INT|Long||INTEGER|INTEGER|  
|DT_I8|BIGINT|BIGINT|||bigint|bigint|  
|DT_NUMERIC|decimal, numeric|decimal, numeric|Decimal|NUMBER, INT|decimal, numeric|decimal, numeric|  
|DT_R4|REAL|REAL|Único||real|real|  
|DT_R8|FLOAT|FLOAT|Doble|FLOAT, REAL|FLOAT, DOUBLE|FLOAT, DOUBLE|  
|DT_STR|char, varchar||varchar||char, varchar|char, varchar|  
|DT_UI1|TINYINT|TINYINT|Byte||||  
|DT_UI2|||||||  
|DT_UI4|||||||  
|DT_UI8|||||||  
|DT_WSTR|nchar, nvarchar, sql_variant, xml|char, varchar, nchar, nvarchar, sql_variant, xml|LongText|CHAR, ROWID, VARCHAR2, NVARCHAR2, NCHAR|GRAPHIC, VARGRAPHIC|GRAPHIC, VARGRAPHIC|  
|DT_IMAGE|imagen|imagen|LongBinary|LONG RAW, BLOB, LOBLOCATOR, BFILE, VARGRAPHIC, LONG VARGRAPHIC, definido por el usuario|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA, BLOB|  
|DT_NTEXT|ntext|text, ntext||LONG, CLOB, NCLOB, NVARCHAR, TEXT|LONG VARCHAR, NCHAR, NVARCHAR, TEXT|LONG VARCHAR, DBCLOB, NCHAR, NVARCHAR, TEXT|  
|DT_TEXT|texto||||LONG VARCHAR FOR BIT DATA|LONG VARCHAR FOR BIT DATA, CLOB|  
  
 Para obtener información sobre la asignación de tipos de datos en el flujo de datos, vea [Trabajar con tipos de datos del flujo de datos](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog, sobre la [comparación de rendimiento entre las técnicas de conversión de tipos de datos en SSIS 2008](https://go.microsoft.com/fwlink/?LinkId=220823), en blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte también  
 [Datos de flujos de datos](../../integration-services/data-flow/data-in-data-flows.md)  
  
  
