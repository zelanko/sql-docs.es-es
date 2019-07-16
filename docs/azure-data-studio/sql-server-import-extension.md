---
title: Extensión de importación SQL Server
titleSuffix: Azure Data Studio
description: Instalar y usar la extensión de importación de SQL Server (versión preliminar) para Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 012c2c880e81c095e90086cf26ebffd6117d534e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959120"
---
# <a name="sql-server-import-extension-preview"></a>Extensión de importación de SQL Server (versión preliminar)

La extensión de importación de SQL Server (versión preliminar) convierte archivos .txt y .csv en una tabla SQL. Este asistente usa un marco de trabajo de Microsoft Research conocido como [Program Synthesis using ejemplos (PROSE)](https://microsoft.github.io/prose/) para analizar el archivo con la entrada de usuario mínimos de forma inteligente. Es un marco eficaz para el tratamiento de datos, y es la misma tecnología que alimenta Flash Fill en Microsoft Excel

Para obtener más información sobre la versión SSMS de esta característica, puede leer [en este artículo](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard).


## <a name="install-the-sql-server-import-extension"></a>Instalar la extensión de importación de SQL Server

1. Para abrir el Administrador de extensiones y tener acceso a las extensiones disponibles, seleccione el icono de extensiones o **extensiones** en el **vista** menú.
2. Seleccione una extensión disponible para ver sus detalles.

   ![Administrador de extensiones de importación](media/sql-server-import-extension/import-wizard-install.png)

1. Seleccione la extensión que desee y **instalar** lo.
2. Seleccione **recarga** para habilitar la extensión (solo es necesario instalar una extensión por primera vez).

## <a name="start-import-wizard"></a>Iniciar a Asistente para importación

1. Para iniciar la importación de SQL Server, en primer lugar realice una conexión a un servidor en la pestaña servidores.
2. Después de realizar una conexión, explorar en profundidad la base de datos de destino que desea importar un archivo en una tabla SQL.
3. Haga doble clic en la base de datos y haga clic en **Asistente para importación**.
    ![Asistente para importación abierto](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>Importación de un archivo
1. Cuando hace clic para iniciar al asistente, el servidor y base de datos están ya rellena automáticamente. Si hay otras conexiones activas, puede seleccionar en la lista desplegable. 
    
    Seleccione un archivo haciendo clic en **Examinar.** Debería rellenar automáticamente el nombre de tabla según el nombre de archivo, pero se puede también cambiar usted mismo.

    De forma predeterminada, el esquema será dbo, pero puede cambiarlo. Haga clic en **Siguiente** para continuar.
    ![archivo de entrada](media/sql-server-import-extension/import-wizard-input-file.png)
1. El asistente generará una vista previa en función de las primeras 50 filas. No hay ninguna acción adicional en esta página no sea de comprobación de que los datos sean precisos. Haga clic en **Siguiente** para continuar.
    ![Asistente para importación abierto](media/sql-server-import-extension/import-wizard-preview-data.png)
2. En esta página, puede realizar cambios en el nombre de columna, tipo de datos, si es una clave principal o permitir que los valores NULL. Puede realizar cambios tantos como sea necesario. Haga clic en **importar datos** para continuar.
    ![Asistente para importación abierto](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. Esta página proporciona un resumen de las acciones elegido. También puede ver si la tabla inserta correctamente o no. 

    Puede hacer clic en **hecho anterior** si necesita realizar cambios, o **nuevo archivo de importación** rápidamente importar otro archivo.
    ![Asistente para importación abierto](media/sql-server-import-extension/import-wizard-summary.png)
1. Compruebe si la tabla se importaron correctamente mediante la actualización de la base de datos de destino o que se ejecuta una consulta SELECT en el nombre de tabla.

## <a name="next-steps"></a>Pasos siguientes
- Para obtener más información sobre el Asistente para importación, lea el [entrada de blog](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/).
- Para obtener más información sobre PROSE, lea el [documentación.](https://microsoft.github.io/prose/)
