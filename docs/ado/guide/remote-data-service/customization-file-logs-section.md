---
title: Sección Logs del archivo de personalización | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: a368e264-865c-41ee-be00-d9097255c2ea
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c136282f7d337791046d009c9729fefee0d27112
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="customization-file-logs-section"></a>Sección de registros del archivo de personalización
El **registros** sección contiene una entrada de archivo de registro, que especifica el nombre del archivo que registra los errores durante la operación de la **DataFactory**.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
 Un archivo de registro tiene el formato:  
  
```  
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>Comentarios  
  
|Parte|Description|  
|----------|-----------------|  
|**Err**|Una cadena literal que indica que esta es una entrada de archivo de registro.|  
|*FileName*|Un nombre completo de ruta de acceso y el archivo. El nombre de archivo típico es **c:\msdfmap.log**.|  
  
 El archivo de registro contendrá el nombre de usuario, el valor HRESULT, la fecha y la hora de cada error.  
  
## <a name="see-also"></a>Vea también  
 [Sección Connect del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Opciones de cliente necesarias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción de los archivos de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


