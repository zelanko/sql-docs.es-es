---
title: Asignación de Sybase ASE y tipos de datos SQL Server (SybaseToSQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 26cfb02981c77368ab61ef68911d3d64380fc41d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>Asignación de Sybase ASE y tipos de datos SQL Server (SybaseToSQL)
Los tipos de base de datos de Sybase Adaptive Server Enterprise (ASE) difieren entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tipos de base de datos de SQL Azure. Al convertir objetos de base de datos de ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de SQL Azure, debe especificar cómo se asignan los tipos de datos de ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Puede aceptar las asignaciones de tipos de datos de forma predeterminada, o puede personalizar las asignaciones como se muestra en las secciones siguientes.  
  
## <a name="default-mappings"></a>Asignaciones predeterminadas  
SSMA tiene un conjunto predeterminado de asignaciones de tipos de datos. Para obtener la lista de asignaciones predeterminadas, vea [configuración del proyecto &#40;Type Mapping&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de asignación de herencia  
Puede personalizar las asignaciones de tipos en el nivel de proyecto, el nivel de categoría de objeto (por ejemplo, todos los procedimientos almacenados) o el nivel de objeto. Configuración se hereda del nivel superior, a menos que se reemplaza en un nivel inferior. Por ejemplo, si asigna **smallmoney** a **dinero** en el nivel de proyectos, todos los objetos en el proyecto usará esta asignación a menos que personalice la asignación en el nivel de objeto o el nivel de categoría de objeto.  
  
Al ver el **Type Mapping** ficha SSMA, el fondo está codificada por color para mostrar las asignaciones de tipos se heredan. El fondo de una asignación de tipo es amarillo para cualquier asignación de tipo heredado y blanco para cualquier asignación especificada en el nivel actual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizar asignaciones de tipos de datos  
El siguiente procedimiento muestra cómo asignar tipos de datos en el proyecto, la base de datos o el nivel de objeto.  
  
**Para asignar tipos de datos**  
  
1.  Para personalizar la asignación de tipos de datos para todo el proyecto, abra el **configuración del proyecto** cuadro de diálogo:  
  
    1.  En el **herramientas** menú, seleccione **configuración del proyecto**.  
  
    2.  En el panel izquierdo, seleccione **asignación de tipo**.  
  
        El gráfico de asignación de tipo y los botones aparecen en el panel derecho.  
  
    O bien, para personalizar el tipo de datos de asignación en la base de datos, tabla, vista o el nivel de procedimiento almacenado, seleccione la base de datos, la categoría de objeto o el objeto en el Explorador de metadatos de Sybase:  
  
    1.  En el Explorador de metadatos de Sybase, seleccione la carpeta u objeto que desea personalizar.  
  
    2.  En el panel derecho, haga clic en el **Type Mapping** ficha.  
  
2.  Para agregar una nueva asignación, haga lo siguiente:  
  
    1.  Haga clic en **Agregar**.  
  
    2.  En **como tipo de origen**, seleccione el tipo de datos de ASE para asignar.  
  
    3.  Si el tipo requiere una longitud, especifique la longitud mínima de datos para la asignación en el **de** cuadro y especifique la longitud máxima de los datos para la asignación en el **a** cuadro.  
  
        Esto le permite personalizar la asignación de datos para los valores más pequeños y más grandes del mismo tipo de datos.  
  
    4.  En **tipo de destino**, seleccione el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tipo de datos de SQL Azure.  
  
        Algunos tipos requieren una longitud del tipo de datos de destino. Si es necesario, escriba la nueva longitud de datos en el **reemplazar con** cuadro.  
  
    5.  Haga clic en **Aceptar**.  
  
3.  Para editar una asignación de tipos de datos, haga lo siguiente:  
  
    1.  Haga clic en **Editar**.  
  
    2.  En **como tipo de origen**, seleccione el tipo de datos de ASE para asignar.  
  
    3.  Si el tipo requiere una longitud, especifique la longitud mínima de datos para la asignación en el **de** cuadro y especifique la longitud máxima de los datos para la asignación en el **a** cuadro.  
  
        Esto le permite personalizar la asignación de datos para los valores más pequeños y más grandes del mismo tipo de datos.  
  
    4.  En **tipo de destino**, seleccione el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tipo de datos de SQL Azure.  
  
        Algunos tipos requieren una longitud del tipo de datos de destino. Si es necesario, escriba la nueva longitud de datos en el **reemplazar con** cuadro y, a continuación, haga clic en **Aceptar**.  
  
4.  Para quitar una asignación de tipo de datos personalizado, haga lo siguiente:  
  
    1.  Seleccione la fila en la lista de asignación de tipo que contiene la asignación de tipo de datos que desea quitar.  
  
    2.  Haga clic en **Quitar**.  
  
        No se puede quitar asignaciones heredadas. Sin embargo, asignaciones heredadas son reemplazadas por las asignaciones personalizadas en un objeto específico o una categoría de objeto.  
  
## <a name="next-steps"></a>Pasos siguientes  
El paso siguiente del proceso de migración consiste en [crear un informe de evaluación](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) o [objetos de base de datos de Sybase ASE de convertir a la sintaxis de SQL Server o SQL Azure](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3). Si crea un informe de evaluación, los objetos de Sybase ASE se convierten automáticamente durante la evaluación.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos de SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
