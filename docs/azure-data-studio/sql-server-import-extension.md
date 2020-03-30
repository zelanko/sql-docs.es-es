---
title: Extensión de importación de SQL Server
titleSuffix: Azure Data Studio
description: Instalación y uso de la extensión de importación de SQL Server (versión preliminar) para Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 012c2c880e81c095e90086cf26ebffd6117d534e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "67959120"
---
# <a name="sql-server-import-extension-preview"></a>Extensión de importación de SQL Server (versión preliminar)

La extensión de importación de SQL Server (versión preliminar) convierte los archivos .txt y .csv en una tabla SQL. Este asistente emplea un marco de Microsoft Research conocido como [Program Synthesis uing Examples (PROSE)](https://microsoft.github.io/prose/) para analizar de forma inteligente el archivo con una mínima intervención del usuario. Es un marco eficaz para la limpieza y transformación de datos y es la misma tecnología que proporciona el relleno rápido en Microsoft Excel.

Para obtener más información sobre la versión de SSMS de esta característica, lea [este artículo](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard).


## <a name="install-the-sql-server-import-extension"></a>Instalación de la extensión de importación de SQL Server

1. Para abrir el administrador de extensiones y acceder a las extensiones disponibles, seleccione el icono de extensiones, o bien seleccione **Extensiones** en el menú **Ver**.
2. Seleccione una extensión disponible para ver sus detalles.

   ![Administrador de la extensión de importación](media/sql-server-import-extension/import-wizard-install.png)

1. Seleccione la extensión que quiera e **instálela**.
2. Seleccione **Recargar** para habilitar la extensión (solo es necesario la primera vez que se instala una extensión).

## <a name="start-import-wizard"></a>Inicie el asistente para importar

1. Para iniciar la importación de SQL Server, primero establezca una conexión con un servidor en la pestaña Servidores.
2. Después de establecer una conexión, explore en profundidad la base de datos de destino en la que quiere importar un archivo a una tabla SQL.
3. Haga clic con el botón derecho en la base de datos y haga clic en **Asistente para importación**.
    ![abrir asistente para importación](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>Importar un archivo
1. Al hacer clic con el botón derecho para iniciar el asistente, el servidor y la base de datos ya se rellenan automáticamente. Si hay otras conexiones activas, puede seleccionarlas en la lista desplegable. 
    
    Haga clic en **Examinar** para seleccionar un archivo. Debería rellenar automáticamente el nombre de la tabla en función del nombre de archivo, pero también puede cambiarlo usted.

    De forma predeterminada, el esquema será DBO, pero puede cambiarlo. Haga clic en **Siguiente** para continuar.
    ![archivo de entrada](media/sql-server-import-extension/import-wizard-input-file.png)
1. El asistente generará una vista previa basada en las primeras 50 filas. No hay ninguna acción adicional en esta página que no sea comprobar que los datos parecen precisos. Haga clic en **Siguiente** para continuar.
    ![abrir asistente para importación](media/sql-server-import-extension/import-wizard-preview-data.png)
2. En esta página, puede realizar cambios en el nombre de columna, el tipo de datos, si es una clave principal o permitir valores NULL. Puede realizar todos los cambios que quiera. Haga clic en **Importar datos** para continuar.
    ![abrir asistente para importación](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. Esta página proporciona un resumen de las acciones elegidas. También puede ver si la tabla se insertó correctamente o no. 

    Puede hacer clic en **Listo, Anterior** si necesita realizar cambios o **Import new file** (Importar archivo nuevo) para importar rápidamente otro archivo.
    ![abrir asistente para importación](media/sql-server-import-extension/import-wizard-summary.png)
1. Compruebe si la tabla se importó correctamente actualizando la base de datos de destino o ejecutando una consulta SELECT en el nombre de la tabla.

## <a name="next-steps"></a>Pasos siguientes
- Para obtener más información sobre el Asistente para importación, lea esta [entrada de blog](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/).
- Para obtener más información sobre PROSE, lea [la documentación.](https://microsoft.github.io/prose/)
