---
title: SQLBindParameter | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
caps.latest.revision: 46
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 71451888bab19c3247a86d4e0f222a527fa424b9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104241"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
  `SQLBindParameter` puede eliminar la carga de conversión de datos cuando se utiliza para proporcionar datos para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client, lo que da lugar a importantes mejoras de rendimiento para el cliente y el servidor de componentes de aplicaciones. Entre otras ventajas se incluyen la pérdida reducida de precisión al insertar o actualizar los tipos de datos numéricos aproximados.  
  
> [!NOTE]  
>  Al insertar los datos de tipo `char` y `wchar` en una columna de imagen, se usa el tamaño de los datos pasados, a diferencia del tamaño de los datos después de la conversión a un formato binario.  
  
 Si el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client encuentra un error en un elemento de matriz único de una matriz de parámetros, el controlador continúa ejecutando la instrucción para los elementos de matriz restantes. Si la aplicación ha enlazado una matriz de elementos de estado de parámetro para la instrucción, las filas de parámetros que generan errores se pueden determinar de la matriz.  
  
 Al usar el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, especifique SQL_PARAM_INPUT al enlazar parámetros de entrada. Especifique únicamente SQL_PARAM_OUTPUT o SQL_PARAM_INPUT_OUTPUT al enlazar parámetros de procedimientos almacenados definidos con la palabra clave OUTPUT.  
  
 [SQLRowCount](sqlrowcount.md) no es confiable con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador de ODBC de Native Client si un elemento de matriz de una matriz de parámetros enlazados produce un error en la ejecución de la instrucción. El atributo de instrucción ODBC SQL_ATTR_PARAMS_PROCESSED_PTR notifica el número de filas procesadas antes de que se produzca el error. A continuación, la aplicación puede atravesar su matriz de estado de parámetro para detectar el número de instrucciones ejecutado correctamente, si es necesario.  
  
## <a name="binding-parameters-for-sql-character-types"></a>Enlazar parámetros para tipos de caracteres SQL  
 Si el tipo de datos SQL que se pasa es un tipo de caracteres, *ColumnSize* es el tamaño en caracteres (no en bytes). Si la longitud de la cadena de datos en bytes es mayor que 8000, *ColumnSize* debe establecerse en `SQL_SS_LENGTH_UNLIMITED`, que indica que no hay ningún límite para el tamaño del tipo SQL.  
  
 Por ejemplo, si el tipo de datos SQL es `SQL_WVARCHAR`, *ColumnSize* no debe ser mayor que 4000. Si la longitud de datos real es mayor que 4000, a continuación, *ColumnSize* debe establecerse en `SQL_SS_LENGTH_UNLIMITED` para que `nvarchar(max)` controlador va a utilizar.  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter y parámetros con valores de tabla  
 Al igual que otros tipos de parámetros, los parámetros con valores de tabla se enlazan mediante SQLBindParameter.  
  
 Una vez enlazado un parámetro con valores de tabla, también se enlazan sus columnas. Para enlazar las columnas, se llama a [SQLSetStmtAttr](sqlsetstmtattr.md) para establecer SQL_SOPT_SS_PARAM_FOCUS en el ordinal del parámetro con valores de tabla. A continuación, llame a SQLBindParameter para cada columna en el parámetro con valores de tabla. Para volver a los enlaces de parámetro de nivel superior, establezca SQL_SOPT_SS_PARAM_FOCUS en 0.  
  
 Para obtener información acerca de cómo asignar parámetros a campos de descriptor de parámetros con valores de tabla, vea [enlace y Data Transfer of Table-Valued parámetros y valores de columna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>SQLBindParameter admite las características mejoradas de fecha y hora  
 Valores de parámetro de tipos de fecha y hora se convierten como se describe en [conversiones de C a SQL](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md). Tenga en cuenta que los parámetros de tipo `time` y `datetimeoffset` debe tener *ValueType* especificado como `SQL_C_DEFAULT` o `SQL_C_BINARY` si sus estructuras correspondientes (`SQL_SS_TIME2_STRUCT` y `SQL_SS_TIMESTAMPOFFSET_STRUCT`) se usan.  
  
 Para obtener más información, consulte [fecha y hora mejoras &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>Compatibilidad con SQLBindParameter para los UDT CLR grandes  
 `SQLBindParameter` admite tipos CLR definidos por el usuario (UDT) grandes. Para obtener más información, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Detalles de implementación de API de ODBC](odbc-api-implementation-details.md)   
 [Función SQLBindParameter](http://go.microsoft.com/fwlink/?LinkId=59328)  
  
  