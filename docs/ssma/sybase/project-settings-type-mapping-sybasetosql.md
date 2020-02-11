---
title: Configuración del proyecto (asignación de tipo) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d7b16bdf3717fa14f91af41663cbd65365eac52a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028662"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>Configuración del proyecto (asignación de tipo) (SybaseToSQL)
La página asignación de tipos del cuadro de diálogo **configuración del proyecto** contiene opciones que personalizan el modo en que SSMA convierte los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sybase Adaptive Server Enterprise (ASE) en tipos de datos.  
  
La página asignación de tipos está disponible en los cuadros de diálogo **configuración del proyecto** y **configuración predeterminada del proyecto** .  
  
-   Para especificar la configuración de asignación de tipos para todos los proyectos de SSMA futuros, en el menú **herramientas** , seleccione **configuración predeterminada del proyecto**, seleccione tipo de proyecto de migración para el que se deben ver o cambiar los valores de configuración en la lista desplegable de la **versión de destino** de la migración y, a continuación, seleccione **asignación de tipos** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración del proyecto actual, en el menú **herramientas** , seleccione **configuración del proyecto**y, a continuación, seleccione **asignación de tipos** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
**Tipo de origen**  
El tipo de datos ASE asignado.  
  
**Tipo de destino**  
El tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de datos de destino para el tipo de datos ase especificado.  
  
Vea la tabla de la siguiente sección para obtener la asignación de tipo de SSMA para Sybase predeterminada.  
  
**Add (Agregar)**  
Haga clic para agregar un tipo de datos a la lista de asignaciones.  
  
**Edición**  
Haga clic en esta opción para modificar el tipo de datos seleccionado en la lista asignación.  
  
**Remove**  
Haga clic en esta opción para quitar la asignación de tipos de datos seleccionada de la lista de asignaciones.  
  
**Restablecer valores predeterminados**  
Haga clic en esta opción para restablecer la lista asignación de tipos a los valores predeterminados de SSMA.  
  
## <a name="default-type-mapping"></a>Asignación de tipos predeterminada  
La tabla siguiente contiene la asignación de tipos predeterminada entre ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los tipos de datos.  
  
|Tipo de datos ASE|Tipo de datos de SQL Server|  
|-----------------|------------------------|  
|**BIGINT**|**BIGINT**|  
|**binary**|**binary**|  
|**binario\*[.. 8000]**|**binario\*[]**|  
|**binario [8001.\*.]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**char varying [\*.. 8000]**|**VARCHAR [\*]**|  
|**char varying [8001..\*.]**|**ntext**|  
|**Char [\*.. 8000]**|**Char [\*]**|  
|**Char [8001..\*;]**|**ntext**|  
|**character**|**char**|  
|**variar caracteres**|**varchar**|  
|**variación de caracteres\*[.. 8000]**|**VARCHAR [\*]**|  
|**variación de caracteres [8001.\*.]**|**ntext**|  
|**carácter [\*.. 8000]**|**Char [\*]**|  
|**carácter [8001..\*]**|**ntext**|  
|**date**|**date**|  
|**datetime**|**datetime2 [3]**|  
|**Dec**|**Decimal**|  
|**Dec [\*.. \*]**|**decimal [\*]**|  
|**Dec [\*.. \*][\*.. \*]**|**decimal [\*] [\*]**|  
|**Decimal**|**Decimal**|  
|**decimal [\*.. \*]**|**decimal [\*]**|  
|**decimal [\*.. \*][\*.. \*]**|**decimal [\*] [\*]**|  
|**double precision**|**Float [53]**|  
|**float**|**Float [53]**|  
|**Float [\*.. 4,5**|**Float [24]**|  
|**Float [16..\*]**|**Float [53]**|  
|**impresión**|**impresión**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar [255]**|  
|**money**|**money**|  
|**carácter nacional**|**nchar**|  
|**carácter nacional [\*.. 4000]**|**nchar [\*]**|  
|**National char varying**|**nvarchar**|  
|**National char varying [\*.. 4000]**|**nvarchar [\*]**|  
|**National char varying [4001..\*.]**|**nvarchar(max)**|  
|**National Char [4001..\*.]**|**nvarchar(max)**|  
|**carácter nacional**|**nchar**|  
|**carácter nacional [\*.. 4000]**|**nchar [\*]**|  
|**carácter nacional [4001..\*.]**|**nvarchar(max)**|  
|**variable de carácter nacional**|**nvarchar**|  
|**variable Nacional de caracteres\*[.. 4000]**|**nvarchar [\*]**|  
|**carácter nacional variable [4001..\*.]**|**nvarchar(max)**|  
|**VARCHAR nacional**|**nvarchar**|  
|**National VARCHAR [\*.. 4000]**|**nvarchar [\*]**|  
|**National VARCHAR [4001..\*.]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar varying**|**nvarchar**|  
|**nchar varying [\*.. 4000]**|**nvarchar [\*]**|  
|**nchar varying [4001..\*.]**|**nvarchar(max)**|  
|**nchar [\*.. 4000]**|**nchar [\*]**|  
|**nchar [4001..\*.]**|**nvarchar(max)**|  
|**alfanumérico**|**alfanumérico**|  
|**Numeric [\*.. \*]**|**Numeric [\*]**|  
|**Numeric [\*.. \*][\*.. \*]**|**Numeric [\*] [\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar [\*.. 4000]**|**nvarchar [\*]**|  
|**nvarchar [4001..\*.]**|**nvarchar(max)**|  
|**impuestos**|**Float [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**SMALLMONEY**|**SMALLMONEY**|  
|**sysname**|**nvarchar [128]**|  
|**sysname [\*.. \*]**|**nvarchar [255]**|  
|**negrita**|**negrita**|  
|**time**|**hora [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**UNICHAR**|**nchar**|  
|**variables UNICHAR**|**nvarchar**|  
|**variables UNICHAR [\*.. 4000]**|**nvarchar [\*]**|  
|**UNICHAR varying [4001..\*.]**|**nvarchar(max)**|  
|**UNICHAR [\*.. 4000]**|**nchar [\*]**|  
|**UNICHAR [4001..\*.]**|**nvarchar(max)**|  
|**texto unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar [\*.. 4000]**|**nvarchar [\*]**|  
|**univarchar [4001..\*.]**|**nvarchar(max)**|  
|**BIGINT sin signo**|**Numeric [20] [0]**|  
|**unsigned int**|**BIGINT**|  
|**smallint sin signo**|**int**|  
|**tinyint sin signo**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary [\*.. 8000]**|**varbinary [\*]**|  
|**varbinary [8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**VARCHAR [\*.. 8000]**|**VARCHAR [\*]**|  
|**VARCHAR [8001..\*]**|**ntext**|  
  
