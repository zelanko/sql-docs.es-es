---
title: "Sección UserList del archivo de personalización | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d9e2ea77de53256e075db07b8f809298e74628d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="customization-file-userlist-section"></a>Sección UserList del archivo de personalización
El **userlist** sección pertenece a la **conectar** sección con la misma sección *identificador* parámetro.  
  
 En esta sección puede contener una *entrada de acceso de usuario*, que especifica el acceso de derechos para el usuario especificado y reemplaza el *predeterminado* *tiene acceso a entrada* en debúsquedadecoincidencias**conectar** sección.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
 Una entrada de acceso de usuario tiene el formato:  
  
 *nombre de usuario***=**   
 ***accessRights***  
  
|Parte|Description|  
|----------|-----------------|  
|*nombre de usuario*|El *nombre de usuario* de la persona que utiliza esta conexión. Establece los nombres de usuario válido con IIS **Service Manager** cuadro de diálogo.|  
|***accessRights***|Uno de los siguientes derechos de acceso:<br /><br /> -   **NoAccess** : usuario no puede obtener acceso al origen de datos.<br />-   **ReadOnly** : el usuario puede leer el origen de datos.<br />-   **Lectura y escritura** : usuario puede leer o escribir en el origen de datos.|  
  
## <a name="see-also"></a>Vea también  
 [Sección Connect del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Opciones de cliente necesarias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción de los archivos de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


