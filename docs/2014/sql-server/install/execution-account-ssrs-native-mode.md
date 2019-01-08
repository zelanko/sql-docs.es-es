---
title: Cuenta de ejecución (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.executionaccount.F1
ms.assetid: 440b5a09-5fd4-4c3a-b510-f3c33cbf1c82
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9ba41b602ec91516e87b7fe5ec0276c586b17613
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352980"
---
# <a name="execution-account-ssrs-native-mode"></a>Cuenta de ejecución (Modo nativo de SSRS)
  Utilice esta página para configurar una cuenta que se utilizará en el procesamiento en modo desatendido. Esta cuenta se utiliza bajo circunstancias especiales cuando no están disponibles otros orígenes de credenciales:  
  
-   Cuando el servidor de informes se conecta a un origen de datos que no requiere credenciales. Entre los ejemplos de orígenes de datos que quizás no exijan credenciales se incluyen los documentos XML y algunas aplicaciones de base de datos del lado cliente.  
  
-   Cuando el servidor de informes se conecta a otro servidor para recuperar archivos de imágenes u otros recursos externos a los que se hace referencia en un informe.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 La configuración de esta cuenta es opcional, aunque si no se configura, se limita el uso de las conexiones e imágenes externas a algunos orígenes de datos. Cuando se recuperan archivos de imagen externos, el servidor de informes comprueba si se puede realizar una conexión anónima. Si la conexión está protegida por contraseña, el servidor de informes utiliza la cuenta de procesamiento desatendido de informes para conectar con el servidor remoto. Cuando se recuperan datos de un informe, el servidor de informes suplanta al usuario actual, solicita al usuario que proporcione credenciales, utiliza credenciales almacenadas o utiliza la cuenta de procesamiento desatendido si la conexión de origen de datos especifica **Ninguno** como tipo de credencial. El servidor de informes no permite que sus credenciales de cuenta de servicio sean delegadas ni suplantadas cuando se realiza una conexión con otro equipo, por lo que tiene que utilizar la cuenta de procesamiento desatendido si no hay otras credenciales disponibles.  
  
 La cuenta que especifique debe ser distinta a la utilizada para ejecutar la cuenta de servicio. Si configura esta cuenta, se almacena en el archivo RSReportServer.config como un valor cifrado. Si ejecuta el servidor de informes en una implementación que admita la ampliación a varios servidores, debe configurar esta cuenta del mismo modo en cada servidor de informes.  
  
 Puede utilizar cualquier cuenta de usuario de Windows. Para obtener mejores resultados, elija una cuenta que tenga permisos de lectura y de inicio de sesión en red para que admita conexiones con otros equipos. Debe tener permisos de lectura para todas las imágenes o archivos de datos externos que desee utilizar en sus informes. No especifique ninguna cuenta local a no ser que todos los orígenes de datos de informe e imágenes externas estén almacenados en el equipo del servidor de informes. Utilice la cuenta solo para el procesamiento de informes en modo desatendido.  
  
> [!NOTE]  
>  Si está utilizando [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] con Advanced Services, solo tiene que configurar esta cuenta si va a hacer referencia a las imágenes externas de un informe y se necesita permiso para obtener acceso al archivo de imagen. SQL Server Express no admite la conexión del origen de datos a un servidor remoto. Para una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Características compatibles con las ediciones de SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473).  
  
 Para abrir esta página, inicie el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y seleccione **Cuenta de ejecución** en el panel de navegación. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opciones  
 **Especificar una cuenta de ejecución**  
 Seleccione para especificar una cuenta.  
  
 **Cuenta**  
 Especifique una cuenta de usuario de dominio de Windows. Use este formato: *\<dominio>\\<cuenta de usuario\>*.  
  
 **Contraseña**  
 Escriba la contraseña.  
  
 **Confirmar contraseña**  
 Vuelva a escribir la contraseña.  
  
## <a name="see-also"></a>Vea también  
 [Temas de Ayuda de F1 de administrador de configuración de Reporting Services &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
  
  
