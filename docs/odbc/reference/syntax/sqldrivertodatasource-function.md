---
title: Función SQLDriverToDataSource ( SQLDriverToDataSource) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverToDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverToDataSource
helpviewer_keywords:
- SQLDriverToDataSource function [ODBC]
ms.assetid: 0de28eb5-8aa9-43e4-a87f-7dbcafe800dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89e7db7e4b20a35e047dca94cb72d8a6888fb670
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302756"
---
# <a name="sqldrivertodatasource-function"></a>Función SQLDriverToDataSource
**SQLDriverToDataSource** admite traducciones para controladores ODBC. Las aplicaciones habilitadas para ODBC no llaman a esta función; las aplicaciones solicitan la traducción a través de **SQLSetConnectAttr**. El controlador asociado con el *ConnectionHandle* especificado en **SQLSetConnectAttr** llama al archivo DLL especificado para realizar traducciones de todos los datos que fluyen desde el controlador al origen de datos. Se puede especificar un archivo DLL de traducción predeterminado en el archivo de inicialización ODBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLDriverToDataSource(  
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
 [Entrada] Valor de la opción.  
  
 *fSqlType*  
 [Entrada] El tipo de datos ODBC SQL. Este argumento indica al controlador cómo convertir *rgbValueIn* en un formulario aceptable por el origen de datos. Para obtener una lista de tipos de datos SQL válidos, vea [Tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md).  
  
 *rgbValueIn*  
 [Entrada] Valor que se va a traducir.  
  
 *cbValueIn*  
 [Entrada] Longitud de *rgbValueIn*.  
  
 *rgbValueOut*  
 [Salida] Resultado de la traducción.  
  
> [!NOTE]  
>  El archivo DLL de traducción no termina en null este valor.  
  
 *cbValueOutMax*  
 [Entrada] Longitud de *rgbValueOut*.  
  
 *pcbValueOut*  
 [Salida] El número total de bytes (excluyendo el byte de terminación nula) disponiblepara devolver en *rgbValueOut*.  
  
 Para los datos binarios o de caracteres, si es mayor o igual que *cbValueOutMax*, los datos de *rgbValueOut* se truncan en bytes *cbValueOutMax.*  
  
 Para todos los demás tipos de datos, se omite el valor de *cbValueOutMax* y el archivo DLL de traducción supone que el tamaño de *rgbValueOut* es el tamaño del tipo de datos C predeterminado del tipo de datos SQL especificado con *fSqlType*.  
  
 El *argumento pcbValueOut* puede ser un puntero nulo.  
  
 *szErrorMsg*  
 [Salida] Puntero al almacenamiento para un mensaje de error. Se trata de una cadena vacía a menos que se haya producido un error en la traducción.  
  
 *cbErrorMsgMax*  
 [Entrada] Longitud de *szErrorMsg*.  
  
 *pcbErrorMsg*  
 [Salida] Puntero al número total de bytes (excluyendo el byte de terminación nula) disponibles para devolver en *szErrorMsg*. Si esto es mayor o igual que *cbErrorMsg*, los datos de *szErrorMsg* se truncan a *cbErrorMsgMax* menos el carácter de terminación nula. El argumento *pcbErrorMsg* puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 TRUESi la traducción se realizó correctamente, FALSE si se produjo un error en la traducción.  
  
## <a name="comments"></a>Comentarios  
 El controlador llama a **SQLDriverToDataSource** para traducir todos los datos (instrucciones SQL, parámetros, etc.) pasando del controlador al origen de datos. Es posible que el archivo DLL de traducción no traduzca algunos datos, según el tipo de datos y el propósito del archivo DLL de traducción. Por ejemplo, un archivo DLL que traduce datos de caracteres de una página de códigos a otra omite todos los datos numéricos y binarios.  
  
 El valor de *fOption* se establece en el valor de *vParam* especificado mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_OPTION. Es un valor de 32 bits que tiene un significado específico para un archivo DLL de traducción determinado. Por ejemplo, podría especificar una traducción de un determinado juego de caracteres.  
  
 Si se especifica el mismo búfer para *rgbValueIn* y *rgbValueOut*, la traducción de datos en el búfer se realizará en su lugar.  
  
 Aunque *cbValueIn*, *cbValueOutMax*y *pcbValueOut* son del tipo SDWORD, **SQLDriverToDataSource** no admite necesariamente punteros enormes.  
  
 Si **SQLDriverToDataSource** devuelve FALSE, es posible que se haya producido un truncamiento de datos durante la traducción. Si *pcbValueOut* (el número de bytes disponibles para devolver en el búfer de salida) es mayor que *cbValueOutMax* (la longitud del búfer de salida), se produjo el truncamiento. El controlador debe determinar si el truncamiento era aceptable o no. Si no se produjo el truncamiento, **SQLDriverToDataSource** devolvió FALSE debido a otro error. En cualquier caso, se devuelve un mensaje de error específico en *szErrorMsg*.  
  
 Para obtener más información sobre la traducción de datos, vea [DLL de traducción](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Traducción de datos devueltos desde el origen de datos|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|Devolver la configuración de un atributo de conexión|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Establecer un atributo de conexión|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
