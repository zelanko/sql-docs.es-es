---
title: Virtualización de datos externos en SQL Server 2019 CTP 2.0 | Microsoft Docs
description: ''
author: Abiola
ms.author: aboke
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: dfd4460c51e4aeef8e9faff8479e7edf2678c35f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627323"
---
# <a name="use-the-data-external-table-wizard-with-external-tables"></a>Uso del Asistente para tablas externas de datos con tablas externas

Uno de los escenarios clave de SQL Server 2019 CTP 2.0 es la posibilidad de virtualizar datos.  Este proceso permite que los datos permanezcan en su ubicación original, pero puede **virtualizarlos** en una instancia de SQL Server para que se puedan consultar como cualquier otra tabla de SQL Server. De este modo, se reduce al máximo la necesidad de realizar procesos ETL. Esto es posible gracias a los conectores de PolyBase. Para obtener más información sobre la virtualización de datos, consulte nuestro documento de [introducción a PolyBase](polybase-guide.md).

## <a name="launch-the-external-table-wizard"></a>Inicio del Asistente para tablas externas

Conéctese a la instancia maestra utilizando la dirección IP o el número de puerto (31433) obtenidos al final del script de implementación. Expanda el nodo **Bases de datos** en el Explorador de objetos. A continuación, seleccione una de las bases de datos donde desea virtualizar los datos a partir de una instancia existente de SQL Server. Haga clic con el botón derecho en la base de datos y seleccione **Create External Table** en el menú contextual. Esta acción inicia el Asistente para virtualizar datos. También puede iniciar el Asistente para virtualizar datos desde la paleta de comandos escribiendo Ctrl+Mayús+P (en Windows) y Cmd+Mayús+P (en Mac).

![Asistente para virtualizar datos](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>Selección de un origen de datos

Si inicia al asistente desde una de las bases de datos, puede ver que la lista desplegable de destino se rellena automáticamente. También tiene la opción de especificar o cambiar la base de datos de destino en esta pantalla. Los tipos de orígenes de datos externos compatibles con el asistente son SQL Server y Oracle.

> [!NOTE]
>SQL Server aparece resaltado de forma predeterminada.


![Selección de un origen de datos](media/data-virtualization/select-data-source.png)

Haga clic en Siguiente para continuar al paso siguiente del asistente que establece la clave maestra de base de datos.

## <a name="create-database-master-key"></a>Creación de la clave maestra de base de datos

En este paso, se le pedirá que cree una clave maestra de base de datos. Esto es necesario porque protege las credenciales que utiliza un origen de datos externo. Elija una contraseña segura para la clave maestra. Debe realizar una copia de seguridad de la clave maestra mediante BACKUP MASTER KEY y almacenar dicha copia de seguridad en un lugar seguro y fuera de las instalaciones.

![Creación de la clave maestra de una base de datos](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> Si ya tiene una clave maestra de base de datos, se restringirán los campos de entrada y puede omitir este paso. Puede hacer simplemente clic en "Siguiente" para continuar a la siguiente página del asistente.

> [!NOTE]
> Si no elige una contraseña segura, el asistente se cerrará en el último paso. Se trata de un problema conocido que se solucionará en la próxima versión para que sea más intuitiva.

## <a name="enter-the-external-data-source-credentials"></a>Especificación de las credenciales del origen de datos externo

En este paso, especifique el origen de datos externo y los detalles de las credenciales. Este paso crea un objeto de origen de datos externo y, a continuación, usa las credenciales del objeto de base de datos para conectarse al origen de datos. Proporcione un nombre al origen de datos externo (ejemplo: Prueba) y especifique los detalles de conexión de SQL Server: el nombre del servidor y el nombre de base de datos donde desea que se cree el origen de datos externo en ese servidor.

El paso siguiente consiste en configurar las credenciales, así que indique un nombre de credenciales; se trata del nombre de las credenciales de ámbito de base de datos utilizadas para almacenar de forma segura la información de inicio de sesión del origen de datos externo que está creando (ejemplo: PruebaCred). Proporcione el nombre de usuario y la contraseña para conectarse al origen de datos.

![Credenciales del origen de datos externo](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>Asignación de tablas externas de datos

En la ventana siguiente, podrá seleccionar las tablas de las que desea crear vistas externas. Al seleccionar las bases de datos primarias, se incluirán todas las secundarias también. Cuando se seleccionan las tablas, puede verse una tabla de asignación en el lado derecho. Aquí puede realizar cualquier modificación de tipos o cambiar el nombre de la tabla externa seleccionada.

![Credenciales del origen de datos externo](media/data-virtualization/data-table-mapping.png)

> [!NOTE]
>Al hacer doble clic en otra tabla seleccionada, se cambiará la vista de asignación.

> [!IMPORTANT]
>La opción de tipo de fotografía no es compatible aún con la herramienta Tabla externa. Crear una vista externa con un tipo de foto en ella producirá un error después de crear la tabla. Sin embargo, la tabla se crea igualmente.

## <a name="summary"></a>Resumen

Este paso proporciona un resumen de las selecciones. Proporciona el nombre de las credenciales de ámbito de base de datos y los objetos de origen de datos externo que se crearán en la base de datos de destino. En este paso, verá la opción **Generar Script**, que creará en T-SQL los scripts con la sintaxis para crear el origen de datos externo, o **Crear**, que generará el objeto de origen de datos externo.

![Pantalla de resumen](media/data-virtualization/virtualize-data-summary.png)

Si hace clic en "Crear", podrá ver el objeto de origen de datos externo creado en la base de datos de destino.

![Orígenes de datos externos](media/data-virtualization/external-data-sources.png)

Si hace clic en **Generar Script**, verá la consulta Transact-SQL que se genera para crear el objeto de origen de datos externo.

![Generar script](media/data-virtualization/generated-script.png)

> [!NOTE]
> Generar script solo debería verse en la última página del asistente. Actualmente, se muestra en todas las páginas.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos de SQL Server y los escenarios relacionados, consulte [What is SQL Server Big Data Cluster?](../../big-data-cluster/big-data-cluster-overview.md) (¿Qué son los clústeres de macrodatos de SQL Server?)
