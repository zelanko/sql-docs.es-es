---
title: "Asignación de DB2 y tipos de datos SQL Server (DB2ToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: e7e939a8-5e76-4509-beaf-5acd1cab505e
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce0e2311d040705713b51bf007b9334bccaa69ff
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="mapping-db2-and-sql-server-data-types-db2tosql"></a>Asignación de DB2 y tipos de datos SQL Server (DB2ToSQL)
Los tipos de base de datos de DB2 difieren entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos base de datos. Al convertir objetos de base de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos, debe especificar cómo se asignan los tipos de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Puede aceptar las asignaciones de tipos de datos de forma predeterminada, o puede personalizar las asignaciones como se muestra en las secciones siguientes.  
  
## <a name="default-mappings"></a>Asignaciones predeterminadas  
SSMA tiene un conjunto predeterminado de asignaciones de tipos de datos. Para obtener la lista de asignaciones predeterminadas, vea [configuración del proyecto &#40; Asignación de tipos de &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-type-mapping-db2tosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de asignación de herencia  
Puede personalizar las asignaciones de tipos en el nivel de proyecto, el nivel de categoría de objeto (por ejemplo, todos los procedimientos almacenados) o el nivel de objeto. Configuración se hereda del nivel superior, a menos que se invaliden en un nivel inferior. Por ejemplo, si asigna **smallmoney** a **dinero** en el nivel de proyecto, todos los objetos en el proyecto usará esta asignación a menos que personalice la asignación en el nivel de objeto o una categoría.  
  
Al ver el **Type Mapping** ficha SSMA, el fondo está codificada por color para mostrar las asignaciones de tipos se heredan. El fondo de una asignación de tipo es amarillo para cualquier asignación de tipo heredado y blanco para cualquier asignación que se especifica en el nivel actual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizar asignaciones de tipos de datos  
El siguiente procedimiento muestra cómo asignar tipos de datos en el proyecto, la base de datos o el nivel de objeto:  
  
**Para asignar tipos de datos**  
  
1.  Para personalizar la asignación de tipos de datos para todo el proyecto, abra el **configuración del proyecto** cuadro de diálogo:  
  
    1.  En el **herramientas** menú, seleccione **configuración del proyecto**.  
  
    2.  En el panel izquierdo, seleccione **asignación de tipo**.  
  
        El gráfico de asignación de tipo y los botones aparecen en el panel derecho.  
  
    O bien, para personalizar el tipo de datos de asignación en la base de datos, tabla, vista o el nivel de procedimiento almacenado, seleccione la base de datos, la categoría de objeto o el objeto en el Explorador de metadatos de DB2:  
  
    1.  En el Explorador de metadatos de DB2, seleccione la carpeta o el objeto que se va a personalizar.  
  
    2.  En el panel derecho, haga clic en el **Type Mapping** ficha.  
  
2.  Para agregar una nueva asignación, haga lo siguiente:  
  
    1.  Haga clic en **Agregar**.  
  
    2.  En **como tipo de origen**, seleccione el tipo de datos de DB2 para asignar.  
  
    3.  Si el tipo requiere una longitud, especifique la longitud mínima de datos para la asignación en el **de** cuadro y la longitud máxima de los datos en el **a** cuadro.  
  
        Esto le permite personalizar la asignación de datos para los valores más pequeños y más grandes del mismo tipo de datos.  
  
    4.  En **tipo de destino**, seleccione el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos.  
  
        Algunos tipos requieren una longitud del tipo de datos de destino. Si es necesario, escriba la nueva longitud de datos en el **reemplazar con** cuadro.  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  Para modificar una asignación de tipos de datos, haga lo siguiente:  
  
    1.  Haga clic en **Editar**.  
  
    2.  En **como tipo de origen**, seleccione el tipo de datos de DB2 para asignar.  
  
    3.  Si el tipo requiere una longitud, especifique la longitud mínima de datos para la asignación en el **de** cuadro y la longitud máxima de los datos en el **a** cuadro.  
  
        Esto le permite personalizar la asignación de datos para los valores más pequeños y más grandes del mismo tipo de datos.  
  
    4.  En **tipo de destino**, seleccione el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos.  
  
        Algunos tipos requieren una longitud del tipo de datos de destino. Si es necesario, escriba la nueva longitud de datos en el **reemplazar con** cuadro y, a continuación,[!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
4.  Para quitar una asignación de tipo de datos personalizado, haga lo siguiente:  
  
    1.  Seleccione la fila en la lista de asignación de tipo que contiene la asignación de tipo de datos que desea quitar.  
  
    2.  Haga clic en **Quitar**.  
  
        No se puede quitar asignaciones heredadas. Sin embargo, asignaciones heredadas son reemplazadas por las asignaciones personalizadas en un objeto específico o una categoría de objeto.  
  
## <a name="next-steps"></a>Pasos siguientes  
El paso siguiente del proceso de migración consiste en [evaluación informe &#40; DB2ToSQL &#41;](../../ssma/db2/assessment-report-db2tosql.md) o [convertir esquemas de DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md). Si crea un informe de evaluación, los objetos de DB2 se convierten automáticamente durante la evaluación.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de DB2 a SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
