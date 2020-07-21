---
title: Importar en un proyecto de base de datos
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLPROJECTIMPORTSNAPSHOTSUMMARYDIALOG.DIALOG
- SQL.DATA.TOOLS.SQLPROJECTIMPORTDATABASESUMMARYDIALOG.DIALOG
- SQL.DATA.TOOLS.IMPORTSCRIPTWIZARD.SUMMARY
ms.assetid: d0a0a394-6cb6-416a-a25f-9babf8ba294a
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 0cfdbb9cb094188e372424257656953b62635996
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246449"
---
# <a name="import-into-a-database-project"></a>Importar en un proyecto de base de datos

Puede usar Importar para rellenar un proyecto con nuevos objetos a partir de una base de datos activa o un .dacpac, o para actualizar los objetos existentes en el proyecto con una nueva definición a partir de un script. Hay algunas diferencias de comportamiento que hay que destacar entre estas tres rutas, que se describen a continuación.  
  
**Menú de importación**  
  
![Menú de importación de SSDT](../ssdt/media/ssdt-import.gif "Menú de importación de SSDT")  
  
**Secciones de este tema**  
  
[Importar el origen: aplicación de capa de datos o de base de datos (*.dacpac)](#bkmk_import_source_db)  
  
[Importar el origen: Script (*.sql)](#bkmk_import_source_script)  
  
[Importar objetos cifrados](#bkmk_import_encrypted)  
  
## <a name="import-source-database-or-data-tier-application-dacpac"></a><a name="bkmk_import_source_db"></a>Importar el origen: aplicación de capa de datos o de base de datos (*.dacpac)  
La capacidad de importar el esquema a partir de una base de datos o un archivo .dacpac solo está disponible si no hay objetos de esquema ya definidos en el proyecto. Esto no incluye los scripts RefactorLogs ni Pre/Post-Deployment.  
  
En la importación, las definiciones de objeto se incluirán en archivos de proyecto con los valores predeterminados de la organización de SSDT para los nuevos objetos: nuevos archivos para los objetos de nivel superior, elementos secundarios jerárquicos definidos en el mismo archivo que el primario, restricciones de tabla y columna definidas insertadas siempre que sea posible. Para definir más la visibilidad y el control de cada objeto, use Comparación de esquema en lugar de Importar.  
  
Si el origen de la importación contiene scripts previos o posteriores a la implementación, RefactorLogs o definiciones de variables SQLCMD, se importarán en el proyecto. Si el proyecto ya contiene alguno de estos artefactos, los archivos importados se agregarán a una carpeta **Omitido al importar** del proyecto.  
  
**Carpeta Omitido al importar**  
  
![SSDT se omite en la carpeta de importación](../ssdt/media/ssdt-ignoredonimport.gif "SSDT se omite en la carpeta de importación")  
  
## <a name="import-source-script-sql"></a><a name="bkmk_import_source_script"></a>Importar el origen: Script (*.sql)  
Todos los objetos del origen de importación que *no* existan ya en el proyecto se agregarán y todos los objetos del origen de importación que *ya* existan en el proyecto sobrescribirán la definición de objeto del proyecto.  
  
> [!NOTE]  
> Hay dos errores conocidos en esta ruta que se corregirán en una versión futura:  
>   
> -   Si las restricciones de tabla o columna se definen fuera de la instrucción CREATE TABLE en la definición de tabla del proyecto, la importación sobrescribirá la definición de tabla de modo que la restricción se inserte. Sin embargo, dejará la restricción de fuera de línea, lo que provoca restricciones duplicadas en el proyecto.  
> -   Las claves maestras o las claves de cifrado de base de datos del script de origen que ya existan en el proyecto se duplicarán al importar. Quitar duplicados para compilar el proyecto.  
  
El proceso Importar a partir del script no comprenderá scripts previos o posteriores a la implementación, variables SQLCMD ni archivos RefactorLog. Estas y cualquier otra construcción no admitida que se detecte en la importación se colocará en un archivo **ScriptsIgnoredOnImport.sql** de una carpeta **Scripts** del proyecto.  
  
 
## <a name="import-encrypted-objects"></a><a name="bkmk_import_encrypted"></a>Importar objetos cifrados  
Al importar los objetos cifrados en un proyecto de base de datos, el cuerpo total de la definición de objeto no siempre puede recuperarse del servidor. Por tanto, el comportamiento de la importación puede ser diferente al tratar con esta clase de objetos.  
  
Cuando toda la definición de objeto no se pueda recuperar, se incluirá el encabezado o pie del objeto con un cuerpo ficticio. Puede esperar encontrar este comportamiento al importar o usar la comparación de esquema siempre que el origen sea una base de datos activa o un archivo .dacpac extraído de una base de datos.  
  
**Script con un cuerpo ficticio**  
  
![Script con un cuerpo ficticio](../ssdt/media/ssdt-procwithencryption.gif "Script con un cuerpo ficticio")  
  
En el caso en que la definición completa del objeto esté disponible y pueda recuperarse, la importación y comparación del esquema la llevarán al proyecto en su totalidad. Esto ocurre al actualizar el proyecto a partir de un script, un archivo .dacpac generado a partir de un proyecto de base de datos u otro proyecto de base de datos.  
  
