---
title: Configuración de propiedades de origen de datos para un informe paginado (SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
ms.assetid: 27af5195-c845-40e0-9a9c-efe569424022
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5e134c81fd697d4aa6fc7e5b620c1a71ff462b73
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "65573193"
---
# <a name="configure-data-source-properties-for-a-paginated-report"></a>Configuración de propiedades de origen de datos para un informe paginado
  Al ejecutar un informe paginado, el servidor de informes recupera la información de las propiedades para determinar la manera de conectarse a un origen de datos. El tipo de origen de datos, la cadena de conexión y la información de credenciales se especifican en las páginas de propiedades Origen de datos del informe publicado. Puede establecer las propiedades para variar la información de conexión a un origen de datos de los valores originales que se especificaron cuando se creó el informe.  
  
 Como alternativa, si tiene un origen de datos compartido predefinido que ya especifica la información de conexión que desear usar, puede especificar un origen de datos compartido en su lugar. Para usar un origen de datos compartido, haga clic en **Un origen de datos compartido** en la página de propiedades Origen de datos del informe.  
  
## <a name="to-configure-an-embedded-data-source"></a>Para configurar un origen de datos incrustado  
  
1.  En el portal web, navegue al informe para el que quiera configurar un origen de datos específico del informe.  
  
3.  Haga clic en los puntos suspensivos ( **...** ) de la esquina superior derecha > **Administrar**.  
  
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
  
 Para obtener más información sobre cómo configurar credenciales, vea [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). Para más información sobre la cuenta de ejecución desatendida, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="see-also"></a>Consulte también  
[Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
[Administrar orígenes de datos de informe](../../reporting-services/report-data/manage-report-data-sources.md)
  
