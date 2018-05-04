---
title: Sección Connect del archivo de personalización | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12d1560220a9c281425a1d75c43f0ef95845d611
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="customization-file-connect-section"></a>Sección Connect del archivo de personalización
El comportamiento predeterminado del controlador es Denegar todas las conexiones. El **conectar** sección especifica las excepciones de ese comportamiento. Por ejemplo, si todos los **conectar** secciones están ausentes o vacías, a continuación, de forma predeterminada no se pudo establecer ninguna conexión.  
  
 El **conectar** sección puede contener:  
  
-   Una entrada de acceso predeterminada que especifica el valor predeterminado de lectura y escritura operaciones permitidas en esta conexión. Si no hay ninguna entrada de acceso predeterminada en la sección, se omitirá la sección.  
  
-   Una nueva cadena de conexión que reemplaza la cadena de conexión de cliente.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
 Una entrada de acceso predeterminada tiene el formato:  
  
```  
  
Access=  
accessRight  
  
```  
  
 Una entrada de cadena de conexión de reemplazo tiene el formato:  
  
```  
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>Comentarios  
  
|Parte|Description|  
|----------|-----------------|  
|**Conectar**|Una cadena literal que indica que esta es una entrada de cadena de conexión.|  
|***connectionString***|Cadena que reemplaza la cadena de conexión de cliente completa.|  
|**Acceso**|Una cadena literal que indica que esta es una entrada de acceso.|  
|***accessRight***|Uno de los siguientes derechos de acceso:<br /><br /> -   **NoAccess** : usuario no puede obtener acceso al origen de datos.<br />-   **ReadOnly** : el usuario puede leer el origen de datos.<br />-   **Lectura y escritura** : usuario puede leer o escribir en el origen de datos.|  
  
 Si desea permitir cualquier conexión (de hecho, deshabilitar el comportamiento predeterminado del controlador), establezca la entrada de acceso en la **conectarse de forma predeterminada** sección a `Access=ReadWrite`y eliminar o marque como comentario cualquier otro **conectar** *identificador* sección.  
  
## <a name="see-also"></a>Vea también  
 [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Opciones de cliente necesarias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción de los archivos de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



