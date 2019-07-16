---
title: Descripción del archivo de personalización | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81a73044c1ab413fb2b49286814f3e6b3951c6c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921969"
---
# <a name="understanding-the-customization-file"></a>Descripción del archivo de personalización
Cada encabezado de sección en el archivo de personalización consta de los corchetes ( **[]** ) que contiene un tipo y un parámetro. Los cuatro tipos de sección se indican mediante las cadenas literales **conectar**, **sql**, **userlist**, o **registros**. El parámetro es la cadena literal, el valor predeterminado, un identificador especificado por el usuario o nada.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por lo tanto, cada sección se marca con uno de los siguientes encabezados de sección:  
  
```console
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 Los encabezados de sección tienen los siguientes elementos.  
  
|Parte|Descripción|  
|----------|-----------------|  
|**connect**|Una cadena literal que modifica una cadena de conexión.|  
|**sql**|Una cadena literal que modifica una cadena de comandos.|  
|**userlist**|Una cadena literal que modifica los derechos de acceso de un usuario específico.|  
|**logs**|Una cadena literal que especifica un archivo de registro de grabación errores operativos.|  
|**default**|Una cadena literal que se usa si se ha especificado o se encuentra ningún identificador.|  
|*identifier*|Una cadena que coincide con una cadena en el **conectar** o **comando** cadena.<br /><br /> -Utilice esta sección si contiene el encabezado de sección **conectar** y la cadena de identificador se encuentra en la cadena de conexión.<br />-Utilice esta sección si contiene el encabezado de sección **sql** y la cadena de identificador se encuentra en la cadena de comandos.<br />-Utilice esta sección si contiene el encabezado de sección **userlist** y la cadena de identificador coincide con un **conectar** identificador de la sección.|  
  
 El **DataFactory** llama al controlador, pasando los parámetros de cliente. El controlador busca cadenas completas en los parámetros de cliente que coinciden con los identificadores en los encabezados de la sección correspondiente. Si se encuentra una coincidencia, el contenido de esa sección se aplica al parámetro de cliente.  
  
 Una sección concreta se usa en las siguientes circunstancias:  
  
-   Un **conectar** sección se usa si la parte del valor del cliente conecta la palabra clave de cadena, "**origen de datos =** _valor_", coincide con un **conectar** identificador de la sección. 
  
-   Un **sql** sección se usa si la cadena de comandos de cliente contiene una cadena que coincide con un **sql** identificador de la sección.  
  
-   Un **conectar** o **sql** sección con un parámetro predeterminado se usa si no hay ningún identificador coincidente.  
  
-   Un **userlist** sección se usa si el **userlist** sección identificador coincidencias un **conectar** identificador de la sección. Si hay una coincidencia, el contenido de la **userlist** sección se aplican a la conexión que se rige por el **conectar** sección.  
  
-   Si la cadena en una cadena de conexión o un comando no coincide con el identificador en cualquier **conectar** o **sql** encabezado de sección y no hay ningún **conectar** o **sql**  sección de encabezado con un parámetro predeterminado, a continuación, se usa la cadena de cliente sin modificación.  
  
-   El **registros** sección se usa siempre que el **DataFactory** está en funcionamiento.  
  
## <a name="see-also"></a>Vea también  
 [Sección de conexión del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sección UserList del archivo personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

