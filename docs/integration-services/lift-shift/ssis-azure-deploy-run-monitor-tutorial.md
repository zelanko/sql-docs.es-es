---
title: Implementar, ejecutar y supervisar un paquete SSIS en Azure | Documentos de Microsoft
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 2e16666c412870cc55024e7156752f43ddbc1800
ms.contentlocale: es-es
ms.lasthandoff: 10/13/2017

---
# <a name="deploy-run-and-monitor-an-ssis-package-on-azure"></a>Implementar, ejecutar y supervisar un paquete SSIS en Azure
Este tutorial muestra cómo implementar un proyecto de SQL Server Integration Services en la base de datos de catálogo de SSISDB en la base de datos de SQL Azure, ejecutar un paquete en el tiempo de ejecución de integración de Azure SSIS y supervisar la ejecución del paquete.

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que tiene versión 17.2 u otra posterior de SQL Server Management Studio. Para descargar la versión más reciente de SSMS, vea [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

También asegúrese de que tiene configurado dicha base de datos y aprovisionar el tiempo de ejecución de integración de Azure SSIS. Para obtener información sobre cómo aprovisionar SSIS en Azure, consulte [elevar y cambiar paquetes de SQL Server Integration Services (SSIS) en Azure](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="connect-to-the-ssisdb-database"></a>Conectarse a la base de datos SSISDB

Usar SQL Server Management Studio para conectarse al catálogo de SSIS en el servidor de base de datos de SQL Azure. Para obtener más información, consulte [conectar a la base de datos de catálogo de SSISDB en Azure](ssis-azure-connect-to-catalog-database.md).

> [!IMPORTANT]
> Un servidor de base de datos de SQL Azure escucha en el puerto 1433. Si está intentando conectarse a un servidor de base de datos de SQL Azure desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

1. Abra SQL Server Management Studio.

2. **Conectarse al servidor**. En el **conectar al servidor** diálogo cuadro, escriba la siguiente información:

   | Configuración       | Valor recomendado | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | El nombre completo del servidor | El nombre debe tener este formato: **mysqldbserver.database.windows.net**. Si necesita el nombre del servidor, consulte [conectar a la base de datos de catálogo de SSISDB en Azure](ssis-azure-connect-to-catalog-database.md). |
   | **Autenticación** | Autenticación de SQL Server | Este tutorial rápido usa la autenticación de SQL. |
   | **Inicio de sesión** | La cuenta de administrador de servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | La contraseña de la cuenta de administrador del servidor | Esta es la contraseña que especificó cuando creó el servidor. |

3. **Conectarse a la base de datos SSISDB**. Seleccione **opciones** para expandir el **conectar al servidor** cuadro de diálogo. En el esquema **conectar al servidor** cuadro de diálogo, seleccione la **propiedades de conexión** ficha. En el **conectar con base de datos** campo, seleccione o especifique `SSISDB`.

4. A continuación, seleccione **conectar**. Se abre la ventana de explorador de objetos en SSMS. 

5. En el Explorador de objetos, expanda **catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos en la base de datos de catálogo de SSIS.

## <a name="deploy-a-project"></a>Implementar un proyecto

### <a name="start-the-integration-services-deployment-wizard"></a>Iniciar al Asistente para la implementación de Integration Services
1. En el Explorador de objetos de SSMS, con el **catálogos de Integration Services** nodo y **SSISDB** el nodo expandido, expanda una carpeta de proyecto.

2.  Seleccione el **proyectos** nodo.

3.  Haga doble clic en el **proyectos** nodo y seleccione **implementar proyecto**. Se abre el Asistente para la implementación de Integration Services. Puede implementar un proyecto desde una base de datos de catálogo de SSIS o desde el sistema de archivos.

### <a name="deploy-a-project-with-the-deployment-wizard"></a>Implementar un proyecto con el Asistente para implementación
1. En el **Introducción** página del Asistente de implementación, revise la introducción. Seleccione **siguiente** para abrir el **Seleccionar origen** página.

2. En el **Seleccionar origen** página, seleccione el proyecto SSIS existente para implementar.
    -   Para implementar un archivo de implementación de proyectos que haya creado, seleccione **Archivo de implementación de proyecto** y especifique la ruta de acceso del archivo .ispac.
    -   Para implementar un proyecto que resida en un catálogo de SSIS, seleccione **catálogo de Integration Services**y, a continuación, escriba el nombre del servidor y la ruta de acceso al proyecto en el catálogo.
    -   Seleccione **siguiente** para ver el **Seleccionar destino** página.
  
3.  En el **Seleccionar destino** página, seleccione el destino para el proyecto.
    -   Escriba el nombre completo del servidor en el formato `<server_name>.database.windows.net`.
    -   A continuación, seleccione **examinar** para seleccionar la carpeta de destino de SSISDB.
    -   Seleccione **siguiente** para abrir el **revisión** página.  
  
4.  En el **revisar** página, revise la configuración seleccionada.
    -   Puede cambiar las selecciones seleccionando **anterior**, o haciendo clic en cualquiera de los pasos en el panel izquierdo.
    -   Seleccione **implementar** para iniciar el proceso de implementación.
  
5.  Una vez completado, el proceso de implementación del **resultados** se abre la página. Esta página muestra si cada acción si se completó correctamente o no.
    -   Si se produjo un error, seleccione **error** en el **resultado** columna para que aparezca una explicación del error.
    -   Si lo desea, seleccione **Guardar informe...**  para guardar los resultados en un archivo XML.
    -   Seleccione **cerrar** para salir del asistente.

## <a name="run-a-package"></a>Ejecutar un paquete

1. En el Explorador de objetos en SSMS, seleccione el paquete que se va a ejecutar.

2. Haga clic en y seleccione **Execute** para abrir el **Ejecutar paquete** cuadro de diálogo.

3.  En el **Ejecutar paquete** diálogo cuadro, configure la ejecución del paquete mediante la configuración en el **parámetros**, **administradores de conexión**, y **avanzadas**  pestañas.

4.  Seleccione **Aceptar** para ejecutar el paquete.

## <a name="monitor-the-running-package-in-ssms"></a>Supervisar la ejecución del paquete en SSMS

Para ver el estado de ejecución operaciones de Integration Services en el servidor de Integration Services, como la implementación, validación y ejecución del paquete, utilice el **operaciones activas** cuadro de diálogo de SSMS. Para abrir el **operaciones activas** cuadro de diálogo, haga clic en **SSISDB**y, a continuación, seleccione **operaciones activas**.

También puede seleccionar un paquete en el Explorador de objetos, el menú contextual y seleccione **informes**, a continuación, **informes estándar**, a continuación, **todas las ejecuciones**.

Para obtener más información sobre cómo supervisar paquetes en ejecución en SSMS, vea [Monitor paquetes en ejecución y otras operaciones](https://docs.microsoft.com/en-us/sql/integration-services/performance/monitor-running-packages-and-other-operations).

## <a name="monitor-the-azure-ssis-integration-runtime"></a>Supervisar el tiempo de ejecución de integración de Azure SSIS

Para obtener información de estado sobre el tiempo de ejecución de integración de Azure SSIS en el que se ejecutan paquetes, use los siguientes comandos de PowerShell: para cada uno de los comandos, proporcionar los nombres de la factoría de datos, el control remoto de Azure SSIS y el grupo de recursos.

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>Obtener los metadatos sobre el tiempo de ejecución de integración de Azure SSIS

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>Obtener el estado del tiempo de ejecución de integración de Azure SSIS

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>Pasos siguientes
- Obtenga información acerca de cómo programar la ejecución del paquete. Para obtener más información, consulte [paquetes de SSIS de programación de ejecución en Azure](ssis-azure-schedule-packages.md)

