---
title: Inicio de sesión de Reporting Services (cuadro de diálogo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 232ee51614a668b07263c3e3a4182f23652135bf
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099868"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Inicio de sesión de Reporting Services (cuadro de diálogo de SSRS)
  Utilice el cuadro de diálogo **Inicio de sesión de Reporting Services** para proporcionar credenciales para publicar informes en el servidor de informes.  
  
-   **Tenga en cuenta** si se trata de la primera vez que se ha publicado un informe en un servidor de informes desde el conjunto de establecer la propiedad de implementación **TargetServerURL** para un proyecto, compruebe que el nombre del servidor especificado es similar a `http://localhost/reportserver`y no `http://localhost/reports`. La consecuencia indirecta de especificar el directorio `reports` del servidor local en lugar del directorio `reportserver` es la apertura de este cuadro de diálogo. Para más información sobre cómo establecer **TargetServerURL**, vea [Establecer propiedades de implementación&#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>Opciones  
 **Server**  
 Muestra el nombre del servidor de informes. Por ejemplo, `http://localhost/reportserver`. Si los servidores de informes usan un puerto distinto del predeterminado, el puerto 80, incluya el número de puerto. Por ejemplo, `http://localhost:81/reportserver`.  
  
 **Nombre de usuario.**  
 Escriba el nombre de usuario con el que iniciar sesión en el servicio web.  
  
 **Contraseña**  
 Escriba la contraseña con la que iniciar sesión en el servicio web.  
  
## <a name="see-also"></a>Vea también  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Especifique la información de credenciales y conexión para orígenes de datos de informe](../report-data/specify-credential-and-connection-information-for-report-data-sources.md) [ayuda de F1 de diseñador de informes](report-designer-f1-help.md)  
  
  
