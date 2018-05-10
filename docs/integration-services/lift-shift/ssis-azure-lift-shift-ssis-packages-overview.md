---
title: Migrar cargas de trabajo de SQL Server Integration Services a la nube mediante lift-and-shift | Microsoft Docs
ms.date: 04/13/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4d3632ff64964f2cdd29778ee2ee700519aff3e8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>Migrar cargas de trabajo de SQL Server Integration Services a la nube mediante lift-and-shift
Los paquetes y las cargas de trabajo de SQL Server Integration Services (SSIS) se pueden mover ahora a la nube de Azure.
-   Almacene y administre paquetes y proyectos de SSIS en la base de datos del catálogo de SSIS (SSISDB) en Azure SQL Database o Instancia administrada de SQL Database (versión preliminar).
-   Ejecute paquetes en una instancia de Azure SSIS Integration Runtime, que se presentó como parte de Azure Data Factory versión 2.
-   Use herramientas conocidas, como SQL Server Management Studio (SSMS) para estas tareas comunes.

## <a name="benefits"></a>Ventajas
El movimiento de las cargas de trabajo de SSIS local a Azure presenta las siguientes ventajas potenciales:
-   **Reduce los costos operativos** y disminuye la carga de administrar la infraestructura que tiene cuando ejecuta SSIS localmente en máquinas virtuales de Azure.
-   **Aumenta la alta disponibilidad** con la capacidad de especificar varios nodos por clúster, así como las características de alta disponibilidad de Azure y de Azure SQL Database.
-   **Aumenta la escalabilidad** con la capacidad de especificar varios núcleos por nodo (escalabilidad vertical) y varios nodos por clúster (escalabilidad horizontal).

## <a name="architecture-overview"></a>Información general sobre la arquitectura
En la tabla siguiente se resaltan las diferencias entre SSIS local y SSIS en Azure. La diferencia más importante es la separación del almacenamiento y el proceso.

| Storage | Tiempo de ejecución | Escalabilidad |
|---|---|---|
| Local (SQL Server) | Tiempo de ejecución de SSIS hospedado por SQL Server | Escalabilidad horizontal de SSIS (en SQL Server 2017 y versiones posteriores)<br/><br/>Soluciones personalizadas (en versiones anteriores de SQL Server) |
| En Azure [SQL Database o Instancia administrada de SQL Database (versión preliminar)] | Azure SSIS Integration Runtime, un componente de Azure Data Factory versión 2. | Opciones de escalabilidad para SSIS IR |
| | | |

Azure Data Factory hospeda el motor en tiempo de ejecución para paquetes SSIS en Azure. El motor en tiempo de ejecución se denomina Azure SSIS Integration Runtime (SSIS IR).

Al aprovisionar SSIS IR, puede realizar la escalabilidad vertical y horizontal especificando los valores de las siguientes opciones:
-   El tamaño del nodo (incluido el número de núcleos) y el número de nodos del clúster.
-   La instancia existente de Azure SQL Database para hospedar la base de datos del catálogo de SSIS (SSISDB), y el nivel de servicio de la base de datos.
-   Las ejecuciones en paralelo máximas por nodo.

Solamente debe aprovisionar SSIS IR una vez. Después de eso, puede usar herramientas conocidas, como SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) para implementar, configurar, ejecutar, supervisar, programar y administrar paquetes.

> [!NOTE]
> Durante esta versión preliminar pública, Azure SSIS Integration Runtime no está disponible aún en todas las regiones. Para obtener información acerca de las regiones admitidas, consulte [Productos disponibles por región - Microsoft Azure](https://azure.microsoft.com/regions/services/).

Data Factory también admite otros tipos de Integration Runtime. Para obtener más información sobre SSIS IR y los otros tipos de Integration Runtime, vea [Integration Runtime en Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime).

## <a name="version-info"></a>Información de la versión

Puede implementar en Azure un paquete creado con cualquier versión de SSIS. Al implementar un paquete en Azure, si no hay ningún error de validación, el paquete se actualiza automáticamente al formato de paquete más reciente. Dicho de otra manera, siempre se actualiza a la versión más reciente de SSIS.

El proceso de implementación valida los paquetes para garantizar que se puedan ejecutar en Azure-SSIS Integration Runtime. Para obtener más información, vea [Validación de paquetes de SSIS implementados en Azure](ssis-azure-validate-packages.md).

## <a name="prerequisites"></a>Prerequisites

Las funcionalidades descritas en este artículo requieren las siguientes versiones de SQL Server Data Tools (SSDT):
-   Para Visual Studio 2017, versión 15.3 (versión preliminar) o una versión posterior.
-   Para Visual Studio 2015, versión 17.2 o una versión posterior.

Para obtener más información sobre los requisitos previos de Azure, vea [Implementación de paquetes SSIS en Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal).

## <a name="provision-ssis-on-azure"></a>Aprovisionar SSIS en Azure
Para poder implementar y ejecutar paquetes SSIS en Azure, debe aprovisionar la base de datos del catálogo de SSIS (SSISDB) y Azure SSIS Integration Runtime. Siga los pasos de aprovisionamiento del artículo [Implementación de paquetes SSIS en Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal).

El **nombre de SQL Database** que hospeda SSISDB se convierte en la primera parte del nombre de cuatro partes que se usará al implementar y administrar paquetes de SSDT y SSMS (`<sql_database_name>.database.windows.net`).

Para obtener información sobre cómo conectarse a la base de datos del catálogo de SSIS, vea [Conectarse a la base de datos del catálogo de SSISDB en Azure](ssis-azure-connect-to-catalog-database.md).

## <a name="design-packages"></a>Diseñar paquetes
Debe continuar con el **diseño y la compilación de paquetes** localmente en SSDT, o bien en Visual Studio con SSDT instalado.

Para obtener información sobre cómo conectarse a orígenes de datos locales desde la nube con la **autenticación de Windows**, vea [Conectarse a orígenes de datos locales y a recursos compartidos de archivos de Azure con la autenticación de Windows](ssis-azure-connect-with-windows-auth.md).

Para obtener información sobre cómo conectarse a los archivos y recursos compartidos de archivos, vea [Almacenar y recuperar archivos en recursos compartidos de archivos de forma local y en Azure con SSIS](ssis-azure-files-file-shares.md).

Al aprovisionar una instancia de SQL Database para hospedar SSISDB, también se instalan Azure Feature Pack para SSIS y el componente redistribuible de Access. Estos componentes proporcionan conectividad a varios orígenes de datos de **Azure** y a archivos de **Excel y Access**, así como a los orígenes de datos compatibles con los componentes integrados.

También puede instalar otros componentes. Para obtener más información, consulte [Custom setup for the Azure-SSIS integration runtime](/azure/articles/data-factory/how-to-configure-azure-ssis-ir-custom-setup.md) (Configuración personalizada de Integration Runtime de SSIS de Azure).

## <a name="deploy-and-run-packages"></a>Implementar y ejecutar paquetes
Tiene que usar el **modelo de implementación de proyectos**, y no el modelo de implementación de paquetes, al implementar proyectos en SSISDB en Azure.

Para implementar proyectos y ejecutar paquetes en Azure, puede usar una de las distintas herramientas conocidas y opciones de scripting:
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (de SSMS, Visual Studio Code u otra herramienta)
-   Una herramienta de línea de comandos
-   PowerShell
-   C# y el modelo de objetos de administración de SSIS

Para comenzar, consulte [Implementar, ejecutar y supervisar un paquete SSIS en Azure](ssis-azure-deploy-run-monitor-tutorial.md).

## <a name="monitor-packages"></a>Supervisar paquetes
Para supervisar paquetes en ejecución en SSMS, puede usar una de las siguientes herramientas de informes de SSMS.
-   Haga clic con el botón derecho en **SSISDB** y, a continuación, seleccione **Operaciones activas** para abrir el cuadro de diálogo **Operaciones activas**.
-   Seleccione un paquete en el Explorador de objetos, haga clic con el botón derecho y seleccione **Informes**. A continuación, elija **Informes estándar** y **Todas las ejecuciones**.

## <a name="schedule-packages"></a>Programar paquetes
Para programar la ejecución de paquetes almacenados en SQL Database, puede usar las siguientes herramientas:
-   Agente SQL Server local
-   Actividad de procedimiento almacenado de SQL Server de Azure Data Factory

Para obtener más información, consulte [Programar la ejecución de paquetes SSIS en Azure](ssis-azure-schedule-packages.md).

## <a name="next-steps"></a>Pasos siguientes
Para comenzar con las cargas de trabajo de SSIS en Azure, consulte los artículos siguientes:
-   [Implementación de paquetes SSIS en Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)
-   [Deploy, run, and monitor an SSIS package on Azure](ssis-azure-deploy-run-monitor-tutorial.md) (Implementar, ejecutar y supervisar un paquete SSIS en Azure)
