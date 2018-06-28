---
title: Implementar y ejecutar paquetes SSIS en Azure | Microsoft Docs
description: Obtenga información sobre cómo se pueden mover los proyectos, paquetes y cargas de trabajo de SQL Server Integration Services (SSIS) a la nube de Microsoft Azure.
ms.date: 06/07/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0fa7a72e86f596cd0e5d18a0c0dbeb1015233f20
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403297"
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>Migrar cargas de trabajo de SQL Server Integration Services a la nube mediante lift-and-shift
Ahora los proyectos, paquetes y cargas de trabajo de SQL Server Integration Services (SSIS) se pueden mover a la nube de Azure.
-   Almacene y administre paquetes y proyectos de SSIS en el catálogo de SSIS (SSISDB) en Azure SQL Database o Instancia administrada de SQL Database (versión preliminar).
-   Ejecute paquetes en una instancia de Azure SSIS Integration Runtime, un componente de Azure Data Factory.
-   Use herramientas conocidas, como SQL Server Management Studio (SSMS), para llevar a cabo tareas comunes.

## <a name="benefits"></a>Ventajas
El movimiento de las cargas de trabajo de SSIS local a Azure presenta las siguientes ventajas potenciales:
-   **Reduce los costos operativos** y disminuye la carga de administrar la infraestructura que tiene cuando ejecuta SSIS localmente en máquinas virtuales de Azure.
-   **Aumenta la alta disponibilidad** con la capacidad de especificar varios nodos por clúster, así como las características de alta disponibilidad de Azure y de Azure SQL Database.
-   **Aumenta la escalabilidad** con la capacidad de especificar varios núcleos por nodo (escalabilidad vertical) y varios nodos por clúster (escalabilidad horizontal).

## <a name="architecture-overview"></a>Información general sobre la arquitectura
En la tabla siguiente se resaltan las diferencias entre SSIS local y SSIS en Azure. La diferencia más importante es la separación del almacenamiento y el tiempo de ejecución. Azure Data Factory hospeda el motor en tiempo de ejecución para paquetes SSIS en Azure. El motor en tiempo de ejecución se denomina Azure SSIS Integration Runtime (Azure SSIS IR). Para más información, vea [Azure SSIS Integration Runtime](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime).

| Storage | Tiempo de ejecución | Escalabilidad |
|---|---|---|
| Local (SQL Server) | Tiempo de ejecución de SSIS hospedado por SQL Server | Escalabilidad horizontal de SSIS (en SQL Server 2017 y versiones posteriores)<br/><br/>Soluciones personalizadas (en versiones anteriores de SQL Server) |
| En Azure [SQL Database o Instancia administrada de SQL Database (versión preliminar)] | Azure SSIS Integration Runtime, un componente de Azure Data Factory | Opciones de escalado de Azure SSIS Integration Runtime |
| | | |

Solo tiene que aprovisionar Azure SSIS IR una vez. Después de eso, puede usar herramientas conocidas, como SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) para implementar, configurar, ejecutar, supervisar, programar y administrar paquetes.

## <a name="version-support"></a>Compatibilidad de versiones

Puede implementar en Azure un paquete creado con cualquier versión de SSIS. Al implementar un paquete en Azure, si no hay ningún error de validación, el paquete se actualiza automáticamente al formato de paquete más reciente. Dicho de otra manera, siempre se actualiza a la versión más reciente de SSIS.

El proceso de implementación valida los paquetes para garantizar que se puedan ejecutar en Azure-SSIS Integration Runtime. Para obtener más información, vea [Validación de paquetes de SSIS implementados en Azure](ssis-azure-validate-packages.md).

## <a name="prerequisites"></a>Prerequisites

Para implementar paquetes de SSIS en Azure, debe disponer de una de las siguientes versiones de SQL Server Data Tools (SSDT):
-   Para Visual Studio 2017, versión 15.3 o una versión posterior.
-   Para Visual Studio 2015, versión 17.2 o una versión posterior.

Para obtener información sobre los requisitos previos de Azure SSIS Integration Runtime, vea [Implementar y ejecutar un paquete SSIS en Azure: requisitos previos](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure#prerequisites).

> [!NOTE]
> Durante esta versión preliminar pública, Azure SSIS Integration Runtime no está disponible aún en todas las regiones. Para obtener información acerca de las regiones admitidas, consulte [Productos disponibles por región - Microsoft Azure](https://azure.microsoft.com/regions/services/).

## <a name="provision-ssis-on-azure"></a>Aprovisionar SSIS en Azure

**Aprovisionamiento**. Para poder implementar y ejecutar paquetes SSIS en Azure, debe aprovisionar el catálogo de SSIS (SSISDB) y Azure SSIS Integration Runtime. Siga los pasos de aprovisionamiento del artículo: [Implementar y ejecutar un paquete SSIS en Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure).

**Escalabilidad vertical y horizontal**. Al aprovisionar Azure SSIS IR, puede realizar la escalabilidad vertical y horizontal especificando los valores de las siguientes opciones:
-   El tamaño del nodo (incluido el número de núcleos) y el número de nodos del clúster.
-   La instancia existente de Azure SQL Database para hospedar la base de datos del catálogo de SSIS (SSISDB), y el nivel de servicio de la base de datos.
-   Las ejecuciones en paralelo máximas por nodo.

**Mejorar el rendimiento**. Para obtener más información, vea [Configuración de Azure SSIS Integration Runtime para conseguir un alto rendimiento](https://docs.microsoft.com/azure/data-factory/configure-azure-ssis-integration-runtime-performance).

## <a name="design-packages"></a>Diseñar paquetes

Debe continuar con el **diseño y la compilación de paquetes** localmente en SSDT, o bien en Visual Studio con SSDT instalado.

### <a name="connect-to-data-sources"></a>Conectarse a orígenes de datos

Para obtener información sobre cómo conectarse a orígenes de datos locales desde la nube con la **autenticación de Windows**, vea [Conexión a orígenes de datos y a recursos compartidos de archivos con la autenticación de Windows](ssis-azure-connect-with-windows-auth.md).

Para obtener información sobre cómo conectarse a archivos y recursos compartidos de archivos, vea [Abrir y guardar archivos con paquetes SSIS implementados en Azure](ssis-azure-files-file-shares.md).

### <a name="available-ssis-components"></a>Componentes de SSIS disponibles

Al aprovisionar una instancia de SQL Database para hospedar SSISDB, también se instalan Azure Feature Pack para SSIS y el componente redistribuible de Access. Estos componentes proporcionan conectividad a varios orígenes de datos de **Azure** y a archivos de **Excel y Access**, así como a los orígenes de datos compatibles con los componentes integrados.

También se pueden instalar componentes adicionales: por ejemplo, se puede instalar un controlador que no esté instalado de forma predeterminada. Para obtener más información, consulte [Custom setup for the Azure-SSIS integration runtime](/azure/articles/data-factory/how-to-configure-azure-ssis-ir-custom-setup) (Configuración personalizada de Integration Runtime de SSIS de Azure).

Si es un ISV, puede actualizar la instalación de los componentes con licencia para que estén disponibles en Azure. Para más información, vea [Desarrollo de componentes personalizados de pago o con licencia para Azure SSIS Integration Runtime](https://docs.microsoft.com/azure/data-factory/how-to-develop-azure-ssis-ir-licensed-components).

### <a name="transaction-support"></a>Compatibilidad con transacciones

Con SQL Server local y en máquinas virtuales de Azure, puede usar las transacciones del Coordinador de transacciones distribuidas de Microsoft (MSDTC). Para configurar MSDTC en cada nodo de Azure SSIS IR, use la capacidad de configuración personalizada. Para obtener más información, consulte [Custom setup for the Azure-SSIS integration runtime](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup) (Configuración personalizada de Integration Runtime de SSIS de Azure).

Con Azure SQL Database solo puede usar transacciones elásticas. Para más información, vea [Distributed transactions across cloud databases](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-transactions-overview) (Transacciones distribuidas por bases de datos de nube).

## <a name="deploy-and-run-packages"></a>Implementar y ejecutar paquetes

Para empezar, vea [Implementar y ejecutar un paquete SSIS en Azure](ssis-azure-deploy-run-monitor-tutorial.md).

### <a name="connect-to-ssisdb"></a>Conectarse a SSISDB

El **nombre de SQL Database** que hospeda SSISDB se convierte en la primera parte del nombre de cuatro partes que se usará al implementar y ejecutar paquetes de SSDT y SSMS con el siguiente formato: `<sql_database_name>.database.windows.net`. Para obtener información sobre cómo conectarse a la base de datos del catálogo de SSIS en Azure, vea [Conectarse al catálogo de SSIS (SSISDB) en Azure](ssis-azure-connect-to-catalog-database.md).

### <a name="deploy-projects-and-packages"></a>Implementación de proyectos y paquetes

Tiene que usar el **modelo de implementación de proyectos**, y no el modelo de implementación de paquetes, al implementar proyectos en SSISDB en Azure.

Para implementar proyectos en Azure, puede usar una de las distintas herramientas conocidas y opciones de scripting:
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (de SSMS, Visual Studio Code u otra herramienta)
-   Una herramienta de línea de comandos
-   PowerShell o C#, y el modelo de objetos de administración de SSIS

Para obtener un ejemplo de implementación en el que se usa SSMS y el Asistente para implementación de Integration Services, vea [Implementar y ejecutar un paquete SSIS en Azure](ssis-azure-deploy-run-monitor-tutorial.md).

### <a name="run-packages"></a>Ejecutar paquetes

Para obtener información general de los métodos que se pueden usar para ejecutar paquetes SSIS implementados en Azure, vea [Run an SSIS package in Azure](ssis-azure-run-packages.md) (Ejecutar un paquete SSIS en Azure).

## <a name="pass-runtime-values-with-environments"></a>Pasar valores en tiempo de ejecución con los entornos

Para pasar uno o más valores de tiempo de ejecución a los paquetes que se ejecutan como parte de una canalización de Azure Data Factory, cree entornos de ejecución de SSIS en SSISDB con SQL Server Management Studio (SSMS). En cada entorno, cree variables y asigne valores que se correspondan a los parámetros para los proyectos o paquetes. Configure los paquetes SSIS en SSMS para asociar esas variables de entorno con los parámetros del proyecto o paquete. Al ejecutar los paquetes en una canalización de Azure Data Factory, cambie entre los entornos especificando otras rutas de acceso de entorno en la pestaña Configuración de la interfaz de usuario Ejecutar una actividad de paquete SSIS.

Para obtener más información sobre los entornos SSIS, vea [Crear y asignar un entorno de servidor](../packages/deploy-integration-services-ssis-projects-and-packages.md#create-and-map-a-server-environment). Para obtener más información sobre cómo ejecutar un paquete como parte de una canalización de Azure Data Factory, vea [Ejecución de un paquete de SSIS mediante una actividad de SSIS de Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity).

## <a name="monitor-packages"></a>Supervisar paquetes
Para supervisar paquetes en ejecución en SSMS, puede usar las siguientes herramientas de informes de SSMS.
-   Haga clic con el botón derecho en **SSISDB** y, a continuación, seleccione **Operaciones activas** para abrir el cuadro de diálogo **Operaciones activas**.
-   Seleccione un paquete en el Explorador de objetos, haga clic con el botón derecho y seleccione **Informes**. A continuación, elija **Informes estándar** y **Todas las ejecuciones**.

Para supervisar Azure SSIS Integration Runtime, vea [Monitor the Azure-SSIS integration runtime](https://docs.microsoft.com/azure/data-factory/monitor-integration-runtime#azure-ssis-integration-runtime) (Supervisión de Azure SSIS Integration Runtime).

## <a name="schedule-packages"></a>Programar paquetes
Para programar la ejecución de paquetes almacenados en Azure SQL Database, puede usar una variedad de herramientas. Para obtener más información, vea [Programar paquetes SSIS en Azure](ssis-azure-schedule-packages.md).

## <a name="next-steps"></a>Pasos siguientes
Para comenzar con las cargas de trabajo de SSIS en Azure, consulte los artículos siguientes:
-   [Implementación de paquetes de SQL Server Integration Services en Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)
-   [Implementar y ejecutar un paquete SSIS en Azure](ssis-azure-deploy-run-monitor-tutorial.md)
