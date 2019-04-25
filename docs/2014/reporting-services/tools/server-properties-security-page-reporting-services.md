---
title: Propiedades del servidor (página de seguridad) - Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 95c237945cdb21921f04d16adc782ce0b60b533a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62635039"
---
# <a name="server-properties-security-page---reporting-services"></a>Propiedades del servidor (página de seguridad) - Reporting Services
  Use esta página para desactivar características que pueden poner en peligro un servidor de informes. Al desactivar estas características, se limitará alguna funcionalidad, pero puede mejorar la seguridad total del servidor de informes mitigando amenazas concretas.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia del servidor de informes, haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**. Haga clic en **Seguridad** para abrir esta página.  
  
## <a name="options"></a>Opciones  
 **Habilitar la seguridad integrada de Windows para orígenes de datos de informe**  
 Especifique si puede realizarse una conexión a un origen de datos de informe con el token de seguridad de Windows del usuario que solicitó el informe.  
  
 Si desactiva esta característica, la característica de Seguridad integrada de Windows en las páginas de propiedades de origen de dato del informe no estará disponible. Si los orígenes de datos del informe se configuran para la seguridad integrada de Windows y desactiva posteriormente esta característica, el servidor de informes actualizará inmediatamente todas las propiedades de conexión a un origen de datos para solicitar las credenciales.  
  
 **Habilitar la notificación ad hoc**  
 Especifica si los usuarios pueden realizar consultas ad hoc desde un informe del Generador de informes, en el que los nuevos informes se generan automáticamente cuando un usuario hace clic en los datos de interés.  
  
 Al establecer esta opción se determina si la propiedad `EnableLoadReportDefinition` en el servidor de informes está se establece en `True` o `False`. Si borra esta opción, la propiedad se establecerá en `False` y el servidor de informes no generará informes click-through que se crean durante la exploración de datos. Se bloquearán todas las llamadas al método `LoadReportDefinition`.  
  
 Al desactivar esta opción, se mitiga una amenaza en la que un usuario malintencionado inicia un ataque por denegación de servicio sobrecargando el servidor de informes con solicitudes `LoadReportDefinition`.  
  
## <a name="see-also"></a>Vea también  
 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectar con un servidor de informes en Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Especifique la información de credenciales y conexión para orígenes de datos de informes] (.. /Report-Data/Specify-Credential-and-Connection-Information-for-Report-Data-Sources.MD [servidor de informes en Management Studio ayuda F1](report-server-in-management-studio-f1-help.md)  
  
  
