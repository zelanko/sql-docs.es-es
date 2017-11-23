---
title: "(Asignación de tipos) de la configuración del proyecto (MySQLToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
caps.latest.revision: "13"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 445f69a6c78293f74dfea35f40ea99c380108e72
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="project-settings-type-mapping-mysqltosql"></a>(Asignación de tipos) de la configuración del proyecto (MySQLToSQL)
La configuración del proyecto de asignación de tipo permite definir asignaciones de tipos de valor predeterminado para el proyecto SSMA.  

Asignación de tipos está disponible en los cuadros de diálogo de configuración del proyecto y la configuración predeterminada del proyecto:  
  
-   Utilice el cuadro de diálogo de configuración del proyecto para establecer las opciones de configuración para el proyecto actual. Para obtener acceso a la configuración de la asignación de tipo, en el menú Herramientas, seleccione la configuración del proyecto y, a continuación, haga clic en asignación de tipos en el panel izquierdo.  
  
-   Utilice el cuadro de diálogo de configuración de proyecto predeterminada para establecer las opciones de configuración para todos los proyectos. Para tener acceso a la asignación de tipo configuración, en el menú Herramientas, seleccione la configuración predeterminada del proyecto, tipo de proyecto de migración select para la que se requiere para ver / cambiar de configuración **versión de destino de migración** lista desplegable y, a continuación, haga clic en asignación de tipos en el panel izquierdo.  
  
## <a name="options"></a>Opciones  
  
##### <a name="source-type"></a>Tipo de origen  
Es el tipo de datos de MySQL, que debe asignarse al tipo de datos de la base de datos de destino.  
  
##### <a name="target-type"></a>Tipo de destino  
Escriba los datos de la base de datos de destino para el tipo de datos de MySQL especificado.  
  
##### <a name="add"></a>Agregar  
Haga clic para agregar un tipo de datos a la lista de asignación.  
  
##### <a name="edit"></a>Editar  
Haga clic para editar el tipo de datos seleccionado en la lista de asignación.  
  
##### <a name="remove"></a>Quitar  
Haga clic para quitar la asignación de tipos de datos seleccionados de la lista de asignación.  
  
##### <a name="reset-to-default"></a>Valores predeterminados  
Haga clic para restablecer la lista de asignación de tipo para los valores predeterminados SSMA.  
  
## <a name="type-mappings"></a>Asignaciones de tipos  
La tabla siguiente muestran las asignaciones predeterminadas entre tipos de datos de origen y de destino  
  
|||  
|-|-|  
|**Tipo de datos de MySQL**|**Tipo de datos SQL Server**|  
|bigint|bigint|  
|bigint [*.. 255]|bigint|  
|binary|binario [1]|  
|binario [de 0.. 1]|binario [1]|  
|binario [2..255]|binario [*]|  
|bit|binario [1]|  
|bits [0..8]|binario [1]|  
|bits [17..24]|binario [3]|  
|bits [25..32]|binario [4]|  
|bits [33..40]|binario [5]|  
|bits [41..48]|binario [6]|  
|bits [49..56]|binario [7]|  
|bits [57..64]|binario [8]|  
|bits [9..16]|binarios [2]|  
|blob|varbinary(max)|  
|BLOB [de 0.. 1]|varbinary [1]|  
|BLOB [2..8000]|varbinary [*]|  
|BLOB [8001.. *]|varbinary(max)|  
|bool|bit|  
|boolean|bit|  
|char|nchar [1]|  
|Char (bytes)|binario [1]|  
|bytes de carácter [de 0.. 1]|binario [1]|  
|bytes de Char [2..255]|binario [*]|  
|char [de 0.. 1]|nchar [1]|  
|Char [2..255]|nchar [*]|  
|character|nchar [1]|  
|carácter variable [de 0.. 1]|nvarchar [1]|  
|carácter variable [2..255]|nvarchar|  
|carácter [de 0.. 1]|nchar [1]|  
|caracteres [2..255]|nchar [*]|  
|date|date|  
|datetime|datetime2 [0]|  
|dec|decimal|  
|DEC [*.. 65]|decimal [*] [0]|  
|DEC [*.. 65][\*.. 30]|decimal [*] [\*]|  
|decimal|decimal|  
|decimal [*.. 65]|decimal [*] [0]|  
|decimal [*.. 65][\*.. 30]|decimal [*] [\*]|  
|double|float [53]|  
|precisión doble|float [53]|  
|precisión doble [*.. 255][\*.. 30]|numérico [*] [\*]|  
|Double [*.. 255][\*.. 30]|numérico [*] [\*]|  
|fijo|numeric|  
|fija [*.. 65][\*.. 30]|numérico [*] [\*]|  
|float|float [24]|  
|float [*.. 255][\*.. 30]|numérico [*] [\*]|  
|float [*.. 53]|float [53]|  
|int|int|  
|int [*.. 255]|int|  
|integer|int|  
|entero [*.. 255]|int|  
|longblob|varbinary(max)|  
|LONGTEXT|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|int|  
|mediumint [*.. 255]|int|  
|mediumtext|nvarchar(max)|  
|Car.|nchar [1]|  
|char nacional [de 0.. 1]|nchar [1]|  
|National char [2..255]|nchar [*]|  
|caracteres no nacionales|nchar [1]|  
|national character varying de|nvarchar [1]|  
|caracteres no nacionales distintos [de 0.. 1]|nvarchar [1]|  
|caracteres no nacionales variable [2..4000]|nvarchar [*]|  
|national character varying de [4001.. *]|nvarchar(max)|  
|caracteres no nacionales [de 0.. 1]|nchar [1]|  
|caracteres no nacionales [2..255]|nchar [*]|  
|varchar nacional|nvarchar [1]|  
|varchar nacional [de 0.. 1]|nvarchar [1]|  
|varchar nacional [2..4000]|nvarchar [*]|  
|varchar nacional [4001.. *]|nvarchar(max)|  
|nchar|nchar [1]|  
|nchar varchar|nvarchar [1]|  
|nchar varchar [de 0.. 1]|nvarchar [1]|  
|nchar varchar [2..4000]|nvarchar [*]|  
|nchar varchar [4001.. *]|nvarchar(max)|  
|nchar [de 0.. 1]|nchar [1]|  
|nchar [2..255]|nchar [*]|  
|numeric|numeric|  
|numérico [*.. 65]|numérico [*] [0]|  
|numérico [*.. 65][\*.. 30]|numérico [*] [\*]|  
|nvarchar|nvarchar [1]|  
|nvarchar [de 0.. 1]|nvarchar [1]|  
|nvarchar [2..4000]|nvarchar [*]|  
|nvarchar [4001.. *]|nvarchar(max)|  
|real|float [53]|  
|real [*.. 255][\*.. 30]|numérico [*] [\*]|  
|Serie|bigint|  
|smallint|smallint|  
|smallint [*.. 255]|smallint|  
|texto|nvarchar(max)|  
|texto [de 0.. 1]|nvarchar [1]|  
|texto [2..4000]|nvarchar [*]|  
|texto [4001.. *]|nvarchar(max)|  
|time|time|  
|timestamp|datetime|  
|tinyblob|varbinary [255]|  
|tinyint|smallint|  
|tinyint [*.. 255]|smallint|  
|tinytext|nvarchar [255]|  
|bigint sin signo|bigint|  
|sin signo bigint [*.. 255]|bigint|  
|dec sin signo|decimal|  
|dec sin signo [*.. 65]|decimal [*] [0]|  
|dec sin signo [*.. 65][\*.. 30]|decimal [*] [\*]|  
|decimal sin signo|decimal|  
|decimal sin signo [*.. 65]|decimal [*] [0]|  
|decimal sin signo [*.. 65][\*.. 30]|decimal [*] [\*]|  
|doble sin signo|float [53]|  
|sin signo de precisión doble|float [53]|  
|sin signo de doble precisión [*.. 255][\*.. 30]|numérico [*] [\*]|  
|sin signo double [*.. 255][\*.. 30]|numérico [*] [\*]|  
|sin signo fijo|numeric|  
|sin signo fijo [*.. 65][\*.. 30]|numérico [*] [\*]|  
|float sin signo|float [24]|  
|float sin signo [*.. 255][\*.. 30]|numérico [*] [\*]|  
|float sin signo [*.. 53]|float [53]|  
|unsigned int|bigint|  
|int sin signo [*.. 255]|bigint|  
|entero sin signo|bigint|  
|entero sin signo [*.. 255]|bigint|  
|mediumint sin signo|int|  
|mediumint sin signo [*.. 255]|int|  
|numérico sin signo|numeric|  
|numérico sin signo [*.. 65]|numérico [*] [0]|  
|numérico sin signo [*.. 65][\*.. 30]|numérico [*] [\*]|  
|real sin signo|float [53]|  
|sin signo real [*.. 255[[\*.. 30]|numérico [*] [\*]|  
|smallint sin signo|int|  
|smallint sin signo [*.. 255]|int|  
|tinyint sin signo|tinyint|  
|tinyint sin signo [*.. 255]|tinyint|  
|varbinary [de 0.. 1]|varbinary [1]|  
|varbinary [2..8000]|varbinary [*]|  
|varbinary [8001.. *]|varbinary(max)|  
|varchar [de 0.. 1]|nvarchar [1]|  
|varchar [2..4000]|nvarchar [*]|  
|varchar [4001.. *]|nvarchar(max)|  
|year|smallint|  
|año [2..2]|smallint|  
|año [4..4]|smallint|  
  
##### <a name="add"></a>Agregar  
Haga clic para agregar un tipo de datos a la lista de asignación.  
  
##### <a name="edit"></a>Editar  
Haga clic para editar un tipo de datos en la lista de asignación.  
  
##### <a name="remove"></a>Quitar  
Haga clic para quitar la asignación de tipos de datos seleccionados de la lista de asignación.  
  
##### <a name="reset-to-default"></a>Valores predeterminados  
Haga clic para restablecer todas las asignaciones de tipo de datos a los valores predeterminados SSMA.  
  
