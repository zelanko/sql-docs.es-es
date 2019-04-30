---
title: Configuración global (cuadros de diálogo) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 360e01bb-6347-4e2b-acda-0daa161ed33b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c0ac65e0973ac9e862a73dd9c04a916156c8a314
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298798"
---
# <a name="global-settings-dialogs-db2tosql"></a>Configuración global (cuadros de diálogo) (DB2ToSQL)
Use la página de los cuadros de diálogo de la **configuración Global** cuadro de diálogo para especificar la acción predeterminada del usuario y la configuración de advertencia de SSMA.  
  
Para obtener acceso a la configuración del cuadro de diálogo en el **herramientas** menú, seleccione **configuración Global**, haga clic en **GUI** en la parte inferior del panel izquierdo y a continuación, seleccione **decuadrosdediálogo**.  
  
## <a name="options"></a>Opciones  
**Advertir antes de sobrescribir los objetos**  
Cuando SSMA convierte los objetos en SQL Server, algunos objetos ya existan en los metadatos del proyecto SQL Server. Estos objetos es posible que ya se han convertido o los objetos simplemente pueden tener el mismo nombre en el esquema de destino que los objetos que se va a convertir.  
  
Use esta opción para especificar si SSMA debe solicitarle para sobrescribir las definiciones de objeto duplicados:  
  
-   Si selecciona **True**, SSMA mostrará un cuadro de diálogo de advertencia cuando encuentra un objeto duplicado. En este cuadro de diálogo, puede especificar para sobrescribir los objetos individuales o todos los objetos duplicados, u omitir los objetos individuales o todos los objetos duplicados.  
  
-   Si selecciona **False**, **acción predeterminada de sobrescritura de objeto** opción aparece donde especifica la acción predeterminada.  
  
**Acción predeterminada de sobrescritura de objeto**  
Esta opción aparece si selecciona **False** para el **Avisar antes de sobrescribir objetos** opción.  
  
Use esta opción para especificar el comportamiento de sobrescritura de objeto predeterminado:  
  
-   Si selecciona **True**, SSMA sobrescribirá automáticamente los objetos en los metadatos de proyecto de SQL Server que tienen el mismo nombre y están en el mismo esquema de destino que el objeto que se va a convertir.  
  
-   Si selecciona **False**, SSMA no sobrescribe los metadatos del objeto durante la conversión.  
  
