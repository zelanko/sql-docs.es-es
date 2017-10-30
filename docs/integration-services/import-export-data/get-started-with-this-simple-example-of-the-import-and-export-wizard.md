---
title: "Empezar a trabajar con este ejemplo sencillo de la importación y el Asistente para exportación | Documentos de Microsoft"
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 59c7e1cc3c31f77652acb21d375e1294bdc93397
ms.openlocfilehash: 9eee58be471d8b39b051c1343f9eb26a2960b6d6
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>Empezar a trabajar con este ejemplo sencillo de la importación y el Asistente para exportación
Obtenga información acerca de lo que puede esperar en la importación de SQL Server y el Asistente para exportación recorriendo un escenario común: importar datos desde una hoja de cálculo de Excel a una base de datos de SQL Server. Incluso si piensa utilizar un origen diferente y un destino diferente, este tema muestra la mayoría de lo que necesita saber sobre cómo ejecutar el asistente.

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>¿Requisito previo: es el Asistente para instalar en el equipo?
Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="heres-the-excel-source-data-for-this-example"></a>Estos son los datos de origen de Excel para este ejemplo
Estos son los datos de origen que se van a copiar - una pequeña tabla de dos columnas en la hoja de cálculo WizardWalkthrough del libro de WizardWalkthrough.xlsx Excel.

![Datos de origen de Excel](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>Esta es la base de datos de destino de SQL Server para este ejemplo
A continuación (en SQL Server Management Studio) es la base de datos de destino de SQL Server a la que va a copiar los datos de origen. La tabla de destino no está ahí: va a dejar que el asistente creará la tabla para usted.

![Base de datos de destino de SQL Server](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>Paso 1: iniciar el Asistente
Inicie al asistente desde el grupo de Microsoft SQL Server 2016 en el menú Inicio de Windows.

![Asistente de inicio](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> En este ejemplo, se puede seleccionar al Asistente de 32 bits porque tiene la versión de 32 bits de Microsoft Office instalada. Como resultado, tendrá que usar el proveedor de datos de 32 bits para conectarse a Excel. Para muchos otros orígenes de datos, normalmente puede elegir al Asistente de 64 bits.
>
> Para usar la versión de 64 bits de la importación de SQL Server y el Asistente para exportación, tendrá que instalar a SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

Para obtener más información, vea [Start the SQL Server Import and Export Wizard](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)(Iniciar el Asistente para importación y exportación de SQL Server).

## <a name="step-2---view-the-welcome-page"></a>Paso 2: ver la página de bienvenida
Es la primera página del Asistente para la **bienvenida** página. 

Probablemente no desea ver esta página de nuevo, por lo que continúe y haga clic en **no mostrar esta página nuevo**.

![Bienvenido al Asistente](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>Paso 3: selección de Excel como origen de datos
En la página siguiente, **elegir un origen de datos**, Microsoft Excel se puede seleccionar como origen de datos. A continuación, examina para seleccionar el archivo de Excel. Por último, especifique la versión de Excel que usó para crear el archivo.

![Elija el origen de datos de Excel](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

Para obtener más información sobre cómo conectarse a Excel, vea [conectar a un origen de datos de Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md). Para obtener más información acerca de esta página del asistente, consulte [elegir un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md).

## <a name="step-4---pick-sql-server-as-your-destination"></a>Paso 4: selección de SQL Server como destino
En la página siguiente, **elegir un destino**, elija Microsoft SQL Server como su destino escogiendo uno de los proveedores de datos en la lista que se conecta a SQL Server. En este ejemplo, se elige la **.Net Framework Data Provider for SQL Server**.

La página muestra una lista de propiedades del proveedor. Muchas de ellas son hostiles nombres y valores familiarizados. Afortunadamente, para conectarse a cualquier base de datos de empresa, normalmente tendrá que proporcionar solo tres piezas de información. Puede pasar por alto los valores predeterminados para las demás opciones.

|Obtener la información necesaria|.NET framework Data Provider para la propiedad de SQL Server|
|---|---|
|Nombre del servidor|**Origen de datos**|
|Información de autenticación (inicio de sesión)|**La seguridad integrada de**; o **Id. de usuario** y **contraseña**<br/>Si desea ver una lista desplegable de las bases de datos en el servidor, primero debe proporcionar información de inicio de sesión válido.|
|Nombre de la base de datos|**Catálogo original**|

![Elija el destino de SQL Server](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

Para obtener más información sobre cómo conectarse a SQL Server, vea [conectar a un origen de datos de SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md). Para obtener más información acerca de esta página del asistente, consulte [elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>Paso 5: copiar una tabla en lugar de escribir una consulta
En la página siguiente, **especificar copia de tabla o consulta**, especifica que van a copiar toda la tabla de datos de origen. No desea escribir una consulta en el lenguaje SQL para seleccionar los datos que se va a copiar.

![Especificar para copiar una tabla](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

Para obtener más información acerca de esta página del asistente, consulte [especificar copia de tabla o consulta](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).

## <a name="step-6---pick-the-table-to-copy"></a>Paso 6: seleccionar la tabla que se va a copiar
En la página siguiente, **seleccionar tablas de origen y vistas**, seleccione la tabla o tablas que se van a copiar desde el origen de datos. A continuación, asigne cada tabla de origen seleccionada a una tabla de destino nuevos o existentes.

En este ejemplo, de forma predeterminada el asistente ha asignado la **WizardWalkthrough$** hoja de cálculo en el **origen** columna a una nueva tabla con el mismo nombre en el destino de SQL Server. (El libro de Excel solo contiene una sola hoja de cálculo).
-   El signo de dólar ($) en el nombre de la tabla de origen indica una hoja de cálculo de Excel. (Un conjunto con nombre un rango en Excel se representa solamente por su nombre.)
-   El estallido en el icono de la tabla de destino indica que el asistente va a crear una nueva tabla de destino.

![Seleccione la tabla (antes de cambiar el nombre)](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

Probablemente desea quitar el signo de dólar ($) del nombre de la nueva tabla de destino.

![Seleccione la tabla (después de cambiar el nombre)](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

Para obtener más información acerca de esta página del asistente, consulte [seleccionar tablas de origen y vistas](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).

## <a name="optional-step-7---review-the-column-mappings"></a>Paso opcional 7 - revisar las asignaciones de columnas
Antes de abandonar la **seleccionar tablas de origen y vistas** , opcionalmente, haz clic en el **editar asignaciones** para abrir el **asignaciones de columnas** cuadro de diálogo. A continuación, en la **asignaciones** tabla, vea cómo el asistente va a asignar las columnas de la hoja de cálculo de origen a columnas de la nueva tabla de destino.

![Ver asignaciones de columna](../../integration-services/import-export-data/media/view-column-mappings.jpg)

Para obtener más información acerca de esta página del asistente, consulte [asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

## <a name="optional-step-8---review-the-create-table-statement"></a>Paso opcional 8 - revisar la instrucción CREATE TABLE
Mientras el **asignaciones de columnas** cuadro de diálogo está abierto, puede hacer clic en el **Editar SQL** para abrir el **instrucción Create Table de SQL** cuadro de diálogo. Aquí verá el **CREATE TABLE** instrucción generado por el Asistente para crear la nueva tabla de destino. Normalmente no es necesario cambiar la instrucción.

![Instrucción CREATE TABLE de vista](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

Para obtener más información acerca de esta página del asistente, consulte [instrucción Create Table de SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).

## <a name="optional-step-9---preview-the-data-to-copy"></a>Paso opcional 9 - vista previa de los datos que se va a copiar
Tras hacer clic en **Aceptar** para cerrar el **instrucción Create Table de SQL** diálogo cuadro, a continuación, haga clic en **Aceptar** otra vez para cerrar el **asignaciones de columnas** cuadro de diálogo, está en el **seleccionar tablas de origen y vistas** página. Opcionalmente, haga clic en el **vista previa** botón para ver un ejemplo de los datos que la va a copiar el asistente. En este ejemplo parece funcionar correctamente.

![Vista previa de datos para copiar](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

Para obtener más información acerca de esta página del asistente, consulte [vista previa de datos](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>Paso 10: Sí, puede ejecutar la operación de importación y exportación
En la página siguiente, **guardar y ejecutar paquete**, deja **ejecutar inmediatamente** habilitado para copiar los datos en cuanto haga clic en **finalizar** en la página siguiente. O puede omitir la página siguiente, haga clic en **finalizar** en el **guardar y ejecutar paquete** página.

![Ejecutar el paquete](../../integration-services/import-export-data/media/run-the-package.jpg)

Para obtener más información acerca de esta página del asistente, consulte [guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>Paso 11: finalizar al asistente y ejecute la operación de importación y exportación
Si hace clic en **siguiente** en lugar de **finalizar** en el **guardar y ejecutar paquete** página, a continuación, en la página siguiente, **Complete el asistente**, verá un resumen de lo que el asistente va a realizar. Haga clic en **finalizar** para ejecutar la operación de importación y exportación.

![Finalizar el asistente](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

Para obtener más información acerca de esta página del asistente, consulte [Complete el asistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).

## <a name="step-12---review-what-the-wizard-did"></a>Paso 12: revisar lo hizo en el Asistente
En la página final, observar a medida que el asistente finalice cada tarea, a continuación, revise los resultados. La línea resaltada indica que el Asistente para copia los datos correctamente. Está terminado.

![El asistente se realizó correctamente](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

Para obtener más información acerca de esta página del asistente, consulte [operación en curso](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md).

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>Esta es la nueva tabla de datos que se copian en SQL Server
A continuación (en SQL Server Management Studio) verá la nueva tabla de destino creado por el Asistente en SQL Server.

![Datos copiados a SQL Server](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

Aquí (nuevo en SSMS) se muestran los datos que el asistente ha copiado a SQL Server.

![Datos copiados a SQL Server 2](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>Más información  
Más información sobre cómo funciona el asistente.
-   **Más información sobre el asistente.** Si quiere obtener información general sobre el asistente, consulte [Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

-   **Obtenga información acerca de los pasos del asistente.** Si desea obtener información acerca de los pasos del asistente, seleccione la página que desee en la lista aquí - [los pasos de la importación de SQL Server y el Asistente para exportación de](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). También hay una página independiente de la documentación de cada página del asistente.

-   **Obtenga información acerca de cómo conectarse a orígenes de datos y destinos.** Si desea obtener información acerca de cómo conectarse a los datos, seleccione la página que desee en la lista aquí - [conectar a orígenes de datos con la importación de SQL Server y el Asistente para exportación de](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Hay una página independiente de la documentación de cada uno de varios orígenes de datos de uso frecuente.



