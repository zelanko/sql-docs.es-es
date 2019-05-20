---
title: Comenzar con este sencillo ejemplo del Asistente para importación y exportación | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1f05baa17bb09b5cafcd775160d2f585004d00b1
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723833"
---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>Comenzar con este sencillo ejemplo del Asistente para importación y exportación

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Para obtener información acerca de lo que puede esperar del Asistente para importación y exportación de SQL Server, siga los pasos de este escenario común: importar datos desde una hoja de cálculo de Excel a una base de datos de SQL Server. Incluso si piensa utilizar un origen y un destino diferentes, este tema le muestra la mayoría de conocimientos necesarios para ejecutar el asistente.

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>Requisito previo: ¿Está instalado el asistente en el equipo?
Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="heres-the-excel-source-data-for-this-example"></a>Datos de origen de Excel para este ejemplo
Estos son los datos de origen que se van a copiar: una pequeña tabla de dos columnas en la hoja de cálculo WizardWalkthrough del libro de Excel WizardWalkthrough.xlsx.

![Datos de origen de Excel](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>Base de datos de destino de SQL Server para este ejemplo
Esta es la base de datos de destino de SQL Server (en SQL Server Management Studio) a la que se van a copiar los datos de origen. La tabla de destino no está ahí: el asistente creará la tabla por usted.

![Base de datos de destino de SQL Server](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>Paso 1: Iniciar el asistente
Inicie el asistente desde el grupo Microsoft SQL Server 2016 en el menú Inicio de Windows.

![Iniciar el asistente](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> En este ejemplo, se selecciona el asistente de 32 bits porque está instalada la versión de 32 bits de Microsoft Office. Como resultado, debe usarse el proveedor de datos de 32 bits para conectarse a Excel. Para muchos otros orígenes de datos, normalmente puede usarse el asistente de 64 bits.
>
> Para usar la versión de 64 bits del Asistente para importación y exportación de SQL Server, tendrá que instalar SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

Para obtener más información, vea [Start the SQL Server Import and Export Wizard](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)(Iniciar el Asistente para importación y exportación de SQL Server).

## <a name="step-2---view-the-welcome-page"></a>Paso 2: Visualizar la página de bienvenida
La primera página del asistente es la **página de bienvenida**. 

Seguramente no quiere volver a ver esta página, así que puede hacer clic en **No volver a mostrar esta página**.

![Bienvenida al asistente](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>Paso 3: Seleccionar Excel como origen de datos
En la página siguiente, **Seleccionar un origen de datos**, seleccione Microsoft Excel como origen de datos. A continuación, use el explorador para seleccionar el archivo de Excel. Por último, especifique la versión de Excel que usó para crear el archivo.

> [!IMPORTANT]
> Para obtener información detallada sobre cómo conectarse a archivos de Excel y sobre las limitaciones y problemas conocidos a la hora de cargar datos de o a archivos de Excel, vea [Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).

![Selección del origen de datos de Excel](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

Para obtener más información acerca de esta página del asistente, consulte [Choose a Data Source](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) (Selección de un origen de datos).

## <a name="step-4---pick-sql-server-as-your-destination"></a>Paso 4: Seleccionar SQL Server como destino
En la página siguiente, **Seleccionar un destino**, para elegir Microsoft SQL Server como destino, seleccione uno de los proveedores de datos en la lista que se conecte a SQL Server. Para este ejemplo, seleccione **Proveedor de datos de .NET Framework para SQL Server**.

En la página se muestra una lista de propiedades del proveedor. Muchas de ellas aparecen con nombres y valores de configuración extraños. Afortunadamente, para conectarse a cualquier base de datos empresarial, normalmente, solo tendrá que proporcionar tres datos. Puede ignorar los valores predeterminados de las demás opciones.

|Información requerida|Propiedad de Proveedor de datos de .NET Framework para SQL Server|
|---|---|
|Nombre del servidor|**Origen de datos**|
|Información de autenticación (inicio de sesión)|**Seguridad integrada**, o bien **Id. de usuario** y **Contraseña**<br/>Si quiere ver una lista desplegable de las bases de datos del servidor, primero debe proporcionar información de inicio de sesión válida.|
|Nombre de la base de datos|**Catálogo original**|

![Selección del destino de SQL Server](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

Para obtener más información sobre cómo conectarse a SQL Server, consulte [Connect to a SQL Server Data Source](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md) (Conexión a un origen de datos de SQL Server). Para obtener más información acerca de esta página del asistente, consulte [Choose a Destination](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md) (Selección de un destino).

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>Paso 5: Copiar una tabla en lugar de escribir una consulta
En la página siguiente, **Especificar copia de tabla o consulta**, especifica que quiere copiar toda la tabla de datos de origen. Su objetivo no es escribir una consulta en lenguaje SQL para seleccionar los datos que se van a copiar.

![Especificación para copiar una tabla](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

Para obtener más información acerca de esta página del asistente, consulte [Specify Table Copy or Query](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md) (Especificación de copia de tabla o consulta).

## <a name="step-6---pick-the-table-to-copy"></a>Paso 6: Seleccionar la tabla que se va a copiar
En la página siguiente, **Seleccionar tablas y vistas de origen**, seleccione la tabla o tablas que quiere copiar desde el origen de datos. A continuación, asigne cada una de las tablas de origen seleccionadas a una tabla de destino nueva o existente.

En este ejemplo, el asistente asignó de forma predeterminada la hoja de cálculo **WizardWalkthrough$** de la columna **Origen** a una nueva tabla con el mismo nombre en el destino de SQL Server. (El libro de Excel solo contiene una hoja de cálculo).
-   El signo de dólar ($) en el nombre de la tabla de origen indica que se trata de una hoja de cálculo de Excel. (En Excel, un rango con nombre se representa solamente por el nombre).
-   La estrella de la tabla de destino indica que el asistente va a crear una nueva tabla de destino.

![Selección de la tabla (antes de cambiar el nombre)](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

Es recomendable quitar el signo de dólar ($) del nombre de la nueva tabla de destino.

![Selección de la tabla (después de cambiar el nombre)](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

Para obtener más información acerca de esta página del asistente, consulte [Select Source Tables and Views](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) (Selección de tablas y vistas de origen).

## <a name="optional-step-7---review-the-column-mappings"></a>Paso 7 (opcional): Revisar las asignaciones de columnas
Antes de abandonar la página **Seleccionar tablas y vistas de origen**, puede hacer clic en el botón **Editar asignaciones** para abrir el cuadro de diálogo **Asignaciones de columnas**. A continuación, en la tabla **Asignaciones**, podrá ver cómo el asistente va a asignar las columnas de la hoja de cálculo de origen a las columnas de la nueva tabla de destino.

![Visualización de las asignaciones de columna](../../integration-services/import-export-data/media/view-column-mappings.jpg)

Para obtener más información acerca de esta página del asistente, consulte [Column Mappings](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md) (Asignaciones de columnas).

## <a name="optional-step-8---review-the-create-table-statement"></a>Paso 8 (opcional): Revisar la instrucción CREATE TABLE
Mientras el cuadro de diálogo **Asignaciones de columnas** esté abierto, puede hacer clic en el botón **Editar SQL** para abrir el cuadro de diálogo **Instrucción Create Table de SQL**. Aquí verá la instrucción **CREATE TABLE** que generó el asistente para crear la nueva tabla de destino. Normalmente, no será necesario cambiar la instrucción.

![Visualización de la instrucción CREATE TABLE](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

Para obtener más información acerca de esta página del asistente, consulte [Create Table SQL Statement](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md) (Instrucción Create Table de SQL).

## <a name="optional-step-9---preview-the-data-to-copy"></a>Paso 9 (opcional): Vista previa de los datos que se van a copiar
Tras hacer clic en **Aceptar** para cerrar el cuadro de diálogo **Instrucción Create Table de SQL**, haga clic en **Aceptar** otra vez para cerrar el cuadro de diálogo **Asignaciones de columnas**. Ahora se encuentra de nuevo en la página **Seleccionar tablas y vistas de origen**. Opcionalmente, haga clic en el botón **Vista previa** para ver una muestra de los datos que va a copiar el asistente. En este ejemplo, todo parece correcto.

![Vista previa de los datos que se copiarán](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

Para obtener más información acerca de esta página del asistente, consulte [Preview Data](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md) (Vista previa de los datos).

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>Paso 10: Ejecutar la operación de importación y exportación
En la página siguiente, **Guardar y ejecutar el paquete**, mantenga habilitada la opción **Ejecutar inmediatamente** para copiar los datos en cuanto haga clic en **Finalizar** en la página siguiente. Alternativamente, para omitir la página siguiente, haga clic en **Finalizar** en la página **Guardar y ejecutar el paquete**.

![Ejecución del paquete](../../integration-services/import-export-data/media/run-the-package.jpg)

Para obtener más información acerca de esta página del asistente, consulte [Save and Run Package](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md) (Guardar y ejecutar el paquete).

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>Paso 11: Finalizar el asistente y ejecutar la operación de importación y exportación
Si hizo clic en **Siguiente** en lugar de en **Finalizar** en la página **Guardar y ejecutar el paquete**, en la página siguiente, **Finalización del asistente**, verá un resumen de lo que va a hacer el asistente. Haga clic en **Finalizar** para ejecutar la operación de importación y exportación.

![Finalizar el asistente](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

Para obtener más información acerca de esta página del asistente, consulte [Complete the Wizard](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md) (Finalización del asistente).

## <a name="step-12---review-what-the-wizard-did"></a>Paso 12: Revisar lo que hizo el asistente
En la página final, observe el asistente a medida que finalice cada tarea y, a continuación, revise los resultados. La línea resaltada indica que el asistente copió sus datos correctamente. Ya hemos terminado.

![Ejecución correcta del asistente](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

Para obtener más información acerca de esta página del asistente, consulte [Performing Operation](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md) (Operación en curso).

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>Nueva tabla de datos que se copiaron a SQL Server
Aquí (en SQL Server Management Studio) verá la nueva tabla de destino que el asistente creó en SQL Server.

![Datos copiados a SQL Server](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

Aquí (de nuevo en SSMS) se muestran los datos que el asistente copió a SQL Server.

![Datos copiados a SQL Server 2](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>Más información  
Obtenga más información sobre cómo funciona el asistente.
-   **Obtenga más información sobre el asistente.** Si quiere obtener información general sobre el asistente, consulte [Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

-   **Obtenga más información sobre los pasos del asistente.** Si está buscando información sobre los pasos del asistente, seleccione la página que quiera de esta lista: [Steps in the SQL Server Import and Export Wizard](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md) (Pasos del Asistente para importación y exportación de SQL Server). También hay una página independiente de documentación para cada página del asistente.

-   **Obtenga información sobre cómo conectarse a orígenes y destinos de datos.** Si está buscando información sobre cómo conectarse a sus datos, seleccione la página que quiera de esta lista: [Connect to data sources with the SQL Server Import and Export Wizard](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md) (Conexión a orígenes de datos con el Asistente para importación y exportación de SQL Server). Hay una página independiente de documentación para cada origen de datos de uso frecuente.

-   **Obtenga más información sobre cómo cargar datos de y a Excel.** Si busca información sobre cómo conectarse a archivos de Excel y sobre las limitaciones y problemas conocidos a la hora de cargar datos de o a archivos de Excel, vea [Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).
