---
title: Evaluar una empresa y consolidar los informes de evaluación (SQL Server) | Microsoft Docs
description: Obtenga información sobre cómo usar DMA para evaluar una empresa y consolidar los informes de evaluación antes de actualizar SQL Server o la migración a Azure SQL Database.
ms.custom: ''
ms.date: 08/28/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 05c3df493c809132d6fbfad1d96cc84d4d873dd3
ms.sourcegitcommit: fb269accc3786715c78f8b6e2ec38783a6eb63e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2018
ms.locfileid: "43152636"
---
# <a name="assess-an-enterprise-and-consolidate-assessment-reports-with-dma"></a>Evaluar una empresa y consolidar los informes de evaluación con DMA

Las siguientes instrucciones paso a paso para ayudarán a usar Data Migration Assistant para realizar una evaluación escalada correcta para la actualización local de SQL Server o SQL Server se ejecuta en máquinas virtuales de Azure, o para migrar a Azure SQL Database.

## <a name="prerequisites"></a>Requisitos previos

- Designar un equipo de herramientas de la red desde el que se iniciará DMA. Asegúrese de que este equipo tiene conectividad a sus destinos de SQL Server.
- Descargue e instale:
    - [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.6 o superior.
    - [PowerShell](http://aka.ms/wmf5download) v5.0 o superior.
    - [.NET framework](https://www.microsoft.com/download/details.aspx?id=30653) v4.5 o posterior.
    - [SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.0 o posterior.
    - [Power BI desktop](https://docs.microsoft.com/power-bi/desktop-get-the-desktop).
- Descargar y extraer:
    - El [plantilla DMA informes Power BI](https://msdnshared.blob.core.windows.net/media/2018/04/PowerBI-Reports1.zip).
    - El [LoadWarehouse script](https://msdnshared.blob.core.windows.net/media/2018/03/LoadWarehouse.zip).

## <a name="loading-the-powershell-modules"></a>Cargando los módulos de PowerShell
Guardado de los módulos de PowerShell en el directorio de módulos de PowerShell le permite llamar a los módulos sin necesidad de cargarlos explícitamente antes de su uso.

Para cargar los módulos, realice los pasos siguientes:
1. Vaya a C:\Program Files\WindowsPowerShell\Modules y, a continuación, cree una carpeta denominada **DataMigrationAssistant**.
2. Abra el [módulos de PowerShell](https://msdnshared.blob.core.windows.net/media/2018/03/PowerShell-Modules.zip)y, a continuación, guardarlos en la carpeta que creó.

      ![Módulos de PowerShell](../dma/media//dma-consolidatereports/dma-powershell-modules.png)

    Cada carpeta contiene el archivo. psm1 asociado, como se muestra en el gráfico siguiente:

   ![Archivos. psm1 de módulos de PowerShell](../dma/media//dma-consolidatereports/dma-powershell-modules-psm1-files.png)

   > [!NOTE]
   > La carpeta y archivo. psm1 contiene deben tener el mismo nombre.

   > [!IMPORTANT]
   > Es posible que deba desbloquee los archivos de PowerShell después de guardar en el directorio de WindowsPowerShell para asegurarse de que los módulos que se cargó correctamente. Para desbloquear un archivo de PowerShell, haga doble clic en el archivo, seleccione **propiedades**, seleccione el **desbloquear** cuadro de texto y, a continuación, seleccione **Aceptar**.

   ![propiedades del archivo. psm1](../dma/media//dma-consolidatereports/dma-psm1-file-properties.png)

    PowerShell ahora debe cargar estos módulos automáticamente cuando se inicia una nueva sesión de PowerShell.

## <a name="create-an-inventory-of-sql-servers"></a>Crear un inventario de servidores SQL Server
Antes de ejecutar el script de PowerShell para evaluar los servidores SQL Server, deberá crear un inventario de los servidores SQL Server que desea evaluar.

Este inventario puede estar en uno de dos formas:
- Archivo CSV de Excel
- Tabla de SQL Server

### <a name="if-using-a-csv-file"></a>Si usa un archivo CSV
Cuando se usa un archivo csv para importar los datos, asegúrese de que hay solo dos columnas de datos – **nombre de instancia** y **nombre de base de datos**, y que las columnas no tienen filas de encabezado.
 
 ![contenido del archivo CSV](../dma/media//dma-consolidatereports/dma-csv-file-contents.png)

### <a name="if-using-sql-server-table"></a>Si usa la tabla de SQL Server
Crear una base de datos denominada **EstateInventory** y una tabla denominada **DatabaseInventory**. La tabla que contiene estos datos de inventario puede tener cualquier número de columnas, siempre que existan cuatro columnas siguientes:
- ServerName
- InstanceName
- DatabaseName
- AssessmentFlag

![Contenido de la tabla de SQL Server](../dma/media//dma-consolidatereports/dma-sql-server-table-contents.png)

Si esta base de datos no está en el equipo de herramientas, asegúrese de que el equipo de herramientas tiene conectividad de red a esta instancia de SQL Server.

La ventaja de usar una tabla de SQL Server a través de un archivo CSV es que puede usar la columna de marca de evaluación para controlar la instancia / base de datos que obtiene recogido para evaluación, lo que hace que sea más fácil separar las evaluaciones en fragmentos más pequeños.  A continuación, puede abarcar varias evaluaciones (consulte la sección acerca de cómo ejecutar una evaluación más adelante en este artículo), (vea la sección acerca de cómo ejecutar una evaluación más adelante en este artículo), que es más fácil que mantener varios archivos CSV.

Tenga en cuenta que dependiendo del número de objetos y su complejidad, una evaluación puede tardar demasiado tiempo (horas +), por lo que es recomendable separar la evaluación en fragmentos más manejables.

## <a name="running-a-scaled-assessment"></a>Ejecutar una evaluación escalada
Después de cargar los módulos de PowerShell en el directorio modules y crear un inventario, deberá ejecutar una evaluación de escalado, abra PowerShell y ejecute la función dmaDataCollector.
 
  ![anuncios de dmaDataCollector (función)](../dma/media//dma-consolidatereports/dma-dmaDataCollector-function-listing.png)

Los parámetros asociados con la función dmaDataCollector se describen en la tabla siguiente.

|Parámetro  |Descripción
|---------|---------|
|**getServerListFrom** | El inventario. Los valores posibles son **SqlServer** y **CSV**. |
|**Nombre de servidor** | El nombre de instancia de SQL Server del inventario cuando se usa **SqlServer** en el **getServerListFrom** parámetro. |
|**DatabaseName** | La base de datos que hospeda la tabla de inventario. |
|**AssessmentName** | El nombre de la evaluación de DMA. |
|**TargetPlatform** | El tipo de destino de evaluación que se desea realizar.  Los valores posibles son **AzureSQLDatabase**, **SQLServer2012**, **SQLServer2014**, **SQLServer2016**,  **SQLServerLinux2017**, y **SQLServerWindows2017**. |
|**AuthenticationMethod** | El método de autenticación para conectarse a los destinos de SQL Server van a evaluar. Los valores posibles son **SQLAuth** y **WindowsAuth**. |
|**OutputLocation** | El directorio en el que se va a almacenar el archivo JSON evaluación de archivo de salida. Según el número de bases de datos que se evalúa y el número de objetos dentro de las bases de datos, las evaluaciones pueden tardar demasiado tiempo. Después de han completado todas las evaluaciones, se escribirá el archivo. |

Si se produce un error inesperado, se terminará la ventana de comandos que se inicia por este proceso.  Revise el registro de errores para determinar por qué se produjo un error.
 
  ![Ubicación de registro de errores](../dma/media//dma-consolidatereports/dma-error-log-file-location.png)

## <a name="consuming-the-assessment-json-file"></a>Consumir el archivo JSON de evaluación

Una vez finalizada la evaluación, ahora está listo para importar los datos en SQL Server para su análisis. Para consumir el archivo JSON de evaluación, abra PowerShell y ejecute la función dmaProcessor.
 
  ![anuncio de función dmaProcessor](../dma/media//dma-consolidatereports/dma-dmaProcessor-function-listing.png)

Los parámetros asociados con la función dmaProcessor se describen en la tabla siguiente.

|Parámetro  |Descripción
|---------|---------|
|**encarguen**  | La ubicación a la que se procesará el archivo JSON. Los valores posibles son **SQLServer** y **AzureSQLDatabase**. |
|**Nombre de servidor** | La instancia de SQL Server a la que se procesarán los datos.  Si especifica **AzureSQLDatabase** para el **encarguen** parámetro, a continuación, incluir solo el nombre de SQL Server (no incluya. database.windows.net). Se le pedirá para dos inicios de sesión cuando el destino es Azure SQL Database; la primera es sus credenciales de inquilino de Azure, mientras que el segundo es el inicio de sesión de administrador para el servidor de SQL Azure. |
|**CreateDMAReporting** | La base de datos de almacenamiento provisional para crear para procesar el archivo JSON.  Si la base de datos especificada ya existe y se establece este parámetro en uno, los objetos no se crean.  Este parámetro es útil para volver a crear un único objeto que se ha quitado. |
|**CreateDataWarehouse** | Crea el almacenamiento de datos que se usará en el informe de Power BI. |
|**DatabaseName** | El nombre de la base de datos DMAReporting. |
|**warehouseName** | El nombre de la base de datos de almacén de datos. |
|**jsonDirectory** | El directorio que contiene el archivo JSON de la evaluación.  Si hay varios archivos JSON en el directorio, a continuación, son procesan uno a uno. |

La función dmaProcessor solo tardará unos segundos en procesar un único archivo.

## <a name="loading-the-data-warehouse"></a>Cargando el almacenamiento de datos
Después de la dmaProcessor haya acabado de procesar los archivos de la evaluación, los datos se cargarán en la base de datos DMAReporting en la tabla DatosSoftware. En este momento, deberá cargar el almacenamiento de datos.

1. Use el script LoadWarehouse para rellenar los valores que faltan en las dimensiones.

    La secuencia de comandos tomará los datos de la tabla DatosSoftware en la base de datos DMAReporting y cargarlos en el almacén.  Si se han producido errores durante este proceso de carga, es probable que son consecuencia de las entradas que faltan en las tablas de dimensiones.

2. Cargar el almacenamiento de datos.
 
      ![LoadWarehouse contenido cargado](../dma/media//dma-consolidatereports/dma-LoadWarehouse-loaded.png)

## <a name="set-your-database-owners"></a>Establecer los propietarios de base de datos
Aunque no es obligatorio, para obtener el máximo partido de los informes, se recomienda que establezca los propietarios de base de datos en el **dimDBOwner** de dimensión y, a continuación, actualice **DBOwnerKey** en el  **FactAssessment** tabla.  Este proceso permitirá segmentar y filtrar el informe de Power BI en función de los propietarios de base de datos específica.

También puede usar la secuencia de comandos LoadWarehouse para proporcionar las instrucciones de TSQL básicas para establecer los propietarios de base de datos.

  ![Propietarios de configuración LoadWarehouse](../dma/media//dma-consolidatereports/dma-LoadWarehouse-set-owners.png)

## <a name="dma-reports"></a>Informes DMA

1. Abra la plantilla de DMA informes Power BI en Power BI Desktop.
2. Escriba los detalles del servidor que señalan a su **DMAWarehouse** de base de datos y, a continuación, seleccione **carga**.

    > [!IMPORTANT]
    > No presione ENTRAR para aceptar los valores.

      ![Carga plantilla de DMA informes Power BI](../dma/media//dma-consolidatereports/dma-reports-powerbi-template-loaded.png)

   Después de que el informe actualice los datos de la **DMAWarehouse** base de datos, se le presentará un informe similar al siguiente.

   ![Vista de informe DMAWarehouse](../dma/media//dma-consolidatereports/dma-DMAWarehouse-report.png)

   > [!TIP]
   > Si no ve los datos esperados, pruebe a cambiar el marcador activo.  Para obtener más información, consulte la sección de funcionalidad.

## <a name="working-with-dma-reports"></a>Trabajar con informes DMA
Para trabajar con un informe DMA, use las segmentaciones para filtrar por:
- Nombre de la instancia
- Nombre de la base de datos
- Nombre de equipo

También puede usar marcadores para cambiar el contexto de generación de informes entre:
- Evaluaciones en la nube
- Evaluaciones de forma local

  ![Marcadores de informe DMA](../dma/media//dma-consolidatereports/dma-report-bookmarks.png)

> [!NOTE]
> Si sólo realiza una evaluación de Azure SQL Database, se rellenan solo los informes en la nube. Por el contrario, si sólo realiza una evaluación en el entorno local, se rellenan solo los informes locales. Sin embargo, si se realizan una instancia de Azure y una evaluación local y, a continuación, cargar ambas evaluaciones en el almacenamiento, puede cambiar entre los informes en la nube y local mediante CTRL-clic el icono asociado.

## <a name="reports-visuals"></a>Objetos visuales de informes
En las secciones siguientes se muestran los detalles que se muestran en los informes de Power BI.

### <a name="readiness-"></a>% De disponibilidad

  ![Porcentaje de preparación de DMA](../dma/media//dma-consolidatereports/dma-readiness-percentage.png)

Este objeto visual se actualiza según el contexto de selección (todo, la instancia, base de datos [múltiplos de]).

### <a name="readiness-count"></a>Recuento de preparación

  ![Recuento de preparación de DMA](../dma/media//dma-consolidatereports/dma-readiness-count.png)

Este objeto visual muestra el número de bases de datos que esté listo para migrar el recuento de las bases de datos que aún no están preparados para la migración.

### <a name="readiness-bucket"></a>Depósito de preparación

  ![Depósito de preparación de DMA](../dma/media//dma-consolidatereports/dma-readiness-bucket.png)

Este objeto visual muestra un desglose de las bases de datos por los depósitos de preparación para la siguiente:
- LISTAS DE 100%
- LISTAS DE 75-99%
- LISTAS DE 50-75%
- NO ESTÁ LISTO

### <a name="issues-word-cloud"></a>Word de problemas en la nube
 
  ![Problemas DMA WordCloud](../dma/media//dma-consolidatereports/dma-issues-word-cloud.png)

Este objeto visual muestra los problemas que actualmente se están produciendo dentro en el contexto de selección (todo, la instancia, base de datos [múltiplos de]). Cuanto mayor sea la palabra aparece en pantalla, mayor será el número de problemas de esa categoría. Mantiene el puntero del mouse sobre una palabra, muestra el número de problemas que se producen en esa categoría.

### <a name="database-readiness"></a>Preparación de la base de datos

  ![Informe de preparación de la base de datos de DMA](../dma/media//dma-consolidatereports/dma-database-readiness-report.png)

En esta sección es la parte principal del informe, que muestra la preparación de una base de datos de instancia. Este informe tiene una jerarquía de profundidad de:
- InstanceDatabase
- ChangeCategory
- Title
- ObjectType
- ImpactedObjectName

 ![Obtención de detalles de informe de preparación de la base de datos de DMA](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown.png)

Este informe también sirve como punto de filtro para crear el informe de Plan de recuperación.

Para profundizar en el informe de Plan de recuperación, haga doble clic en un punto de datos en este gráfico, seleccione **obtención de detalles**y, a continuación, seleccione **planes de corrección**.

Esta tarea filtra el informe del plan de corrección para el nivel de jerarquía actual según el punto en el que deba seleccionar la opción de obtención de detalles.

  ![Preparación de la base de datos de DMA informes detallados filtrados](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown-filtered.png)

  ![Informe del Plan de corrección de DMA](../dma/media//dma-consolidatereports/dma-remediation-plan-report.png)

También puede usar el informe del Plan de corrección en su propio para crear una solución personalizada plan mediante el uso de los filtros en la **visualizaciones filtros** hoja.
 
  ![Opciones de filtro de informe de Plan de corrección de DMA](../dma/media//dma-consolidatereports/dma-remediation-plan-report-filter-options.png)

### <a name="script-disclaimer"></a>Declinación de responsabilidades de secuencia de comandos
*Los scripts de ejemplo proporcionados en este artículo no se admiten en ningún servicio o programa de soporte técnico standard de Microsoft. Todos los scripts se proporcionan tal cual sin garantía de ningún tipo. Microsoft renuncia a toda garantía expresa que incluye, sin limitación, cualquier implícito garantías de comerciabilidad o idoneidad para un propósito específico. Todo el riesgo que surja del uso o funcionamiento de los scripts de ejemplo y documentación de su responsabilidad. En ningún caso Microsoft, sus autores o cualquier otro implicado en la creación, producción o entrega de los scripts serán responsables por ningún daño índole (incluidos, sin limitación, daños por pérdida de beneficios empresariales, interrupción del negocio, pérdida de información empresarial, o en otra pérdida pecuniaria) que se deriven del uso o la incapacidad de usar los scripts de ejemplo o la documentación, aunque se haya notificado a Microsoft de la posibilidad de dichos daños.  Busque el permiso antes de volver a exponer estas secuencias de comandos en otros repositorios/sitios/blogs.*