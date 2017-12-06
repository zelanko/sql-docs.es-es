---
title: "(Asignación de tipos) de la configuración del proyecto (SybaseToSQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea1b35e6943e89236aee72e7b0c31c545e100f88
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="project-settings-type-mapping-sybasetosql"></a>(Asignación de tipos) de la configuración del proyecto (SybaseToSQL)
La página de asignación de tipo de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA convierte los tipos de datos de Sybase Adaptive Server Enterprise (ASE) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos.  
  
La página de asignación de tipo está disponible en la **configuración del proyecto** y **la configuración predeterminada del proyecto** cuadros de diálogo.  
  
-   Para especificar la configuración de asignación de tipo para todos los proyectos futuros de SSMA, en la **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que se requiere para puede ver o cambiar de configuración **versión de destino de migración** de lista desplegable y, a continuación, seleccione **asignación de tipos de** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú, seleccione **configuración del proyecto**y, a continuación, seleccione **Type Mapping** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
**Tipo de origen**  
El tipo de datos de ASE asignado.  
  
**Tipo de destino**  
El destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos para el tipo de datos de ASE especificado.  
  
Vea la tabla en la sección siguiente para el valor predeterminado SSMA para Sybase asignación de tipo.  
  
**Agregar**  
Haga clic para agregar un tipo de datos a la lista de asignación.  
  
**Editar**  
Haga clic para editar el tipo de datos seleccionado en la lista de asignación.  
  
**Quitar**  
Haga clic para quitar la asignación de tipos de datos seleccionados de la lista de asignación.  
  
**Restablecer valores predeterminados**  
Haga clic para restablecer la lista de asignación de tipo para los valores predeterminados SSMA.  
  
## <a name="default-type-mapping"></a>Asignación de tipos predeterminados  
En la tabla siguiente contiene la asignación de tipo de valor predeterminado entre ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos.  
  
|Tipo de datos de ASE|Tipo de datos de SQL Server|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binario**|**binario**|  
|**binario [\*... 8000]**|**binario [\*]**|  
|**binario [8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**carácter variable**|**varchar**|  
|**char varying [\*... 8000]**|**varchar [\*]**|  
|**char varying [8001..\*]**|**varchar(max)**|  
|**char[\*.. 8000]**|**char[\*]**|  
|**Char [8001..\*;]**|**varchar(max)**|  
|**carácter**|**char**|  
|**carácter variable**|**varchar**|  
|**carácter variable [\*... 8000]**|**varchar [\*]**|  
|**carácter variable [8001..\*]**|**varchar(max)**|  
|**caracteres [\*... 8000]**|**char[\*]**|  
|**caracteres [8001..\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2 [3]**|  
|**diciembre**|**decimal**|  
|**dec[\*.. \*]**|**decimal [\*]**|  
|**dec[\*.. \*][\*.. \*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**decimal [\*... \*]**|**decimal [\*]**|  
|**decimal [\*... \*][\*.. \*]**|**decimal[\*][\*]**|  
|**precisión doble**|**float [53]**|  
|**float**|**float [53]**|  
|**float [\*... 15]**|**float [24]**|  
|**float [16..\*]**|**float [53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar [255]**|  
|**money**|**money**|  
|**Car.**|**nchar**|  
|**National char [\*... 4000]**|**nchar [\*]**|  
|**variación car.**|**nvarchar**|  
|**variación car [\*... 4000]**|**nvarchar [\*]**|  
|**variación car [4001..\*]**|**nvarchar(max)**|  
|**National char [4001..\*]**|**nvarchar(max)**|  
|**caracteres no nacionales**|**nchar**|  
|**caracteres no nacionales [\*... 4000]**|**nchar [\*]**|  
|**caracteres no nacionales [4001..\*]**|**nvarchar(max)**|  
|**national character varying de**|**nvarchar**|  
|**national character varying de [\*... 4000]**|**nvarchar [\*]**|  
|**national character varying de [4001..\*]**|**nvarchar(max)**|  
|**varchar nacional**|**nvarchar**|  
|**varchar nacional [\*... 4000]**|**nvarchar [\*]**|  
|**varchar nacional [4001..\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar varying**|**nvarchar**|  
|**nchar varying [\*... 4000]**|**nvarchar [\*]**|  
|**nchar varying [4001..\*]**|**nvarchar(max)**|  
|**nchar [\*... 4000]**|**nchar [\*]**|  
|**nchar [4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numérico [\*... \*]**|**numérico [\*]**|  
|**numérico [\*... \*][\*.. \*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar [\*... 4000]**|**nvarchar [\*]**|  
|**nvarchar [4001..\*]**|**nvarchar(max)**|  
|**real**|**float [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar [128]**|  
|**sysname [\*... \*]**|**nvarchar [255]**|  
|**text**|**text**|  
|**time**|**hora [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**UNICHAR**|**nchar**|  
|**UNICHAR variable**|**nvarchar**|  
|**variable UNICHAR [\*... 4000]**|**nvarchar [\*]**|  
|**variable UNICHAR [4001..\*]**|**nvarchar(max)**|  
|**UNICHAR [\*... 4000]**|**nchar [\*]**|  
|**UNICHAR [4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar [\*... 4000]**|**nvarchar [\*]**|  
|**univarchar [4001..\*]**|**nvarchar(max)**|  
|**bigint sin signo**|**numérico [20] [0]**|  
|**int sin signo**|**bigint**|  
|**smallint sin signo**|**int**|  
|**tinyint sin signo**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary [\*... 8000]**|**varbinary [\*]**|  
|**varbinary [8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar [\*... 8000]**|**varchar [\*]**|  
|**varchar [8001..\*]**|**varchar(max)**|  
  
