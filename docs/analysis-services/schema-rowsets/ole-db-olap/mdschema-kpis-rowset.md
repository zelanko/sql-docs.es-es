---
title: Conjunto de filas MDSCHEMA_KPIS | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_KPIS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_KPIS rowset
ms.assetid: 40fb5112-6a90-4455-82b3-8b6322490222
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 273adea0694ae9b59b2a49f26d04165c3fe948d4
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="mdschemakpis-rowset"></a>Conjunto de filas MDSCHEMA_KPIS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Describe los indicadores clave de rendimiento (KPI) dentro de una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **MDSCHEMA_KPIS** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Base de datos de origen.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|No compatible.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Cubo primario del KPI.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|Grupo de medida asociado para el KPI.<br /><br /> Puede utilizar esta columna para determinar las dimensiones del KPI. Si "**\<NULL >**", todos los grupos de medida dimensionarán el KPI.<br /><br /> El valor predeterminado es "**\<NULL >**".|  
|**NOMBRE_KPI**|**DBTYPE_WSTR**|Nombre del KPI.|  
|**KPI_CAPTION**|**DBTYPE_WSTR**|Etiqueta o título asociado al KPI. Se utiliza principalmente para la presentación. Si no existe ningún título, **nombre_kpi** se devuelve.|  
|**KPI_DESCRIPTION**|**DBTYPE_WSTR**|Descripción del KPI en lenguaje natural.|  
|**KPI_DISPLAY_FOLDER**|**DBTYPE_WSTR**|Cadena que identifica la ruta de la carpeta que usa la aplicación cliente para mostrar el miembro. La aplicación cliente define el separador de niveles de carpetas. Para las herramientas y clientes proporcionados por [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], la barra diagonal inversa (\\) es el separador de niveles. Asignar varias carpetas para mostrar, utilice un punto y coma (;) para separar las carpetas.|  
|**KPI_VALUE**|**DBTYPE_WSTR**|Nombre único del miembro en la dimensión de medidas para el valor del KPI.|  
|**KPI_GOAL**|**DBTYPE_WSTR**|Nombre único del miembro en la dimensión de medidas para el objetivo del KPI.<br /><br /> Devuelve **NULL** si no hay ningún objetivo definido.|  
|**KPI_STATUS**|**DBTYPE_WSTR**|Nombre único del miembro en la dimensión de medidas para el estado del KPI.<br /><br /> Devuelve **NULL** si no hay ningún estado definido.|  
|**KPI_TREND**|**DBTYPE_WSTR**|Nombre único del miembro en la dimensión de medidas para la tendencia del KPI.<br /><br /> Devuelve **NULL** si no hay ninguna tendencia definida.|  
|**KPI_STATUS_GRAPHIC**|**DBTYPE_WSTR**|Representación gráfica predeterminada del KPI.|  
|**KPI_TREND_GRAPHIC**|**DBTYPE_WSTR**|Representación gráfica predeterminada del KPI.|  
|**KPI_WEIGHT**|**DBTYPE_WSTR**|Nombre único del miembro en la dimensión de medidas para el peso del KPI.|  
|**KPI_CURRENT_TIME_MEMBER**|**DBTYPE_WSTR**|Nombre único del miembro en la dimensión de tiempo que define el contexto temporal del KPI.<br /><br /> Devuelve **NULL** si no hay ningún miembro de hora definido.|  
|**KPI_PARENT_KPI_NAME**|**DBTYPE_WSTR**|Nombre del KPI primario.|  
|**ÁMBITO**|**DBTYPE_I4**|Ámbito del KPI. El KPI puede ser de sesión o global.<br /><br /> Esta columna admite cualquiera de los siguientes valores:<br /><br /> MDKPI_SCOPE_GLOBAL=1<br /><br /> MDKPI_SCOPE_SESSION=2|  
|**ANOTACIONES**|**DBTYPE_WSTR**|(Opcional) Conjunto de notas en formato XML.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **MDSCHEMA_KPIS** se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**NOMBRE_KPI**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) La restricción predeterminada es un valor de **1**. Un mapa de bits con uno de los siguientes valores válidos:<br /><br /> **1** CUBO<br /><br /> **2** DIMENSIÓN|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
