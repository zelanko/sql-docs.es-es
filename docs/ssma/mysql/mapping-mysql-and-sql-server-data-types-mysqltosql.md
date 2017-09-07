---
title: "Asignación de tipos de datos SQL Server (MySQLToSQL) y MySQL | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
caps.latest.revision: 15
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3dd2adf0b8f6379bd11dc80de4cc2aedf5b3c102
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>Asignación de tipos de datos SQL Server (MySQLToSQL) y MySQL
Los tipos de base de datos de MySQL difieren entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tipos de base de datos de SQL Azure. Al convertir objetos de base de datos de MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de SQL Azure, debe especificar cómo se asignan los tipos de datos de MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Puede aceptar las asignaciones de tipos de datos de forma predeterminada, o puede personalizar las asignaciones como se muestra en los procedimientos siguientes.  
  
## <a name="default-mappings"></a>Asignaciones predeterminadas  
SSMA tiene un conjunto predeterminado de asignaciones de tipos de datos. Para obtener la lista de asignaciones predeterminadas, vea [configuración del proyecto &#40; Asignación de tipos de &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de asignación de herencia  
Puede personalizar las asignaciones de tipos en el nivel de proyecto, el nivel de categoría de objeto (por ejemplo, todos los procedimientos almacenados) o el nivel de objeto. Configuración se hereda del nivel superior, a menos que se invaliden en un nivel inferior. Por ejemplo, si asigna **smallint** a **int** en el nivel de proyecto, todos los objetos en el proyecto usará esta asignación a menos que personalice la asignación en el nivel de objeto o una categoría.  
  
Al ver el **Type Mapping** ficha SSMA, el fondo está codificada por color para mostrar las asignaciones de tipos se heredan. El fondo de una asignación de tipo es amarillo para cualquier asignación de tipo heredado y blanco para cualquier asignación que se especifica en el nivel actual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizar asignaciones de tipos de datos  
  
-   **Para asignar tipos de datos:**  
  
    Los procedimientos siguientes muestran cómo asignar tipos de datos en el proyecto, la base de datos o el nivel de objeto de base de datos:  
  
    1.  Para personalizar la asignación de tipos de datos para todo el proyecto, abra el **configuración del proyecto** cuadro de diálogo. En el menú Herramientas, seleccione **configuración del proyecto**.  
  
        En el panel izquierdo, seleccione **asignación de tipo**. El gráfico de asignación de tipo y los botones aparecen en el panel derecho.  
  
    2.  Para personalizar las asignaciones de tipos de datos en el nivel de base de datos o una tabla, seleccione la tabla o base de datos en el Explorador de metadatos de MySQL. En el Explorador de metadatos de MySQL, seleccione la carpeta o el objeto que se va a personalizar.  
  
        En el panel derecho, haga clic en **asignación de tipo**.  
  
-   **Para agregar una nueva asignación, haga lo siguiente:**  
  
    1.  En el panel de asignación de tipo, haga clic en **agregar** .  
  
    2.  En el nuevo tipo de cuadro de diálogo de asignación, en **como tipo de origen**, seleccione el tipo de datos de MySQL para asignar.  
  
    3.  Si el tipo requiere una longitud, especifique las longitudes de datos mínimo y máximo para la asignación seleccionando la **de** y **a** casillas de verificación y, a continuación, escriba los valores.  
  
    4.  Esto le permite personalizar la asignación de datos para los valores más pequeños y más grandes del mismo tipo de datos. En **tipo de destino**, seleccione el destino SQL Server o el tipo de datos de SQL Azure.  
  
        1.  Algunos tipos requieren una longitud del tipo de datos de destino. Si es necesario, escriba la nueva longitud de datos en el **reemplazar con** cuadro y, a continuación, haga clic en **Aceptar**.  
  
        2.  Algunos tipos requieren un tipo de datos de destino **precisión** y **escala**. Si es necesario, escriba la nueva precisión y escala en el **reemplazar con** cuadro y, a continuación, haga clic en **Aceptar**.  
  
-   **Para editar una asignación de tipo, realice lo siguiente:**  
  
    1.  En el panel de asignación de tipo, haga clic en **editar**.  
  
    2.  En la asignación de tipos de lista en el cuadro de diálogo, **como tipo de origen**, seleccione el tipo de datos de MySQL para asignar.  
  
    3.  Si el tipo requiere una longitud, especifique las longitudes de datos mínimo y máximo para la asignación seleccionando la **de** y **a** casillas de verificación y, a continuación, escriba los valores.  
  
    Esto le permite personalizar la asignación de datos para los valores más pequeños y más grandes del mismo tipo de datos. En **tipo de destino**, seleccione el destino SQL Server o el tipo de datos de SQL Azure.  
  
    1.  Algunos tipos requieren una longitud del tipo de datos de destino. Si es necesario, escriba la nueva longitud de datos en el **reemplazar con** cuadro y, a continuación, haga clic en **Aceptar**.  
  
    2.  Algunos tipos requieren un tipo de datos de destino **precisión** y **escala** . Si es necesario, escriba la nueva precisión y escala en el **reemplazar con** cuadro y, a continuación, haga clic en **Aceptar** .  
  
-   **Para quitar una asignación de tipo de datos, haga lo siguiente:**  
  
    1.  En el panel de asignación de tipos, seleccione la fila en la lista de asignación de tipo que contiene la asignación de tipo de datos que desea quitar.  
  
    2.  Haga clic en **Quitar**.  
  
## <a name="next-step"></a>Paso siguiente  
El paso siguiente del proceso de migración consiste en [crear un informe de evaluación](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec) o [MySQL convertir objetos de base de datos a la sintaxis de SQL Server o SQL Azure](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7). Si crea un informe, los objetos de MySQL se convierten automáticamente durante la evaluación.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de MySQL a SQL Server: base de datos de SQL Azure &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

