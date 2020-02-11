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
ms.openlocfilehash: 558fd9c8379808e6c2f109a9c9584e8831cddd0f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922766"
---
# <a name="customization-file-userlist-section"></a>Sección UserList del archivo de personalización
La sección **userList** pertenece a la sección **Connect** con el mismo parámetro de *identificador* de sección.  
  
 Esta sección puede contener una *entrada de acceso de usuario*, que especifica derechos de acceso para el usuario especificado e invalida la *entrada de acceso* *predeterminada* en la sección **conexión** coincidente.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
 Una entrada de acceso de usuario tiene el siguiente formato:  
  
 _nombre de usuario_**=**   
 **_accessRights_**  
  
|Parte|Descripción|  
|----------|-----------------|  
|*Nombre*|El *nombre de usuario* de la persona que emplea esta conexión. Los nombres de usuario válidos se establecen con el cuadro de diálogo de **Service Manager** de IIS.|  
|**_accessRights_**|Uno de los siguientes derechos de acceso:<br /><br /> -   **NoAccess** : el usuario no puede tener acceso al origen de datos.<br />-   **ReadOnly** : el usuario puede leer el origen de datos.<br />-   **ReadWrite** : el usuario puede leer o escribir en el origen de datos.|  
  
## <a name="see-also"></a>Consulte también  
 [Sección de conexión del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros de archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección SQL de archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


