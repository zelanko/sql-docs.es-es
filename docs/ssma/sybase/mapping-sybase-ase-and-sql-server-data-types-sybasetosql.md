---
title: Asignación de Sybase ASE y tipos de datos SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8e50253b7c7fb6c59b4303c528c1ef7267ccf644
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62706071"
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>Asignación de tipos de datos de Sybase ASE y de SQL Server (SybaseToSQL)
Tipos de base de datos de Sybase Adaptive Server Enterprise (ASE) difieren de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tipos de base de datos de SQL Azure. Al convertir los objetos de base de datos de ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u objetos de SQL Azure, debe especificar cómo se asignan los tipos de datos de ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Puede aceptar las asignaciones de tipos de datos de forma predeterminada, o puede personalizar las asignaciones como se muestra en las secciones siguientes.  
  
## <a name="default-mappings"></a>Asignaciones predeterminadas  
SSMA tiene un conjunto predeterminado de asignaciones de tipos de datos. Para obtener la lista de asignaciones predeterminadas, vea [configuración del proyecto &#40;Type Mapping&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de asignación de herencia  
Puede personalizar las asignaciones de tipos en el nivel de proyecto, el nivel de categoría de objeto (por ejemplo, todos los procedimientos almacenados) o el nivel de objeto. Configuración se hereda del nivel superior, a menos que se reemplaza en un nivel inferior. Por ejemplo, si asigna **smallmoney** a **dinero** en el nivel de proyectos, todos los objetos en el proyecto usará esta asignación a menos que personalice la asignación en el nivel de categoría de objeto o el nivel de objeto.  
  
Cuando ve el **Type Mapping** ficha en SSMA, el fondo está codificada por colores para mostrar qué asignaciones de tipos se heredan. El fondo de una asignación de tipo está en amarillo para cualquier asignación de tipo heredado y en blanco para cualquier asignación especificada en el nivel actual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizar asignaciones de tipos de datos  
El siguiente procedimiento muestra cómo asignar tipos de datos en el proyecto, la base de datos o el nivel de objeto.  
  
**Para asignar tipos de datos**  
  
1.  Para personalizar la asignación de tipos de datos para todo el proyecto, abra el **configuración del proyecto** cuadro de diálogo:  
  
    1.  En el **herramientas** menú, seleccione **configuración del proyecto**.  
  
    2.  En el panel izquierdo, seleccione **Type Mapping**.  
  
        El gráfico de asignación de tipo y los botones aparecen en el panel derecho.  
  
    O bien, para personalizar el tipo de datos de asignación en la base de datos, tabla, vista o el nivel de procedimiento almacenado, seleccione la base de datos, la categoría de objeto o el objeto en el Explorador de metadatos de Sybase:  
  
    1.  En el Explorador de metadatos de Sybase, seleccione la carpeta o el objeto que desea personalizar.  
  
    2.  En el panel derecho, haga clic en el **Type Mapping** ficha.  
  
2.  Para agregar una nueva asignación, realice lo siguiente:  
  
    1.  Haga clic en **Agregar**.  
  
    2.  En **tipo de origen**, seleccione el tipo de datos de ASE para asignar.  
  
    3.  Si el tipo requiere una longitud, especifique la longitud mínima de datos para la asignación en el **desde** cuadro y especifique la longitud máxima de los datos para la asignación en el **a** cuadro.  
  
        Esto le permite personalizar la asignación de datos para los valores más pequeños y más grandes del mismo tipo de datos.  
  
    4.  En **tipo de destino**, seleccione el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tipo de datos de SQL Azure.  
  
        Algunos tipos requieren una longitud del tipo de datos de destino. Si es necesario, escriba la nueva longitud de datos en el **reemplace** cuadro.  
  
    5.  Haga clic en **Aceptar**.  
  
3.  Para editar una asignación de tipos de datos, realice lo siguiente:  
  
    1.  Haga clic en **Editar**.  
  
    2.  En **tipo de origen**, seleccione el tipo de datos de ASE para asignar.  
  
    3.  Si el tipo requiere una longitud, especifique la longitud mínima de datos para la asignación en el **desde** cuadro y especifique la longitud máxima de los datos para la asignación en el **a** cuadro.  
  
        Esto le permite personalizar la asignación de datos para los valores más pequeños y más grandes del mismo tipo de datos.  
  
    4.  En **tipo de destino**, seleccione el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tipo de datos de SQL Azure.  
  
        Algunos tipos requieren una longitud del tipo de datos de destino. Si es necesario, escriba la nueva longitud de datos en el **reemplace** cuadro y, a continuación, haga clic en **Aceptar**.  
  
4.  Para quitar una asignación de tipos de datos personalizados, realice lo siguiente:  
  
    1.  Seleccione la fila en la lista de asignación de tipo que contiene la asignación de tipos de datos que desea quitar.  
  
    2.  Haga clic en **Quitar**.  
  
        No se puede quitar asignaciones heredadas. Sin embargo, las asignaciones heredadas son reemplazadas por asignaciones personalizadas en un objeto específico o una categoría de objeto.  
  
## <a name="next-steps"></a>Pasos siguientes  
El siguiente paso del proceso de migración consiste en [crear un informe de evaluación](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) o [objetos de base de datos de Sybase ASE de convertir a sintaxis de SQL Server o SQL Azure](converting-sybase-ase-database-objects-sybasetosql.md). Si crea un informe de evaluación, los objetos de Sybase ASE se convierten automáticamente durante la evaluación.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
