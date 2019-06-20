---
title: Sección de conexión del archivo de personalización | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c9ec47ffb89724e8a7991dae1d2296aa813e0c5e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704314"
---
# <a name="customization-file-connect-section"></a>Sección de conexión del archivo de personalización
El comportamiento predeterminado del controlador es Denegar todas las conexiones. El **conectar** sección especifica las excepciones de ese comportamiento. Por ejemplo, si todos los **conectar** secciones están ausentes o vacías y, después, de forma predeterminada se pudo establecer ninguna conexión.  
  
 El **conectar** sección puede contener:  
  
-   Una entrada de acceso predeterminada que especifica el valor predeterminado leer y escribir operaciones permitidas en esta conexión. Si no hay ninguna entrada de acceso predeterminada en la sección, se omitirá la sección.  
  
-   Una cadena de conexión nueva que reemplaza la cadena de conexión de cliente.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
 Es una entrada de acceso predeterminada del formulario:  
  
```console
  
Access=  
accessRight  
  
```  
  
 Una entrada de cadena de conexión de reemplazo tiene el formato:  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>Comentarios  
  
|Parte|Descripción|  
|----------|-----------------|  
|**Conectar**|Una cadena literal que indica que esta es una entrada de cadena de conexión.|  
|**_connectionString_**|Cadena que reemplaza la cadena de conexión de cliente completa.|  
|**Acceso**|Una cadena literal que indica que esta es una entrada de acceso.|  
|**_accessRight_**|Uno de los derechos de acceso siguiente:<br /><br /> -   **NoAccess** -usuario no puede obtener acceso al origen de datos.<br />-   **ReadOnly** -usuario puede leer el origen de datos.<br />-   **Lectura y escritura** -usuario puede leer o escribir en el origen de datos.|  
  
 Si desea permitir cualquier conexión (en vigor, deshabilitar el comportamiento predeterminado del controlador), establezca la entrada de acceso el **conectarse de forma predeterminada** sección a `Access=ReadWrite`y elimine o comente cualquier otro **conectar** _identificador_ sección.  
  
## <a name="see-also"></a>Vea también  
 [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sección UserList del archivo personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



