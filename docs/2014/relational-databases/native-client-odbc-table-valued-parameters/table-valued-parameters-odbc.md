---
title: Parámetros con valores de tabla (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC)
- ODBC, table-valued parameters
ms.assetid: ef06cd13-18e2-4c65-8ede-c3955d820e54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31ed60f10f12bbc11037a64caa50802360b919de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62467305"
---
# <a name="table-valued-parameters-odbc"></a>Parámetros con valores de tabla (ODBC)
  La compatibilidad con ODBC para parámetros con valores de tabla permite a una aplicación cliente enviar datos parametrizados al servidor más eficazmente, enviando varias filas al servidor con una llamada.  
  
 Para obtener información acerca de los parámetros con valores de tabla en el servidor, consulte [usar parámetros &#40;motor de base de datos&#41;](../tables/use-table-valued-parameters-database-engine.md).  
  
 En ODBC, hay dos formas de enviar parámetros con valores de tabla al servidor:  
  
-   Todos los datos de parámetro con valores de tabla pueden estar en memoria en el momento en que se llama a SQLExecDirect o SQLExecute. Estos datos se almacenan en matrices si hay varias filas en el valor de tabla.  
  
-   Una aplicación puede especificar datos en ejecución para un parámetro con valores de tabla cuando se llama a SQLExecDirect o SQLExecute. En este caso, las filas de datos para el valor de tabla se pueden proporcionar en lotes o de uno en uno para reducir los requerimientos de memoria.  
  
 La primera opción habilita los procedimientos almacenados para encapsular más lógica de negocios. Por ejemplo, un procedimiento almacenado único podría encapsular una transacción de entrada de pedido entera cuando los elementos del pedido se pasan como un parámetro con valores de tabla. Esta opción es muy eficaz, porque se requiere solo un único ciclo de ida y vuelta al servidor. Alternativamente, podría utilizar diferentes procedimientos para administrar por separado el encabezado y los elementos del pedido, lo que requeriría más código y un contrato más complejo entre el cliente y servidor.  
  
 El segundo método proporciona un mecanismo eficaz para las operaciones masivas con cantidades muy grandes de datos. Esto habilita a una aplicación para transmitir en secuencias filas de datos al servidor sin tener que almacenar primero todos en memoria.  
  
 Puede crear restricciones y claves principales al crear la variable de tabla. Las restricciones constituyen un buen medio de asegurarse de que los datos de una tabla cumplan requisitos concretos.  
  
## <a name="in-this-section"></a>En esta sección  
 [Usos de parámetros con valores de tabla de ODBC](uses-of-odbc-table-valued-parameters.md)  
 Describe los escenarios de usuario principales para parámetros con valores de tabla y ODBC.  
  
 [Tipo SQL de ODBC para parámetros con valores de tabla](odbc-sql-type-for-table-valued-parameters.md)  
 Describe el tipo SQL_SS_TABLE. Se trata de un nuevo tipo SQL de ODBC que admite parámetros con valores de tabla.  
  
 [Campos de descriptor de parámetros con valores de tabla](table-valued-parameter-descriptor-fields.md)  
 Describe campos de descriptor que admiten parámetros con valores de tabla.  
  
 [Campos de descriptor para columnas de parámetros con valores de tabla](descriptor-fields-for-table-valued-parameter-constituent-columns.md)  
 Describe campos de descriptor que tienen significado para parámetros con valores de tabla.  
  
 [Campos de registros de diagnóstico para parámetros con valores de tabla](table-valued-parameter-diagnostic-record-fields.md)  
 Describe dos campos de diagnóstico agregados a los registros de diagnóstico para admitir los parámetros con valores de tabla.  
  
 [Atributos de instrucción que afectan a parámetros con valores de tabla](statement-attributes-that-affect-table-valued-parameters.md)  
 Describe un nuevo campo de encabezado de descriptor que habilita la manipulación de columnas de parámetros con valores de tabla.  
  
 [Enlace y transferencia de datos de valores de columnas y parámetros con valores de tabla](binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)  
 Describe el enlace de parámetros y cómo pasar un parámetro con valores de tabla al servidor.  
  
 [Metadatos de parámetros con valores de tabla para instrucciones preparadas](table-valued-parameter-metadata-for-prepared-statements.md)  
 Describe cómo una aplicación puede obtener metadatos para una llamada a procedimiento preparada.  
  
 [Metadatos de parámetros con valores de tabla adicionales](additional-table-valued-parameter-metadata.md)  
 Describe cómo utilizar SQLColumns, SQLProcedureColumns y SQLTables para recuperar metadatos para un parámetro con valores de tabla.  
  
 [Conversión de datos de parámetros con valores de tabla y otros errores y advertencias](table-valued-parameter-data-conversion-and-other-errors-and-warnings.md)  
 Describe cómo procesar los errores en valores de columna de parámetro con valores de tabla.  
  
 [Compatibilidad entre versiones](cross-version-compatibility.md)  
 Describe conflictos que se pueden producir cuando un cliente o un servidor de una versión anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] utiliza parámetros con valores de tabla.  
  
 [Resumen de la API de parámetros con valores de tabla de ODBC](odbc-table-valued-parameter-api-summary.md)  
 Muestra la lista de funciones ODBC que admiten parámetros con valores de tabla.  
  
 [Ejemplos de programación de parámetros con valores de tabla ODBC](../../database-engine/dev-guide/odbc-table-valued-parameter-programming-examples.md)  
 Describe cómo realizar tareas comunes.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [Parámetros con valores de tabla &#40;SQL Server Native Client&#41;](../native-client/features/table-valued-parameters-sql-server-native-client.md)  
  
  
