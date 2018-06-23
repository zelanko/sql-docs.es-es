---
title: Conjunto de filas MDSCHEMA_KPIS | Documentos de Microsoft
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
- MDSCHEMA_KPIS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_KPIS rowset
ms.assetid: 40fb5112-6a90-4455-82b3-8b6322490222
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 28a5f4af179c058f822a773dc691383dbee028fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203050"
---
# <a name="mdschemakpis-rowset"></a>Conjunto de filas MDSCHEMA_KPIS
  Describe los indicadores clave de rendimiento (KPI) incluidos en una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_KPIS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||Base de datos de origen.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Cubo primario del KPI.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||Grupo de medida asociado para el KPI.<br /><br /> Puede utilizar esta columna para determinar las dimensiones del KPI. Si "**\<NULL >**", todos los grupos de medida dimensionarán el KPI.<br /><br /> El valor predeterminado es "**\<NULL >**".|  
|`KPI_NAME`|`DBTYPE_WSTR`||Nombre del KPI.|  
|`KPI_CAPTION`|`DBTYPE_WSTR`||Etiqueta o título asociado al KPI. Se utiliza principalmente para la presentación. Si no existe ningún título, se devuelve `KPI_NAME`.|  
|`KPI_DESCRIPTION`|`DBTYPE_WSTR`||Descripción del KPI en lenguaje natural.|  
|`KPI_DISPLAY_FOLDER`|`DBTYPE_WSTR`||Cadena que identifica la ruta de la carpeta que usa la aplicación cliente para mostrar el miembro. La aplicación cliente define el separador de niveles de carpetas. Para las herramientas y clientes proporcionados por [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], la barra diagonal inversa (\\) es el separador de niveles. Asignar varias carpetas para mostrar, utilice un punto y coma (;) para separar las carpetas.|  
|`KPI_VALUE`|`DBTYPE_WSTR`||Nombre único del miembro en la dimensión de medidas para el valor del KPI.|  
|`KPI_GOAL`|`DBTYPE_WSTR`||Nombre único del miembro en la dimensión de medidas para el objetivo del KPI.<br /><br /> Devuelve `NULL` si no hay ningún objetivo definido.|  
|`KPI_STATUS`|`DBTYPE_WSTR`||Nombre único del miembro en la dimensión de medidas para el estado del KPI.<br /><br /> Devuelve `NULL` si no hay ningún estado definido.|  
|`KPI_TREND`|`DBTYPE_WSTR`||Nombre único del miembro en la dimensión de medidas para la tendencia del KPI.<br /><br /> Devuelve `NULL` si no hay ninguna tendencia definida.|  
|`KPI_STATUS_GRAPHIC`|`DBTYPE_WSTR`||Representación gráfica predeterminada del KPI.|  
|`KPI_TREND_GRAPHIC`|`DBTYPE_WSTR`||Representación gráfica predeterminada del KPI.|  
|`KPI_WEIGHT`|`DBTYPE_WSTR`||Nombre único del miembro en la dimensión de medidas para el peso del KPI.|  
|`KPI_CURRENT_TIME_MEMBER`|`DBTYPE_WSTR`||Nombre único del miembro en la dimensión de tiempo que define el contexto temporal del KPI.<br /><br /> Devuelve `NULL` si no hay ningún miembro de hora definido.|  
|`KPI_PARENT_KPI_NAME`|`DBTYPE_WSTR`||Nombre del KPI primario.|  
|`SCOPE`|`DBTYPE_I4`||Ámbito del KPI. El KPI puede ser de sesión o global.<br /><br /> Esta columna admite cualquiera de los siguientes valores:<br /><br /> -MDKPI_SCOPE_GLOBAL = 1<br />-MDKPI_SCOPE_SESSION = 2|  
|`ANNOTATIONS`|`DBTYPE_WSTR`||(Opcional) Conjunto de notas en formato XML.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_KPIS` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`KPI_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -   `1` CUBO<br />-   `2` DIMENSIÓN<br /><br /> La restricción predeterminada es un valor de `1`.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  