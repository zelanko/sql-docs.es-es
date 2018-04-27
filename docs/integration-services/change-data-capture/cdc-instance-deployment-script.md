---
title: Script de implementación de instancia CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8fa82822-ac99-48ef-a18d-f4f3a77105b4
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eaa5e76954f4ad9f694128d72fb647ee72395610
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="cdc-instance-deployment-script"></a>Script de implementación de instancia CDC
  El cuadro de diálogo Script de implementación de instancia CDC muestra el script de implementación de la instancia CDC. Este script se puede usar para volver a crear la base de datos CDC con todos sus artefactos en otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente.  
  
 Al completarse el script de implementación, debe asegurarse de lo siguiente:  
  
-   El script de implementación da por supuesto que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino se preparó para CDC de Oracle mediante la Consola de configuración del servicio CDC de Oracle o mediante el **script de preparación** que el programa crea.  
  
-   La parte del script que se emplea para habilitar la base de datos para CDC debe ejecutarla un `sysadmin`.  
  
-   El script no conserva la contraseña de minería de registros de Oracle. Es necesario establecerla manualmente después de que se ejecute el script y se inicie el servicio CDC de Oracle.  
  
 Seleccione las opciones siguientes en el cuadro de diálogo **Script de implementación de instancia CDC** .  
  
 **Guardar como**  
 Guarda el script en un archivo de texto que puede guardar en cualquier ubicación que desee. Puede copiar el archivo con el script a cualquier otro servidor para ejecutarlo en él.  
  
 **Copiar**  
 Copia el script en el Portapapeles. Puede pegar el script en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o en cualquier editor de texto para ejecutar los scripts posteriormente.  
  
## <a name="see-also"></a>Ver también  
 [Preparar SQL Server para CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
