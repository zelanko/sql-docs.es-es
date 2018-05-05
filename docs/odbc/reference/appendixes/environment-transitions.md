---
title: Transiciones de entorno | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6152a2ee5f21d20a6bf0ddea568e807443dfd00
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="environment-transitions"></a>Transiciones de entorno
Entornos de ODBC tienen los tres estados siguientes.  
  
|State|Description|  
|-----------|-----------------|  
|E0|Entorno sin asignar|  
|E1|Entorno asignada, sin asignar la conexión|  
|E2|Asigna el entorno, asignada la conexión|  
  
 Las tablas siguientes muestran cómo afecta cada función ODBC al estado del entorno.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Asignado|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|(IH) [2]|E2 [5]<br />(HY010) [6]|--[4]|  
|(IH) [3]|(IH)|--[4]|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
 [4] llamar a **SQLAllocHandle** con *OutputHandlePtr* que apunta a un identificador válido sobrescribe este identificador. Podría tratarse de un error de programación de la aplicación.  
  
 [5] el atributo de entorno SQL_ATTR_ODBC_VERSION hubiera establecido en el entorno.  
  
 [6], el atributo de entorno SQL_ATTR_ODBC_VERSION no se hubiera establecido en el entorno.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources y SQLDrivers  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Asignado|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--[1]<br />(HY010) [2]|  
  
 [1], el atributo de entorno SQL_ATTR_ODBC_VERSION hubiera establecido en el entorno.  
  
 [2], el atributo de entorno SQL_ATTR_ODBC_VERSION no se hubiera establecido en el entorno.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Asignado|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--[3]<br />(HY010) [4]|--[3]<br />(HY010) [4]|  
|(IH) [2]|(IH)|--|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3], el atributo de entorno SQL_ATTR_ODBC_VERSION hubiera establecido en el entorno.  
  
 [4], el atributo de entorno SQL_ATTR_ODBC_VERSION no se hubiera establecido en el entorno.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Asignado|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|E0|(HY010)|  
|(IH) [2]|(IH)|--[4]<br />E1 [5]|  
|(IH) [3]|(IH)|--|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
 [4] hubo otros identificadores de conexión asignado.  
  
 [5] el identificador de conexión especificado en *controlar* era el identificador único de conexión asignado.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField y SQLGetDiagRec  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Asignado|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--|--|  
|(IH) [2]|(IH)|--|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Asignado|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--|  
  
 [1], el atributo de entorno SQL_ATTR_ODBC_VERSION hubiera establecido en el entorno.  
  
 [2], el atributo de entorno SQL_ATTR_ODBC_VERSION no se hubiera establecido en el entorno.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Asignado|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|(HY011)|  
  
 [1], el atributo de entorno SQL_ATTR_ODBC_VERSION hubiera establecido en el entorno.  
  
 [2] el *atributo* argumento no era SQL_ATTR_ODBC_VERSION y el atributo de entorno SQL_ATTR_ODBC_VERSION no hubiera establecido en el entorno.  
  
## <a name="all-other-odbc-functions"></a>Todas las demás funciones ODBC  
  
|E0<br /><br /> Sin asignar|E1<br /><br /> Asignado|E2<br /><br /> Conexión|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
