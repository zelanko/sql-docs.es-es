---
title: Función SQLSetConnectAttrForDbcInfo ( SQLSetConnectAttrForDbcInfo) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f43a0fc6cd02fe566579a543667f9a4c4c1a108
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301892"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>Función SQLSetConnectAttrForDbcInfo
**Conformidad**  
 Versión introducida: CUMPLIMIENTO de estándares ODBC 3.81: ODBC  
  
 **Resumen**  
 **SQLSetConnectAttrForDbcInfo** es el mismo que **SQLSetConnectAttr**, pero establece el atributo en el token de información de conexión en lugar de en el identificador de conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbcInfoToken*  
 [Entrada] Mango de token.  
  
 *Atributo*  
 [Entrada] Atributo que se ha establecido. La lista de atributos válidos es específica del controlador y la misma que para [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 *ValuePtr*  
 [Entrada] Puntero al valor que se va a asociar a *Attribute*. Dependiendo del valor de *Attribute*, *ValuePtr* será un valor entero sin signo de 32 bits o apuntará a una cadena de caracteres terminada en null. Tenga en cuenta que si el *atributo* argumento es un valor específico del controlador, el valor de *ValuePtr* puede ser un entero con signo.  
  
 *StringLength*  
 [Entrada] Si *Attribute* es un atributo definido por ODBC y *ValuePtr* apunta a una cadena de caracteres o un búfer binario, este argumento debe ser la longitud de **ValuePtr*. Para los datos de cadena de caracteres, este argumento debe contener el número de bytes de la cadena.  
  
 Si *Attribute* es un atributo definido por ODBC y *ValuePtr* es un entero, *StringLength* se omite.  
  
 Si *Attribute* es un atributo definido por el controlador, la aplicación indica la naturaleza del atributo para el Administrador de controladores estableciendo el *StringLength* argumento. *StringLength* puede tener los siguientes valores:  
  
-   Si *ValuePtr* es un puntero a una cadena de caracteres, *StringLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si *ValuePtr* es un puntero a un búfer binario, la aplicación coloca el resultado de la macro SQL_LEN_BINARY_ATTR(*length*) en *StringLength*. Esto coloca un valor negativo en *StringLength*.  
  
-   Si *ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, *StringLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si *ValuePtr* contiene un valor de longitud fija, *StringLength* es SQL_IS_INTEGER o SQL_IS_UINTEGER, según corresponda.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Igual que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), excepto que el Administrador de controladores usará un **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN y un **identificador** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Observaciones  
 **SQLSetConnectAttrForDbcInfo** es el mismo que **SQLSetConnectAttr**, pero establece el atributo en el token de información de conexión, en lugar de en el identificador de conexión. Por ejemplo, si **SQLSetConnectAttr** no reconoce un atributo, **SQLSetConnectAttrForDbcInfo** también debe devolver SQL_ERROR para ese atributo.  
  
 Siempre que el controlador devuelve SQL_ERROR o SQL_INVALID_HANDLE, el controlador debe omitir este atributo para calcular el identificador del grupo. Además, el Administrador de controladores obtendrá la información de diagnóstico de *hDbcInfoToken*y devolverá SQL_SUCCESS_WITH_INFO a la aplicación en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) y [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). Por lo tanto, una aplicación puede recuperar detalles sobre por qué no se pueden establecer algunos atributos.  
  
 Las aplicaciones no deben llamar a esta función directamente. Un controlador ODBC que admite la agrupación de conexiones con reconocimiento de controladores debe implementar esta función.  
  
 Incluya sqlspi.h para el desarrollo de controladores ODBC.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollo de un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones conscientes del conductor](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
