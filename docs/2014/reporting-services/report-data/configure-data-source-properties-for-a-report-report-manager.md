---
title: Configurar propiedades de origen de datos para un informe (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
ms.assetid: 27af5195-c845-40e0-9a9c-efe569424022
caps.latest.revision: 43
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3cd47633f58369b7cb432fbe28382ac93c4fbec7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230615"
---
# <a name="configure-data-source-properties-for-a-report--report-manager"></a>Configurar propiedades de origen de datos para un informe (Administrador de informes)
  Al ejecutar un informe, el servidor de informes recupera información de propiedad para determinar la manera de conectarse a un origen de datos. El tipo de origen de datos, la cadena de conexión y la información de credenciales se especifican en las páginas de propiedades Origen de datos del informe publicado. Puede establecer las propiedades para variar la información de conexión a un origen de datos de los valores originales que se especificaron cuando se creó el informe.  
  
 Como alternativa, si tiene un origen de datos compartido predefinido que ya especifica la información de conexión que desear usar, puede especificar un origen de datos compartido en su lugar. Para usar un origen de datos compartido, haga clic en **Un origen de datos compartido** en la página de propiedades Origen de datos del informe.  
  
### <a name="to-configure-an-embedded-data-source"></a>Para configurar un origen de datos incrustado  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  En el Administrador de informes, navegue hasta la página **Contenido** . Navegue al informe para el que desee configurar un origen de datos específico y abra el informe.  
  
3.  Haga clic en la pestaña **Propiedades** . Se abre la página de propiedades **General**.  
  
4.  Haga clic en la pestaña **Orígenes de datos** . Esto abre la página de propiedades Origen de datos del informe.  
  
5.  Haga clic en **Un origen de datos personalizado** para especificar información de conexión a un origen de datos dentro del informe.  
  
6.  En la lista **Tipo de conexión** , especifique la extensión de procesamiento de datos que se utiliza para procesar datos desde el origen de datos.  
  
7.  En **Cadena de conexión**, especifique la cadena de conexión que usa el servidor de informes para conectarse al origen de datos. Se recomienda que no especifique credenciales en la cadena de conexión.  
  
     En el ejemplo siguiente, se muestra una cadena de conexión para establecer conexión con la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] local:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  En **Conectar utilizando**, especifique cómo se obtienen las credenciales cuando se ejecuta el informe:  
  
    -   Si desea solicitar al usuario un nombre de inicio de sesión y una contraseña, haga clic en **Credenciales suministradas por el usuario que ejecuta el informe**.  
  
    -   Si va a usar el origen de datos con informes que son compatibles con suscripciones u otras operaciones programadas (por ejemplo, la generación automatizada de historiales de informes), haga clic en **Credenciales almacenadas de forma segura en el servidor de informes**.  
  
    -   Si desea que el servidor de informes envíe las credenciales del usuario que tiene acceso al informe al servidor que hospeda el origen de datos externo, haga clic en **Seguridad integrada de Windows NT**. En este caso, no se solicita al usuario que escriba un nombre de usuario ni una contraseña.  
  
    -   Si el origen de datos no usa credenciales (por ejemplo, si el origen de datos es un archivo XML al que se tiene acceso desde el sistema de archivos), haga clic en **No se necesitan credenciales**. Solo debería especificar este tipo de credencial si es válido para el origen de datos. Si selecciona esta opción para un origen de datos que requiere autenticación, se producirá un error en la conexión. Si selecciona esta opción, asegúrese de que configura la cuenta de ejecución desatendida que permite al servidor de informes conectar a otros equipos para recuperar datos o archivos cuando las credenciales del usuario no están disponibles.  
  
 Para obtener más información sobre cómo configurar credenciales, vea [especificar credenciales y la información de conexión de orígenes de datos de informe](specify-credential-and-connection-information-for-report-data-sources.md). Para más información sobre la cuenta de ejecución desatendida, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="see-also"></a>Vea también  
 [El contenido de página &#40;el Administrador de informes&#41;](../contents-page-report-manager.md)   
 [Nuevo origen de datos &#40;página del Administrador de informes&#41;](../new-data-source-page-report-manager.md)   
 [Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)   
 [Administrar orígenes de datos de informe](manage-report-data-sources.md)   
 [Crear, eliminar o modificar un origen de datos compartido &#40;el Administrador de informes&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Orígenes de datos &#40;página de propiedades del Administrador de informes&#41;](../data-sources-properties-page-report-manager.md)  
  
  
