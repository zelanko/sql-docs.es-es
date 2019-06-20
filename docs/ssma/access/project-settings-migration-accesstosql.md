---
title: Configuración (migración) (AccessToSQL) del proyecto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 441366208d2bfd886794dd7e50dca7e0aef7b3ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299290"
---
# <a name="project-settings-migration-accesstosql"></a>Configuración del proyecto (migración) (AccessToSQL)
La configuración del proyecto de migración le permite configurar cómo se migran datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
El panel de la migración está disponible en el **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Use la **configuración del proyecto** cuadro de diálogo para establecer las opciones de configuración para el proyecto actual. Para obtener acceso a la configuración de migración, en el **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en  **Migración**.  
  
-   Use la **configuración de proyecto predeterminada** cuadro de diálogo para establecer las opciones de configuración para todos los proyectos. Para acceder a la configuración de migración, en el **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto en **versión de destino de migración** cuadro combinado de los cuales se acceso a la configuración, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
## <a name="options"></a>Opciones  
**Restricciones CHECK**  
Especifica si SSMA debe comprobar restricciones cuando agrega datos a las tablas.  
  
-   **Modo predeterminado**: False  
  
-   **Modo optimista**: True  
  
-   **Modo completo**: False  
  
**Activar desencadenadores**  
Especifica si SSMA debe activar desencadenadores de inserción cuando se agregan datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas.  
  
-   **Modo predeterminado**: False  
  
-   **Modo optimista**: True  
  
-   **Modo completo**: False  
  
**Mantener valores de identidad**  
Especifica si SSMA conserva los valores de identidad de acceso cuando se agregan datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si este valor es False, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna los valores de identidad.  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: True  
  
-   **Modo completo**: False  
  
**Mantener valores NULL**  
Especifica si SSMA conserva valores null en los datos de origen cuando se agregan datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independientemente de los valores predeterminados que se especifican en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
**Bloqueos de tabla**  
Especifica si SSMA bloquea las tablas cuando agrega datos a las tablas durante la migración de datos. Si el valor es False, SSMA utiliza bloqueos de fila.  
  
-   **Modo predeterminado**: True  
  
-   **Modo optimista**: True  
  
-   **Modo completo**: True  
  
**Reemplazar las fechas no compatibles**  
Especifica si debería corregir la fechas de acceso anteriores a la primera SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fecha de fecha y hora (01 de enero de 1753).  
  
-   Para conservar los valores de fecha actual, seleccione **no hacen nada**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aceptará las fechas anteriores 01 de enero de 1753 en una columna de fecha y hora. Si usa las fechas anteriores, debe convertir los valores de fecha y hora para los valores de caracteres.  
  
-   Para convertir las fechas anteriores 01 de enero de 1753 a NULL, seleccione **reemplace con NULL**.  
  
-   Para reemplazar las fechas anteriores 01 de enero de 1753 con una fecha admitida, seleccione **reemplazar con más cercano de fecha admitido**. Si selecciona este valor, más cercano de forma predeterminada se seleccionará admitido fecha como 01 de enero de 1753.  
  
**Tamaño de lote**  
Tamaño de lote utilizado durante la migración de datos. Se registra una transacción después de cada lote. De forma predeterminada, el tamaño del lote para todos los esquemas es 10000.  
  
## <a name="see-also"></a>Vea también  
[Reference(Access) de interfaz de usuario](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
