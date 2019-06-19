---
title: Objeto de enlace de datos de la libreta de direcciones | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 31efe56dcb5ae926d5da08aa00a1005597b17b91
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718620"
---
# <a name="address-book-data-binding-object"></a>Objeto de enlace de datos de la libreta de direcciones
La aplicación Libreta de direcciones utiliza el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto que se va a enlazar los datos de la base de datos de SQL Server a un objeto visual (en este caso, una tabla DHTML) en la página de aplicación cliente HTML. La lógica del programa VBScript controlada por eventos usa el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) para:  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
-   Consultar la base de datos, enviar actualizaciones a la base de datos y actualizar la cuadrícula de datos.  
  
-   Permitir a los usuarios mover a la primera, a continuación, anterior, o el último registro en la cuadrícula de datos.  
  
 El código siguiente define el **RDS. DataControl** componente:  
  
```vb
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 Define la etiqueta de objeto del **RDS. DataControl** componente en el programa. La etiqueta incluye dos tipos de parámetros:  
  
-   Los asociados a la etiqueta de objeto genérica.  
  
-   Los elementos específicos del **RDS. DataControl** objeto.  
  
## <a name="generic-object-tag-parameters"></a>Parámetros de la etiqueta de objeto genérico  
 En la tabla siguiente se describe los parámetros asociados con la etiqueta de objeto.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|***IDENTIFICADOR DE CLASE***|Un número único de 128 bits que identifica el tipo de objeto incrustado en el sistema. Este identificador se mantiene en el registro del sistema del equipo local. (Para los identificadores de clase de la **RDS. DataControl** de objetos, consulte [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md).)|  
|***ID***|Define un identificador para todo el documento para el objeto incrustado que se utiliza para identificarlo en el código.|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDS. Parámetros Tag DataControl  
 En la tabla siguiente se describe los parámetros específicos de la **RDS. DataControl** objeto. (Para obtener una lista completa de la **RDS. DataControl** objeto parámetros y cuándo implementarlos, consulte [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md).)  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|[SERVER](../../../ado/reference/rds-api/server-property-rds.md)|Si está utilizando HTTP, el valor es el nombre del equipo servidor precedido por `https://`.|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|Proporciona la información de conexión necesaria para la **RDS. DataControl** para conectarse a SQL Server.|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|Establece o devuelve la cadena de consulta utilizada para recuperar el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).|  
  
## <a name="see-also"></a>Vea también  
 [Botones de comando de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


