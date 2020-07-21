---
title: Configuración del proyecto (migración) (AccessToSQL) | Microsoft Docs
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
ms.openlocfilehash: 3e3d979b6f3c5943723fb5dd8f37831adfbc1305
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67929394"
---
# <a name="project-settings-migration-accesstosql"></a>Configuración del proyecto (migración) (AccessToSQL)
La configuración del proyecto de migración le permite configurar cómo se migran los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos a o SQL Azure.  
  
El panel Migración está disponible en los cuadros de diálogo Configuración del **proyecto** y **configuración predeterminada del proyecto** .  
  
-   Utilice el cuadro de diálogo **configuración del proyecto** para establecer las opciones de configuración del proyecto actual. Para obtener acceso a la configuración de migración, en el menú **herramientas** , seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
-   Utilice el cuadro de diálogo **configuración predeterminada del proyecto** para establecer las opciones de configuración de todos los proyectos. Para obtener acceso a la configuración de migración, en el menú **herramientas** , seleccione **configuración predeterminada del proyecto**, seleccione el tipo de proyecto en el cuadro combinado de la **versión de destino** de la migración del que desea obtener acceso a la configuración, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
## <a name="options"></a>Opciones  
**Restricciones CHECK**  
Especifica si SSMA debe comprobar las restricciones cuando agrega datos a las tablas.  
  
-   **Modo predeterminado**: false  
  
-   **Modo optimista**: true  
  
-   **Modo completo**: false  
  
**Activar desencadenadores**  
Especifica si SSMA debe activar los desencadenadores de inserción cuando agrega datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a las tablas.  
  
-   **Modo predeterminado**: false  
  
-   **Modo optimista**: true  
  
-   **Modo completo**: false  
  
**Mantener valores de identidad**  
Especifica si SSMA conserva los valores de identidad de acceso cuando agrega datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si este valor es false, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna los valores de identidad.  
  
-   **Modo predeterminado**: true  
  
-   **Modo optimista**: true  
  
-   **Modo completo**: false  
  
**Mantener valores NULL**  
Especifica si SSMA conserva los valores NULL en los datos de origen cuando agrega datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independientemente de los valores predeterminados que se especifiquen en. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   **Modo predeterminado**: true  
  
-   **Modo optimista**: false  
  
-   **Modo completo**: true  
  
**Bloqueos de tabla**  
Especifica si SSMA bloquea las tablas cuando agrega datos a las tablas durante la migración de datos. Si el valor es false, SSMA utiliza bloqueos de fila.  
  
-   **Modo predeterminado**: true  
  
-   **Modo optimista**: true  
  
-   **Modo completo**: true  
  
**Reemplazar fechas no admitidas**  
Especifica si SSMA debe corregir las fechas de acceso anteriores a la fecha de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fecha y hora más antigua (01 de enero 1753).  
  
-   Para mantener los valores de fecha actuales, seleccione **no hacer nada**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no aceptará fechas anteriores al 01 de enero de 1753 en una columna de fecha y hora. Si utiliza fechas anteriores, debe convertir los valores DATETIME en valores de caracteres.  
  
-   Para convertir las fechas anteriores al 01 de enero de 1753 a NULL, seleccione **reemplazar con NULL**.  
  
-   Para reemplazar las fechas anteriores al 01 de enero de 1753 con una fecha admitida, seleccione **reemplazar con la fecha más cercana admitida**. Si selecciona este valor, de forma predeterminada, la fecha admitida más cercana se seleccionará como 01 de enero de 1753.  
  
**Tamaño de lote**  
Tamaño de lote usado durante la migración de datos. Una transacción se registra después de cada lote. De forma predeterminada, el tamaño del lote para todos los esquemas es 10000.  
  
## <a name="see-also"></a>Consulte también  
[Referencia de la interfaz de usuario (acceso)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
