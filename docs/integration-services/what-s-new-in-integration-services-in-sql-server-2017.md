---
title: "¿Qué &#39; s de Integration Services en SQL Server de 2017 | Documentos de Microsoft"
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 2d47d1bb82b586890e3bfc250cf09e929a64fb25
ms.contentlocale: es-es
ms.lasthandoff: 08/23/2017

---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>¿Qué &#39; s de Integration Services en SQL Server de 2017
En este tema, se describen las características que se han agregado o actualizado en [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].

>   [!NOTE]
> SQL Server 2017 también incluye las características de SQL Server 2016 y las características agregadas en las actualizaciones de SQL Server 2016. Para obtener información sobre las nuevas características de SSIS en SQL Server 2016, consulte [Novedades de Integration Services en SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md).

## <a name="highlights-of-this-release"></a>Aspectos destacados de esta versión

Estos son las características nuevas más importantes de Integration Services para SQL Server 2017.

-   **Escalar horizontalmente**. Distribuir la ejecución de paquetes SSIS más fácilmente en varios equipos de trabajo y administrar ejecuciones y los trabajadores de un único equipo maestro. Para obtener más información, consulte [horizontalmente Integration Services](../integration-services/scale-out/integration-services-ssis-scale-out.md).

-   **Servicios de integración en Linux**. Ejecutar paquetes SSIS en equipos Linux. Para obtener más información, consulte [de extracción, transformación y carga datos en Linux con SSIS](../linux/sql-server-linux-migrate-ssis.md).

-   **Mejoras de la conectividad**. Conectarse a las fuentes de OData de Microsoft Dynamics AX Online y Microsoft Dynamics CRM Online con los componentes actualizados de OData. 

## <a name="new-in-the-azure-feature-pack"></a>Nuevo en el Feature Pack de Azure

Además de las mejoras de conectividad en SQL Server Integration Services Feature Pack para Azure ha agregado compatibilidad para almacén de Azure Data Lake. Para obtener más información, consulte [Azure Feature Pack para Integration Services (SSIS)](azure-feature-pack-for-integration-services-ssis.md).

## <a name="new-in-sql-server-data-tools-ssdt"></a>Nuevo en SQL Server Data Tools (SSDT)

Ahora puede desarrollar proyectos de SSIS y paquetes destinados a versiones de SQL Server 2012 a través de 2017 en 2017 de Visual Studio o en Visual Studio 2015. Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>Nuevo en SSIS en SQL Server de 2017 RC1

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>Características nuevas y modificadas en horizontalmente para SSIS

-   Patrón de escalabilidad horizontal ahora admite alta disponibilidad. Puede habilitar Always On para SSISDB y configurar para el servidor de agrupación en clústeres de conmutación por error de Windows Server que hospeda el servicio escala Out maestro. Al aplicar este cambio al maestro fuera de la escala, evitar un único punto de error y proporcionar una alta disponibilidad para la implementación completa horizontalmente.
-   Se mejoró el control de conmutación por error de los registros de ejecución de Trabajadores de escalabilidad horizontal. Los registros de ejecución se guardan en disco local en caso de que el trabajador de salida de escala se detiene inesperadamente. Posteriormente, cuando se reinicia el trabajo, vuelve a cargar los registros persistentes y continúa guardarlas en SSISDB.
-   Se cambió el nombre del parámetro *runincluster* del procedimiento almacenado **[catálogo].[create_execution]** a *runinscaleout* para mejorar la coherencia y la legibilidad. Este cambio de nombre del parámetro tiene las siguientes consecuencias:
    -   Si tiene secuencias de comandos existentes para ejecutar paquetes en horizontalmente, tendrá que cambiar el nombre del parámetro de *runincluster* a *runinscaleout* para que las secuencias de comandos funcione en RC1.
    -   SQL Server Management Studio (SSMS) 17.1 y versiones anteriores no se pueden activar la ejecución del paquete en horizontalmente en RC1. El mensaje de error es este: "*@runincluster* no es un parámetro para el procedimiento **create_execution**". Este problema se corrige en la versión siguiente de SSMS, la versión 17.2. 17.2 y versiones posteriores de SSMS admite la nueva ejecución de paquete y el nombre de parámetro en horizontalmente. Hasta que SSMS versión 17,2 está disponible para solucionar este problema, puede usar la versión existente de SSMS para generar el script de ejecución de paquetes y después cambiar el nombre de la *runincluster* parámetro *runinscaleout* en la secuencia de comandos y ejecute el script.
-   El catálogo de SSIS tiene una nueva propiedad global para especificar el modo predeterminado de ejecución de los paquetes de SSIS. Esta nueva propiedad se aplica cuando se llama a la **[catalog]. [ create_execution]** procedimiento almacenado con el *runinscaleout* parámetro establecido en null. Este modo también se aplica a trabajos del Agente SQL de SSIS. Puede establecer la propiedad global nuevo en el cuadro de diálogo de propiedades para el nodo SSISDB en SSMS, o con el siguiente comando:
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>Nuevo en SSIS en la CTP de SQL Server de 2017 2.1

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>Características nuevas y modificadas en horizontalmente para SSIS

-   Ahora puede usar el **Use32BitRuntime** parámetro cuando se desencadena la ejecución en horizontalmente.
-   Se ha mejorado el rendimiento de inicio de sesión para SSISDB para ejecuciones de paquetes en horizontalmente. Ahora, los registros de mensaje de evento y el contexto del mensaje se escriben en SSISDB en modo por lotes en lugar de uno a uno. Estas son algunas notas adicionales sobre esta mejora:        
    - Algunos informes en la versión actual de SQL Server Management Studio (SSMS) actualmente no mostrar estos registros para las ejecuciones en horizontalmente. Prevemos que se admitirán en la próxima versión de SSMS. Los informes afectados incluyen la *todas las conexiones* informe, el *contexto del Error* informes y el *información de conexión* sección en el panel de servicios de integración.
    - Una nueva columna **event_message_guid** se ha agregado. Utilice esta columna para unir [catalog]. la vista [event_message_context] y [catalog]. ver [event_messages] en lugar de usar **event_message_id** al consultar estos registros de ejecuciones en horizontalmente.
-   Para obtener la aplicación de administración para SSIS horizontalmente, [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.1 o una versión posterior.

## <a name="new-in-ssis-in-sql-server-2017-ctp-20"></a>Nuevo en SSIS en SQL Server de 2017 CTP 2.0

No hay ningún nuevas características SSIS en SQL Server de 2017 CTP 2.0.

## <a name="new-in-ssis-in-sql-server-2017-ctp-14"></a>Nuevo en SSIS en la CTP de SQL Server de 2017 1.4

No hay ningún nuevas características SSIS en 1.4 de CTP de SQL Server de 2017.

## <a name="new-in-ssis-in-sql-server-2017-ctp-13"></a>Nuevo en SSIS en la CTP de SQL Server de 2017 1.3

No hay ningún nuevas características SSIS en 1.3 de CTP de SQL Server de 2017.

## <a name="new-in-ssis-in-sql-server-2017-ctp-12"></a>Nuevo en SSIS en la CTP de SQL Server de 2017 1.2

No hay ningún nuevas características SSIS en SQL Server de 2017 CTP 1.2.

## <a name="new-in-ssis-in-sql-server-2017-ctp-11"></a>Nuevo en SSIS en la CTP de SQL Server de 2017 1.1

No hay ningún nuevas características SSIS en SQL Server de 2017 CTP 1.1.

## <a name="new-in-ssis-in-sql-server-2017-ctp-10"></a>Nuevo en SSIS en SQL Server de 2017 CTP 1.0

### <a name="scale-out-for-ssis"></a>Escalado horizontal para SSIS

La característica de escalado horizontal facilita mucho la ejecución de [!INCLUDE[ssIS_md](../includes/ssis-md.md)] en varios equipos. 
   
Después de instalar el patrón y los trabajadores de escalado horizontal, se puede distribuir el paquete para su ejecución automática en diferentes trabajadores. Si la ejecución finaliza inesperadamente, se vuelve a intentar automáticamente. Además, todas las ejecuciones y los trabajadores pueden administrarse de manera centralizada mediante el patrón.
   
Para obtener más información, consulte [Escalado horizontal de Integration Services](../integration-services/scale-out/integration-services-ssis-scale-out.md).
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Compatibilidad con recursos de Microsoft Dynamics Online

El origen OData y el administrador de conexiones OData ahora admiten la conexión a fuentes de OData de Microsoft Dynamics AX Online y Microsoft Dynamics CRM Online.


