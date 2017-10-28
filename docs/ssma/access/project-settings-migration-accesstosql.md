---
title: "Configuración (migración) (AccessToSQL) del proyecto | Documentos de Microsoft"
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
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3faaf19a1c591628ef97c4fe33fa0a54d4b077d5
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-migration-accesstosql"></a>Configuración del proyecto (migración) (AccessToSQL)
La configuración del proyecto de migración le permite configurar la forma en que se migren los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.  
  
El panel de migración está disponible en la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Use la **configuración del proyecto** cuadro de diálogo para establecer las opciones de configuración para el proyecto actual. Para acceder a la configuración de la migración, en el **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
-   Use la **configuración de proyecto predeterminada** cuadro de diálogo para establecer las opciones de configuración para todos los proyectos. Para acceder a la configuración de la migración, en el **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto en **versión de destino de migración** cuadro combinado de los cuales desea acceder a la configuración, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
## <a name="options"></a>Opciones  
**Restricciones CHECK**  
Especifica si SSMA debe comprobar restricciones cuando agrega datos a tablas.  
  
-   **Modo predeterminado**: False  
  
-   **Modo optimista**: True  
  
-   **Modo completo**: False  
  
**Activar desencadenadores**  
Especifica si SSMA debe activar desencadenadores de inserción cuando agrega datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tablas.  
  
-   **Modo predeterminado**: False  
  
-   **Modo optimista**: True  
  
-   **Modo completo**: False  
  
**Mantener valores de identidad**  
Especifica si SSMA conserva los valores de identidad de acceso cuando agrega datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Si este valor es False, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] asigna valores de identidad.  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: True  
  
-   **Modo completo**: False  
  
**Mantener valores NULL**  
Especifica si SSMA conserva valores null en los datos de origen cuando agrega datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], independientemente de los valores predeterminados que se especifican en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
**Bloqueos de tabla**  
Especifica si SSMA bloquea las tablas cuando agrega datos a tablas durante la migración de datos. Si el valor es False, SSMA utiliza bloqueos de fila.  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: True  
  
-   **Modo completo**: True  
  
**Reemplace las fechas no compatibles**  
Especifica si SSMA debe corregir las fechas de acceso que son anteriores a la más antigua [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] fecha de fecha y hora (01 de enero de 1753).  
  
-   Para mantener los valores de fecha actual, seleccione **no hacen nada**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]no aceptará las fechas anteriores 01 de enero de 1753 en una columna de fecha y hora. Si utiliza las fechas anteriores, debe convertir los valores de fecha y hora a valores de caracteres.  
  
-   Para convertir las fechas anteriores 01 de enero de 1753 a NULL, seleccione **reemplace con NULL**.  
  
-   Para reemplazar las fechas anteriores 01 de enero de 1753 con una fecha admitida, seleccione **reemplazar con más cercano de fecha admitido**. Si selecciona este valor más cercano de forma predeterminada se seleccionará compatible fecha como 01 de enero de 1753.  
  
**Tamaño del lote**  
Tamaño de lote utilizado durante la migración de datos. Se registra una transacción después de cada lote. De forma predeterminada, el tamaño del lote para todos los esquemas es 10000.  
  
## <a name="see-also"></a>Vea también  
[Reference(Access) de interfaz de usuario](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  

