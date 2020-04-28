---
title: Configuración global (cuadros de diálogo) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 43989355-cebf-4d8b-ba3d-fa8546e70230
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 4fc68e8b8d3fc009b766f0fb0be97f1124797764
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68259648"
---
# <a name="global-settings-dialogs--oracletosql"></a>Configuración global (cuadros de diálogo) (OracleToSQL)
Use la página cuadros de diálogo del cuadro de diálogo **configuración global** para especificar la configuración predeterminada de la acción del usuario y de la advertencia para SSMA.  
  
Para tener acceso a la configuración del cuadro de diálogo en el menú **herramientas** , seleccione **configuración global**, haga clic en **GUI** en la parte inferior del panel izquierdo y, a continuación, seleccione **cuadros de diálogo**.  
  
## <a name="options"></a>Opciones  
**Advertir antes de sobrescribir objetos**  
Cuando SSMA convierte objetos en SQL Server, es posible que algunos objetos ya existan en los metadatos del SQL Server del proyecto. Es posible que estos objetos ya se hayan convertido o que los objetos simplemente tengan el mismo nombre en el esquema de destino que los objetos que se van a convertir.  
  
Use esta opción para especificar si SSMA debe pedirle que se sobrescriban las definiciones de objetos duplicados:  
  
-   Si selecciona **true**, SSMA mostrará un cuadro de diálogo de advertencia cuando encuentre un objeto duplicado. En este cuadro de diálogo, puede especificar para sobrescribir objetos individuales o todos los objetos duplicados, o para omitir objetos individuales o todos los objetos duplicados.  
  
-   Si selecciona **false**, aparece la opción de **acción predeterminada sobrescribir objeto** en la que se especifica la acción predeterminada.  
  
**Acción predeterminada para sobrescribir objetos**  
Esta opción aparece si selecciona **false** para la opción **advertir antes de sobrescribir objetos** .  
  
Use esta opción para especificar el comportamiento de sobrescritura del objeto predeterminado:  
  
-   Si selecciona **true**, SSMA sobrescribirá automáticamente los objetos de los metadatos del proyecto SQL Server que tengan el mismo nombre y estén en el mismo esquema de destino que el objeto que se va a convertir.  
  
-   Si selecciona **false**, SSMA no sobrescribirá los metadatos del objeto durante la conversión.  
  
