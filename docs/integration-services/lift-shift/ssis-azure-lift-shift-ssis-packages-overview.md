---
title: Levantar y mover las cargas de trabajo de SQL Server Integration Services a la nube | Documentos de Microsoft
ms.date: 10/09/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 85ab11747276f0c6c58b13cd409df3e5774915ae
ms.contentlocale: es-es
ms.lasthandoff: 10/10/2017

---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>Levantar y mover las cargas de trabajo de SQL Server Integration Services a la nube
Ahora puede mover los paquetes de SQL Server Integration Services (SSIS) y las cargas de trabajo a la nube de Azure.
-   Almacenar y administrar proyectos de SSIS y paquetes en la base de datos de catálogo de SSIS (SSISDB) en la base de datos de SQL Azure.
-   Ejecutar paquetes en una instancia de Azure SSIS integración Runtime, que se incluyeron como parte de la factoría de datos de Azure versión 2.
-   Use herramientas conocidas como SQL Server Management Studio (SSMS) para estas tareas comunes.

## <a name="benefits"></a>Ventajas
Mover las cargas de trabajo SSIS de local a Azure tiene las siguientes ventajas potenciales:
-   **Reducir los costes operativos** mediante la reducción de la infraestructura local.
-   **Aumentar la disponibilidad alta** con varios nodos por clúster, así como las características de alta disponibilidad de Azure y de base de datos de SQL Azure.
-   **Aumentar la escalabilidad** con la capacidad de especificar varios núcleos por nodo (ampliación vertical) y varios nodos por clúster (escalado horizontal).
-   **Evitar las limitaciones** de la ejecución de SSIS en máquinas virtuales de Azure.

## <a name="architecture-overview"></a>Introducción a la arquitectura
En la tabla siguiente se resalta las diferencias entre SSIS de forma local y SSIS en Azure. La diferencia más importante es la separación del almacenamiento de información de proceso.

| Almacenamiento | Tiempo de ejecución | Escalabilidad |
|---|---|---|
| De forma local (SQL Server) | En tiempo de ejecución SSIS hospedada por SQL Server | SSIS horizontalmente (en SQL Server 2017 y versiones posteriores)<br/><br/>Soluciones personalizadas (en las versiones anteriores de SQL Server) |
| En Azure (base de datos SQL) | Azure SSIS integración en tiempo de ejecución, un componente de Data Factory de Azure versión 2 | Opciones de escalado para el control remoto de SSIS |
| | | |

Factoría de datos de Azure hospeda el motor en tiempo de ejecución para paquetes SSIS en Azure. El motor en tiempo de ejecución se denomina el Runtime de integración de SSIS (IR de SSIS) de Azure.

Al aprovisionar el control remoto de SSIS, puede escalar verticalmente y escalar horizontalmente especificando valores para las siguientes opciones:
-   El tamaño del nodo (incluido el número de núcleos) y el número de nodos del clúster.
-   La instancia existente de la base de datos de SQL de Azure para hospedar la base de datos de catálogo de SSIS (SSISDB) y el nivel de servicio para la base de datos.
-   Las ejecuciones en paralelo máximas por nodo.

Solamente debe aprovisionar los infrarrojos SSIS una vez. Después de eso, puede usar herramientas conocidas, como SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) para implementar, configurar, ejecutar, supervisar, programar y administrar paquetes.

> [!NOTE]
> Durante esta versión preliminar pública, el tiempo de ejecución de integración de SSIS de Azure solo está disponible en las regiones de Estados Unidos Asia y Europa del Norte.

Factoría de datos también admite otros tipos de tiempos de ejecución de integración. Para obtener más información sobre el control remoto de SSIS y los otros tipos de tiempos de ejecución de integración, vea [en tiempo de ejecución de integración de Data Factory de Azure](https://docs.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime).

## <a name="prerequisites"></a>Requisitos previos
Las capacidades descritas en este tema requieren la versión 17.2 o una versión posterior de SQL Server Data Tools (SSDT), pero no requieren 2017 de SQL Server o SQL Server 2016. Al implementar paquetes en Azure, el Asistente para la implementación de paquetes siempre actualiza los paquetes al formato de paquete más reciente.

Para obtener más información sobre los requisitos previos de Azure, consulte [elevar y cambiar paquetes de SQL Server Integration Services (SSIS) en Azure](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="ssis-features-on-azure"></a>Características SSIS en Azure

Al aprovisionar una instancia de base de datos de SQL para hospedar SSISDB, se instalan el Feature Pack de Azure para SSIS y el paquete redistribuible de acceso. Estos componentes proporcionan conectividad a los archivos de Excel y Access y a diversos orígenes de datos de Azure. No se puede instalar componentes de terceros para SSIS en este momento.

El nombre de la base de datos de SQL que hospeda SSISDB se convierte en la primera parte del nombre de cuatro partes que se utilizará al implementar y administrar los paquetes de SSDT y SSMS - `<sql_database_name>.database.windows.net`.

Tendrá que usar el modelo de implementación del proyecto, no el modelo de implementación de paquete, para los proyectos que se implementa en SSISDB en la base de datos de SQL Azure.

Continuar a diseñar y compilar paquetes locales en SSDT, o en Visual Studio con SSDT instalado.

Para obtener información sobre cómo conectarse a orígenes de datos locales de la nube con la autenticación de Windows, vea [conectar a orígenes de datos locales con autenticación de Windows](ssis-azure-connect-with-windows-auth.md).

## <a name="common-tasks"></a>Tareas comunes

### <a name="provision"></a>Aprovisionamiento
Antes de que puede implementar y ejecutar paquetes SSIS en Azure, tendrá que aprovisionar la base de datos de catálogo de SSISDB y el tiempo de ejecución de integración de SSIS de Azure. Siga el aprovisionamiento de los pasos de este artículo: [elevar y cambiar paquetes de SQL Server Integration Services (SSIS) en Azure](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure).

### <a name="deploy-and-run-packages"></a>Implementar y ejecutar paquetes
Para implementar proyectos y ejecutar paquetes en la base de datos SQL, puede usar una de varias herramientas conocidas y opciones de scripting:
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (de SSMS, código de Visual Studio u otra herramienta)
-   Una herramienta de línea de comandos
-   PowerShell
-   C# y el modelo de objetos de administración de SSIS

### <a name="monitor-packages"></a>Paquetes de Monitor
Para supervisar paquetes en ejecución en SSMS, puede usar una de las siguientes herramientas de generación de informes en SSMS.
-   Haga clic en **SSISDB**y, a continuación, seleccione **operaciones activas** para abrir el **operaciones activas** cuadro de diálogo.
-   Seleccionar un paquete en el Explorador de objetos, el menú contextual y seleccione **informes**, a continuación, **informes estándar**, a continuación, **todas las ejecuciones**.

### <a name="schedule-packages"></a>Paquetes de programación
Para programar la ejecución de paquetes almacenados en la base de datos SQL, puede usar las siguientes herramientas:
-   Agente SQL Server local
-   La actividad de SQL Server Stored Procedure de generador de datos

Para obtener más información, consulte [ejecución en Azure del paquete SSIS de programación](ssis-azure-schedule-packages.md).

## <a name="next-steps"></a>Pasos siguientes
Para empezar a trabajar con las cargas de trabajo SSIS en Azure, vea los siguientes artículos:
-   [Levantar y mover paquetes de SQL Server Integration Services (SSIS) en Azure](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure)
-   [Implementar, ejecutar y supervisar un paquete SSIS en Azure](ssis-azure-deploy-run-monitor-tutorial.md)

