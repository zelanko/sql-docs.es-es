---
title: Asignación de tipos de datos SQL Server (OracleToSQL) y Oracle | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 6948b81ca2460d4de74393aa880f95fe3f11dfb1
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395001"
---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>Asignación de tipos de datos de Oracle y de SQL Server (OracleToSQL)
Tipos de base de datos de Oracle se diferencian [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos base de datos. Al convertir los objetos de base de datos de Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, debe especificar cómo asignar tipos de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede aceptar las asignaciones de tipos de datos de forma predeterminada, o puede personalizar las asignaciones como se muestra en las secciones siguientes.  
  
## <a name="default-mappings"></a>Asignaciones predeterminadas  
SSMA tiene un conjunto predeterminado de asignaciones de tipos de datos. Para obtener la lista de asignaciones predeterminadas, vea [configuración del proyecto &#40;Type Mapping&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de asignación de herencia  
Puede personalizar las asignaciones de tipos en el nivel de proyecto, el nivel de categoría de objeto (por ejemplo, todos los procedimientos almacenados) o el nivel de objeto. Configuración se hereda del nivel superior, a menos que se invaliden en un nivel inferior. Por ejemplo, si asigna **smallmoney** a **dinero** en el nivel de proyecto, todos los objetos en el proyecto usará esta asignación a menos que personalice la asignación en el nivel de objeto o una categoría.  
  
Cuando ve el **Type Mapping** ficha en SSMA, el fondo está codificada por colores para mostrar qué asignaciones de tipos se heredan. El fondo de una asignación de tipo está en amarillo para cualquier asignación de tipo heredado y en blanco para cualquier asignación que se especifica en el nivel actual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizar asignaciones de tipos de datos  
El siguiente procedimiento muestra cómo asignar tipos de datos en el proyecto, la base de datos o el nivel de objeto:  
  
**Para asignar tipos de datos**  
  
1.  Para personalizar la asignación de tipos de datos para todo el proyecto, abra el **configuración del proyecto** cuadro de diálogo:  
  
    1.  En el **herramientas** menú, seleccione **configuración del proyecto**.  
  
    2.  En el panel izquierdo, seleccione **Type Mapping**.  
  
        El gráfico de asignación de tipo y los botones aparecen en el panel derecho.  
  
    O bien, para personalizar el tipo de datos de asignación en la base de datos, tabla, vista o el nivel de procedimiento almacenado, seleccione la base de datos, la categoría de objeto o el objeto en el Explorador de metadatos de Oracle:  
  
    1.  En el Explorador de metadatos de Oracle, seleccione la carpeta o el objeto que se va a personalizar.  
  
    2.  En el panel derecho, haga clic en el **Type Mapping** ficha.  
  
2.  Para agregar una nueva asignación, realice lo siguiente:  
  
    1.  Haga clic en **Agregar**.  
  
    2.  En **tipo de origen**, seleccione el tipo de datos de Oracle para asignar.  
  
    3.  Si el tipo requiere una longitud, especifique la longitud mínima de datos para la asignación en el **desde** cuadro y la longitud máxima de los datos en el **a** cuadro.  
  
        Esto le permite personalizar la asignación de datos para los valores más pequeños y más grandes del mismo tipo de datos.  
  
    4.  En **tipo de destino**, seleccione el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.  
  
        Algunos tipos requieren una longitud del tipo de datos de destino. Si es necesario, escriba la nueva longitud de datos en el **reemplace** cuadro.  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Para modificar una asignación de tipos de datos, realice lo siguiente:  
  
    1.  Haga clic en **Editar**.  
  
    2.  En **tipo de origen**, seleccione el tipo de datos de Oracle para asignar.  
  
    3.  Si el tipo requiere una longitud, especifique la longitud mínima de datos para la asignación en el **desde** cuadro y la longitud máxima de los datos en el **a** cuadro.  
  
        Esto le permite personalizar la asignación de datos para los valores más pequeños y más grandes del mismo tipo de datos.  
  
    4.  En **tipo de destino**, seleccione el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.  
  
        Algunos tipos requieren una longitud del tipo de datos de destino. Si es necesario, escriba la nueva longitud de datos en el **reemplace** cuadro y, a continuación, [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Para quitar una asignación de tipos de datos personalizados, realice lo siguiente:  
  
    1.  Seleccione la fila en la lista de asignación de tipo que contiene la asignación de tipos de datos que desea quitar.  
  
    2.  Haga clic en **Quitar**.  
  
        No se puede quitar asignaciones heredadas. Sin embargo, las asignaciones heredadas son reemplazadas por asignaciones personalizadas en un objeto específico o una categoría de objeto.  
  
## <a name="next-steps"></a>Pasos siguientes  
El siguiente paso del proceso de migración consiste en [crear un informe de evaluación](assessing-oracle-schemas-for-conversion-oracletosql.md) o [convertir los objetos de base de datos de Oracle en la sintaxis de SQL Server](converting-oracle-schemas-oracletosql.md). Si crea un informe de evaluación, los objetos de Oracle se convierten automáticamente durante la evaluación.  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
