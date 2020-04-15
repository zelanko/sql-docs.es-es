---
title: Transiciones de medio ambiente ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebfb5475d24d5fc70c4cb46a666b2573066565a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283305"
---
# <a name="environment-transitions"></a>Transiciones de entorno
Los entornos ODBC tienen los tres estados siguientes.  
  
|State|Descripción|  
|-----------|-----------------|  
|E0|Entorno no asignado|  
|E1|Entorno asignado, conexión no asignada|  
|E2|Entorno asignado, conexión asignada|  
  
 En las tablas siguientes se muestra cómo afecta cada función ODBC al estado del entorno.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Allocated|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|(IH) [2]|E2[5]<br />(HY010) [6]|--[4]|  
|(IH) [3]|(IH)|--[4]|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DBC.  
  
 [3] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
 [4] Llamar a **SQLAllocHandle** con *OutputHandlePtr* apuntando a un identificador válido sobrescribe ese identificador. Esto podría ser un error de programación de aplicaciones.  
  
 [5] El atributo de entorno SQL_ATTR_ODBC_VERSION se había establecido en el entorno.  
  
 [6] El atributo de entorno SQL_ATTR_ODBC_VERSION no se había establecido en el entorno.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources y SQLDrivers  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Allocated|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--[1]<br />(HY010) [2]|  
  
 [1] El atributo de entorno SQL_ATTR_ODBC_VERSION se había establecido en el entorno.  
  
 [2] El atributo de entorno SQL_ATTR_ODBC_VERSION no se había establecido en el entorno.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Allocated|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--[3]<br />(HY010) [4]|--[3]<br />(HY010) [4]|  
|(IH) [2]|(IH)|--|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DBC.  
  
 [3] El atributo de entorno SQL_ATTR_ODBC_VERSION se había establecido en el entorno.  
  
 [4] El atributo de entorno SQL_ATTR_ODBC_VERSION no se había establecido en el entorno.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Allocated|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|E0|(HY010)|  
|(IH) [2]|(IH)|--[4]<br />E1[5]|  
|(IH) [3]|(IH)|--|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DBC.  
  
 [3] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
 [4] Había otros manejadores de conexión asignados.  
  
 [5] El identificador de conexión especificado en *Handle* era el único identificador de conexión asignado.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField y SQLGetDiagRec  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Allocated|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--|--|  
|(IH) [2]|(IH)|--|  
  
 [1] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_ENV.  
  
 [2] Esta fila muestra transiciones cuando *HandleType* se SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Allocated|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--|  
  
 [1] El atributo de entorno SQL_ATTR_ODBC_VERSION se había establecido en el entorno.  
  
 [2] El atributo de entorno SQL_ATTR_ODBC_VERSION no se había establecido en el entorno.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Allocated|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|(HY011)|  
  
 [1] El atributo de entorno SQL_ATTR_ODBC_VERSION se había establecido en el entorno.  
  
 [2] El argumento *Attribute* no era SQL_ATTR_ODBC_VERSION, y el atributo de entorno SQL_ATTR_ODBC_VERSION no se había establecido en el entorno.  
  
## <a name="all-other-odbc-functions"></a>Todas las demás funciones ODBC  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Allocated|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
