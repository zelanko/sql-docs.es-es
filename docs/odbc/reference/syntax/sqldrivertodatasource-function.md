---
title: Función SQLDriverToDataSource | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 844e11e72bb46b69229a9a4747ac7e64f013f14e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537167"
---
# <a name="sqldrivertodatasource-function"></a>Función SQLDriverToDataSource
**SQLDriverToDataSource** admite traducciones para los controladores ODBC. Esta función no se invoca mediante aplicaciones habilitadas para ODBC; las aplicaciones solicitan la traducción a través de **SQLSetConnectAttr**. El controlador asociado con el *ConnectionHandle* especificado en **SQLSetConnectAttr** llama a la DLL especificada para llevar a cabo las traducciones de todos los datos que fluyen desde el controlador para el origen de datos. Un archivo DLL de traducción predeterminado puede especificarse en el archivo de inicialización de ODBC.  
  
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
 [Entrada] Valor de opción.  
  
 *fSqlType*  
 [Entrada] El tipo de datos SQL de ODBC. Este argumento indica al controlador cómo convertir *rgbValueIn* en una forma aceptable, el origen de datos. Para obtener una lista de tipos de datos SQL válidos, vea [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md).  
  
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
 El controlador llama a **SQLDriverToDataSource** para traducir todos los datos (instrucciones SQL, parámetros etc.) pasar desde el controlador para el origen de datos. El archivo DLL de traducción no es posible que traduzca algunos datos, según el tipo de datos y el propósito de la DLL de traducción. Por ejemplo, un archivo DLL que traduce los datos de caracteres de una página de códigos a otra omite todos los datos numéricos y binarios.  
  
 El valor de *fOption* se establece en el valor de *vParam* especificado mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_OPTION. Es un valor de 32 bits que tiene un significado específico para un archivo DLL de traducción determinada. Por ejemplo, podría especificar que un carácter determinado traducción del conjunto.  
  
 Si se especifica el mismo búfer para *rgbValueIn* y *rgbValueOut*, se realizará la traducción de datos en el búfer en su lugar.  
  
 Aunque *cbValueIn*, *cbValueOutMax*, y *pcbValueOut* son del tipo SDWORD, **SQLDriverToDataSource** no significa necesariamente que admite punteros enormes.  
  
 Si **SQLDriverToDataSource** devuelve FALSE, el truncamiento de datos podría haberse producido durante la traducción. Si *pcbValueOut* (el número de bytes disponible para devolver en el búfer de salida) es mayor que *cbValueOutMax* (la longitud del búfer de salida), a continuación, se ha producido un truncamiento. El controlador debe determinar si el truncamiento fue aceptable. Si no se produjo un truncamiento, el **SQLDriverToDataSource** devolvió FALSE debido a otro error. En cualquier caso, se devuelve un mensaje de error específico en *szErrorMsg*.  
  
 Para obtener más información acerca de la traducción de datos, vea [archivos DLL de traducción](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Traducir los datos devueltos desde el origen de datos|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|Devuelve el valor de un atributo de conexión|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Establecer un atributo de conexión|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
