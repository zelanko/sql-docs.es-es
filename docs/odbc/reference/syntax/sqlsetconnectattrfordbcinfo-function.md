---
title: "Función SQLSetConnectAttrForDbcInfo | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f470fe00f7e0d39d2ea474558f21584a75bb42f5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo (función)
**Conformidad**  
 Versión introdujo: ODBC 3,81 normativas: ODBC  
  
 **Resumen**  
 **SQLSetConnectAttrForDbcInfo** es el mismo que **SQLSetConnectAttr**, sino que establece el atributo en el token de la información de conexión en lugar de en el identificador de conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbcInfoToken*  
 [Entrada] Identificador del token.  
  
 *Atributo*  
 [Entrada] Atributo que se establecerá. La lista de atributos válidas es específico del controlador y los mismos que para [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 *ValuePtr*  
 [Entrada] Puntero a la capacidad de asociarse *atributo*. Dependiendo del valor de *atributo*, *ValuePtr* será un valor entero sin signo de 32 bits o hará referencia a una cadena de caracteres terminada en null. Tenga en cuenta que si el *atributo* argumento es un valor específico del controlador, el valor de *ValuePtr* puede ser un entero con signo.  
  
 *StringLength*  
 [Entrada] Si *atributo* es un atributo definido en ODBC y *ValuePtr* apunta a una cadena de caracteres o un búfer binario, este argumento debe ser la longitud de **ValuePtr*. Para los datos de cadena de caracteres, este argumento debe contener el número de bytes en la cadena.  
  
 Si *atributo* es un atributo definido en ODBC y *ValuePtr* es un entero, *StringLength* se omite.  
  
 Si *atributo* es un atributo definido por el controlador, la aplicación indica la naturaleza del atributo para el Administrador de controladores al establecer el *StringLength* argumento. *StringLength* puede tener los valores siguientes:  
  
-   Si *ValuePtr* es un puntero a una cadena de caracteres, a continuación, *StringLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si *ValuePtr* es un puntero a un búfer binario, a continuación, la aplicación coloca el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en *StringLength*. Esto coloca un valor negativo en *StringLength*.  
  
-   Si *ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, a continuación, *StringLength* debería tener el valor SQL_IS_POINTER.  
  
-   Si *ValuePtr* contiene un valor de longitud fija, a continuación, *StringLength* es SQL_IS_INTEGER o SQL_IS_UINTEGER, según corresponda.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Igual que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), excepto en que va a usar el Administrador de controladores un **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN y un **controlar** de *hDbcInfoToken* .  
  
## <a name="remarks"></a>Comentarios  
 **SQLSetConnectAttrForDbcInfo** es el mismo que **SQLSetConnectAttr**, pero establece el atributo en el token de información de conexión, en lugar de en el identificador de conexión. Por ejemplo, si **SQLSetConnectAttr** no reconoce un atributo, **SQLSetConnectAttrForDbcInfo** también debe devolver SQL_ERROR para ese atributo.  
  
 Cada vez que el controlador devuelve SQL_ERROR o SQL_INVALID_HANDLE, el controlador debe pasar por alto este atributo para calcular el identificador de grupo. Además, el Administrador de controladores obtendrá la información de diagnóstico de *hDbcInfoToken*y devuelve SQL_SUCCESS_WITH_INFO para la aplicación en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) y [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). Por lo tanto, una aplicación puede recuperar detalles sobre por qué no se puede establecer algunos atributos.  
  
 Las aplicaciones no deben llamar directamente a esta función. Un controlador ODBC que admite la agrupación de conexiones dependientes del controlador debe implementar esta función.  
  
 Incluir sqlspi.h para el desarrollo del controlador ODBC.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
