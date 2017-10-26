---
title: "Método setURL (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dd1f100fcf00678741675c113512eb95a3484368
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="seturl-method-sqlserverdatasource"></a>Método setURL (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece la dirección URL que se utiliza para conectarse al origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *dirección URL*  
  
 A **cadena** que contiene la dirección URL.  
  
## <a name="remarks"></a>Comentarios  
 Por motivos de seguridad, no debe incluir la contraseña en la dirección URL proporcionada al método setURL. Esto se debe a que los servidores de aplicación Java de otro fabricante muy a menudo muestran el conjunto de valores para la propiedad URL en la interfaz de usuario para la configuración del origen de datos. En su lugar, use la [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) método para establecer el valor de contraseña. Los servidores de aplicación Java no mostrarán las contraseñas que se establezcan en su origen de datos de la interfaz de usuario para la configuración.  
  
> [!NOTE]  
>  Si no se llama al método setURL antes de llamar a la [getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md) método getURL devuelve el valor predeterminado de "SQLServer: / /".  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

