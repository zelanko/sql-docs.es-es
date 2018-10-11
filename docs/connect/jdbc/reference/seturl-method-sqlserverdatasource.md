---
title: Método setURL (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29e1b67caaf566f04cf01c7c93a5e8d2445c31ef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633953"
---
# <a name="seturl-method-sqlserverdatasource"></a>Método setURL (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve la dirección URL que se utiliza para la conexión al origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *url*  
  
 Objeto **String** que contiene la dirección URL.  
  
## <a name="remarks"></a>Notas  
 Por razones de seguridad, no debería incluir la contraseña en la dirección URL que se proporciona al método setURL. Esto se debe a que los servidores de aplicación Java de otro fabricante muy a menudo muestran el conjunto de valores para la propiedad URL en la interfaz de usuario para la configuración del origen de datos. En su lugar, utilice el método [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) para establecer el valor de la contraseña. Los servidores de aplicación Java no mostrarán las contraseñas que se establezcan en su origen de datos de la interfaz de usuario para la configuración.  
  
> [!NOTE]  
>  Si no se llama al método setURL antes de llamar al método [getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md), getURL devuelve el valor predeterminado de "jdbc:sqlserver://."  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
