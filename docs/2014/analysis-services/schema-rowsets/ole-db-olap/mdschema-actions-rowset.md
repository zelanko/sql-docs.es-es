---
title: Conjunto de filas MDSCHEMA_ACTIONS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_ACTIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_ACTIONS rowset
ms.assetid: f73081f8-ac51-4286-b46e-2b34e792c3e0
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c7382056922a52e734df61015df85930682d0db0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319375"
---
# <a name="mdschemaactions-rowset"></a>Conjunto de filas MDSCHEMA_ACTIONS
  Describe las acciones que pueden estar disponibles para la aplicación cliente.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_ACTIONS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||El nombre de la base de datos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||No compatible. Siempre contiene `VT_NULL`.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo al que pertenece esta acción.|  
|`ACTION_NAME`|`DBTYPE_WSTR`||El nombre de esta acción.|  
|`ACTION_TYPE`|`DBTYPE_I4`||Un mapa de bits que se utiliza para especificar el método de activación de la acción. El archivo Msmd.h define las constantes de valor de bit siguientes para este mapa de bits:<br /><br /> -   `MDACTION_TYPE_URL` (`0x01`)<br />-   `MDACTION_TYPE_HTML` (`0x02`)<br />-   `MDACTION_TYPE_STATEMENT` (`0x04`)<br />-   `MDACTION_TYPE_DATASET` (`0x08`)<br />-   `MDACTION_TYPE_ROWSET` (`0x10`)<br />-   `MDACTION_TYPE_COMMANDLINE` (`0x20`)<br />-   `MDACTION_TYPE_PROPRIETARY` (`0x40`)<br />-   `MDACTION_TYPE_REPORT` (`0x80`)<br />-   `MDACTION_TYPE_DRILLTHROUGH` (`0x100`)|  
|`COORDINATE`|`DBTYPE_WSTR`||Una expresión multidimensional (MDX) que especifica un objeto o una coordenada en el espacio multidimensional en el que se realiza la acción. La aplicación cliente es responsable de proporcionar el valor de esta columna de restricción.<br /><br /> `CORDINATE` debe resolver como el objeto especificado en `COORDINATE_TYPE`.|  
|`COORDINATE_TYPE`|`DBTYPE_I4`||Un mapa de bits que especifica cómo `COORDINATE` interpreta la columna de restricción.  El archivo Msmd.h define las constantes de valor de bit siguientes para este mapa de bits:<br /><br /> -   `MDACTION_COORDINATE_CUBE` (`1`)<br />-   `MDACTION_COORDINATE_DIMENSION` (`2`)<br />     hace referencia a las jerarquías de las dimensiones.<br />-   `MDACTION_COORDINATE_LEVEL` (`3`)<br />-   `MDACTION_COORDINATE_MEMBER` (`4`)<br />-   `MDACTION_COORDINATE_SET` (`5`)<br />-   `MDACTION_COORDINATE_CELL` (`6`)|  
|`ACTION_CAPTION`|`DBTYPE_WSTR`||El nombre de acción si no se ha especificado ningún título y no se ha especificado ninguna traducción en la DDL.<br /><br /> Si se ha especificado un título o traducciones, y `CaptionIsMDX` es falso, una de las cadenas siguientes:<br /><br /> -La traducción del idioma correspondiente.<br />-El título especificado si se ha encontrado ninguna traducción para el idioma especificado.<br />-El nombre de acción si se ha encontrado ninguna traducción y el título no se ha especificado en DDL.<br /><br /> Si se han especificado un título o traducciones, y `CaptionIsMDX` es verdadero, la cadena que es el resultado de buscar la traducción adecuada para el idioma especificado o la traducción especificada en el título DDL, y calculando la fórmula para crear la cadena.<br /><br /> Si la acción se especifica en un script de MDX, no hay ninguna traducción y el título siempre se trata como expresión MDX.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción fácil de comprender de la acción.|  
|`CONTENT`|`DBTYPE_WSTR`||La expresión o contenido de la acción que se va a ejecutar.|  
|`APPLICATION`|`DBTYPE_WSTR`||Nombre de la aplicación que se utilizará para ejecutar la acción.|  
|`INVOCATION`|`DBTYPE_I4`||Información sobre cómo se debería invocar la acción:<br /><br /> -   `MDACTION_INVOCATION_INTERACTIVE` (`1`) indica una acción normal utilizada durante las operaciones normales. Este el valor predeterminado de esta columna.<br />-   `MDACTION_INVOCATION_ON_OPEN` (`2`) indica que la acción debe realizarse cuando se abre por primera vez el cubo.<br />-   `MDACTION_INVOCATION_BATCH` (`4`) indica que la acción se realiza como parte de una operación por lotes o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tarea.<br /><br /> Estos valores de enumeración se definen en el archivo Msmd.h.|  
  
 El conjunto de filas se ordena en `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `ACTION_NAME`.  
  
> [!NOTE]  
>  Las acciones del tipo `MDACTION_TYPE_PROPRIETARY` deben proporcionar un valor para la columna `APPLICATION`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_ACTIONS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Obligatorio|  
|`ACTION_NAME`|`DBTYPE_WSTR`|Opcional|  
|`ACTION_TYPE`|`DBTYPE_I4`|Opcional|  
|`COORDINATE`|`DBTYPE_WSTR`|Obligatorio|  
|`COORDINATE_TYPE`|`DBTYPE_I4`|Obligatorio|  
|`INVOCATION`|`DBTYPE_I4`|(Opcional) La columna de restricción `INVOCATION` tiene como valor predeterminado el valor de `MDACTION_INVOCATION_INTERACTIVE`. Para recuperar todas las acciones, utilice el valor `MDACTION_INVOCATION_ALL` en la columna de restricción `INVOCATION`.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -1 CUBO<br />-DIMENSIÓN DE 2<br /><br /> La restricción predeterminada es un valor de 1.|  
  
> [!IMPORTANT]  
>  La columna de restricción `INVOCATION` tiene un valor predeterminado de `MDACTION_INVOCATION_INTERACTIVE`. Cualquier conjunto de filas de esquema que no especifique explícitamente un valor para esta columna contiene únicamente las filas con este valor. Si desea que el conjunto de filas contenga el conjunto completo de acciones, utilice la constante `MDACTION_INVOCATION_ALL` en la columna de restricción `INVOCATION`.  
  
 Las aplicaciones cliente pueden definir más de una `ACTION_TYPE` utilizando el operador OR.  
  
## <a name="remarks"></a>Notas  
 En la siguiente tabla se recogen las combinaciones válidas de `COORDINATE` y `COORDINATE_TYPE`.  
  
|Tipo de objeto COORDINATE|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|`Cube`|`MDACTION_COORDINATE_CUBE`|  
|`Dimension`|`MDACTION_COORDINATE_DIMENSION`<br /><br /> `MDACTION_COORDINATE_LEVEL`<br /><br /> `MDACTION_COORDINATE_MEMBER`<br /><br /> `MDACTION_COORDINATE_SET`<br /><br /> `MDACTION_COORDINATE_CELL`|  
|`Hierarchy`|`MDACTION_COORDINATE_DIMENSION`|  
|`Level`|`MDACTION_COORDINATE_LEVEL`|  
|`Member`|`MDACTION_COORDINATE_MEMBER`|  
|`Set`|`MDACTION_COORDINATE_SET`|  
|`cell`|`MDACTION_COORDINATE_CELL`|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
