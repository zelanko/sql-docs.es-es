---
title: "(Asignación de tipos) de la configuración del proyecto (MySQLToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
caps.latest.revision: 
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ca62e82b85d401f99a6e59f6f440d9a6519e58d
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2018
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
|bigint[*..255]|bigint|  
|binary|binario [1]|  
|binario [de 0.. 1]|binario [1]|  
|binario [2..255]|binary[*]|  
|bit|binario [1]|  
|bit[0..8]|binario [1]|  
|bit[17..24]|binario [3]|  
|bit[25..32]|binario [4]|  
|bit[33..40]|binario [5]|  
|bit[41..48]|binario [6]|  
|bit[49..56]|binario [7]|  
|bit[57..64]|binario [8]|  
|bit[9..16]|binarios [2]|  
|blob|varbinary(max)|  
|blob[0..1]|varbinary [1]|  
|blob[2..8000]|varbinary[*]|  
|blob[8001..*]|varbinary(max)|  
|bool|bit|  
|boolean|bit|  
|char|nchar[1]|  
|Char (bytes)|binario [1]|  
|bytes de carácter [de 0.. 1]|binario [1]|  
|bytes de Char [2..255]|binary[*]|  
|char[0..1]|nchar[1]|  
|char[2..255]|nchar[*]|  
|character|nchar[1]|  
|carácter variable [de 0.. 1]|nvarchar[1]|  
|carácter variable [2..255]|nvarchar|  
|character[0..1]|nchar[1]|  
|character[2..255]|nchar[*]|  
|date|date|  
|datetime|datetime2[0]|  
|dec|decimal|  
|dec[*..65]|decimal[*][0]|  
|dec[*..65][\*..30]|decimal[*][\*]|  
|decimal|decimal|  
|decimal[*..65]|decimal[*][0]|  
|decimal[*..65][\*..30]|decimal[*][\*]|  
|double|float[53]|  
|precisión doble|float[53]|  
|precisión doble [*.. 255][\*.. 30]|numeric[*][\*]|  
|double[*..255][\*..30]|numeric[*][\*]|  
|fijo|numeric|  
|fixed[*..65][\*..30]|numeric[*][\*]|  
|float|float[24]|  
|float[*..255][\*..30]|numeric[*][\*]|  
|float[*..53]|float[53]|  
|int|int|  
|int[*..255]|int|  
|integer|int|  
|integer[*..255]|int|  
|longblob|varbinary(max)|  
|LONGTEXT|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|int|  
|mediumint[*..255]|int|  
|mediumtext|nvarchar(max)|  
|Car.|nchar[1]|  
|char nacional [de 0.. 1]|nchar[1]|  
|National char [2..255]|nchar[*]|  
|caracteres no nacionales|nchar[1]|  
|national character varying de|nvarchar[1]|  
|caracteres no nacionales distintos [de 0.. 1]|nvarchar[1]|  
|caracteres no nacionales variable [2..4000]|nvarchar[*]|  
|national character varying de [4001.. *]|nvarchar(max)|  
|caracteres no nacionales [de 0.. 1]|nchar[1]|  
|caracteres no nacionales [2..255]|nchar[*]|  
|varchar nacional|nvarchar[1]|  
|varchar nacional [de 0.. 1]|nvarchar[1]|  
|varchar nacional [2..4000]|nvarchar[*]|  
|varchar nacional [4001.. *]|nvarchar(max)|  
|NCHAR|nchar[1]|  
|nchar varchar|nvarchar[1]|  
|nchar varchar [de 0.. 1]|nvarchar[1]|  
|nchar varchar[2..4000]|nvarchar[*]|  
|nchar varchar[4001..*]|nvarchar(max)|  
|nchar[0..1]|nchar[1]|  
|nchar[2..255]|nchar[*]|  
|numeric|numeric|  
|numeric[*..65]|numeric[*][0]|  
|numeric[*..65][\*..30]|numeric[*][\*]|  
|nvarchar|nvarchar[1]|  
|nvarchar[0..1]|nvarchar[1]|  
|nvarchar[2..4000]|nvarchar[*]|  
|nvarchar[4001..*]|nvarchar(max)|  
|real|float[53]|  
|real[*..255][\*..30]|numeric[*][\*]|  
|Serie|bigint|  
|smallint|smallint|  
|smallint[*..255]|smallint|  
|texto|nvarchar(max)|  
|text[0..1]|nvarchar[1]|  
|text[2..4000]|nvarchar[*]|  
|text[4001..*]|nvarchar(max)|  
|time|time|  
|TIMESTAMP|datetime|  
|tinyblob|varbinary [255]|  
|tinyint|smallint|  
|tinyint[*..255]|smallint|  
|tinytext|nvarchar[255]|  
|bigint sin signo|bigint|  
|sin signo bigint [*.. 255]|bigint|  
|dec sin signo|decimal|  
|dec sin signo [*.. 65]|decimal[*][0]|  
|dec sin signo [*.. 65][\*.. 30]|decimal[*][\*]|  
|decimal sin signo|decimal|  
|decimal sin signo [*.. 65]|decimal[*][0]|  
|decimal sin signo [*.. 65][\*.. 30]|decimal[*][\*]|  
|doble sin signo|float[53]|  
|sin signo de precisión doble|float[53]|  
|sin signo de doble precisión [*.. 255][\*.. 30]|numeric[*][\*]|  
|sin signo double [*.. 255][\*.. 30]|numeric[*][\*]|  
|sin signo fijo|numeric|  
|sin signo fijo [*.. 65][\*.. 30]|numeric[*][\*]|  
|float sin signo|float[24]|  
|float sin signo [*.. 255][\*.. 30]|numeric[*][\*]|  
|float sin signo [*.. 53]|float[53]|  
|unsigned int|bigint|  
|int sin signo [*.. 255]|bigint|  
|entero sin signo|bigint|  
|entero sin signo [*.. 255]|bigint|  
|mediumint sin signo|int|  
|mediumint sin signo [*.. 255]|int|  
|numérico sin signo|numeric|  
|numérico sin signo [*.. 65]|numeric[*][0]|  
|numérico sin signo [*.. 65][\*.. 30]|numeric[*][\*]|  
|real sin signo|float[53]|  
|sin signo real [*.. 255[[\*.. 30]|numeric[*][\*]|  
|smallint sin signo|int|  
|smallint sin signo [*.. 255]|int|  
|tinyint sin signo|tinyint|  
|tinyint sin signo [*.. 255]|tinyint|  
|varbinary [de 0.. 1]|varbinary [1]|  
|varbinary[2..8000]|varbinary[*]|  
|varbinary[8001..*]|varbinary(max)|  
|varchar[0..1]|nvarchar[1]|  
|varchar[2..4000]|nvarchar[*]|  
|varchar[4001..*]|nvarchar(max)|  
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
  
