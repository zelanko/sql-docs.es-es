---
title: Sección UserList del archivo de personalización | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5feb29337ccd0ee79cd1b6f98187cc6fdb52a942
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130675"
---
# <a name="customization-file-userlist-section"></a>Sección UserList del archivo de personalización
El **userlist** sección pertenece a la **conectar** sección con la misma sección *identificador* parámetro.  
  
 En esta sección puede contener una *entrada de acceso de usuario*, que habilita el acceso a derechos para el usuario especificado y reemplaza el *predeterminada* *tiene acceso a entrada* coincidente**conectar** sección.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
 Es una entrada de acceso de usuario del formulario:  
  
 _Nombre de usuario_ **=**   
 **_accessRights_**  
  
|Parte|Descripción|  
|----------|-----------------|  
|*userName*|El *nombre de usuario* de la persona que utiliza esta conexión. Nombres de usuario válidos se establecen con IIS **Service Manager** cuadro de diálogo.|  
|**_accessRights_**|Uno de los derechos de acceso siguiente:<br /><br /> -   **NoAccess** -usuario no puede obtener acceso al origen de datos.<br />-   **ReadOnly** -usuario puede leer el origen de datos.<br />-   **Lectura y escritura** -usuario puede leer o escribir en el origen de datos.|  
  
## <a name="see-also"></a>Vea también  
 [Sección de conexión del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


