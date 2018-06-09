---
title: (Asignación de tipos) de la configuración del proyecto (AccessToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bd5bc6a0db71d2836c068a261681d813bc2011b3
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774471"
---
# <a name="project-settings-type-mapping-accesstosql"></a>(Asignación de tipos) de la configuración del proyecto (AccessToSQL)
La configuración del proyecto de asignación de tipo permite definir asignaciones de tipos de valor predeterminado para el proyecto SSMA. También puede especificar asignaciones de tipos para objetos individuales de la base de datos. Para obtener más información, consulte [tipos de datos de destino y origen de asignación](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).  
  
Asignación de tipos está disponible en la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo:  
  
-   Use la **configuración del proyecto** cuadro de diálogo para establecer las opciones de configuración para el proyecto actual. Para acceder a la configuración de la asignación de tipo, en la **herramientas** menú, seleccione **configuración del proyecto**y, a continuación, haga clic en **asignación de tipos de** en el panel izquierdo.  
  
-   Use la **configuración de proyecto predeterminada** cuadro de diálogo para establecer las opciones de configuración para todos los proyectos. Para acceder a la configuración de la asignación de tipo, en la **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que se requiere para ver / cambiar de configuración **versión de destino de migración** de lista desplegable y, a continuación, haga clic en **asignación de tipos de** en el panel izquierdo.  
  
## <a name="options"></a>Opciones  
**Tipo de origen**  
El tipo de datos de acceso para asignar.  
  
**Tipo de destino**  
El destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tipo de datos de SQL Azure para el tipo de datos de acceso especificado.  
  
En la tabla siguiente muestra las asignaciones predeterminadas entre tipos de datos de origen y de destino.  
  
|Tipo de datos de Access|Tipo de datos de SQL Server|  
|--------------------|------------------------|  
|**binario [\*... \*]**|**varbinary [\*]**|  
|**boolean**|**bit**|  
|**Bytes**|**tinyint**|  
|**Moneda**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**GUID**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**Long**|**int**|  
|**LONGBINARY**|**varbinary(max)**|  
|**Memorando**|**nvarchar(max)**|  
|**memorando** : para Access 97|**ntext**|  
|**Único**|**real**|  
|**texto [\*... \*]**|**nvarchar [\*]**|  
|**texto [\*... \*]** : para Access 97|**varchar [\*]**|  
  
**Agregar**  
Haga clic para agregar un tipo de datos a la lista de asignación.  
  
**Editar**  
Haga clic para editar un tipo de datos en la lista de asignación.  
  
**Quitar**  
Haga clic para quitar la asignación de tipos de datos seleccionados de la lista de asignación.  
  
**Restablecer valores predeterminados**  
Haga clic para restablecer todas las asignaciones de tipo de datos a los valores predeterminados SSMA.  
  
## <a name="see-also"></a>Vea también  
[Asignación de tipos de datos de origen y de destino](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
[Reference(Access) de interfaz de usuario](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
