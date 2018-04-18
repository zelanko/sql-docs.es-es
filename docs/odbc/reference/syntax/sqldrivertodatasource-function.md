---
title: Función SQLDriverToDataSource | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1dcb53a08e3e20457a3ad616cd7b3d45fec2962
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqldrivertodatasource-function"></a>SQLDriverToDataSource (función)
**SQLDriverToDataSource** admite traducciones para los controladores ODBC. No se llama a esta función mediante aplicaciones habilitadas para ODBC; las aplicaciones solicitan traducción a través de **SQLSetConnectAttr**. El controlador asociado a la *IdentificadorConexión* especificado en **SQLSetConnectAttr** llama a la DLL especificada para llevar a cabo las traducciones de todos los datos fluyen desde el controlador al origen de datos. Un archivo DLL de traducción predeterminado puede especificarse en el archivo de inicialización de ODBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Valor de opción.  
  
 *fSqlType*  
 [Entrada] El tipo de datos SQL de ODBC. Este argumento indica al controlador cómo convertir *rgbValueIn* en un formato aceptable por el origen de datos. Para obtener una lista de tipos de datos SQL válidos, consulte [tipos de datos de SQL](../../../odbc/reference/appendixes/sql-data-types.md).  
  
 *rgbValueIn*  
 [Entrada] Valor que se va a traducir.  
  
 *cbValueIn*  
 [Entrada] Longitud de *rgbValueIn*.  
  
 *rgbValueOut*  
 [Salida] Resultado de la traducción.  
  
> [!NOTE]  
>  El archivo DLL de traducción no null de finalización de este valor.  
  
 *cbValueOutMax*  
 [Entrada] Longitud de *rgbValueOut*.  
  
 *pcbValueOut*  
 [Salida] El número total de bytes (excepto el byte de finalización en null) disponible para devolver en *rgbValueOut*.  
  
 Para datos de caracteres o binarios, si es mayor o igual que *cbValueOutMax*, los datos de *rgbValueOut* se trunca a *cbValueOutMax* bytes.  
  
 Para los demás tipos de datos, el valor de *cbValueOutMax* se omite y el archivo DLL de traducción se da por supuesto que el tamaño de *rgbValueOut* es el tamaño del tipo de datos C predeterminado del tipo de datos SQL especificado con *fSqlType*.  
  
 El *pcbValueOut* argumento puede ser un puntero nulo.  
  
 *szErrorMsg*  
 [Salida] Puntero al almacenamiento para un mensaje de error. Se trata de una cadena vacía a menos que falle la traducción.  
  
 *cbErrorMsgMax*  
 [Entrada] Longitud de *szErrorMsg*.  
  
 *pcbErrorMsg*  
 [Salida] Puntero al número total de bytes (excepto el byte de finalización en null) disponible para devolver en *szErrorMsg*. Si es mayor o igual que *cbErrorMsg*, los datos de *szErrorMsg* se trunca a *cbErrorMsgMax* menos el carácter de terminación null. El *pcbErrorMsg* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 Es TRUE si la conversión fue correcta, FALSE si la conversión produce un error.  
  
## <a name="comments"></a>Comentarios  
 El controlador llama **SQLDriverToDataSource** para traducir todos los datos (instrucciones SQL, parámetros etc.) pasar desde el controlador al origen de datos. El archivo DLL de traducción no podría traducir algunos datos, según el tipo de datos y el propósito de la traducción del archivo DLL. Por ejemplo, un archivo DLL que traduce los datos de caracteres de una página de códigos a otra omite todos los datos numéricos y binarios.  
  
 El valor de *fOption* se establece en el valor de *vParam* mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_OPTION. Es un valor de 32 bits que tiene un significado específico para un archivo DLL de traducción determinada. Por ejemplo, podría especificar que un determinado carácter traducción del conjunto.  
  
 Si se especifica el mismo búfer para *rgbValueIn* y *rgbValueOut*, se realizará la traducción de datos en el búfer en su lugar.  
  
 Aunque *cbValueIn*, *cbValueOutMax*, y *pcbValueOut* son del tipo SDWORD, **SQLDriverToDataSource** no significa necesariamente que admiten punteros muy grandes.  
  
 Si **SQLDriverToDataSource** devuelve FALSE, el truncamiento de datos se hayan producido durante la traducción. Si *pcbValueOut* (el número de bytes disponible para devolver en el búfer de salida) es mayor que *cbValueOutMax* (la longitud del búfer de salida), a continuación, se ha producido truncamiento. El controlador debe determinar si el truncamiento era aceptable. Si no se ha producido truncamiento, el **SQLDriverToDataSource** devolvió FALSE debido a otro error. En cualquier caso, se devuelve un mensaje de error específico en *szErrorMsg*.  
  
 Para obtener más información acerca de cómo traducir datos, vea [archivos DLL de traducción](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Traducir los datos devueltos desde el origen de datos|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|Devolver el valor de un atributo de conexión|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Establecer un atributo de conexión|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
