---
title: Función SQLDataSourceToDriver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSourceToDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSourceToDriver
helpviewer_keywords:
- SQLDataSourceToDriver function [ODBC]
ms.assetid: 0d87fcac-30a0-4303-ad8f-a5b53f4b428d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0ad4a98689db00c6dcb484e7a04bb973d2e1761
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259396"
---
# <a name="sqldatasourcetodriver-function"></a>Función SQLDataSourceToDriver
**SQLDataSourceToDriver** supportstranslations para controladores ODBC. Esta función no se invoca mediante aplicaciones habilitadas para ODBC; las aplicaciones solicitan la traducción a través de **SQLSetConnectAttr**. El controlador asociado con el *ConnectionHandle* especificado en **SQLSetConnectAttr** llama a la DLL especificada para llevar a cabo las traducciones de todos los datos que fluyen desde el origen de datos para el controlador. Un archivo DLL de traducción predeterminado puede especificarse en el archivo de inicialización de ODBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLDataSourceToDriver(  
     UDWORD     fOption,  
     SWORD      fSqlType,  
     PTR        rgbValueIn,  
     SDWORD     cbValueIn,  
     PTR        rgbValueOut,  
     SDWORD     cbValueOutMax,  
     SDWORD *   pcbValueOut,  
     UCHAR *    szErrorMsg,  
     SWORD      cbErrorMsgMax,  
     SWORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>Argumentos  
 *fOption*  
 [Entrada] Valor de opción.  
  
 *fSqlType*  
 [Entrada] El tipo de datos SQL. Este argumento indica al controlador cómo convertir *rgbValueIn* en un formato aceptable por la aplicación. Para obtener una lista de tipos de datos SQL válidos, vea el [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) sección en el apéndice D: Tipos de datos.  
  
 *rgbValueIn*  
 [Entrada] Valor que se va a traducir.  
  
 *cbValueIn*  
 [Entrada] Longitud de *rgbValueIn*.  
  
 *rgbValueOut*  
 [Salida] Resultado de la traducción.  
  
> [!NOTE]  
>  El archivo DLL de traducción no termine en null este valor.  
  
 *cbValueOutMax*  
 [Entrada] Longitud de *rgbValueOut*.  
  
 *pcbValueOut*  
 [Salida] El número total de bytes (sin incluir los bytes de terminación null) disponibles para devolver en *rgbValueOut*.  
  
 Para caracteres o datos binarios, si es mayor o igual a *cbValueOutMax*, los datos de *rgbValueOut* se trunca a *cbValueOutMax* bytes.  
  
 Para los demás tipos de datos, el valor de *cbValueOutMax* se omite y el archivo DLL de traducción se da por supuesto que el tamaño de *rgbValueOut* es el tamaño del tipo de datos C predeterminado del tipo de datos SQL especificado con *fSqlType*.  
  
 El *pcbValueOut* argumento puede ser un puntero nulo.  
  
 *szErrorMsg*  
 [Salida] Puntero al almacenamiento para un mensaje de error. Se trata de una cadena vacía a menos que la traducción no se pudo.  
  
 *cbErrorMsgMax*  
 [Entrada] Longitud de *szErrorMsg*.  
  
 *pcbErrorMsg*  
 [Salida] Puntero al número total de bytes (sin incluir los bytes de terminación null) disponibles para devolver en *szErrorMsg*. Si es mayor o igual a *cbErrorMsg*, los datos de *szErrorMsg* se trunca a *cbErrorMsgMax* menos el carácter de terminación null. El *pcbErrorMsg* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 TRUE si la conversión fue correcta, es FALSE si la traducción no se pudo.  
  
## <a name="comments"></a>Comentarios  
 El controlador llama a **SQLDataSourceToDriver** para traducir alldata (datos del conjunto de resultados, los nombres de tabla, recuentos de filas, los mensajes de error y así sucesivamente) pasar de los datos de origen para el controlador. El archivo DLL de traducción no puede traducir algunos datos, según el tipo de datos y el propósito de la traducción de archivo DLL; Por ejemplo, un archivo DLL que traduce los datos de caracteres de una página de códigos a otra omite todos los datos numéricos y binarios.  
  
 El valor de *fOption* se establece en el valor de *vParam* especificado mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_OPTION. Es un valor de 32 bits que tiene un significado específico para un archivo DLL de traducción determinada. Por ejemplo, podría especificar que un carácter determinado traducción del conjunto.  
  
 Si se especifica el mismo búfer para *rgbValueIn* y *rgbValueOut*, se realizará la traducción de datos en el búfer en su lugar.  
  
 Aunque *cbValueIn*, *cbValueOutMax*, y *pcbValueOut* son del tipo SDWORD, **SQLDataSourceToDriver** no significa necesariamente que admite punteros enormes.  
  
 Si **SQLDataSourceToDriver** devuelve FALSE, el truncamiento de datos podría haberse producido durante la traducción. Si *pcbValueOut* (el número de bytes disponible para devolver en el búfer de salida) es mayor que *cbValueOutMax* (la longitud del búfer de salida), a continuación, se ha producido un truncamiento. El controlador debe determinar si el truncamiento fue aceptable. Si no se produjo un truncamiento, el **SQLDataSourceToDriver** devolvió FALSE debido a otro error. En cualquier caso, se devuelve un mensaje de error específico en *szErrorMsg*.  
  
 Para obtener más información acerca de la traducción de datos, vea [archivos DLL de traducción](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Traducción de datos que se envían al origen de datos|[SQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|Devuelve el valor de un atributo de conexión|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Establecer un atributo de conexión|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
