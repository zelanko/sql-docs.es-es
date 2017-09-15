---
title: "Comprender el archivo de personalización | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cadf89ac579b11ab829ecd288fec77df81eb0603
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-the-customization-file"></a>Descripción de los archivos de personalización
Cada encabezado de sección en el archivo de personalización consta de corchetes (**[]**) que contiene un tipo y un parámetro. Los cuatro tipos de sección se indican mediante las cadenas literales **conectar**, **sql**, **userlist**, o **registros**. El parámetro es la cadena literal, el valor predeterminado, un identificador especificado por el usuario o nada.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por lo tanto, cada sección se marca con uno de los encabezados de la sección siguiente:  
  
```  
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 Los encabezados de sección tienen los siguientes elementos.  
  
|Parte|Description|  
|----------|-----------------|  
|**conectar**|Una cadena literal que modifica una cadena de conexión.|  
|**SQL**|Una cadena literal que modifica una cadena de comandos.|  
|**lista de usuarios**|Una cadena literal que modifica los derechos de acceso de un usuario específico.|  
|**registros**|Una cadena literal que especifica un archivo de registro de errores operacionales de grabación.|  
|**valor predeterminado**|Una cadena literal que se usa si se especifica o se encuentra ningún identificador.|  
|*identificador*|Una cadena que coincide con una cadena en el **conectar** o **comando** cadena.<br /><br /> -Utilice esta sección si el encabezado de sección contiene **conectar** y se encuentra la cadena de identificador en la cadena de conexión.<br />-Utilice esta sección si el encabezado de sección contiene **sql** y se encuentra la cadena de identificador en la cadena de comandos.<br />-Utilice esta sección si el encabezado de sección contiene **userlist** y la cadena de identificador coincide con un **conectar** identificador de la sección.|  
  
 El **DataFactory** llama al controlador, pasando parámetros de cliente. El controlador busca cadenas completas en los parámetros de cliente que coincide con los identificadores en los encabezados de la sección correspondiente. Si se encuentra una coincidencia, el contenido de esa sección se aplica a los parámetros de cliente.  
  
 Una sección concreta se usa en las siguientes circunstancias:  
  
-   A **conectar** sección se usa si la parte del valor del cliente conecta la palabra clave de cadena, "**origen de datos =***valor*", coincide con un **conectar** identificador de la sección*.*  
  
-   Un **sql** sección se usa si la cadena de comandos de cliente contiene una cadena que coincide con un **sql** identificador de la sección.  
  
-   A **conectar** o **sql** sección con un parámetro predeterminado se utiliza si no hay ningún identificador coincidente.  
  
-   A **userlist** sección se usa si la **userlist** sección identificador coincidencias un **conectar** identificador de la sección. Si se encuentra una coincidencia, el contenido de la **userlist** sección se aplican a la conexión que rige la **conectar** sección.  
  
-   Si la cadena en una cadena de conexión o de comandos no coincide con el identificador en cualquier **conectar** o **sql** encabezado de sección y no hay ningún **conectar** o **sql ** sección encabezado con un parámetro predeterminado, a continuación, se usa la cadena de cliente sin modificación.  
  
-   El **registros** sección se usa siempre que el **DataFactory** está en funcionamiento.  
  
## <a name="see-also"></a>Vea también  
 [Sección Connect del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Opciones de cliente necesarias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Escribir su propio controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)





















